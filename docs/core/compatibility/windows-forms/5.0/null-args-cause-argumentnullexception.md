---
title: 'Zmiana istotna: metody WinForms teraz generują ArgumentNullException'
description: Dowiedz się więcej na temat istotnej zmiany w programie .NET 5,0, w której niektóre metody Windows Forms teraz zgłaszają ArgumentNullException dla argumentów o wartości null.
ms.date: 09/18/2020
ms.openlocfilehash: 77280827d44b0e58533339a09357d518a0bfe508
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95761612"
---
# <a name="winforms-methods-now-throw-argumentnullexception"></a><span data-ttu-id="71ddd-103">Metody WinForms teraz generują ArgumentNullException</span><span class="sxs-lookup"><span data-stu-id="71ddd-103">WinForms methods now throw ArgumentNullException</span></span>

<span data-ttu-id="71ddd-104">Niektóre metody Windows Forms teraz throw <xref:System.ArgumentNullException> dla argumentów o wartości null, w których wcześniej wywołały <xref:System.NullReferenceException> .</span><span class="sxs-lookup"><span data-stu-id="71ddd-104">Some Windows Forms methods now throw an <xref:System.ArgumentNullException> for null arguments, where previously they threw a <xref:System.NullReferenceException>.</span></span>

## <a name="change-description"></a><span data-ttu-id="71ddd-105">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="71ddd-105">Change description</span></span>

<span data-ttu-id="71ddd-106">Wcześniej niektóre metody Windows Forms zgłosiły, <xref:System.NullReferenceException> Jeśli przekazano argument, który miał wartość null.</span><span class="sxs-lookup"><span data-stu-id="71ddd-106">Previously, certain Windows Forms methods threw a <xref:System.NullReferenceException> if passed an argument that was null.</span></span> <span data-ttu-id="71ddd-107">Począwszy od platformy .NET 5,0, metody te teraz generują <xref:System.ArgumentNullException> argumenty dla argumentów o wartości null.</span><span class="sxs-lookup"><span data-stu-id="71ddd-107">Starting in .NET 5.0, these methods now throw an <xref:System.ArgumentNullException> for null arguments, instead.</span></span>

<span data-ttu-id="71ddd-108">Zgłaszanie jest <xref:System.ArgumentNullException> zgodne z zachowaniem środowiska uruchomieniowego .NET.</span><span class="sxs-lookup"><span data-stu-id="71ddd-108">Throwing an <xref:System.ArgumentNullException> conforms to the behavior of the .NET runtime.</span></span> <span data-ttu-id="71ddd-109">Usprawnia to również środowisko debugowania przez wyraźne poinformowanie, że argument ma wartość null i który argument jest.</span><span class="sxs-lookup"><span data-stu-id="71ddd-109">It also improves the debugging experience by clearly communicating that an argument is null and which argument it is.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="71ddd-110">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="71ddd-110">Version introduced</span></span>

<span data-ttu-id="71ddd-111">.NET 5,0</span><span class="sxs-lookup"><span data-stu-id="71ddd-111">.NET 5.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="71ddd-112">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="71ddd-112">Recommended action</span></span>

<span data-ttu-id="71ddd-113">Jeśli wywołasz dowolną z tych metod, a kod aktualnie przechwytuje <xref:System.NullReferenceException> dla argumentów o wartości null, Przechwyć <xref:System.ArgumentNullException> zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="71ddd-113">If you call any of these methods and your code currently catches a <xref:System.NullReferenceException> for null arguments, catch an <xref:System.ArgumentNullException> instead.</span></span> <span data-ttu-id="71ddd-114">Ponadto należy rozważyć zaktualizowanie kodu, aby uniemożliwić przekazywanie argumentów o wartości null do wymienionych metod.</span><span class="sxs-lookup"><span data-stu-id="71ddd-114">In addition, consider updating the code to prevent passing null arguments to the listed methods.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="71ddd-115">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="71ddd-115">Affected APIs</span></span>

<span data-ttu-id="71ddd-116">Poniższa tabela zawiera listę odpowiednich metod i parametrów:</span><span class="sxs-lookup"><span data-stu-id="71ddd-116">The following table lists the affected methods and parameters:</span></span>

> [!div class="mx-tdBreakAll"]
> | <span data-ttu-id="71ddd-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="71ddd-117">Method</span></span> | <span data-ttu-id="71ddd-118">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="71ddd-118">Parameter name</span></span> | <span data-ttu-id="71ddd-119">Dodana wersja</span><span class="sxs-lookup"><span data-stu-id="71ddd-119">Version added</span></span> |
> |-|-|-|
> | <xref:System.Windows.Forms.Control.ControlCollection.%23ctor(System.Windows.Forms.Control)> | `owner` | <span data-ttu-id="71ddd-120">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-120">Preview 1</span></span> |
> | <xref:System.Windows.Forms.TabControl.GetToolTipText(System.Object)?displayProperty=nameWithType> | `item` | <span data-ttu-id="71ddd-121">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-121">Preview 1</span></span> |
> | <xref:System.Windows.Forms.TableLayoutControlCollection.%23ctor(System.Windows.Forms.TableLayoutPanel)> | `container` | <span data-ttu-id="71ddd-122">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-122">Preview 1</span></span> |
> | <xref:System.Windows.Forms.ToolStripRenderer.OnRenderArrow(System.Windows.Forms.ToolStripArrowRenderEventArgs)?displayProperty=nameWithType> | `e` | <span data-ttu-id="71ddd-123">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-123">Preview 1</span></span> |
> | <xref:System.Windows.Forms.ToolStripRenderer.OnRenderItemCheck(System.Windows.Forms.ToolStripItemImageRenderEventArgs)?displayProperty=nameWithType> | `e` | <span data-ttu-id="71ddd-124">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-124">Preview 1</span></span> |
> | <xref:System.Windows.Forms.ToolStripRenderer.OnRenderItemImage(System.Windows.Forms.ToolStripItemImageRenderEventArgs)?displayProperty=nameWithType> | `e` | <span data-ttu-id="71ddd-125">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-125">Preview 1</span></span> |
> | <xref:System.Windows.Forms.ToolStripRenderer.OnRenderItemText(System.Windows.Forms.ToolStripItemTextRenderEventArgs)?displayProperty=nameWithType> | `e` | <span data-ttu-id="71ddd-126">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-126">Preview 1</span></span> |
> | <xref:System.Windows.Forms.ToolStripRenderer.OnRenderStatusStripSizingGrip(System.Windows.Forms.ToolStripRenderEventArgs)?displayProperty=nameWithType> > | `e` | <span data-ttu-id="71ddd-127">Wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="71ddd-127">Preview 1</span></span> |
> | <xref:System.Windows.Forms.DataGridViewComboBoxEditingControl.ApplyCellStyleToEditingControl(System.Windows.Forms.DataGridViewCellStyle)?displayProperty=nameWithType> | `dataGridViewCellStyle` | <span data-ttu-id="71ddd-128">Preview 2</span><span class="sxs-lookup"><span data-stu-id="71ddd-128">Preview 2</span></span> |
> | <xref:System.Windows.Forms.RichTextBox.LoadFile(System.IO.Stream,System.Windows.Forms.RichTextBoxStreamType)?displayProperty=nameWithType> | `data` | <span data-ttu-id="71ddd-129">Preview 2</span><span class="sxs-lookup"><span data-stu-id="71ddd-129">Preview 2</span></span> |
> | <xref:System.Windows.Forms.ListBox.IntegerCollection.%23ctor(System.Windows.Forms.ListBox)> | `owner` | <span data-ttu-id="71ddd-130">Wersja zapoznawcza 5</span><span class="sxs-lookup"><span data-stu-id="71ddd-130">Preview 5</span></span> |
> | <xref:System.Windows.Forms.ListBox.IntegerCollection.CopyTo(System.Array,System.Int32)?displayProperty=nameWithType> | `destination` | <span data-ttu-id="71ddd-131">Wersja zapoznawcza 5</span><span class="sxs-lookup"><span data-stu-id="71ddd-131">Preview 5</span></span> |
> | <xref:System.Windows.Forms.ListViewGroup.System%23Runtime%23Serialization%23ISerializable%23GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | `info` | <span data-ttu-id="71ddd-132">Wersja zapoznawcza 5</span><span class="sxs-lookup"><span data-stu-id="71ddd-132">Preview 5</span></span> |
> | <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.%23ctor(System.String,System.Int32,System.Int32)> | `className` | <span data-ttu-id="71ddd-133">Wersja zapoznawcza 5</span><span class="sxs-lookup"><span data-stu-id="71ddd-133">Preview 5</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.%23ctor(System.Windows.Forms.ListBox)> | `owner` | <span data-ttu-id="71ddd-134">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-134">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.%23ctor(System.Windows.Forms.ListBox,System.Object[])> | <span data-ttu-id="71ddd-135">`owner`, `value`</span><span class="sxs-lookup"><span data-stu-id="71ddd-135">`owner`, `value`</span></span> | <span data-ttu-id="71ddd-136">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-136">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.%23ctor(System.Windows.Forms.ListBox,System.Windows.Forms.ListBox.ObjectCollection)> | <span data-ttu-id="71ddd-137">`owner`, `value`</span><span class="sxs-lookup"><span data-stu-id="71ddd-137">`owner`, `value`</span></span> | <span data-ttu-id="71ddd-138">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-138">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.AddRange(System.Object[])?displayProperty=nameWithType> | `items` | <span data-ttu-id="71ddd-139">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-139">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.AddRange(System.Windows.Forms.ListBox.ObjectCollection)?displayProperty=nameWithType> | `value` | <span data-ttu-id="71ddd-140">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-140">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.CopyTo(System.Object[],System.Int32)?displayProperty=nameWithType> | `destination` | <span data-ttu-id="71ddd-141">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-141">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListBox.ObjectCollection.System%23Collections%23ICollection%23CopyTo(System.Array,System.Int32)?displayProperty=nameWithType> | `destination` | <span data-ttu-id="71ddd-142">Wersja zapoznawcza 6</span><span class="sxs-lookup"><span data-stu-id="71ddd-142">Preview 6</span></span> |
> | <xref:System.Windows.Forms.ListView.SelectedIndexCollection.%23ctor(System.Windows.Forms.ListView)> | `owner` | <span data-ttu-id="71ddd-143">Wersja zapoznawcza 7</span><span class="sxs-lookup"><span data-stu-id="71ddd-143">Preview 7</span></span> |
> | <xref:System.Windows.Forms.TreeNodeCollection.Find(System.String,System.Boolean)?displayProperty=nameWithType> | <span data-ttu-id="71ddd-144">`key` jest `null` lub puste</span><span class="sxs-lookup"><span data-stu-id="71ddd-144">`key` is `null` or empty</span></span> | <span data-ttu-id="71ddd-145">Wersja zapoznawcza 8</span><span class="sxs-lookup"><span data-stu-id="71ddd-145">Preview 8</span></span> |
> | <xref:System.Windows.Forms.ListView.ListViewItemCollection.Find(System.String,System.Boolean)?displayProperty=nameWithType> | <span data-ttu-id="71ddd-146">`key` jest `null` lub puste</span><span class="sxs-lookup"><span data-stu-id="71ddd-146">`key` is `null` or empty</span></span> | <span data-ttu-id="71ddd-147">RC1</span><span class="sxs-lookup"><span data-stu-id="71ddd-147">RC1</span></span> |
> | <xref:System.Windows.Forms.ScrollableControl.OnPaintBackground(System.Windows.Forms.PaintEventArgs)?displayProperty=nameWithType> | `e` | <span data-ttu-id="71ddd-148">RC1</span><span class="sxs-lookup"><span data-stu-id="71ddd-148">RC1</span></span> |

<!--

### Affected APIs

- `M:System.Windows.Forms.Control.ControlCollection.#ctor(System.Windows.Forms.Control)`
- `M:System.Windows.Forms.TabControl.GetToolTipText(System.Object)`
- `M:System.Windows.Forms.TableLayoutControlCollection.#ctor(System.Windows.Forms.TableLayoutPanel)`
- `M:System.Windows.Forms.ToolStripRenderer.OnRenderArrow(System.Windows.Forms.ToolStripArrowRenderEventArgs)`
- `M:System.Windows.Forms.ToolStripRenderer.OnRenderItemImage(System.Windows.Forms.ToolStripItemImageRenderEventArgs)`
- `M:System.Windows.Forms.ToolStripRenderer.OnRenderItemCheck(System.Windows.Forms.ToolStripItemImageRenderEventArgs)`
- `M:System.Windows.Forms.ToolStripRenderer.OnRenderItemText(System.Windows.Forms.ToolStripItemTextRenderEventArgs)`
- `M:System.Windows.Forms.ToolStripRenderer.OnRenderStatusStripSizingGrip(System.Windows.Forms.ToolStripRenderEventArgs)`
- `M:System.Windows.Forms.DataGridViewComboBoxEditingControl.ApplyCellStyleToEditingControl(System.Windows.Forms.DataGridViewCellStyle)`
- `M:System.Windows.Forms.RichTextBox.LoadFile(System.IO.Stream,System.Windows.Forms.RichTextBoxStreamType)`
- `M:System.Windows.Forms.ListViewGroup.System#Runtime#Serialization#ISerializable#GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)`
- `M:System.Windows.Forms.VisualStyles.VisualStyleRenderer.#ctor(System.String,System.Int32,System.Int32)`
- `M:System.Windows.Forms.ListBox.IntegerCollection.#ctor(System.Windows.Forms.ListBox)`
- `M:System.Windows.Forms.ListBox.IntegerCollection.CopyTo(System.Array,System.Int32)`
- `M:System.Windows.Forms.ListBox.ObjectCollection.#ctor(System.Windows.Forms.ListBox)`
- `M:System.Windows.Forms.ListBox.ObjectCollection.#ctor(System.Windows.Forms.ListBox,System.Object[])`
- `M:System.Windows.Forms.ListBox.ObjectCollection.#ctor(System.Windows.Forms.ListBox,System.Windows.Forms.ListBox.ObjectCollection)`
- `M:System.Windows.Forms.ListBox.ObjectCollection.AddRange(System.Object[])`
- `M:System.Windows.Forms.ListBox.ObjectCollection.AddRange(System.Windows.Forms.ListBox.ObjectCollection)`
- `M:System.Windows.Forms.ListBox.ObjectCollection.CopyTo(System.Object[],System.Int32)`
- `M:System.Windows.Forms.ListBox.ObjectCollection.System#Collections#ICollection#CopyTo(System.Array,System.Int32)`
- `M:System.Windows.Forms.ListView.SelectedIndexCollection.#ctor(System.Windows.Forms.ListView)`
- `M:System.Windows.Forms.TreeNodeCollection.Find(System.String,System.Boolean)`
- `M:System.Windows.Forms.ListView.ListViewItemCollection.Find(System.String,System.Boolean)`
- `M:System.Windows.Forms.ScrollableControl.OnPaintBackground(System.Windows.Forms.PaintEventArgs)`

### Category

Windows Forms

-->
