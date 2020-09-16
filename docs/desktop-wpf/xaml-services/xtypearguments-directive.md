---
title: x:TypeArguments — dyrektywa
ms.date: 03/30/2017
f1_keywords:
- x:TypeArguments
- xTypeArguments
- TypeArguments
helpviewer_keywords:
- x:TypeArguments attribute [XAML Services]
- TypeArguments attribute in XAML [XAML Services]
- XAML [XAML Services], x:TypeArguments attribute
ms.assetid: 86561058-d393-4a44-b5c3-993a4513ea74
ms.openlocfilehash: 430ab65af52282ccb1d429cd2523efe213f13609
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543554"
---
# <a name="xtypearguments-directive"></a><span data-ttu-id="c49ce-102">x:TypeArguments — dyrektywa</span><span class="sxs-lookup"><span data-stu-id="c49ce-102">x:TypeArguments Directive</span></span>

<span data-ttu-id="c49ce-103">Przekazuje argumenty typu ograniczającego ogólnego do konstruktora typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="c49ce-103">Passes constraining type arguments of a generic to the constructor of the generic type.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="c49ce-104">Użycie atrybutu języka XAML</span><span class="sxs-lookup"><span data-stu-id="c49ce-104">XAML Attribute Usage</span></span>

```xaml
<object x:TypeArguments="typeString" .../>
```

## <a name="xaml-values"></a><span data-ttu-id="c49ce-105">Wartości XAML</span><span class="sxs-lookup"><span data-stu-id="c49ce-105">XAML Values</span></span>

|||
|-|-|
|`object`|<span data-ttu-id="c49ce-106">Deklaracja elementu obiektu typu XAML, która jest obsługiwana przez typ ogólny środowiska CLR.</span><span class="sxs-lookup"><span data-stu-id="c49ce-106">An object element declaration of a XAML type, which is backed by a CLR generic type.</span></span> <span data-ttu-id="c49ce-107">Jeśli `object` odwołuje się do typu XAML, który nie pochodzi z domyślnej przestrzeni nazw XAML, program `object` wymaga prefiksu, aby wskazać przestrzeń nazw XAML, gdzie `object` istnieje.</span><span class="sxs-lookup"><span data-stu-id="c49ce-107">If `object` refers to a XAML type that is not from the default XAML namespace, `object` requires a prefix to indicate the XAML namespace where `object` exists.</span></span>|
|`typeString`|<span data-ttu-id="c49ce-108">Ciąg, który deklaruje co najmniej jedną nazwę typu XAML jako ciągi znaków, który dostarcza argumentów typu dla typu ogólnego CLR.</span><span class="sxs-lookup"><span data-stu-id="c49ce-108">A string that declares one or more XAML type names as strings, which supplies the type arguments for the CLR generic type.</span></span> <span data-ttu-id="c49ce-109">Zobacz uwagi, aby uzyskać dodatkowe informacje o składni.</span><span class="sxs-lookup"><span data-stu-id="c49ce-109">See Remarks for additional syntax notes.</span></span>|

## <a name="remarks"></a><span data-ttu-id="c49ce-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c49ce-110">Remarks</span></span>

<span data-ttu-id="c49ce-111">W większości przypadków typy XAML, które są używane jako element informacji w `typeString` ciągu, są poprzedzone prefiksem.</span><span class="sxs-lookup"><span data-stu-id="c49ce-111">In most cases, the XAML types that are used as an information item in a `typeString` string are prefixed.</span></span> <span data-ttu-id="c49ce-112">Typowe typy ograniczeń ogólnych CLR (na przykład <xref:System.Int32> i <xref:System.String> ) pochodzą z bibliotek klas podstawowych CLR.</span><span class="sxs-lookup"><span data-stu-id="c49ce-112">Typical types of CLR generic constraints (for example, <xref:System.Int32> and <xref:System.String>) come from CLR base class libraries.</span></span> <span data-ttu-id="c49ce-113">Te biblioteki nie są zamapowane na typowe obszary nazw języka XAML specyficzne dla platformy i dlatego wymagają mapowania prefiksów dla użycia XAML.</span><span class="sxs-lookup"><span data-stu-id="c49ce-113">Those libraries are not mapped to typical framework-specific default XAML namespaces, and therefore, require a prefix mapping for XAML usage.</span></span>

<span data-ttu-id="c49ce-114">Można określić więcej niż jedną nazwę typu XAML przy użyciu ogranicznika przecinka.</span><span class="sxs-lookup"><span data-stu-id="c49ce-114">You can specify more than one XAML type name by using a comma delimiter.</span></span>

<span data-ttu-id="c49ce-115">Jeśli ogólne ograniczenia same używają typów ogólnych, argumenty zagnieżdżonych typów ograniczeń mogą być zawarte w nawiasach ().</span><span class="sxs-lookup"><span data-stu-id="c49ce-115">If the generic constraints themselves use generic types, the nested constraint type arguments can be contained by parentheses ().</span></span>

<span data-ttu-id="c49ce-116">Należy zauważyć, że ta definicja `x:TypeArguments` jest specyficzna dla usług .NET XAML i tworzenia kopii zapasowych przy użyciu środowiska CLR.</span><span class="sxs-lookup"><span data-stu-id="c49ce-116">Note that this definition of `x:TypeArguments` is specific to .NET XAML Services and using CLR backing.</span></span> <span data-ttu-id="c49ce-117">Definicję poziomu języka można znaleźć w [ \[ sekcji MS-XAML \] 5.3.11](/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span><span class="sxs-lookup"><span data-stu-id="c49ce-117">A language-level definition can be found in [\[MS-XAML\] Section 5.3.11](/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span></span>

## <a name="usage-examples"></a><span data-ttu-id="c49ce-118">Przykłady użycia</span><span class="sxs-lookup"><span data-stu-id="c49ce-118">Usage Examples</span></span>

<span data-ttu-id="c49ce-119">W poniższych przykładach założono, że są zadeklarowane następujące definicje przestrzeni nazw XAML:</span><span class="sxs-lookup"><span data-stu-id="c49ce-119">For these examples, assume that the following XAML namespace definitions are declared:</span></span>

```xaml
xmlns:sys="clr-namespace:System;assembly=mscorlib"
xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"
```

### <a name="liststring"></a><span data-ttu-id="c49ce-120">Staw\<String></span><span class="sxs-lookup"><span data-stu-id="c49ce-120">List\<String></span></span>

<span data-ttu-id="c49ce-121">`<scg:List x:TypeArguments="sys:String" ...>` tworzy wystąpienie elementu New <xref:System.Collections.Generic.List%601> z <xref:System.String> argumentem typu.</span><span class="sxs-lookup"><span data-stu-id="c49ce-121">`<scg:List x:TypeArguments="sys:String" ...>` instantiates a new <xref:System.Collections.Generic.List%601> with a <xref:System.String> type argument.</span></span>

### <a name="dictionarystringstring"></a><span data-ttu-id="c49ce-122">Słownik\<String,String></span><span class="sxs-lookup"><span data-stu-id="c49ce-122">Dictionary\<String,String></span></span>

<span data-ttu-id="c49ce-123">`<scg:Dictionary x:TypeArguments="sys:String,sys:String" ...>` tworzy wystąpienie nowego <xref:System.Collections.Generic.Dictionary%602> z dwoma <xref:System.String> argumentami typu.</span><span class="sxs-lookup"><span data-stu-id="c49ce-123">`<scg:Dictionary x:TypeArguments="sys:String,sys:String" ...>` instantiates a new <xref:System.Collections.Generic.Dictionary%602> with two <xref:System.String> type arguments.</span></span>

### <a name="queuekeyvaluepairstringstring"></a><span data-ttu-id="c49ce-124">Kolejka<KeyValuePair\<String,String>></span><span class="sxs-lookup"><span data-stu-id="c49ce-124">Queue<KeyValuePair\<String,String>></span></span>

<span data-ttu-id="c49ce-125">`<scg:Queue x:TypeArguments="scg:KeyValuePair(sys:String,sys:String)" ...>` tworzy wystąpienie nowego <xref:System.Collections.Generic.Queue%601> , który ma ograniczenie z <xref:System.Collections.Generic.KeyValuePair%602> argumentami typu ograniczenia wewnętrznego <xref:System.String> i <xref:System.String> .</span><span class="sxs-lookup"><span data-stu-id="c49ce-125">`<scg:Queue x:TypeArguments="scg:KeyValuePair(sys:String,sys:String)" ...>` instantiates a new <xref:System.Collections.Generic.Queue%601> that has a constraint of <xref:System.Collections.Generic.KeyValuePair%602> with the inner constraint type arguments <xref:System.String> and <xref:System.String>.</span></span>

## <a name="xaml-2006-and-wpf-generic-xaml-usages"></a><span data-ttu-id="c49ce-126">XAML 2006 i WPF — ogólne użycia XAML</span><span class="sxs-lookup"><span data-stu-id="c49ce-126">XAML 2006 and WPF Generic XAML Usages</span></span>

<span data-ttu-id="c49ce-127">W przypadku użycia języka XAML 2006 i języka XAML, który jest używany przez aplikacje WPF, istnieją następujące ograniczenia dotyczące `x:TypeArguments` użycia typów ogólnych w języku XAML:</span><span class="sxs-lookup"><span data-stu-id="c49ce-127">For XAML 2006 usage, and XAML that is used for WPF applications, the following restrictions exist for `x:TypeArguments` and generic type usages from XAML in general:</span></span>

- <span data-ttu-id="c49ce-128">Tylko element główny pliku XAML może obsługiwać ogólne użycie XAML, które odwołuje się do typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="c49ce-128">Only the root element of a XAML file can support a generic XAML usage that references a generic type.</span></span>

- <span data-ttu-id="c49ce-129">Element główny musi być mapowany do typu ogólnego z co najmniej jednym argumentem typu.</span><span class="sxs-lookup"><span data-stu-id="c49ce-129">The root element must map to a generic type with at least one type argument.</span></span> <span data-ttu-id="c49ce-130">Może to być na przykład <xref:System.Windows.Navigation.PageFunction%601>.</span><span class="sxs-lookup"><span data-stu-id="c49ce-130">An example is <xref:System.Windows.Navigation.PageFunction%601>.</span></span> <span data-ttu-id="c49ce-131">Funkcje strony są głównym scenariuszem obsługi ogólnych zastosowań XAML w programie WPF.</span><span class="sxs-lookup"><span data-stu-id="c49ce-131">The page functions are the primary scenario for XAML generic usage support in WPF.</span></span>

- <span data-ttu-id="c49ce-132">Element główny elementu XAML elementu generycznego musi również deklarować klasy częściowej przy użyciu `x:Class` .</span><span class="sxs-lookup"><span data-stu-id="c49ce-132">The root element XAML object element for the generic must also declare a partial class using `x:Class`.</span></span> <span data-ttu-id="c49ce-133">Jest to prawdziwe nawet w przypadku definiowania akcji kompilacji WPF.</span><span class="sxs-lookup"><span data-stu-id="c49ce-133">This is true even if defining a WPF build action.</span></span>

- <span data-ttu-id="c49ce-134">`x:TypeArguments` nie można odwoływać się do zagnieżdżonych ograniczeń ogólnych.</span><span class="sxs-lookup"><span data-stu-id="c49ce-134">`x:TypeArguments` cannot reference nested generic constraints.</span></span>

## <a name="xaml-2009-or-xaml-2006-with-no-wpf-30-or-wpf-35-dependency"></a><span data-ttu-id="c49ce-135">XAML 2009 lub XAML 2006 bez zależności WPF 3,0 lub WPF 3,5</span><span class="sxs-lookup"><span data-stu-id="c49ce-135">XAML 2009 or XAML 2006 with No WPF 3.0 or WPF 3.5 Dependency</span></span>

<span data-ttu-id="c49ce-136">W usługach .NET XAML dla języka XAML 2006 lub XAML 2009 ograniczenia związane z WPF dla ogólnego użycia XAML są swobodne.</span><span class="sxs-lookup"><span data-stu-id="c49ce-136">In .NET XAML Services for either XAML 2006 or XAML 2009, the WPF-related restrictions on generic XAML usage are relaxed.</span></span> <span data-ttu-id="c49ce-137">Można utworzyć wystąpienie elementu ogólnego obiektu w dowolnym miejscu w znaczniku XAML, który może obsługiwać system typu zapasowego i model obiektów.</span><span class="sxs-lookup"><span data-stu-id="c49ce-137">You can instantiate a generic object element at any position in XAML markup that the backing type system and object model can support.</span></span>

<span data-ttu-id="c49ce-138">Jeśli używasz języka XAML 2009 zamiast mapowania typów podstawowych CLR w celu uzyskania typów XAML dla elementów podstawowych języka wspólnego, możesz użyć [typów wbudowanych dla wspólnych prymitywów języka XAML](types-for-primitives.md) jako elementy informacji w `typeString` .</span><span class="sxs-lookup"><span data-stu-id="c49ce-138">If you use XAML 2009 instead of mapping the CLR base types to obtain XAML types for common language primitives, you can use [Built-in Types for Common XAML Language Primitives](types-for-primitives.md) as information items in a `typeString`.</span></span> <span data-ttu-id="c49ce-139">Można na przykład zadeklarować następujące elementy (mapowania prefiksów nie są wyświetlane, ale x jest przestrzenią nazw XAML języka XAML dla XAML 2009):</span><span class="sxs-lookup"><span data-stu-id="c49ce-139">For example, you could declare the following (prefix mappings not shown, but x is the XAML language XAML namespace for XAML 2009):</span></span>

```xaml
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>
```

<span data-ttu-id="c49ce-140">W programie WPF i w przypadku określania wartości docelowej .NET Framework 4 lub .NET Core 3,0 (lub nowszej) można używać funkcji języka XAML 2009 razem z programem, `x:TypeArguments` ale tylko w przypadku swobodnego języka XAML (XAML, który nie jest skompilowany do adiustacji).</span><span class="sxs-lookup"><span data-stu-id="c49ce-140">In WPF and when targeting .NET Framework 4 or .NET Core 3.0 (or later), you can use XAML 2009 features together with `x:TypeArguments` but only for loose XAML (XAML that is not markup-compiled).</span></span> <span data-ttu-id="c49ce-141">Skompilowane znaczniki XAML dla WPF i forma BAML języka XAML nie obsługują obecnie słów kluczowych i funkcji języka XAML 2009.</span><span class="sxs-lookup"><span data-stu-id="c49ce-141">Markup-compiled XAML for WPF and the BAML form of XAML do not currently support the XAML 2009 keywords and features.</span></span> <span data-ttu-id="c49ce-142">Jeśli zachodzi konieczność skompilowania kodu XAML, należy wykonać działania zgodnie z ograniczeniami wymienionymi w sekcji [języka xaml 2006 i WPF ogólnych użycia XAML](#xaml-2006-and-wpf-generic-xaml-usages) .</span><span class="sxs-lookup"><span data-stu-id="c49ce-142">If you need to markup compile the XAML, you must operate under the restrictions noted in the [XAML 2006 and WPF Generic XAML Usages](#xaml-2006-and-wpf-generic-xaml-usages) section.</span></span> <span data-ttu-id="c49ce-143">BAML jest obsługiwana tylko w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c49ce-143">BAML is only supported in .NET Framework.</span></span>

## <a name="see-also"></a><span data-ttu-id="c49ce-144">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c49ce-144">See also</span></span>

- [<span data-ttu-id="c49ce-145">x:Class — dyrektywa</span><span class="sxs-lookup"><span data-stu-id="c49ce-145">x:Class Directive</span></span>](xclass-directive.md)
- [<span data-ttu-id="c49ce-146">x:Type — Rozszerzenie znaczników</span><span class="sxs-lookup"><span data-stu-id="c49ce-146">x:Type Markup Extension</span></span>](xtype-markup-extension.md)
- [<span data-ttu-id="c49ce-147">Typy wbudowane dla wspólnych elementów podstawowych języka XAML</span><span class="sxs-lookup"><span data-stu-id="c49ce-147">Built-in Types for Common XAML Language Primitives</span></span>](types-for-primitives.md)
- [<span data-ttu-id="c49ce-148">Typy ogólne w XAML</span><span class="sxs-lookup"><span data-stu-id="c49ce-148">Generics in XAML</span></span>](generics.md)
