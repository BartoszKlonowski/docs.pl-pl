---
ms.openlocfilehash: 972601874d80d82ebae8b79779acfed82e5570cb
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496922"
---
### <a name="calling-itemsrefresh-on-a-wpf-listbox-listview-or-datagrid-with-items-selected-can-cause-duplicate-items-to-appear-in-the-element"></a><span data-ttu-id="262a4-101">Wywoływanie elementów. Refresh na liście rozwijanej WPF, ListView lub DataGrid z zaznaczonymi elementami może spowodować, że zduplikowane elementy będą widoczne w elemencie</span><span class="sxs-lookup"><span data-stu-id="262a4-101">Calling Items.Refresh on a WPF ListBox, ListView, or DataGrid with items selected can cause duplicate items to appear in the element</span></span>

#### <a name="details"></a><span data-ttu-id="262a4-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="262a4-102">Details</span></span>

<span data-ttu-id="262a4-103">W .NET Framework 4,5, wywołujący element ListBox. Items. Refresh z kodu, podczas gdy elementy są wybrane w, <xref:System.Windows.Controls.ListBox?displayProperty=fullName> mogą spowodować duplikowanie wybranych elementów na liście.</span><span class="sxs-lookup"><span data-stu-id="262a4-103">In the .NET Framework 4.5, calling ListBox.Items.Refresh from code while items are selected in a <xref:System.Windows.Controls.ListBox?displayProperty=fullName> can cause the selected items to be duplicated in the list.</span></span> <span data-ttu-id="262a4-104">Podobny problem występuje w systemie <xref:System.Windows.Controls.ListView?displayProperty=fullName> i <xref:System.Windows.Controls.DataGrid?displayProperty=fullName> .</span><span class="sxs-lookup"><span data-stu-id="262a4-104">A similar issue occurs with <xref:System.Windows.Controls.ListView?displayProperty=fullName> and <xref:System.Windows.Controls.DataGrid?displayProperty=fullName>.</span></span> <span data-ttu-id="262a4-105">Ten problem został rozwiązany w .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="262a4-105">This is fixed in the .NET Framework 4.6.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="262a4-106">Sugestia</span><span class="sxs-lookup"><span data-stu-id="262a4-106">Suggestion</span></span>

<span data-ttu-id="262a4-107">Problem ten może obejść przez programowe usunięcie zaznaczenia elementów przed wywołaniem <xref:System.Windows.Data.CollectionView.Refresh?displayProperty=fullName> , a następnie ponowne wybranie ich po zakończeniu wywołania.</span><span class="sxs-lookup"><span data-stu-id="262a4-107">This issue may be worked around by programmatically unselecting items before <xref:System.Windows.Data.CollectionView.Refresh?displayProperty=fullName> is called and then re-selecting them after the call is completed.</span></span> <span data-ttu-id="262a4-108">Alternatywnie ten problem został rozwiązany w .NET Framework 4,6 i może zostać rozwiązany przez uaktualnienie do tej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="262a4-108">Alternatively, this issue has been fixed in the .NET Framework 4.6 and may be addressed by upgrading to that version of the .NET Framework.</span></span>

| <span data-ttu-id="262a4-109">Nazwa</span><span class="sxs-lookup"><span data-stu-id="262a4-109">Name</span></span>    | <span data-ttu-id="262a4-110">Wartość</span><span class="sxs-lookup"><span data-stu-id="262a4-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="262a4-111">Zakres</span><span class="sxs-lookup"><span data-stu-id="262a4-111">Scope</span></span>   |<span data-ttu-id="262a4-112">Mały</span><span class="sxs-lookup"><span data-stu-id="262a4-112">Minor</span></span>|
|<span data-ttu-id="262a4-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="262a4-113">Version</span></span>|<span data-ttu-id="262a4-114">4.5</span><span class="sxs-lookup"><span data-stu-id="262a4-114">4.5</span></span>|
|<span data-ttu-id="262a4-115">Typ</span><span class="sxs-lookup"><span data-stu-id="262a4-115">Type</span></span>|<span data-ttu-id="262a4-116">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="262a4-116">Runtime</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="262a4-117">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="262a4-117">Affected APIs</span></span>

- <xref:System.Windows.Data.CollectionView.Refresh?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Windows.Data.CollectionView.Refresh`

-->
