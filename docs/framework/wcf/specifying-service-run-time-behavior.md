---
title: Określanie zachowania środowiska uruchomieniowego usługi
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5c5450ea-6af1-4b75-a267-613d0ac54707
ms.openlocfilehash: 61c3b8ebd431c3a16475342984b463d5f8842a89
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235886"
---
# <a name="specifying-service-run-time-behavior"></a>Określanie zachowania środowiska uruchomieniowego usługi

Po zaprojektowaniu kontraktu usługi ([Projektowanie kontraktów usług](designing-service-contracts.md)) i zaimplementowaniu kontraktu dotyczącego usługi ([implementowanie kontraktów usług](implementing-service-contracts.md)) można skonfigurować zachowanie operacji dla środowiska uruchomieniowego usługi. W tym temacie omówiono zachowania usługi i działania udostępniane przez system oraz opisano, gdzie znaleźć więcej informacji na potrzeby tworzenia nowych zachowań. Niektóre zachowania są stosowane jako atrybuty, ale wiele są stosowane przy użyciu pliku konfiguracyjnego aplikacji lub programowo. Aby uzyskać więcej informacji na temat konfigurowania aplikacji usługi, zobacz [Konfigurowanie usług](configuring-services.md).  
  
## <a name="overview"></a>Omówienie  

 Kontrakt definiuje dane wejściowe, dane wyjściowe, typy danych i możliwości usługi tego typu. Implementacja kontraktu usługi tworzy klasę, która w przypadku skonfigurowania powiązania pod adresem spełnia kontrakt, który implementuje. Informacje o umowie, powiązaniu i adresie są znane przez klienta; bez nich klient nie może korzystać z usługi.  
  
 Jednak specyficzne dla operacji, takie jak problemy z wątkiem lub Zarządzanie wystąpieniami, są nieprzezroczyste dla klientów. Po wdrożeniu kontraktu usługi można skonfigurować dużą liczbę cech operacji przy użyciu *zachowań*. Zachowania są obiektami modyfikującymi środowisko uruchomieniowe Windows Communication Foundation (WCF) przez ustawienie właściwości środowiska uruchomieniowego lub wstawienie typu dostosowania do środowiska uruchomieniowego. Aby uzyskać więcej informacji na temat modyfikowania środowiska uruchomieniowego przez tworzenie zachowań zdefiniowanych przez użytkownika, zobacz [Rozszerzanie elementu ServiceHost i warstwy modelu usług](./extending/extending-servicehost-and-the-service-model-layer.md).  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType>Atrybuty i <xref:System.ServiceModel.OperationBehaviorAttribute?displayProperty=nameWithType> są najczęściej przydatne zachowania i uwidaczniają najczęściej żądaną funkcję operacji. Ponieważ są to atrybuty, należy je zastosować do implementacji usługi lub operacji. Inne zachowania, takie jak <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> lub <xref:System.ServiceModel.Description.ServiceDebugBehavior?displayProperty=nameWithType> , są zwykle stosowane przy użyciu pliku konfiguracyjnego aplikacji, chociaż można ich programowo używać.  
  
 Ten temat zawiera omówienie <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> atrybutów i, opis różnych zakresów, w których mogą działać zachowania, oraz Krótki opis wielu zachowań zapewnianych przez system w różnych zakresach, które mogą być przydatne dla deweloperów programu WCF.  
  
## <a name="servicebehaviorattribute-and-operationbehaviorattribute"></a>ServiceBehaviorAttribute i OperationBehaviorAttribute będący  

 Najważniejszymi zachowaniami są <xref:System.ServiceModel.ServiceBehaviorAttribute> atrybuty i <xref:System.ServiceModel.OperationBehaviorAttribute> , których można użyć do sterowania:  
  
- Okresy istnienia wystąpienia  
  
- Obsługa współbieżności i synchronizacji  
  
- Zachowanie konfiguracji  
  
- Zachowanie transakcji  
  
- Zachowanie serializacji  
  
- Przekształcanie metadanych  
  
- Okres istnienia sesji  
  
- Filtrowanie adresów i przetwarzanie nagłówka  
  
- Personifikacja  
  
- Aby użyć tych atrybutów, należy oznaczyć implementację usługi lub operacji przy użyciu atrybutu właściwego dla tego zakresu i ustawić właściwości. Na przykład poniższy kod ilustruje implementację operacji, która używa <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A?displayProperty=nameWithType> właściwości, aby wymagać od wywołujących tej operacji personifikacji.  
  
 [!code-csharp[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/operationbehaviorattribute_impersonation/cs/services.cs#1)]
 [!code-vb[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationbehaviorattribute_impersonation/vb/services.vb#1)]  
  
 Wiele właściwości wymaga dodatkowego wsparcia dla powiązania. Na przykład operacja wymagająca transakcji od klienta musi być skonfigurowana do użycia powiązania, które obsługuje przepływy transakcji.  
  
### <a name="well-known-singleton-services"></a>Well-Known pojedynczych usług  

 Atrybutów i można użyć <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> do kontrolowania określonych okresów istnienia, obu <xref:System.ServiceModel.InstanceContext> i obiektów usługi, które implementują operacje.  
  
 Na przykład <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> Właściwość określa, jak często <xref:System.ServiceModel.InstanceContext> jest wydawany, oraz <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> właściwości i <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=nameWithType> kontroluje czas wydania obiektu usługi.  
  
 Można jednak również utworzyć obiekt usługi samodzielnie i utworzyć hosta usługi za pomocą tego obiektu. W tym celu należy również ustawić <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> Właściwość na <xref:System.ServiceModel.InstanceContextMode.Single> lub wyjątek jest zgłaszany podczas otwierania hosta usługi.  
  
 Użyj <xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29> konstruktora, aby utworzyć taką usługę. Jest to alternatywa dla wdrożenia niestandardowego, <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=nameWithType> gdy chcesz podać konkretne wystąpienie obiektu do użycia przez pojedynczą usługę. Można użyć tego przeciążenia, gdy typ implementacji usługi jest trudny do skonstruowania (na przykład, jeśli nie implementuje konstruktora publicznego bez parametrów).
  
 Należy pamiętać, że gdy obiekt jest dostarczany do tego konstruktora, niektóre funkcje związane z zachowaniem wystąpienia Windows Communication Foundation (WCF) działają inaczej. Na przykład wywoływanie nie <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=nameWithType> ma wpływu, gdy jest podane dobrze znane wystąpienie obiektu. Podobnie wszystkie inne mechanizmy zwalniania wystąpień są ignorowane. <xref:System.ServiceModel.ServiceHost>Klasa zawsze zachowuje się tak, jakby <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> Właściwość została ustawiona na <xref:System.ServiceModel.ReleaseInstanceMode.None?displayProperty=nameWithType> dla wszystkich operacji.  
  
## <a name="other-service-endpoint-contract-and-operation-behaviors"></a>Inne zachowania usługi, punktu końcowego, kontraktu i operacji  

 Zachowania usługi, takie jak <xref:System.ServiceModel.ServiceBehaviorAttribute> atrybut, działają w całej usłudze. Na przykład, jeśli ustawisz <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> Właściwość na, <xref:System.ServiceModel.ConcurrencyMode.Multiple?displayProperty=nameWithType> musisz obsługiwać problemy z synchronizacją wątków w ramach każdej operacji w tej usłudze. Zachowania punktu końcowego działają w punkcie końcowym; wiele zachowań punktu końcowego dostarczonych przez system dotyczy funkcjonalności klienta. Zachowania kontraktów działają na poziomie kontraktu, a zachowania operacji modyfikują dostarczanie operacji.  
  
 Wiele z tych zachowań jest implementowanych na atrybutach i są używane w miarę jak <xref:System.ServiceModel.ServiceBehaviorAttribute> <xref:System.ServiceModel.OperationBehaviorAttribute> atrybuty i — przez zastosowanie ich do odpowiedniej klasy usług lub implementacji operacji. Inne zachowania, takie jak <xref:System.ServiceModel.Description.ServiceMetadataBehavior> obiekty lub <xref:System.ServiceModel.Description.ServiceDebugBehavior> , są zwykle stosowane przy użyciu pliku konfiguracyjnego aplikacji, chociaż mogą być również używane programowo.  
  
 Na przykład publikacja metadanych jest konfigurowana za pomocą <xref:System.ServiceModel.Description.ServiceMetadataBehavior> obiektu. Poniższy plik konfiguracyjny aplikacji przedstawia najbardziej typowe użycie.  
  
 [!code-xml[ServiceMetadataBehavior#1](../../../samples/snippets/csharp/VS_Snippets_CFX/servicemetadatabehavior/cs/hostapplication.exe.config#1)]  
  
 W poniższych sekcjach opisano wiele najbardziej przydatnych zachowań dostarczonych przez system, których można użyć do modyfikacji dostarczania usługi lub klienta w czasie wykonywania. Zapoznaj się z tematem referencyjnym, aby określić, jak korzystać z każdej z nich.  
  
### <a name="service-behaviors"></a>Zachowania usługi  

 Poniższe zachowania działają na usługach.  
  
- <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>. Zastosowano do usługi WCF, aby wskazać, czy ta usługa może być uruchamiana w trybie zgodności ASP.NET.  
  
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. Kontroluje sposób, w jaki usługa autoryzuje oświadczenia klienta.  
  
- <xref:System.ServiceModel.Description.ServiceCredentials>. Konfiguruje poświadczenia usługi. Użyj tej klasy, aby określić poświadczenia dla usługi, takie jak certyfikat X. 509.  
  
- <xref:System.ServiceModel.Description.ServiceDebugBehavior>. Włącza debugowanie i funkcje informacji pomocy dla usługi WCF.  
  
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>. Kontroluje publikację metadanych usługi i skojarzonych z nią informacji.  
  
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>. Określa zachowanie inspekcji zdarzeń zabezpieczeń.  
  
- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>. Konfiguruje ustawienia przepływności w czasie wykonywania, które umożliwiają dostosowanie wydajności usługi.  
  
### <a name="endpoint-behaviors"></a>Zachowania punktu końcowego  

 Poniższe zachowania działają na punktach końcowych. Wiele z tych zachowań jest używanych w aplikacjach klienckich.  
  
- <xref:System.ServiceModel.CallbackBehaviorAttribute>. Konfiguruje implementację usługi wywołania zwrotnego w aplikacji klienckiej dupleksowej.  
  
- <xref:System.ServiceModel.Description.CallbackDebugBehavior>. Włącza debugowanie usługi dla obiektu wywołania zwrotnego WCF.  
  
- <xref:System.ServiceModel.Description.ClientCredentials>. Umożliwia użytkownikowi skonfigurowanie poświadczeń klienta i usługi oraz ustawień uwierzytelniania poświadczeń usługi, które mają być używane na komputerze klienckim.  
  
- <xref:System.ServiceModel.Description.ClientViaBehavior>. Używane przez klientów do określania Uniform Resource Identifier (URI), dla których należy utworzyć kanał transportu.  
  
- <xref:System.ServiceModel.Description.MustUnderstandBehavior>. Nakazuje programowi WCF wyłączenie `MustUnderstand` przetwarzania.  
  
- <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>. Powoduje, że środowisko uruchomieniowe będzie używać synchronicznego procesu odbierania dla kanałów.  
  
- <xref:System.ServiceModel.Description.TransactedBatchingBehavior>. Optymalizuje operacje odbioru dla transportów, które obsługują odbieranie transakcyjne.  
  
### <a name="contract-behaviors"></a>Zachowania kontraktów  

 <xref:System.ServiceModel.DeliveryRequirementsAttribute>. Określa wymagania funkcji, które powiązania muszą zapewnić dla implementacji usługi lub klienta.  
  
### <a name="operation-behaviors"></a>Zachowania operacji  

 Poniższe zachowania operacji określają serializacji i kontroli transakcji dla operacji.  
  
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>. Reprezentuje zachowanie w czasie wykonywania <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> .  
  
- <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>. Kontroluje zachowanie w czasie wykonywania `XmlSerializer` i kojarzy je z operacją.  
  
- <xref:System.ServiceModel.TransactionFlowAttribute>. Określa poziom, w którym operacja usługi akceptuje Nagłówek transakcji.  
  
## <a name="see-also"></a>Zobacz też

- [Konfigurowanie usług](configuring-services.md)
- [Instrukcje: tworzenie wystąpienia usługi kontroli](./feature-details/how-to-control-service-instancing.md)
