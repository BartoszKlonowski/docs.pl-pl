---
title: 'Zmiana podziału: TextInfo. ListSeparator — zmiana wartości'
description: Dowiedz się więcej o różnicach w programie .NET 5,0, gdzie wartość domyślna TextInfo. ListSeparator została zmieniona między wersjami 5,0 i 5.0.1.
ms.date: 12/10/2020
ms.openlocfilehash: 720d46c1908bcd70812f575a90f580470dbc7f32
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596610"
---
# <a name="textinfolistseparator-values-changed"></a><span data-ttu-id="bccac-103">Zmieniono wartości TextInfo. ListSeparator</span><span class="sxs-lookup"><span data-stu-id="bccac-103">TextInfo.ListSeparator values changed</span></span>

<span data-ttu-id="bccac-104">Wartości domyślne <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> dla różnych kultur zostały zmienione we wszystkich systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="bccac-104">The default <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values for different cultures have changed on all operating systems.</span></span>

## <a name="change-description"></a><span data-ttu-id="bccac-105">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="bccac-105">Change description</span></span>

<span data-ttu-id="bccac-106">W programie .NET 5.0.0 jako część [przełącznika z BIBLIOTEK NLS do ICU](icu-globalization-api.md), <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości domyślne dla różnych kultur uległy zmianie w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="bccac-106">In .NET 5.0.0, as part of the [switch from NLS to ICU libraries](icu-globalization-api.md), the default <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values for different cultures changed on Windows.</span></span> <span data-ttu-id="bccac-107">Wartości separatora dziesiętnego uzyskane ze składników międzynarodowych dla standardu Unicode (ICU) zostały użyte jako <xref:System.Globalization.TextInfo.ListSeparator> wartości.</span><span class="sxs-lookup"><span data-stu-id="bccac-107">Decimal separator values, obtained from International Components for Unicode (ICU), were used as the <xref:System.Globalization.TextInfo.ListSeparator> values.</span></span> <span data-ttu-id="bccac-108">W systemie Linux i macOS nie wprowadzono zmian w <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartościach. oznacza to, że nadal używają wartości separatora dziesiętnego.</span><span class="sxs-lookup"><span data-stu-id="bccac-108">On Linux and macOS, there was no change in <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values; that is, they continued to use decimal separator values.</span></span>

<span data-ttu-id="bccac-109">Dla wszystkich systemów operacyjnych w .NET 5.0.1 i nowszych wersjach wartości dla <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> są równoważne wartościom, które byłyby uzyskane z NLS.</span><span class="sxs-lookup"><span data-stu-id="bccac-109">For all operating systems in .NET 5.0.1 and later versions, the values for <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> are equivalent to the values that would be obtained from NLS.</span></span> <span data-ttu-id="bccac-110">W przypadku systemu Windows oznacza to, że wartości są równoważne .NET Framework i .NET Core 1,0-3,1.</span><span class="sxs-lookup"><span data-stu-id="bccac-110">For Windows, this means the values are equivalent to what they were in .NET Framework and .NET Core 1.0 - 3.1.</span></span> <span data-ttu-id="bccac-111">W przypadku systemów Linux i macOS <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości są teraz zgodne z <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartościami dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="bccac-111">For Linux and macOS, the <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values now match the <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values for Windows.</span></span>

<span data-ttu-id="bccac-112">Poniższa tabela zawiera podsumowanie zmian <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości.</span><span class="sxs-lookup"><span data-stu-id="bccac-112">The following table summarizes the changes for <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values.</span></span>

| | <span data-ttu-id="bccac-113">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bccac-113">.NET Framework</span></span><br/><span data-ttu-id="bccac-114">.NET Core 1,0 — 3,1</span><span class="sxs-lookup"><span data-stu-id="bccac-114">.NET Core 1.0 - 3.1</span></span> | <span data-ttu-id="bccac-115">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="bccac-115">.NET 5.0</span></span> | <span data-ttu-id="bccac-116">5.0.1 .NET</span><span class="sxs-lookup"><span data-stu-id="bccac-116">.NET 5.0.1</span></span> |
-|-|-|-
| <span data-ttu-id="bccac-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="bccac-117">**Windows**</span></span> | <span data-ttu-id="bccac-118">Uzyskaj z usługi NLS</span><span class="sxs-lookup"><span data-stu-id="bccac-118">Obtain from NLS</span></span> | <span data-ttu-id="bccac-119">Separator dziesiętny z ICU.</span><span class="sxs-lookup"><span data-stu-id="bccac-119">Decimal separator from ICU.</span></span><br/><span data-ttu-id="bccac-120">Można wrócić do lokalizacji sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bccac-120">Can switch back to NLS.</span></span> | <span data-ttu-id="bccac-121">Równoważne z usługą NLS</span><span class="sxs-lookup"><span data-stu-id="bccac-121">Equivalent to NLS</span></span> |
| <span data-ttu-id="bccac-122">**Linux i macOS**</span><span class="sxs-lookup"><span data-stu-id="bccac-122">**Linux and macOS**</span></span> | <span data-ttu-id="bccac-123">Separator dziesiętny z ICU</span><span class="sxs-lookup"><span data-stu-id="bccac-123">Decimal separator from ICU</span></span> | <span data-ttu-id="bccac-124">Separator dziesiętny z ICU</span><span class="sxs-lookup"><span data-stu-id="bccac-124">Decimal separator from ICU</span></span> | <span data-ttu-id="bccac-125">Równoważne z usługą NLS</span><span class="sxs-lookup"><span data-stu-id="bccac-125">Equivalent to NLS</span></span> |

## <a name="version-introduced"></a><span data-ttu-id="bccac-126">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="bccac-126">Version introduced</span></span>

<span data-ttu-id="bccac-127">5.0.1</span><span class="sxs-lookup"><span data-stu-id="bccac-127">5.0.1</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="bccac-128">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="bccac-128">Reason for change</span></span>

<span data-ttu-id="bccac-129">Deweloperzy zgłosili, że używają <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> właściwości podczas analizowania plików wartości rozdzielanych przecinkami (CSV), a nowe wartości rozstają <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> się nimi.</span><span class="sxs-lookup"><span data-stu-id="bccac-129">Developers reported that they use the <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> property when parsing comma-separated value (CSV) files, and the new <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values broke that parsing.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="bccac-130">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="bccac-130">Recommended action</span></span>

<span data-ttu-id="bccac-131">Jeśli kod opiera się na poprzednich wartościach separatora dziesiętnego, można umieszczaj wymagane <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości.</span><span class="sxs-lookup"><span data-stu-id="bccac-131">If your code relies on the previous decimal separator values, you can hardcode the desired <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> values.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="bccac-132">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="bccac-132">Affected APIs</span></span>

- <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=fullName>

<!--

#### Category

- Globalization

### Affected APIs

- `P:System.Globalization.TextInfo.ListSeparator`

-->
