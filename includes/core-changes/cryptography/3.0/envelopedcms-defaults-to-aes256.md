---
ms.openlocfilehash: e0cdcce9b8c7d591925b08635e3354dadaf22b7b
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87556033"
---
### <a name="envelopedcms-defaults-to-aes-256-encryption"></a><span data-ttu-id="39018-101">EnvelopedCms domyślnie szyfrowanie AES-256</span><span class="sxs-lookup"><span data-stu-id="39018-101">EnvelopedCms defaults to AES-256 encryption</span></span>

<span data-ttu-id="39018-102">Domyślny algorytm szyfrowania symetrycznego używany przez program `EnvelopedCms` został zmieniony z TripleDES na AES-256.</span><span class="sxs-lookup"><span data-stu-id="39018-102">The default symmetric encryption algorithm used by `EnvelopedCms` has changed from TripleDES to AES-256.</span></span>

#### <a name="change-description"></a><span data-ttu-id="39018-103">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="39018-103">Change description</span></span>

<span data-ttu-id="39018-104">W poprzednich wersjach, gdy <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> jest używany do szyfrowania danych bez określania algorytmu szyfrowania symetrycznego za pośrednictwem przeciążenia konstruktora, dane są szyfrowane przy użyciu algorytmu TripleDES/3DES/3DEA/DES3-Ede.</span><span class="sxs-lookup"><span data-stu-id="39018-104">In previous versions, when <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> is used to encrypt data without specifying a symmetric encryption algorithm via a constructor overload, the data is encrypted with the TripleDES/3DES/3DEA/DES3-EDE algorithm.</span></span>

<span data-ttu-id="39018-105">Począwszy od platformy .NET Core 3,0 (za pośrednictwem wersji 4.6.0 pakietu NuGet [System. Security. Cryptography. PKCS](https://www.nuget.org/packages/System.Security.Cryptography.Pkcs/) ), domyślny algorytm został zmieniony na AES-256 na potrzeby modernizacji algorytmu oraz w celu poprawy bezpieczeństwa opcji domyślnych.</span><span class="sxs-lookup"><span data-stu-id="39018-105">Starting with .NET Core 3.0 (via version 4.6.0 of the [System.Security.Cryptography.Pkcs](https://www.nuget.org/packages/System.Security.Cryptography.Pkcs/) NuGet package), the default algorithm has been changed to AES-256 for algorithm modernization and to improve the security of default options.</span></span> <span data-ttu-id="39018-106">Jeśli certyfikat odbiorcy wiadomości ma klucz publiczny (poza EC), operacja szyfrowania może zakończyć się niepowodzeniem z <xref:System.Security.Cryptography.CryptographicException> powodu ograniczeń na platformie podstawowej.</span><span class="sxs-lookup"><span data-stu-id="39018-106">If a message recipient certificate has a (non-EC) Diffie-Hellman public key, the encryption operation may fail with a <xref:System.Security.Cryptography.CryptographicException> due to limitations in the underlying platform.</span></span>

<span data-ttu-id="39018-107">W poniższym przykładowym kodzie dane są szyfrowane przy użyciu TripleDES w przypadku uruchamiania na platformie .NET Core 2,2 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="39018-107">In the following sample code, the data is encrypted with TripleDES if running on .NET Core 2.2 or earlier.</span></span> <span data-ttu-id="39018-108">W przypadku uruchamiania w środowisku .NET Core 3,0 lub nowszym jest on szyfrowany przy użyciu algorytmu AES-256.</span><span class="sxs-lookup"><span data-stu-id="39018-108">If running on .NET Core 3.0 or later, it's encrypted with AES-256.</span></span>

```csharp
EnvelopedCms cms = new EnvelopedCms(content);
cms.Encrypt(recipient);
return cms.Encode();
```

#### <a name="version-introduced"></a><span data-ttu-id="39018-109">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="39018-109">Version introduced</span></span>

<span data-ttu-id="39018-110">3.0</span><span class="sxs-lookup"><span data-stu-id="39018-110">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="39018-111">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="39018-111">Recommended action</span></span>

<span data-ttu-id="39018-112">Jeśli zmiana ma negatywny wpływ na zmiany, można przywrócić szyfrowanie TripleDES przez jawne określenie identyfikatora algorytmu szyfrowania w <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> konstruktorze, który zawiera parametr typu <xref:System.Security.Cryptography.Pkcs.AlgorithmIdentifier> , taki jak:</span><span class="sxs-lookup"><span data-stu-id="39018-112">If you are negatively impacted by the change, you can restore TripleDES encryption by explicitly specifying the encryption algorithm identifier in an <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> constructor that includes a parameter of type <xref:System.Security.Cryptography.Pkcs.AlgorithmIdentifier>, such as:</span></span>

```csharp
Oid tripleDesOid = new Oid("1.2.840.113549.3.7", null);
AlgorithmIdentifier tripleDesIdentifier = new AlgorithmIdentifier(tripleDesOid);
EnvelopedCms cms = new EnvelopedCms(content, tripleDesIdentifier);

cms.Encrypt(recipient);
return cms.Encode()l
```

#### <a name="category"></a><span data-ttu-id="39018-113">Kategoria</span><span class="sxs-lookup"><span data-stu-id="39018-113">Category</span></span>

<span data-ttu-id="39018-114">Kryptografia</span><span class="sxs-lookup"><span data-stu-id="39018-114">Cryptography</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="39018-115">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="39018-115">Affected APIs</span></span>

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor>
- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.ContentInfo)>
- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.SubjectIdentifierType,System.Security.Cryptography.Pkcs.ContentInfo)>

<!--

#### Affected APIs

- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.#ctor`
- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.#ctor(System.Security.Cryptography.Pkcs.ContentInfo)`
- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.SubjectIdentifierType,System.Security.Cryptography.Pkcs.ContentInfo)`

-->
