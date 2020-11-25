---
title: Właściwości zależności
ms.date: 10/22/2008
ms.assetid: 212cfb1e-cec4-4047-94a6-47209b387f6f
ms.openlocfilehash: ab30da59670c146874defe86b1d048f97eebf449
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734767"
---
# <a name="dependency-properties"></a><span data-ttu-id="f0d3d-102">Właściwości zależności</span><span class="sxs-lookup"><span data-stu-id="f0d3d-102">Dependency Properties</span></span>

<span data-ttu-id="f0d3d-103">Właściwość zależności (DP) to zwykła właściwość, która przechowuje jej wartość w magazynie właściwości, zamiast przechowywać ją w zmiennej typu (pole), na przykład.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-103">A dependency property (DP) is a regular property that stores its value in a property store instead of storing it in a type variable (field), for example.</span></span>

 <span data-ttu-id="f0d3d-104">Właściwość dołączona zależność jest rodzajem właściwości zależności modelowanym jako statyczne metody get i Set reprezentujące "właściwości" opisujące relacje między obiektami i ich kontenerami (np. pozycja `Button` obiektu w `Panel` kontenerze).</span><span class="sxs-lookup"><span data-stu-id="f0d3d-104">An attached dependency property is a kind of dependency property modeled as static Get and Set methods representing "properties" describing relationships between objects and their containers (e.g., the position of a `Button` object on a `Panel` container).</span></span>

 <span data-ttu-id="f0d3d-105">✔️ zapewnić właściwości zależności, jeśli potrzebujesz właściwości do obsługi funkcji WPF, takich jak style, wyzwalacze, powiązanie danych, animacje, zasoby dynamiczne i dziedziczenie.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-105">✔️ DO provide the dependency properties, if you need the properties to support WPF features such as styling, triggers, data binding, animations, dynamic resources, and inheritance.</span></span>

## <a name="dependency-property-design"></a><span data-ttu-id="f0d3d-106">Projekt właściwości zależności</span><span class="sxs-lookup"><span data-stu-id="f0d3d-106">Dependency Property Design</span></span>

 <span data-ttu-id="f0d3d-107">✔️ dziedziczyć po <xref:System.Windows.DependencyObject> lub jeden z jego podtypów podczas implementowania właściwości zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-107">✔️ DO inherit from <xref:System.Windows.DependencyObject>, or one of its subtypes, when implementing dependency properties.</span></span> <span data-ttu-id="f0d3d-108">Typ zapewnia bardzo wydajną implementację magazynu właściwości i automatycznie obsługuje powiązanie danych WPF.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-108">The type provides a very efficient implementation of a property store and automatically supports WPF data binding.</span></span>

 <span data-ttu-id="f0d3d-109">✔️ zapewnić zwykłą Właściwość środowiska CLR i publiczne statyczne pole tylko do odczytu przechowujące wystąpienie <xref:System.Windows.DependencyProperty?displayProperty=nameWithType> dla każdej właściwości zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-109">✔️ DO provide a regular CLR property and public static read-only field storing an instance of <xref:System.Windows.DependencyProperty?displayProperty=nameWithType> for each dependency property.</span></span>

 <span data-ttu-id="f0d3d-110">✔️ Implementowanie właściwości zależności przez wywoływanie metod wystąpień <xref:System.Windows.DependencyObject.GetValue%2A?displayProperty=nameWithType> i <xref:System.Windows.DependencyObject.SetValue%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="f0d3d-110">✔️ DO implement dependency properties by calling instance methods <xref:System.Windows.DependencyObject.GetValue%2A?displayProperty=nameWithType> and <xref:System.Windows.DependencyObject.SetValue%2A?displayProperty=nameWithType>.</span></span>

 <span data-ttu-id="f0d3d-111">✔️ Nadaj nazwę statycznemu polu właściwości zależności za pomocą sufiksu nazwy właściwości z "Property".</span><span class="sxs-lookup"><span data-stu-id="f0d3d-111">✔️ DO name the dependency property static field by suffixing the name of the property with "Property."</span></span>

 <span data-ttu-id="f0d3d-112">❌ NIE ustawiaj domyślnych wartości właściwości zależności jawnie w kodzie; Zamiast tego należy je ustawić w metadanych.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-112">❌ DO NOT set default values of dependency properties explicitly in code; set them in metadata instead.</span></span>

 <span data-ttu-id="f0d3d-113">Jeśli jawnie ustawisz właściwość domyślną, można zapobiec ustawianiu tej właściwości przez niejawne środki, takie jak style.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-113">If you set a property default explicitly, you might prevent that property from being set by some implicit means, such as a styling.</span></span>

 <span data-ttu-id="f0d3d-114">❌ NIE należy umieszczać kodu w odniesieniu do właściwości, innym niż standardowy kod, aby uzyskać dostęp do pola statycznego.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-114">❌ DO NOT put code in the property accessors other than the standard code to access the static field.</span></span>

 <span data-ttu-id="f0d3d-115">Ten kod nie zostanie wykonany, jeśli właściwość jest ustawiona w sposób niejawny, na przykład w stylu, ponieważ style używa pola statycznego bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-115">That code won’t execute if the property is set by implicit means, such as a styling, because styling uses the static field directly.</span></span>

 <span data-ttu-id="f0d3d-116">❌ NIE należy używać właściwości zależności do przechowywania zabezpieczonych danych.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-116">❌ DO NOT use dependency properties to store secure data.</span></span> <span data-ttu-id="f0d3d-117">Nawet prywatne właściwości zależności są dostępne publicznie.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-117">Even private dependency properties can be accessed publicly.</span></span>

## <a name="attached-dependency-property-design"></a><span data-ttu-id="f0d3d-118">Projekt właściwości dołączonej zależności</span><span class="sxs-lookup"><span data-stu-id="f0d3d-118">Attached Dependency Property Design</span></span>

 <span data-ttu-id="f0d3d-119">Właściwości zależności opisane w poprzedniej sekcji reprezentują właściwości wewnętrzne typu deklarującego; na przykład `Text` Właściwość jest właściwością `TextButton` , która deklaruje ją.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-119">Dependency properties described in the preceding section represent intrinsic properties of the declaring type; for example, the `Text` property is a property of `TextButton`, which declares it.</span></span> <span data-ttu-id="f0d3d-120">Szczególnym rodzajem właściwości zależności jest dołączona właściwość zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-120">A special kind of dependency property is the attached dependency property.</span></span>

 <span data-ttu-id="f0d3d-121">Klasycznym przykładem dołączonej właściwości jest <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> Właściwość.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-121">A classic example of an attached property is the <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="f0d3d-122">Właściwość reprezentuje położenie kolumny przycisku (nie siatki), ale ma zastosowanie tylko wtedy, gdy przycisk jest zawarty w siatce i dlatego jest "dołączony" do przycisków według siatki.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-122">The property represents Button’s (not Grid’s) column position, but it is only relevant if the Button is contained in a Grid, and so it's "attached" to Buttons by Grids.</span></span>

```xaml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>

    <Button Grid.Column="0">Click</Button>
    <Button Grid.Column="1">Clack</Button>
</Grid>
```

 <span data-ttu-id="f0d3d-123">Definicja dołączonej właściwości wygląda głównie podobnie jak w przypadku właściwości zależności regularnej, z tą różnicą, że metody dostępu są reprezentowane za pomocą statycznych metod get i set:</span><span class="sxs-lookup"><span data-stu-id="f0d3d-123">The definition of an attached property looks mostly like that of a regular dependency property, except that the accessors are represented by static Get and Set methods:</span></span>

```csharp
public class Grid {

    public static int GetColumn(DependencyObject obj) {
        return (int)obj.GetValue(ColumnProperty);
    }

    public static void SetColumn(DependencyObject obj, int value) {
        obj.SetValue(ColumnProperty,value);
    }

    public static readonly DependencyProperty ColumnProperty =
        DependencyProperty.RegisterAttached(
            "Column",
            typeof(int),
            typeof(Grid)
    );
}
```

## <a name="dependency-property-validation"></a><span data-ttu-id="f0d3d-124">Walidacja właściwości zależności</span><span class="sxs-lookup"><span data-stu-id="f0d3d-124">Dependency Property Validation</span></span>

 <span data-ttu-id="f0d3d-125">Właściwości często implementują to, co jest nazywane walidacją.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-125">Properties often implement what is called validation.</span></span> <span data-ttu-id="f0d3d-126">Logika walidacji jest wykonywana, gdy podejmowana jest próba zmiany wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-126">Validation logic executes when an attempt is made to change the value of a property.</span></span>

 <span data-ttu-id="f0d3d-127">Metody dostępu właściwości zależności nie mogą zawierać dowolnego kodu weryfikacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-127">Unfortunately dependency property accessors cannot contain arbitrary validation code.</span></span> <span data-ttu-id="f0d3d-128">Zamiast tego należy określić logikę walidacji właściwości zależności podczas rejestracji właściwości.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-128">Instead, dependency property validation logic needs to be specified during property registration.</span></span>

 <span data-ttu-id="f0d3d-129">❌ NIE należy umieszczać logiki walidacji właściwości zależności we właściwościach dostępu.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-129">❌ DO NOT put dependency property validation logic in the property’s accessors.</span></span> <span data-ttu-id="f0d3d-130">Zamiast tego należy przekazać wywołanie zwrotne walidacji do `DependencyProperty.Register` metody.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-130">Instead, pass a validation callback to `DependencyProperty.Register` method.</span></span>

## <a name="dependency-property-change-notifications"></a><span data-ttu-id="f0d3d-131">Powiadomienia o zmianie właściwości zależności</span><span class="sxs-lookup"><span data-stu-id="f0d3d-131">Dependency Property Change Notifications</span></span>

 <span data-ttu-id="f0d3d-132">❌ NIE implementuje logiki powiadomień o zmianach we właściwościach dostępu zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-132">❌ DO NOT implement change notification logic in dependency property accessors.</span></span> <span data-ttu-id="f0d3d-133">Właściwości zależności mają wbudowaną funkcję powiadomień o zmianach, która musi być używana przez dostarczenie wywołania zwrotnego powiadomienia o zmianie <xref:System.Windows.PropertyMetadata> .</span><span class="sxs-lookup"><span data-stu-id="f0d3d-133">Dependency properties have a built-in change notifications feature that must be used by supplying a change notification callback to the <xref:System.Windows.PropertyMetadata>.</span></span>

## <a name="dependency-property-value-coercion"></a><span data-ttu-id="f0d3d-134">Wymuszone przekształcenie wartości właściwości zależności</span><span class="sxs-lookup"><span data-stu-id="f0d3d-134">Dependency Property Value Coercion</span></span>

 <span data-ttu-id="f0d3d-135">Wymuszanie właściwości odbywa się, gdy wartość określona dla metody ustawiającej właściwość jest modyfikowana przez metodę ustawiającą przed faktycznym zmodyfikowaniem magazynu właściwości.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-135">Property coercion takes place when the value given to a property setter is modified by the setter before the property store is actually modified.</span></span>

 <span data-ttu-id="f0d3d-136">❌ NIE Wdrażaj logiki przekształcenia we właściwościach dostępu zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d3d-136">❌ DO NOT implement coercion logic in dependency property accessors.</span></span>

 <span data-ttu-id="f0d3d-137">Właściwości zależności mają wbudowaną funkcję przymusu i mogą być używane przez dostarczenie wywołania zwrotnego przekształcenia do elementu `PropertyMetadata` .</span><span class="sxs-lookup"><span data-stu-id="f0d3d-137">Dependency properties have a built-in coercion feature, and it can be used by supplying a coercion callback to the `PropertyMetadata`.</span></span>

 <span data-ttu-id="f0d3d-138">*Fragmenty © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*</span><span class="sxs-lookup"><span data-stu-id="f0d3d-138">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="f0d3d-139">*Ponownie Wydrukowano przez uprawnienie Pearson Education, Inc. z [wytycznych dotyczących projektowania platformy: konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, 2. wydanie](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*</span><span class="sxs-lookup"><span data-stu-id="f0d3d-139">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="f0d3d-140">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="f0d3d-140">See also</span></span>

- [<span data-ttu-id="f0d3d-141">Wskazówki dotyczące projektowania struktury</span><span class="sxs-lookup"><span data-stu-id="f0d3d-141">Framework Design Guidelines</span></span>](index.md)
- [<span data-ttu-id="f0d3d-142">Typowe wzorce projektowe</span><span class="sxs-lookup"><span data-stu-id="f0d3d-142">Common Design Patterns</span></span>](common-design-patterns.md)
