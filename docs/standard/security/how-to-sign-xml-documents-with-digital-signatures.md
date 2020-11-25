---
title: 'Instrukcje: Podpisywanie dokumentów XML za pomocą podpisów cyfrowych'
description: Dowiedz się, jak podpisywać dokumenty XML za pomocą podpisów cyfrowych. Użyj klas w przestrzeni nazw System.Security.Cryptography.Xml w programie .NET.
ms.date: 07/14/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- signatures, XML signing
- System.Security.Cryptography.SignedXml class
- digital signatures, XML signing
- System.Security.Cryptography.RSA class
- XML digital signatures
- XML signing
- signing XML
ms.assetid: 99692ac1-d8c9-42d7-b1bf-2737b01037e4
ms.openlocfilehash: 2cb63fd91b1aeb51c762975103ea665e0d8539b1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726681"
---
# <a name="how-to-sign-xml-documents-with-digital-signatures"></a>Instrukcje: Podpisywanie dokumentów XML za pomocą podpisów cyfrowych

Możesz użyć klas w <xref:System.Security.Cryptography.Xml> przestrzeni nazw, aby podpisać dokument XML lub część dokumentu XML z podpisem cyfrowym.  Podpisy cyfrowe XML (XMLDSIG) pozwalają sprawdzić, czy dane nie zostały zmienione po podpisaniu.  Aby uzyskać więcej informacji na temat standardu XMLDSIG, zobacz [składnia i przetwarzanie w formacie XML](https://www.w3.org/TR/xmldsig-core/)zalecenia dotyczące organizacja World Wide Web Consortium (W3C).  
  
> [!NOTE]
> Kod w tym artykule ma zastosowanie do systemu Windows.

Przykład kodu w tej procedurze pokazuje, jak cyfrowo podpisać cały dokument XML i dołączyć podpis do dokumentu w <`Signature`> elementu.  Przykład tworzy klucz podpisywania RSA, dodaje klucz do kontenera klucza zabezpieczeń, a następnie używa klucza do cyfrowego podpisywania dokumentu XML.  Następnie można pobrać klucz w celu zweryfikowania podpisu cyfrowego XML lub można go użyć do podpisania innego dokumentu XML.  
  
Aby uzyskać informacje na temat weryfikowania podpisu cyfrowego XML, który został utworzony przy użyciu tej procedury, zobacz [How to: Verify Digital Signatures of XML Documents](how-to-verify-the-digital-signatures-of-xml-documents.md).  
  
### <a name="to-digitally-sign-an-xml-document"></a>Aby podpisać cyfrowo dokument XML  
  
1. Utwórz <xref:System.Security.Cryptography.CspParameters> obiekt i określ nazwę kontenera kluczy.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToSignXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#2)]  
  
2. Generuj klucz asymetryczny przy użyciu <xref:System.Security.Cryptography.RSACryptoServiceProvider> klasy.  Klucz jest automatycznie zapisywany do kontenera kluczy podczas przekazywania <xref:System.Security.Cryptography.CspParameters> obiektu do konstruktora <xref:System.Security.Cryptography.RSACryptoServiceProvider> klasy.  Ten klucz będzie używany do podpisywania dokumentu XML.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToSignXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#3)]  
  
3. Utwórz <xref:System.Xml.XmlDocument> obiekt przez załadowanie pliku XML z dysku.  <xref:System.Xml.XmlDocument>Obiekt zawiera element XML do zaszyfrowania.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToSignXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#4)]  
  
4. Utwórz nowy <xref:System.Security.Cryptography.Xml.SignedXml> obiekt i przekaż <xref:System.Xml.XmlDocument> do niego obiekt.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToSignXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#5)]  
  
5. Dodaj podpis klucza RSA do <xref:System.Security.Cryptography.Xml.SignedXml> obiektu.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToSignXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#6)]  
  
6. Utwórz obiekt opisujący <xref:System.Security.Cryptography.Xml.Reference> elementy do podpisania.  Aby podpisać cały dokument, należy ustawić <xref:System.Security.Cryptography.Xml.Reference.Uri%2A> Właściwość na `""` .  
  
     [!code-csharp[HowToSignXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToSignXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#7)]  
  
7. Dodaj <xref:System.Security.Cryptography.Xml.XmlDsigEnvelopedSignatureTransform> obiekt do <xref:System.Security.Cryptography.Xml.Reference> obiektu.  Przekształcenie umożliwia weryfikatorowi reprezentowania danych XML w taki sam sposób, w jaki użyto osoby podpisującej.  Dane XML mogą być reprezentowane na różne sposoby, więc ten krok jest niezbędny do weryfikacji.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToSignXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#8)]  
  
8. Dodaj <xref:System.Security.Cryptography.Xml.Reference> obiekt do <xref:System.Security.Cryptography.Xml.SignedXml> obiektu.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#9)]
     [!code-vb[HowToSignXMLDocumentRSA#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#9)]  
  
9. Oblicz podpis, wywołując <xref:System.Security.Cryptography.Xml.SignedXml.ComputeSignature%2A> metodę.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#10)]
     [!code-vb[HowToSignXMLDocumentRSA#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#10)]  
  
10. Pobierz reprezentację XML sygnatury (<`Signature` elementu>) i Zapisz ją w nowym <xref:System.Xml.XmlElement> obiekcie.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#11)]
     [!code-vb[HowToSignXMLDocumentRSA#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#11)]  
  
11. Dołącz element do <xref:System.Xml.XmlDocument> obiektu.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#12)]
     [!code-vb[HowToSignXMLDocumentRSA#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#12)]  
  
12. Zapisz dokument.  
  
     [!code-csharp[HowToSignXMLDocumentRSA#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#13)]
     [!code-vb[HowToSignXMLDocumentRSA#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#13)]  
  
## <a name="example"></a>Przykład  

 W tym przykładzie przyjęto założenie, że plik o nazwie `test.xml` istnieje w tym samym katalogu co skompilowany program.  Można umieścić następujący kod XML w pliku o nazwie `test.xml` i użyć go w tym przykładzie.  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToSignXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#1)]
 [!code-vb[HowToSignXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
  
- W projekcie, który jest przeznaczony dla .NET Framework, należy dołączyć odwołanie do `System.Security.dll` .

- W projekcie przeznaczonym dla platformy .NET Core lub .NET 5 Zainstaluj pakiet NuGet [System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml).
  
- Uwzględnij następujące przestrzenie nazw: <xref:System.Xml> , <xref:System.Security.Cryptography> , i <xref:System.Security.Cryptography.Xml> .  
  
## <a name="net-security"></a>Zabezpieczenia platformy .NET

Nigdy nie przechowuj ani nie przesyłaj klucza prywatnego pary kluczy asymetrycznych w postaci zwykłego tekstu.  Aby uzyskać więcej informacji na temat symetrycznych i asymetrycznych kluczy kryptograficznych, zobacz [generowanie kluczy do szyfrowania i odszyfrowywania](generating-keys-for-encryption-and-decryption.md).  
  
Nie osadzaj klucza prywatnego bezpośrednio w kodzie źródłowym.  Klucze osadzone można łatwo odczytywać z zestawu przy użyciu [Ildasm.exe (Il dezasembler)](../../framework/tools/ildasm-exe-il-disassembler.md) lub otwierając zestaw w edytorze tekstu, takim jak Notatnik.  
  
## <a name="see-also"></a>Zobacz także

- [Model kryptografii](cryptography-model.md)
- [Usługi kryptograficzne](cryptographic-services.md)
- [Kryptografia międzyplatformowa](cross-platform-cryptography.md)
- <xref:System.Security.Cryptography.Xml>
- [Instrukcje: Sprawdzanie podpisów cyfrowych w dokumentach XML](how-to-verify-the-digital-signatures-of-xml-documents.md)
- [Ochrona danych ASP.NET Core](/aspnet/core/security/data-protection/introduction)
