---
ms.openlocfilehash: 6ee290f6722480778381376f588e16877894f232
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606751"
---
### <a name="privatefontcollectionaddfontfile-method-releases-font-resources"></a><span data-ttu-id="61fc7-101">PrivateFontCollection. AddFontFile — metoda zwalnia zasoby czcionek</span><span class="sxs-lookup"><span data-stu-id="61fc7-101">PrivateFontCollection.AddFontFile method releases Font resources</span></span>

#### <a name="details"></a><span data-ttu-id="61fc7-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="61fc7-102">Details</span></span>

<span data-ttu-id="61fc7-103">W .NET Framework 4.7.1 i poprzednich wersjach <xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType> Klasa nie zwolni zasobów czcionki GDI+ po usunięciu <xref:System.Drawing.Text.PrivateFontCollection> <xref:System.Drawing.Font> obiektów, które są dodawane do tej kolekcji przy użyciu <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)> metody.</span><span class="sxs-lookup"><span data-stu-id="61fc7-103">In the .NET Framework 4.7.1 and previous versions, the <xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType> class does not release the GDI+ font resources after the <xref:System.Drawing.Text.PrivateFontCollection> is disposed for <xref:System.Drawing.Font> objects that are added to this collection using the <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)> method.</span></span> <span data-ttu-id="61fc7-104">W .NET Framework 4.7.2 i nowszych <xref:System.Drawing.Text.FontCollection.Dispose%2A> wersji czcionki GDI+, które zostały dodane do kolekcji jako pliki.</span><span class="sxs-lookup"><span data-stu-id="61fc7-104">In the .NET Framework 4.7.2 and later <xref:System.Drawing.Text.FontCollection.Dispose%2A> releases the GDI+ fonts that were added to the collection as files.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="61fc7-105">Sugestia</span><span class="sxs-lookup"><span data-stu-id="61fc7-105">Suggestion</span></span>

<span data-ttu-id="61fc7-106">**Jak wybrać lub wycofać te zmiany** Aby aplikacja mogła korzystać z tych zmian, musi ona działać na .NET Framework 4.7.2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="61fc7-106">**How to opt in or out of these changes** In order for an application to benefit from these changes, it must run on the .NET Framework 4.7.2 or later.</span></span> <span data-ttu-id="61fc7-107">Aplikacja może korzystać z tych zmian w jeden z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="61fc7-107">The application can benefit from these changes in either of the following ways:</span></span>

- <span data-ttu-id="61fc7-108">Zostanie ponownie skompilowana w celu przekierowania .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="61fc7-108">It is recompiled to target the .NET Framework 4.7.2.</span></span> <span data-ttu-id="61fc7-109">Ta zmiana jest domyślnie włączona w Windows Forms aplikacjach przeznaczonych dla .NET Framework 4.7.2 lub nowszych.</span><span class="sxs-lookup"><span data-stu-id="61fc7-109">This change is enabled by default on Windows Forms applications that target the .NET Framework 4.7.2 or later.</span></span>
- <span data-ttu-id="61fc7-110">Jest ona przeznaczona dla .NET Framework 4.7.1 lub wcześniejszej wersji i [wyłączają](../../../../docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) się ze starszych zachowań ułatwień dostępu, dodając następujący `<runtime>` przykład AppContext do sekcji pliku app.config i ustawiając go na `false` , jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="61fc7-110">It targets the .NET Framework 4.7.1 or an earlier version and opts out of the legacy accessibility behaviors by adding the following [AppContext Switch](../../../../docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) to the `<runtime>` section of the app.config file and setting it to `false`, as the following example shows.</span></span>

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Drawing.Text.DoNotRemoveGdiFontsResourcesFromFontCollection=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

<span data-ttu-id="61fc7-111">Aplikacje ukierunkowane na .NET Framework 4.7.2 lub nowsze i chcą zachować starsze zachowanie mogą zrezygnować z niezwolnienia zasobów czcionki przez jawne ustawienie tego przełącznika AppContext na `true` .</span><span class="sxs-lookup"><span data-stu-id="61fc7-111">Applications that target the .NET Framework 4.7.2 or later, and want to preserve the legacy behavior can opt in to not release font resources by explicitly setting this AppContext switch to `true`.</span></span>

| <span data-ttu-id="61fc7-112">Nazwa</span><span class="sxs-lookup"><span data-stu-id="61fc7-112">Name</span></span>    | <span data-ttu-id="61fc7-113">Wartość</span><span class="sxs-lookup"><span data-stu-id="61fc7-113">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="61fc7-114">Zakres</span><span class="sxs-lookup"><span data-stu-id="61fc7-114">Scope</span></span>   | <span data-ttu-id="61fc7-115">Edge</span><span class="sxs-lookup"><span data-stu-id="61fc7-115">Edge</span></span>        |
| <span data-ttu-id="61fc7-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="61fc7-116">Version</span></span> | <span data-ttu-id="61fc7-117">4.7.2</span><span class="sxs-lookup"><span data-stu-id="61fc7-117">4.7.2</span></span>       |
| <span data-ttu-id="61fc7-118">Typ</span><span class="sxs-lookup"><span data-stu-id="61fc7-118">Type</span></span>    | <span data-ttu-id="61fc7-119">Przekierowanie</span><span class="sxs-lookup"><span data-stu-id="61fc7-119">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="61fc7-120">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="61fc7-120">Affected APIs</span></span>

- <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)?displayProperty=nameWithType>
- <xref:System.Drawing.Text.FontCollection.Dispose?displayProperty=nameWithType>
