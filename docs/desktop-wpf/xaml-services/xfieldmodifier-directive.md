---
title: x:FieldModifier — dyrektywa
ms.date: 03/30/2017
helpviewer_keywords:
- FieldModifier attribute in XAML [XAML Services]
- x:FieldModifier attribute [XAML Services]
- XAML [XAML Services], x:FieldModifier attribute
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
ms.openlocfilehash: 3e104b4c464d545e048f29901701c1c3dbb68229
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2020
ms.locfileid: "82071529"
---
# <a name="xfieldmodifier-directive"></a><span data-ttu-id="a0962-102">x:FieldModifier — dyrektywa</span><span class="sxs-lookup"><span data-stu-id="a0962-102">x:FieldModifier Directive</span></span>
<span data-ttu-id="a0962-103">Modyfikuje zachowanie kompilacji XAML, dzięki czemu pola <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> dla odwołań <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> do nazwanych obiektów są definiowane z dostępem zamiast domyślnego zachowania.</span><span class="sxs-lookup"><span data-stu-id="a0962-103">Modifies XAML compilation behavior so that fields for named object references are defined with <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> access instead of the <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> default behavior.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="a0962-104">Użycie atrybutu języka XAML</span><span class="sxs-lookup"><span data-stu-id="a0962-104">XAML Attribute Usage</span></span>

```xaml
<object x:FieldModifier="Public".../>
```

## <a name="xaml-values"></a><span data-ttu-id="a0962-105">Wartości XAML</span><span class="sxs-lookup"><span data-stu-id="a0962-105">XAML Values</span></span>

|||
|-|-|
|<span data-ttu-id="a0962-106">*Publicznego*</span><span class="sxs-lookup"><span data-stu-id="a0962-106">*Public*</span></span>|<span data-ttu-id="a0962-107">Dokładny ciąg, który <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> przekazujesz do określenia w porównaniu <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> różni się, w zależności od języka programowania związane z kodem, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="a0962-107">The exact string you pass to specify <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> versus <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> varies, depending on the code-behind programming language that is used.</span></span> <span data-ttu-id="a0962-108">Zobacz uwagi.</span><span class="sxs-lookup"><span data-stu-id="a0962-108">See Remarks.</span></span>|

## <a name="dependencies"></a><span data-ttu-id="a0962-109">Zależności</span><span class="sxs-lookup"><span data-stu-id="a0962-109">Dependencies</span></span>

 <span data-ttu-id="a0962-110">Jeśli produkcja XAML `x:FieldModifier` używa w dowolnym miejscu, główny element tej produkcji XAML musi zadeklarować [x:Class Directive](xclass-directive.md).</span><span class="sxs-lookup"><span data-stu-id="a0962-110">If a XAML production uses `x:FieldModifier` anywhere, the root element of that XAML production must declare an [x:Class Directive](xclass-directive.md).</span></span>

## <a name="remarks"></a><span data-ttu-id="a0962-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a0962-111">Remarks</span></span>

<span data-ttu-id="a0962-112">`x:FieldModifier`nie jest istotne dla deklarowania ogólnego poziomu dostępu klasy lub jej członków.</span><span class="sxs-lookup"><span data-stu-id="a0962-112">`x:FieldModifier` is not relevant for declaring the general access level of a class or its members.</span></span> <span data-ttu-id="a0962-113">Jest to istotne tylko dla zachowania przetwarzania XAML, gdy określony obiekt XAML, który jest częścią produkcji XAML jest przetwarzany i staje się obiektem, który jest potencjalnie dostępny na wykresie obiektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0962-113">It is relevant only for XAML-processing behavior when a particular XAML object that is part of a XAML production is processed, and becomes an object that is potentially accessible in the object graph of an application.</span></span> <span data-ttu-id="a0962-114">Domyślnie odwołanie do pola dla takiego obiektu jest utrzymywane jako prywatne, co uniemożliwia konsumentom kontroli bezpośrednie modyfikowanie wykresu obiektu.</span><span class="sxs-lookup"><span data-stu-id="a0962-114">By default, the field reference for such an object is kept private, which prevents control consumers from modifying the object graph directly.</span></span> <span data-ttu-id="a0962-115">Zamiast tego oczekuje się, że konsumenci kontroli zmodyfikują wykres obiektów przy użyciu standardowych wzorców, które są włączone przez modele programowania, takie jak uzyskanie katalogu głównego układu, kolekcji elementów podrzędnych, dedykowanych właściwości publicznych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="a0962-115">Instead, control consumers are expected to modify the object graph by using standard patterns that are enabled by programming models, such as by obtaining the layout root, the child element collections, the dedicated public properties, and so on.</span></span>

<span data-ttu-id="a0962-116">Wartość atrybutu `x:FieldModifier` różni się w zależności od języka programowania, a jego przeznaczenie może się różnić w określonych ramach.</span><span class="sxs-lookup"><span data-stu-id="a0962-116">The value for the `x:FieldModifier` attribute varies by programming language, and its purpose can vary in specific frameworks.</span></span> <span data-ttu-id="a0962-117">Ciąg do użycia zależy od tego, <xref:System.CodeDom.Compiler.CodeDomProvider> jak każdy język implementuje jego i <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>konwertery typów zwraca do definiowania znaczeń dla i , i czy w tym języku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="a0962-117">The string to use depends on how each language implements its <xref:System.CodeDom.Compiler.CodeDomProvider> and the type converters it returns to define the meanings for <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> and <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>, and whether that language is case sensitive.</span></span>

- <span data-ttu-id="a0962-118">W przypadku języka C#ciąg, <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> który `public`ma być przekazywalny, to .</span><span class="sxs-lookup"><span data-stu-id="a0962-118">For C#, the string to pass to designate <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> is `public`.</span></span>

- <span data-ttu-id="a0962-119">W przypadku programu Microsoft Visual Basic .NET <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> `Public`ciąg, który ma być przekazyny do wyznaczenia, to .</span><span class="sxs-lookup"><span data-stu-id="a0962-119">For Microsoft Visual Basic .NET, the string to pass to designate <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> is `Public`.</span></span>

- <span data-ttu-id="a0962-120">W przypadku języka C++/CLI nie istnieją obecnie żadne obiekty docelowe dla języka XAML; w związku z tym ciąg do przekazania jest niezdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="a0962-120">For C++/CLI, no targets for XAML currently exist; therefore, the string to pass is undefined.</span></span>

<span data-ttu-id="a0962-121">Można również <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> określić (`internal` `Friend` w języku C#, <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> w języku Visual Basic), ale określenie jest nietypowe, ponieważ `NotPublic` zachowanie jest już domyślne.</span><span class="sxs-lookup"><span data-stu-id="a0962-121">You can also specify <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> (`internal` in C#, `Friend` in Visual Basic) but specifying <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> is unusual because `NotPublic` as the behavior is already the default.</span></span>

<span data-ttu-id="a0962-122"><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>jest zachowaniem domyślnym, ponieważ jest rzadkie, że kod poza zestawem, który skompilował XAML potrzebuje dostępu do elementu utworzonego przez XAML.</span><span class="sxs-lookup"><span data-stu-id="a0962-122"><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> is the default behavior because it is infrequent that code outside the assembly that compiled the XAML needs access to a XAML-created element.</span></span> <span data-ttu-id="a0962-123">Architektura zabezpieczeń WPF wraz z zachowaniem kompilacji XAML nie deklaruje pól, które `x:FieldModifier` przechowują wystąpienia elementu jako publiczne, chyba że specjalnie ustawić, aby umożliwić dostęp publiczny.</span><span class="sxs-lookup"><span data-stu-id="a0962-123">WPF security architecture together with XAML compilation behavior will not declare fields that store element instances as public, unless you specifically set the `x:FieldModifier` to allow public access.</span></span>

<span data-ttu-id="a0962-124">`x:FieldModifier`jest istotne tylko dla elementów z [x:Name Dyrektywy,](xname-directive.md) ponieważ ta nazwa jest używana do odwoływania się do pola po jego publicznych.</span><span class="sxs-lookup"><span data-stu-id="a0962-124">`x:FieldModifier` is only relevant for elements with an [x:Name Directive](xname-directive.md) because that name is used to reference the field after it is public.</span></span>

<span data-ttu-id="a0962-125">Domyślnie klasa częściowa dla elementu głównego jest publiczna; jednak można uczynić go niepubliczne przy użyciu [x:ClassModifier dyrektywy](xclassmodifier-directive.md).</span><span class="sxs-lookup"><span data-stu-id="a0962-125">By default, the partial class for the root element is public; however, you can make it nonpublic by using the [x:ClassModifier Directive](xclassmodifier-directive.md).</span></span> <span data-ttu-id="a0962-126">[X:ClassModifier Dyrektywy](xclassmodifier-directive.md) wpływa również na poziom dostępu wystąpienia klasy elementu głównego.</span><span class="sxs-lookup"><span data-stu-id="a0962-126">The [x:ClassModifier Directive](xclassmodifier-directive.md) also affects the access level of the instance of the root element class.</span></span> <span data-ttu-id="a0962-127">Można umieścić `x:Name` zarówno `x:FieldModifier` i na element główny, ale to tylko sprawia, że publiczna kopia pola elementu głównego, z poziomem dostępu do klasy elementu głównego true nadal kontrolowane przez [x:ClassModifier dyrektywy](xclassmodifier-directive.md).</span><span class="sxs-lookup"><span data-stu-id="a0962-127">You can put both `x:Name` and `x:FieldModifier` on the root element, but this only makes a public field copy of the root element, with the true root element class access level still controlled by [x:ClassModifier Directive](xclassmodifier-directive.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a0962-128">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a0962-128">See also</span></span>

- [<span data-ttu-id="a0962-129">Klasy XAML i niestandardowe dla WPF</span><span class="sxs-lookup"><span data-stu-id="a0962-129">XAML and Custom Classes for WPF</span></span>](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [<span data-ttu-id="a0962-130">Związane z kodem i XAML w WPF</span><span class="sxs-lookup"><span data-stu-id="a0962-130">Code-Behind and XAML in WPF</span></span>](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [<span data-ttu-id="a0962-131">x:Name — dyrektywa</span><span class="sxs-lookup"><span data-stu-id="a0962-131">x:Name Directive</span></span>](xname-directive.md)
- [<span data-ttu-id="a0962-132">Kompilowanie aplikacji WPF (WPF)</span><span class="sxs-lookup"><span data-stu-id="a0962-132">Building a WPF Application (WPF)</span></span>](../../framework/wpf/app-development/building-a-wpf-application-wpf.md)
- [<span data-ttu-id="a0962-133">x:ClassModifier — dyrektywa</span><span class="sxs-lookup"><span data-stu-id="a0962-133">x:ClassModifier Directive</span></span>](xclassmodifier-directive.md)