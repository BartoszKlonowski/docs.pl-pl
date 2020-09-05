---
ms.openlocfilehash: 5c8ea3565fbe599dd53a71ba8bd339704f7d7f8a
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497364"
---
### <a name="signedxml-and-encryptedxml-breaking-changes"></a><span data-ttu-id="788b1-101">Zmiany SignedXml i EncryptedXml</span><span class="sxs-lookup"><span data-stu-id="788b1-101">SignedXml and EncryptedXml Breaking Changes</span></span>

#### <a name="details"></a><span data-ttu-id="788b1-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="788b1-102">Details</span></span>

<span data-ttu-id="788b1-103">W .NET Framework 4.6.2, poprawki zabezpieczeń w <xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=fullName> i <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=fullName> prowadzą do różnych zachowań w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="788b1-103">In .NET Framework 4.6.2, Security fixes in <xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=fullName> and <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=fullName> lead to different run-time behaviors.</span></span> <span data-ttu-id="788b1-104">Przykład:</span><span class="sxs-lookup"><span data-stu-id="788b1-104">For example,</span></span><ul><li><span data-ttu-id="788b1-105">Jeśli dokument ma wiele elementów z tym samym <code>id</code> atrybutem, a podpis jednego z tych elementów jako element główny podpisu, dokument będzie teraz traktowany jako nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="788b1-105">If a document has multiple elements with the same <code>id</code> attribute and a signature targets one of those elements as the root of the signature, the document will now be considered invalid.</span></span></li><li><span data-ttu-id="788b1-106">Dokumenty używające niekanonicznych algorytmów transformacji XPath w odwołaniach są teraz uznawane za nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="788b1-106">Documents using non-canonical XPath transform algorithms in references are now considered invalid.</span></span></li><li><span data-ttu-id="788b1-107">Dokumenty korzystające z algorytmów transformacji XSLT inne niż kanoniczne w odwołaniach są teraz traktowane jako nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="788b1-107">Documents using non-canonical XSLT transform algorithms in references are now consider invalid.</span></span></li><li><span data-ttu-id="788b1-108">Nie będzie można wykonać żadnego programu korzystającego z odłączonych podpisów zasobów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="788b1-108">Any program making use of external resource detached signatures will be unable to do so.</span></span></li></ul>

#### <a name="suggestion"></a><span data-ttu-id="788b1-109">Sugestia</span><span class="sxs-lookup"><span data-stu-id="788b1-109">Suggestion</span></span>

<span data-ttu-id="788b1-110">Deweloperzy mogą chcieć przejrzeć użycie <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> i <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> , jak również typy pochodne od momentu, gdy <xref:System.Security.Cryptography.Xml.Transform> odbiorca dokumentu może nie być w stanie go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="788b1-110">Developers might want to review the usage of <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> and <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform>, as well as types derived from <xref:System.Security.Cryptography.Xml.Transform> since a document receiver may not be able to process it.</span></span>

| <span data-ttu-id="788b1-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="788b1-111">Name</span></span>    | <span data-ttu-id="788b1-112">Wartość</span><span class="sxs-lookup"><span data-stu-id="788b1-112">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="788b1-113">Zakres</span><span class="sxs-lookup"><span data-stu-id="788b1-113">Scope</span></span>   |<span data-ttu-id="788b1-114">Mały</span><span class="sxs-lookup"><span data-stu-id="788b1-114">Minor</span></span>|
|<span data-ttu-id="788b1-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="788b1-115">Version</span></span>|<span data-ttu-id="788b1-116">4.6.2</span><span class="sxs-lookup"><span data-stu-id="788b1-116">4.6.2</span></span>|
|<span data-ttu-id="788b1-117">Typ</span><span class="sxs-lookup"><span data-stu-id="788b1-117">Type</span></span>|<span data-ttu-id="788b1-118">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="788b1-118">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="788b1-119">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="788b1-119">Affected APIs</span></span>

- <xref:System.Security.Cryptography.Xml.Transform?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Xml.XmlDsigXPathTransform?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform?displayProperty=nameWithType>

<!--

#### Affected APIs

- `T:System.Security.Cryptography.Xml.Transform`
- `T:System.Security.Cryptography.Xml.XmlDsigXPathTransform`
- `T:System.Security.Cryptography.Xml.XmlDsigXsltTransform`

-->
