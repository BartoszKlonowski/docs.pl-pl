---
ms.openlocfilehash: dfa8235fcfd868b80d3a610bddb492899519e289
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009071"
---
### <a name="xml-parsing-changes"></a><span data-ttu-id="74941-101">Zmiany analizy XML</span><span class="sxs-lookup"><span data-stu-id="74941-101">XML parsing changes</span></span>

| <span data-ttu-id="74941-102">Nazwa</span><span class="sxs-lookup"><span data-stu-id="74941-102">Name</span></span>    | <span data-ttu-id="74941-103">Wartość</span><span class="sxs-lookup"><span data-stu-id="74941-103">Value</span></span>   |
|:--------|:--------|
| <span data-ttu-id="74941-104">Zakres</span><span class="sxs-lookup"><span data-stu-id="74941-104">Scope</span></span>   | <span data-ttu-id="74941-105">Mały</span><span class="sxs-lookup"><span data-stu-id="74941-105">Minor</span></span>   |
| <span data-ttu-id="74941-106">Wersja</span><span class="sxs-lookup"><span data-stu-id="74941-106">Version</span></span> | <span data-ttu-id="74941-107">4.5.2</span><span class="sxs-lookup"><span data-stu-id="74941-107">4.5.2</span></span>   |
| <span data-ttu-id="74941-108">Typ</span><span class="sxs-lookup"><span data-stu-id="74941-108">Type</span></span>    | <span data-ttu-id="74941-109">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="74941-109">Runtime</span></span> |

#### <a name="details"></a><span data-ttu-id="74941-110">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="74941-110">Details</span></span>

<span data-ttu-id="74941-111">Ze względów bezpieczeństwa wprowadzono następujące zmiany w interfejsach API analizy XML:</span><span class="sxs-lookup"><span data-stu-id="74941-111">For security reasons, the following changes were introduced into XML parsing APIS:</span></span>

- <span data-ttu-id="74941-112"><xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=nameWithType> jest ustawiony na 10 000 000, gdy <xref:System.Xml.XmlReaderSettings> jest zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="74941-112"><xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=nameWithType> is set to 10 million when <xref:System.Xml.XmlReaderSettings> is initialized.</span></span>
- <span data-ttu-id="74941-113"><xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=nameWithType> jest domyślnie ustawiony na wartość `null` .</span><span class="sxs-lookup"><span data-stu-id="74941-113"><xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=nameWithType> is set to `null` by default.</span></span>

> [!NOTE]
> <span data-ttu-id="74941-114"><xref:System.Xml.XmlReaderSettings> jest używany przez wszystkie parsery XML, więc podczas gdy ta zmiana pomaga w <xref:System.Xml.XmlReader> przypadku, ma także wpływ na inne scenariusze.</span><span class="sxs-lookup"><span data-stu-id="74941-114"><xref:System.Xml.XmlReaderSettings> is used by all XML parsers, so while this change helps the <xref:System.Xml.XmlReader> case, it also affects other scenarios.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="74941-115">Sugestia</span><span class="sxs-lookup"><span data-stu-id="74941-115">Suggestion</span></span>

<span data-ttu-id="74941-116">Aby przywrócić poprzednie zachowanie, można ustawić wartość w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="74941-116">To revert to the previous behavior, you can set a value in the registry.</span></span> <span data-ttu-id="74941-117">Dodaj wartość DWORD o nazwie `EnableLegacyXmlSettings` do `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\XML` klucza rejestru i ustaw jej wartość na `1` .</span><span class="sxs-lookup"><span data-stu-id="74941-117">Add a DWORD value named `EnableLegacyXmlSettings` to the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\XML` registry key, and set its value to `1`.</span></span> <span data-ttu-id="74941-118">Zamiast tego można także dodać wartość rejestru do HKEY_CURRENT_USER Hive.</span><span class="sxs-lookup"><span data-stu-id="74941-118">You can also add the registry value in the HKEY_CURRENT_USER hive instead.</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="74941-119">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="74941-119">Affected APIs</span></span>

- <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=fullName>
- <xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=fullName>

<span data-ttu-id="74941-120">Ponadto dotyczy to wszystkich interfejsów API XML, które są zależne od <xref:System.Xml.XmlResolver> programu (bezpośrednio lub pośrednio).</span><span class="sxs-lookup"><span data-stu-id="74941-120">In addition, any XML API that depends on <xref:System.Xml.XmlResolver>, either directly or indirectly, is affected.</span></span>

<!--

#### Affected APIs

- `P:System.Xml.XmlReaderSettings.MaxCharactersFromEntities`
- `P:System.Xml.XmlReaderSettings.XmlResolver`

-->
