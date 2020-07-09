---
title: -Nullable (opcje kompilatora C#)
author: IEvangelist
ms.author: dapine
ms.date: 06/04/2020
f1_keywords:
- /nullable
helpviewer_keywords:
- nullable compiler option [C#]
- /nullable compiler option [C#]
- -nullable compiler option [C#]
ms.openlocfilehash: f1aba7e08f472411640d42f51d78ca6f7e5cc900
ms.sourcegitcommit: 4ad2f8920251f3744240c3b42a443ffbe0a46577
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86100889"
---
# <a name="-nullable-c-compiler-options"></a><span data-ttu-id="2ab4f-102">-Nullable (opcje kompilatora C#)</span><span class="sxs-lookup"><span data-stu-id="2ab4f-102">-nullable (C# Compiler Options)</span></span>

<span data-ttu-id="2ab4f-103">Opcja **-nullable** pozwala określić żądany kontekst dopuszczający wartość null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-103">The **-nullable** option lets you specify the desired nullable context.</span></span>

## <a name="syntax"></a><span data-ttu-id="2ab4f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="2ab4f-104">Syntax</span></span>

```console
-nullable[+ | -]
-nullable:{enable | disable | warnings | annotations}
```

## <a name="arguments"></a><span data-ttu-id="2ab4f-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="2ab4f-105">Arguments</span></span>

<span data-ttu-id="2ab4f-106">`+`&#124;`-`</span><span class="sxs-lookup"><span data-stu-id="2ab4f-106">`+` &#124; `-`</span></span>  
<span data-ttu-id="2ab4f-107">Określanie `+` lub **dopuszczanie wartości null**powoduje, że kompilator włącza kontekst dopuszczający wartości null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-107">Specifying `+`, or just **-nullable**, causes the compiler to enable nullable context.</span></span> <span data-ttu-id="2ab4f-108">Określenie `-` , która obowiązuje, jeśli nie określono **wartości null**, wyłącza kontekst dopuszczający wartości null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-108">Specifying `-`, which is in effect if you do not specify **-nullable**, disables nullable context.</span></span>

<span data-ttu-id="2ab4f-109">`enable`&#124; `disable` &#124; `warnings` &#124;`annotations`</span><span class="sxs-lookup"><span data-stu-id="2ab4f-109">`enable` &#124; `disable` &#124; `warnings` &#124; `annotations`</span></span>  
<span data-ttu-id="2ab4f-110">Określa opcję kontekstową dopuszczającą wartość null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-110">Specifies the nullable context option.</span></span> <span data-ttu-id="2ab4f-111">Podobnie jak w przypadku programu `+` lub `-` , aby włączyć i wyłączyć, ale pozwala na zwiększenie stopnia szczegółowości dla specyficznych dla kontekstu wartości null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-111">Similar to `+` or `-`, to enable and disable, but allows for more granularity of nullable context specificity.</span></span> <span data-ttu-id="2ab4f-112">`enable`Argument, który działa tak samo jak w przypadku określenia **wartości null**, włącza kontekst dopuszczający wartość null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-112">The `enable` argument, which is in effect the same as if you specify **-nullable**, enables the nullable context.</span></span> <span data-ttu-id="2ab4f-113">Określenie `disable` spowoduje wyłączenie kontekstu dopuszczającego wartość null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-113">Specifying `disable` will disable nullable context.</span></span> <span data-ttu-id="2ab4f-114">Gdy podajesz `warnings` argument, **-nullable:** Warnings, jest włączony kontekst ostrzeżenia dopuszczający wartość null.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-114">When providing the `warnings` argument, **-nullable:warnings**, the nullable warning context is enabled.</span></span> <span data-ttu-id="2ab4f-115">Podczas określania `annotations` argumentu **-nullable: adnotacje**kontekst adnotacji z dopuszczaniem wartości null jest włączony.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-115">When specifying the `annotations` argument, **-nullable:annotations**, the nullable annotation context is enabled.</span></span>

## <a name="remarks"></a><span data-ttu-id="2ab4f-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2ab4f-116">Remarks</span></span>

<span data-ttu-id="2ab4f-117">Analiza przepływu służy do wywnioskowania wartości null zmiennych w kodzie wykonywalnym.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-117">Flow analysis is used to infer the nullability of variables within executable code.</span></span> <span data-ttu-id="2ab4f-118">Wywnioskowana wartość null zmiennej jest niezależna od zadeklarowanej wartości null zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-118">The inferred nullability of a variable is independent of the variable's declared nullability.</span></span> <span data-ttu-id="2ab4f-119">Wywołania metod są analizowane nawet wtedy, gdy są warunkowo pominięte.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-119">Method calls are analyzed even when they are conditionally omitted.</span></span> <span data-ttu-id="2ab4f-120">Na przykład <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> w trybie wydania.</span><span class="sxs-lookup"><span data-stu-id="2ab4f-120">For instance, <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> in release mode.</span></span>

<span data-ttu-id="2ab4f-121">Wywołanie metod o następujących atrybutach będzie miało wpływ na analizę przepływu:</span><span class="sxs-lookup"><span data-stu-id="2ab4f-121">Invocation of methods annotated with the following attributes will also affect flow analysis:</span></span>

- <span data-ttu-id="2ab4f-122">Proste warunki wstępne: <xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute> i<xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute></span><span class="sxs-lookup"><span data-stu-id="2ab4f-122">Simple pre-conditions: <xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute> and <xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute></span></span>
- <span data-ttu-id="2ab4f-123">Proste warunki Post: <xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute> i<xref:System.Diagnostics.CodeAnalysis.NotNullAttribute></span><span class="sxs-lookup"><span data-stu-id="2ab4f-123">Simple post-conditions: <xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute> and <xref:System.Diagnostics.CodeAnalysis.NotNullAttribute></span></span>
- <span data-ttu-id="2ab4f-124">Warunkowe warunki końcowe: <xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute> i<xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute></span><span class="sxs-lookup"><span data-stu-id="2ab4f-124">Conditional post-conditions: <xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute> and <xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute></span></span>
- <span data-ttu-id="2ab4f-125"><xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute>(na przykład `DoesNotReturnIf(false)` dla <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> ) i<xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute></span><span class="sxs-lookup"><span data-stu-id="2ab4f-125"><xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute> (for example, `DoesNotReturnIf(false)` for <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>) and <xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute></span></span>
- <xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute>
- <span data-ttu-id="2ab4f-126">Warunki końcowe elementu członkowskiego: <xref:System.Diagnostics.CodeAnalysis.MemberNotNullAttribute.%23ctor(System.String)> i<xref:System.Diagnostics.CodeAnalysis.MemberNotNullAttribute.%23ctor(System.String[])></span><span class="sxs-lookup"><span data-stu-id="2ab4f-126">Member post-conditions: <xref:System.Diagnostics.CodeAnalysis.MemberNotNullAttribute.%23ctor(System.String)> and <xref:System.Diagnostics.CodeAnalysis.MemberNotNullAttribute.%23ctor(System.String[])></span></span>

### <a name="to-set-this-compiler-option-in-a-project"></a><span data-ttu-id="2ab4f-127">Aby ustawić tę opcję kompilatora w projekcie</span><span class="sxs-lookup"><span data-stu-id="2ab4f-127">To set this compiler option in a project</span></span>

<span data-ttu-id="2ab4f-128">Edytuj plik *. csproj* , aby dodać `<Nullable>` tag w `Project/PropertyGroup` hierarchii:</span><span class="sxs-lookup"><span data-stu-id="2ab4f-128">Edit the *.csproj* file to add the `<Nullable>` tag within a `Project/PropertyGroup` hierarchy:</span></span>

```xml
<Project Sdk="...">

  <PropertyGroup>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="2ab4f-129">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2ab4f-129">See also</span></span>

- [<span data-ttu-id="2ab4f-130">Opcje kompilatora C#</span><span class="sxs-lookup"><span data-stu-id="2ab4f-130">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="2ab4f-131">Typy referencyjne dopuszczające wartość null</span><span class="sxs-lookup"><span data-stu-id="2ab4f-131">Nullable reference types</span></span>](../../nullable-references.md)
