---
title: Definiowanie i określanie błędów
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling faults [WCF], specifying
- handling faults [WCF], defining
ms.assetid: c00c84f1-962d-46a7-b07f-ebc4f80fbfc1
ms.openlocfilehash: 67096c4531d13bc66f584c09c458c0a5a2a41c6b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96260906"
---
# <a name="defining-and-specifying-faults"></a>Definiowanie i określanie błędów

Błędy protokołu SOAP umożliwiają przekazywanie informacji o stanie błędu z usługi do klienta i w przypadku dupleksu od klienta do usługi w sposób interoperacyjny. W tym temacie omówiono, kiedy i jak definiować niestandardową zawartość błędów i określić, które operacje mogą je zwrócić. Aby uzyskać więcej informacji na temat sposobu, w jaki usługa lub klient dupleksu może wysyłać te błędy i jak aplikacja klienta lub usługi obsługuje te błędy, zobacz [wysyłanie i otrzymywanie błędów](sending-and-receiving-faults.md). Omówienie obsługi błędów w aplikacjach Windows Communication Foundation (WCF) zawiera temat [określanie i obsługa błędów w kontraktach i usługach](specifying-and-handling-faults-in-contracts-and-services.md).  
  
## <a name="overview"></a>Omówienie  

 Zadeklarowane błędy protokołu SOAP to te, w których operacja ma <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> niestandardowy typ błędu SOAP. Niezadeklarowane błędy SOAP to te, które nie są określone w kontrakcie dla operacji. Ten temat ułatwia zidentyfikowanie tych warunków błędów i utworzenie kontraktu o błędach dla usługi, którego klienci mogą używać do prawidłowego obsługi tych warunków błędów podczas powiadamiania o niestandardowych błędach protokołu SOAP. Podstawowe zadania są następujące:  
  
1. Zdefiniuj warunki błędów, o których powinien wiedzieć klient usługi.  
  
2. Zdefiniuj niestandardową zawartość błędów SOAP dla tych warunków błędu.  
  
3. Oznacz operacje w taki sposób, aby określone błędy SOAP, które zgłaszają, zostały uwidocznione klientom w języku WSDL.  
  
### <a name="defining-error-conditions-that-clients-should-know-about"></a>Definiowanie warunków błędów, które powinny być znane klientom  

 Błędy protokołu SOAP są publicznie opisanymi komunikatami, które zawierają informacje o błędach dla określonej operacji. Ponieważ są one opisane wraz z innymi komunikatami operacji w języku WSDL, klienci znają i w związku z tym oczekują na obsługę takich błędów podczas wywoływania operacji. Jednak ponieważ usługi WCF są zapisywane w kodzie zarządzanym, decydując o tym, które warunki błędu w kodzie zarządzanym mają być konwertowane na błędy i zwracane do klienta, można oddzielić błędy i usterki w usłudze od formalnej rozmowy z błędami, które są dostępne dla klienta.  
  
 Na przykład poniższy kod ilustruje operację, która przyjmuje dwie liczby całkowite i zwraca kolejną liczbę całkowitą. W tym miejscu można zgłaszać kilka wyjątków, dlatego podczas projektowania kontraktu dotyczącego błędu należy określić, które warunki błędów są ważne dla klienta. W takim przypadku usługa powinna wykryć <xref:System.DivideByZeroException?displayProperty=nameWithType> wyjątek.  
  
```csharp  
[ServiceContract]  
public class CalculatorService  
{  
    [OperationContract]
    int Divide(int a, int b)  
    {  
      if (b==0) throw new Exception("Division by zero!");  
      return a/b;  
    }  
}  
```  
  
```vb
<ServiceContract> _
Public Class CalculatorService
    <OperationContract> _
    Public Function Divide(a As Integer, b As Integer) As Integer
        If b = 0 Then Throw New DivideByZeroException("Division by zero!")
        Return a / b
    End Function
End Class
```
  
 W poprzednim przykładzie operacja może zwrócić niestandardowy błąd protokołu SOAP, który jest specyficzny dla dzielenia przez zero, niestandardową usterkę, która jest specyficzna dla operacji matematycznych, ale zawiera informacje specyficzne dla dzielenia przez zero, wiele błędów dla kilku różnych sytuacji błędów lub Brak błędów protokołu SOAP.  
  
### <a name="define-the-content-of-error-conditions"></a>Zdefiniuj zawartość warunków błędów  

 Gdy warunek błędu został zidentyfikowany jako taki, który może zwrócić niestandardowy błąd protokołu SOAP, następnym krokiem jest zdefiniowanie zawartości tego błędu i upewnienie się, że struktura zawartości może być serializowana. Przykład kodu w poprzedniej sekcji zawiera błąd specyficzny dla `Divide` operacji, ale jeśli w usłudze istnieją inne operacje `Calculator` , wówczas pojedynczy niestandardowy błąd protokołu SOAP może poinformować klienta o wszystkich warunkach błędów kalkulatora, które zostały `Divide` uwzględnione. Poniższy przykład kodu pokazuje Tworzenie niestandardowego błędu protokołu SOAP, `MathFault` który może raportować błędy wykonywane przy użyciu wszystkich operacji matematycznych, w tym `Divide` . Chociaż Klasa może określać operację ( `Operation` Właściwość) i wartość opisującą problem ( `ProblemType` Właściwość), Klasa i te właściwości muszą być możliwe do serializacji, aby można je było przesłać do klienta w niestandardowym błędzie protokołu SOAP. W związku z <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> tym <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> atrybuty i są używane do serializacji typu i jego właściwości, jak to możliwe.  
  
 [!code-csharp[Faults#2](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#2)]
 [!code-vb[Faults#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#2)]  
  
 Aby uzyskać więcej informacji o tym, jak zapewnić możliwość serializacji danych, zobacz [określanie transfer danych w kontraktach usług](./feature-details/specifying-data-transfer-in-service-contracts.md). Aby zapoznać się z listą pomocy technicznej dotyczącej serializacji <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> , zobacz [Typy obsługiwane przez serializator kontraktu danych](./feature-details/types-supported-by-the-data-contract-serializer.md).  
  
### <a name="mark-operations-to-establish-the-fault-contract"></a>Oznaczanie operacji w celu ustalenia kontraktu dotyczącego usterek  

 Po zdefiniowaniu struktury danych do serializacji, która jest zwracana jako część niestandardowego błędu SOAP, ostatnim krokiem jest oznaczenie kontraktu operacji jako wyrzuca błąd protokołu SOAP tego typu. W tym celu należy użyć <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> atrybutu i przekazać typ utworzonego niestandardowego typu danych. Poniższy przykład kodu pokazuje, jak używać atrybutu, <xref:System.ServiceModel.FaultContractAttribute> Aby określić, że `Divide` operacja może zwrócić błąd protokołu SOAP typu `MathFault` . Inne operacje oparte na zapisie matematycznym mogą teraz również określać, że mogą zwrócić `MathFault` .  
  
 [!code-csharp[Faults#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#1)]
 [!code-vb[Faults#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#1)]  
  
 Operacja może określić, że zwraca więcej niż jeden błąd niestandardowy przez oznaczenie tej operacji z więcej niż jednym <xref:System.ServiceModel.FaultContractAttribute> atrybutem.  
  
 Następny krok, aby zaimplementować kontrakt błędu w implementacji operacji, został opisany w temacie [wysyłanie i otrzymywanie błędów](sending-and-receiving-faults.md).  
  
#### <a name="soap-wsdl-and-interoperability-considerations"></a>Zagadnienia dotyczące protokołu SOAP, WSDL i współdziałania  

 W niektórych sytuacjach, szczególnie w przypadku współdziałania z innymi platformami, może być ważne, aby kontrolować sposób, w jaki błąd pojawia się w komunikacie protokołu SOAP lub sposób opisywania w metadanych WSDL.  
  
 <xref:System.ServiceModel.FaultContractAttribute>Atrybut ma <xref:System.ServiceModel.FaultContractAttribute.Name%2A> Właściwość, która umożliwia kontrolowanie nazwy elementu błędu WSDL, która jest generowana w metadanych dla tego błędu.  
  
 Zgodnie ze standardem SOAP, błąd może mieć `Action` , a `Code` i `Reason` . `Action`Jest kontrolowana przez <xref:System.ServiceModel.FaultContractAttribute.Action%2A> Właściwość. <xref:System.ServiceModel.FaultException.Code%2A>Właściwość i <xref:System.ServiceModel.FaultException.Reason%2A> Właściwość są właściwościami <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> klasy, która jest klasą nadrzędną ogólnej <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> . `Code`Właściwość zawiera <xref:System.ServiceModel.FaultCode.SubCode%2A> element członkowski.  
  
 W przypadku uzyskiwania dostępu do usług, które generują błędy, istnieją pewne ograniczenia. Usługa WCF obsługuje tylko błędy ze szczegółowymi typami, które opisano w schemacie i są zgodne z kontraktami danych. Na przykład, jak wspomniano powyżej, WCF nie obsługuje błędów, które używają atrybutów XML w ich typach szczegółów lub błędy z więcej niż jednym elementem najwyższego poziomu w sekcji szczegółów.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [Określanie i obsługa błędów w kontraktach i usługach](specifying-and-handling-faults-in-contracts-and-services.md)
- [Wysyłanie i odbieranie błędów](sending-and-receiving-faults.md)
- [Instrukcje: Deklarowanie błędów w kontraktach usługi](how-to-declare-faults-in-service-contracts.md)
- [Omówienie poziomów ochrony](understanding-protection-level.md)
- [Instrukcje: Ustawianie właściwości ProtectionLevel](how-to-set-the-protectionlevel-property.md)
- [Określanie transferu danych w kontraktach usług](./feature-details/specifying-data-transfer-in-service-contracts.md)
