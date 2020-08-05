---
title: Podpisy kryptograficzne
ms.date: 07/14/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- digital signatures
- cryptography [.NET], signatures
- digital signatures, XML signing
- signatures, cryptographic
- digital signatures, generating
- verifying signatures
- generating signatures
- digital signatures, about
- encryption [.NET], signatures
- security [.NET], signatures
- XML signing
- digital signatures, verifying
- signing XML
ms.assetid: aa87cb7f-e608-4a81-948b-c9b8a1225783
ms.openlocfilehash: ce2be1d509da4e399bf87e1c8df7ba061fc2707c
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557011"
---
# <a name="cryptographic-signatures"></a>Podpisy kryptograficzne

Kryptograficzne podpisy cyfrowe korzystają z algorytmów kluczy publicznych w celu zapewnienia integralności danych. Po podpisaniu danych za pomocą podpisu cyfrowego ktoś inny może zweryfikować podpis i może udowodnić, że dane pochodzą od Ciebie i nie zostały zmienione po podpisaniu. Aby uzyskać więcej informacji na temat podpisów cyfrowych, zobacz [usługi kryptograficzne](cryptographic-services.md).

W tym temacie wyjaśniono, jak generować i weryfikować podpisy cyfrowe przy użyciu klas w <xref:System.Security.Cryptography> przestrzeni nazw.

## <a name="generating-signatures"></a>Generowanie podpisów

Podpisy cyfrowe są zwykle stosowane do wartości skrótu, które reprezentują większe dane. Poniższy przykład stosuje podpis cyfrowy do wartości skrótu. Najpierw tworzone jest nowe wystąpienie <xref:System.Security.Cryptography.RSA> klasy w celu wygenerowania pary kluczy publicznych/prywatnych. Następnie <xref:System.Security.Cryptography.RSA> jest przenoszona do nowego wystąpienia <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> klasy. Spowoduje to przeniesienie klucza prywatnego do programu <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> , co w rzeczywistości wykonuje podpis cyfrowy. Przed podpisaniem kodu skrótu należy określić algorytm wyznaczania wartości skrótu. W tym przykładzie zastosowano algorytm SHA1. Na koniec <xref:System.Security.Cryptography.AsymmetricSignatureFormatter.CreateSignature%2A> Metoda jest wywoływana w celu przeprowadzenia podpisywania.

Ze względu na kolizje problemów z algorytmem SHA1 zalecamy SHA256 lub lepszą.

```vb
Imports System.Security.Cryptography

Module Module1
    Sub Main()
        'The hash value to sign.
        Dim hashValue As Byte() = {59, 4, 248, 102, 77, 97, 142, 201, 210, 12, 224, 93, 25, 41, 100, 197, 213, 134, 130, 135}

        'The value to hold the signed value.
        Dim signedHashValue() As Byte

        'Generate a public/private key pair.
        Dim rsa As RSA = RSA.Create()

        'Create an RSAPKCS1SignatureFormatter object and pass it
        'the RSA instance to transfer the private key.
        Dim rsaFormatter As New RSAPKCS1SignatureFormatter(rsa)

        'Set the hash algorithm to SHA1.
        rsaFormatter.SetHashAlgorithm("SHA1")

        'Create a signature for hashValue and assign it to
        'signedHashValue.
        signedHashValue = rsaFormatter.CreateSignature(hashValue)
    End Sub
End Module
```

```csharp
using System;
using System.Security.Cryptography;

class Class1
{
   static void Main()
   {
      //The hash value to sign.
      byte[] hashValue = {59,4,248,102,77,97,142,201,210,12,224,93,25,41,100,197,213,134,130,135};

      //The value to hold the signed value.
      byte[] signedHashValue;

      //Generate a public/private key pair.
      RSA rsa = RSA.Create();

      //Create an RSAPKCS1SignatureFormatter object and pass it the
      //RSA instance to transfer the private key.
      RSAPKCS1SignatureFormatter rsaFormatter = new RSAPKCS1SignatureFormatter(rsa);

      //Set the hash algorithm to SHA1.
      rsaFormatter.SetHashAlgorithm("SHA1");

      //Create a signature for hashValue and assign it to
      //signedHashValue.
      signedHashValue = rsaFormatter.CreateSignature(hashValue);
   }
}
```

## <a name="verifying-signatures"></a>Weryfikowanie podpisów

Aby sprawdzić, czy dane zostały podpisane przez określoną stronę, musisz dysponować następującymi informacjami:

- Klucz publiczny podmiotu, który podpisał dane.

- Podpis cyfrowy.

- Dane, które zostały podpisane.

- Algorytm wyznaczania wartości skrótu używany przez program podpisujący.

Aby sprawdzić podpis podpisany przez <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> klasę, użyj <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> klasy. <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter>Klasa musi być dostarczona z kluczem publicznym osoby podpisującej. W przypadku algorytmu RSA do określenia klucza publicznego będą potrzebne wartości z modułu i wykładnika. (Strona, która wygenerowała parę kluczy publiczny/prywatny powinna podawać te wartości). Najpierw Utwórz <xref:System.Security.Cryptography.RSA> obiekt przechowujący klucz publiczny, który będzie weryfikować podpis, a następnie zainicjuj <xref:System.Security.Cryptography.RSAParameters> strukturę do wartości modulo i wykładnik, które określają klucz publiczny.

Poniższy kod przedstawia tworzenie <xref:System.Security.Cryptography.RSAParameters> struktury. `Modulus`Właściwość jest ustawiona na wartość tablicy bajtowej o nazwie `modulusData` i `Exponent` Właściwość jest ustawiona na wartość tablicy bajtowej o nazwie `exponentData` .

```vb
Dim rsaKeyInfo As RSAParameters
rsaKeyInfo.Modulus = modulusData
rsaKeyInfo.Exponent = exponentData
```

```csharp
RSAParameters rsaKeyInfo;
rsaKeyInfo.Modulus = modulusData;
rsaKeyInfo.Exponent = exponentData;
```

Po utworzeniu <xref:System.Security.Cryptography.RSAParameters> obiektu można zainicjować nowe wystąpienie <xref:System.Security.Cryptography.RSA> klasy implementacji do wartości określonych w <xref:System.Security.Cryptography.RSAParameters> . <xref:System.Security.Cryptography.RSA>Wystąpienie jest z kolei przekazywane do konstruktora elementu, <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> Aby przetransferować klucz.

Poniższy przykład ilustruje ten proces. W tym przykładzie `hashValue` i `signedHashValue` są tablicami bajtów dostarczanych przez stronę zdalną. Strona zdalna podpisała `hashValue` przy użyciu algorytmu SHA1, generując podpis cyfrowy `signedHashValue` . <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter.VerifySignature%2A?displayProperty=nameWithType>Metoda weryfikuje, czy podpis cyfrowy jest prawidłowy i został użyty do podpisania `hashValue` .

Ze względu na kolizje problemów z algorytmem SHA1 zalecamy SHA256 lub lepszą.  Jeśli jednak do utworzenia podpisu użyto algorytmu SHA1, należy użyć algorytmu SHA1 do zweryfikowania podpisu.

```vb
Dim rsa As RSA = RSA.Create()
rsa.ImportParameters(rsaKeyInfo)
Dim rsaDeformatter As New RSAPKCS1SignatureDeformatter(rsa)
rsaDeformatter.SetHashAlgorithm("SHA1")
If rsaDeformatter.VerifySignature(hashValue, signedHashValue) Then
   Console.WriteLine("The signature is valid.")
Else
   Console.WriteLine("The signature is not valid.")
End If
```

```csharp
RSA rsa = RSA.Create();
rsa.ImportParameters(rsaKeyInfo);
RSAPKCS1SignatureDeformatter rsaDeformatter = new RSAPKCS1SignatureDeformatter(rsa);
rsaDeformatter.SetHashAlgorithm("SHA1");
if(rsaDeformatter.VerifySignature(hashValue, signedHashValue))
{
   Console.WriteLine("The signature is valid.");
}
else
{
   Console.WriteLine("The signature is not valid.");
}
```

W tym fragmencie kodu zostanie wyświetlony element " `The signature is valid` ", jeśli sygnatura jest prawidłowa i " `The signature is not valid` ", jeśli nie jest.

## <a name="see-also"></a>Zobacz też

- [Usługi kryptograficzne](cryptographic-services.md)
- [Model kryptografii](cryptography-model.md)
- [Kryptografia międzyplatformowa](cross-platform-cryptography.md)
- [Ochrona danych ASP.NET Core](/aspnet/core/security/data-protection/introduction)
