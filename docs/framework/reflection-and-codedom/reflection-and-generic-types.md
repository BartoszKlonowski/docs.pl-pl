---
title: Odbicie i typy ogólne
description: Wprowadzenie do odbicia i typów ogólnych w programie .NET. W przeciwieństwie do zwykłego typu, typ ogólny jest skojarzony z zestawem parametrów typu lub argumentów typu.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET Framework], reflection emit
- reflection emit, generic types
- reflection, generic types
- type arguments
- generics [.NET Framework], reflection
- viewing type information
- type information, viewing
- types, generic
- type parameters
ms.assetid: f7180fc5-dd41-42d4-8a8e-1b34288e06de
ms.openlocfilehash: 2add589d171163d5497e80ed7b7990c3596add20
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96259918"
---
# <a name="reflection-and-generic-types"></a>Odbicie i typy ogólne

Z punktu widzenia odbicia różnica między typem ogólnym i typem zwykłym polega na tym, że typ ogólny jest skojarzony z tym zestawem parametrów typu (jeśli jest to definicja typu ogólnego) lub argumentów typu (jeśli jest to typ skonstruowany). Metoda ogólna różni się od zwykłej metody w taki sam sposób.  
  
 Istnieją dwa klucze, aby zrozumieć, w jaki sposób odbicie obsługuje typy ogólne i metody:  
  
- Parametry typu dla definicji typu ogólnego i definicji metod ogólnych są reprezentowane przez wystąpienia <xref:System.Type> klasy.  
  
    > [!NOTE]
    > Wiele właściwości i metod <xref:System.Type> ma inne zachowanie, gdy <xref:System.Type> obiekt reprezentuje parametr typu ogólnego. Te różnice opisano w tematach dotyczących właściwości i metod. Na przykład zobacz <xref:System.Type.IsAutoClass%2A> i <xref:System.Type.DeclaringType%2A>. Ponadto niektóre elementy członkowskie są prawidłowe tylko wtedy, gdy <xref:System.Type> obiekt reprezentuje parametr typu ogólnego. Na przykład zobacz <xref:System.Type.GetGenericTypeDefinition%2A>.  
  
- Jeśli wystąpienie <xref:System.Type> reprezentuje typ generyczny, zawiera tablicę typów reprezentujących parametry typu (dla definicji typu ogólnego) lub argumentów typu (dla konstruowanych typów). Ta sama wartość jest równa wystąpieniu <xref:System.Reflection.MethodInfo> klasy, która reprezentuje metodę rodzajową.  
  
 Odbicie zawiera metody <xref:System.Type> i <xref:System.Reflection.MethodInfo> , które umożliwiają dostęp do tablicy parametrów typu i określanie, czy wystąpienie <xref:System.Type> reprezentuje parametr typu, czy rzeczywisty typ.  
  
 Przykładowy kod pokazujący metody omówione tutaj można znaleźć w temacie [How to: badanie i Tworzenie wystąpień typów ogólnych za pomocą odbicia](how-to-examine-and-instantiate-generic-types-with-reflection.md).  
  
 W poniższej dyskusji założono znajomość terminologii ogólnych, takich jak różnica między parametrami typu a argumentami i otwartymi lub zamkniętymi typami skonstruowanymi. Aby uzyskać więcej informacji, zobacz [Ogólne](../../standard/generics/index.md).  

## <a name="is-this-a-generic-type-or-method"></a>Czy jest to ogólny typ czy metoda?  

 W przypadku użycia odbicia do badania nieznanego typu reprezentowanego przez wystąpienie klasy <xref:System.Type> , należy użyć <xref:System.Type.IsGenericType%2A> właściwości, aby określić, czy nieznany typ jest ogólny. Zwraca, `true` Jeśli typ jest ogólny. Podobnie podczas badania nieznanej metody reprezentowanej przez wystąpienie <xref:System.Reflection.MethodInfo> klasy, należy użyć <xref:System.Reflection.MethodBase.IsGenericMethod%2A> właściwości, aby określić, czy metoda jest ogólna.  
  
### <a name="is-this-a-generic-type-or-method-definition"></a>Czy jest to typ ogólny czy definicja metody?  

 Użyj <xref:System.Type.IsGenericTypeDefinition%2A> właściwości, aby określić, czy <xref:System.Type> obiekt reprezentuje definicję typu ogólnego, i użyj metody, <xref:System.Reflection.MethodBase.IsGenericMethodDefinition%2A> Aby określić, czy <xref:System.Reflection.MethodInfo> reprezentuje definicję metody ogólnej.  
  
 Typy ogólne i definicje metod są szablonami, z których tworzone są rodzaje instantiable. Typy ogólne w bibliotece klas .NET Framework, takie jak <xref:System.Collections.Generic.Dictionary%602> , są definicjami typów ogólnych.  
  
### <a name="is-the-type-or-method-open-or-closed"></a>Czy typ lub metoda jest otwarta lub ZAMKNIĘTA?  

 Typ ogólny lub metoda jest zamykana, jeśli podinstantiable typy zostały zastąpione dla wszystkich parametrów typu, w tym wszystkich parametrów typu wszystkich typów otaczających. Wystąpienie typu ogólnego można utworzyć tylko wtedy, gdy jest ono zamknięte. <xref:System.Type.ContainsGenericParameters%2A?displayProperty=nameWithType>Właściwość zwraca, `true` Jeśli typ jest otwarty. Dla metod <xref:System.Reflection.MethodBase.ContainsGenericParameters%2A?displayProperty=nameWithType> Metoda wykonuje tę samą funkcję.

## <a name="generating-closed-generic-types"></a>Generowanie zamkniętych typów ogólnych  

 Jeśli masz typ ogólny lub definicję metody, użyj <xref:System.Type.MakeGenericType%2A> metody, aby utworzyć zamknięty typ ogólny lub <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A> metodę w celu utworzenia <xref:System.Reflection.MethodInfo> dla zamkniętej metody ogólnej.  
  
### <a name="getting-the-generic-type-or-method-definition"></a>Pobieranie typu ogólnego lub definicji metody  

 Jeśli masz otwarty typ ogólny lub metodę, która nie jest typem ogólnym lub definicją metody, nie można utworzyć wystąpień tego wystąpienia i nie można podać parametrów typu, które nie są spełnione. Musisz mieć typ ogólny lub definicję metody. Użyj <xref:System.Type.GetGenericTypeDefinition%2A> metody w celu uzyskania definicji typu ogólnego lub <xref:System.Reflection.MethodInfo.GetGenericMethodDefinition%2A> metody w celu uzyskania definicji metody ogólnej.  
  
 Na przykład jeśli masz <xref:System.Type> obiekt reprezentujący `Dictionary<int, string>` ( `Dictionary(Of Integer, String)` w Visual Basic) i chcesz utworzyć typ `Dictionary<string, MyClass>` , możesz użyć <xref:System.Type.GetGenericTypeDefinition%2A> metody, aby uzyskać <xref:System.Type> reprezentowania, `Dictionary<TKey, TValue>` a następnie użyć <xref:System.Type.MakeGenericType%2A> metody w celu utworzenia <xref:System.Type> reprezentowania `Dictionary<int, MyClass>` .  
  
 Przykład otwartego typu ogólnego, który nie jest typem ogólnym, znajduje się w dalszej części tego tematu.

## <a name="examining-type-arguments-and-type-parameters"></a>Badanie argumentów typu i parametrów typu  

 Użyj <xref:System.Type.GetGenericArguments%2A?displayProperty=nameWithType> metody, aby uzyskać tablicę <xref:System.Type> obiektów reprezentujących parametry typu lub argumenty typu ogólnego, i użyj metody, <xref:System.Reflection.MethodInfo.GetGenericArguments%2A?displayProperty=nameWithType> Aby zrobić to samo dla metody ogólnej.  
  
 Gdy wiesz, że <xref:System.Type> obiekt reprezentuje parametr typu, można odpowiedzieć na wiele dodatkowych pytań. Można określić źródło parametru typu, jego pozycję i jego ograniczenia.  
  
### <a name="type-parameter-or-type-argument"></a>Parametr typu lub argument typu  

 Aby określić, czy konkretny element tablicy jest parametrem typu, czy typem argumentu, użyj <xref:System.Type.IsGenericParameter%2A> właściwości. <xref:System.Type.IsGenericParameter%2A>Właściwość jest, `true` Jeśli element jest parametrem typu.  
  
 Typ ogólny może być otwarty bez standardowej definicji typu, w którym to przypadku ma kombinację argumentów typu i parametrów typu. Na przykład, w poniższym kodzie Klasa `D` pochodzi od typu utworzonego przez podstawianie pierwszego parametru typu `D` dla drugiego parametru typu `B` .  
  
```csharp  
class B<T, U> {}  
class D<V, W> : B<int, V> {}  
```  
  
```vb  
Class B(Of T, U)  
End Class  
Class D(Of V, W)  
    Inherits B(Of Integer, V)  
End Class  
```  
  
```cpp  
generic<typename T, typename U> ref class B {};  
generic<typename V, typename W> ref class D : B<int, V> {};  
```  
  
 Jeśli uzyskasz <xref:System.Type> obiekt reprezentujący `D<V, W>` i użyjesz <xref:System.Type.BaseType%2A> właściwości, aby uzyskać swój typ podstawowy, wynikiem `type B<int, V>` jest otwarty, ale nie jest to definicja typu ogólnego.  
  
### <a name="source-of-a-generic-parameter"></a>Źródło parametru generycznego  

 Parametry typu ogólnego mogą pochodzić z typu, który badasz, z typu otaczającego lub z metody ogólnej. Źródło parametru typu ogólnego można określić w następujący sposób:  
  
- Najpierw użyj właściwości, <xref:System.Type.DeclaringMethod%2A> Aby określić, czy parametr typu pochodzi z metody ogólnej. Jeśli wartość właściwości nie jest odwołaniem null ( `Nothing` w Visual Basic), źródłem jest metoda ogólna.  
  
- Jeśli źródło nie jest metodą rodzajową, użyj właściwości, <xref:System.Type.DeclaringType%2A> Aby określić typ ogólny, do którego należy parametr typu ogólnego.  
  
 Jeśli parametr typu należy do metody ogólnej, <xref:System.Type.DeclaringType%2A> Właściwość zwraca typ, który deklaruje metodę rodzajową, która jest istotna.  
  
### <a name="position-of-a-generic-parameter"></a>Pozycja parametru generycznego  

 W rzadkich sytuacjach należy określić pozycję parametru typu na liście parametrów typu swojej klasy deklarującej. Załóżmy na przykład, że masz <xref:System.Type> obiekt reprezentujący `B<int, V>` Typ z poprzedniego przykładu. <xref:System.Type.GetGenericArguments%2A>Metoda zapewnia listę argumentów typu, a podczas badania można `V` użyć <xref:System.Type.DeclaringMethod%2A> <xref:System.Type.DeclaringType%2A> właściwości i do odnajdywania, skąd pochodzi. Następnie można użyć właściwości, <xref:System.Type.GenericParameterPosition%2A> Aby określić jej położenie na liście parametrów typu, gdzie został zdefiniowany. W tym przykładzie `V` znajduje się na pozycji 0 (zero) na liście parametrów typu, gdzie została zdefiniowana.  
  
### <a name="base-type-and-interface-constraints"></a>Ograniczenia typu podstawowego i interfejsu  

 Użyj <xref:System.Type.GetGenericParameterConstraints%2A> metody w celu uzyskania ograniczenia typu podstawowego i ograniczeń interfejsu parametru typu. Kolejność elementów tablicy nie jest istotna. Element reprezentuje ograniczenie interfejsu, jeśli jest typem interfejsu.  
  
### <a name="generic-parameter-attributes"></a>Atrybuty parametru generycznego  

 <xref:System.Type.GenericParameterAttributes%2A>Właściwość pobiera <xref:System.Reflection.GenericParameterAttributes> wartość wskazującą wariancję (kowariancję lub kontrawariancja) oraz specjalne ograniczenia parametru typu.  
  
#### <a name="covariance-and-contravariance"></a>Kowariancja i kontrawariancja  

 Aby określić, czy parametr typu jest współvariant lub kontrawariantne, Zastosuj <xref:System.Reflection.GenericParameterAttributes.VarianceMask?displayProperty=nameWithType> maskę do <xref:System.Reflection.GenericParameterAttributes> wartości zwracanej przez <xref:System.Type.GenericParameterAttributes%2A> Właściwość. Jeśli wynik to <xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType> , parametr typu jest niezmienny. Zobacz [Kowariancja i kontrawariancja](../../standard/generics/covariance-and-contravariance.md).  
  
#### <a name="special-constraints"></a>Ograniczenia specjalne  

 Aby określić specjalne ograniczenia parametru typu, Zastosuj <xref:System.Reflection.GenericParameterAttributes.SpecialConstraintMask?displayProperty=nameWithType> maskę do <xref:System.Reflection.GenericParameterAttributes> wartości zwracanej przez <xref:System.Type.GenericParameterAttributes%2A> Właściwość. Jeśli wynik to <xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType> , nie ma żadnych specjalnych ograniczeń. Parametr typu może być ograniczony jako typ referencyjny, jako typ wartości niedopuszczający wartości null i mieć konstruktora bez parametrów.

## <a name="invariants"></a>Nieposiadające wariantów  

 Aby zapoznać się z tabelą warunków nievariant dla typowych terminów w odbiciu dla typów ogólnych, zobacz <xref:System.Type.IsGenericType%2A?displayProperty=nameWithType> . Dodatkowe warunki dotyczące metod ogólnych można znaleźć w temacie <xref:System.Reflection.MethodBase.IsGenericMethod%2A?displayProperty=nameWithType> .  

## <a name="related-topics"></a>Tematy pokrewne  
  
|Tytuł|Opis|  
|-----------|-----------------|  
|[Instrukcje: Badanie i tworzenie wystąpień typów ogólnych za pomocą odbicia](how-to-examine-and-instantiate-generic-types-with-reflection.md)|Pokazuje, jak używać właściwości i metod <xref:System.Type> i <xref:System.Reflection.MethodInfo> do badania typów ogólnych.|  
|[Typy ogólne](../../standard/generics/index.md)|Opisuje funkcję generyczną i sposób jej obsługi w .NET Framework.|  
|[Instrukcje: Definiowanie typu ogólnego przy użyciu emisji odbicia](how-to-define-a-generic-type-with-reflection-emit.md)|Pokazuje, jak używać emisji odbicia do generowania typów ogólnych w zestawach dynamicznych.|  
|[Wyświetlanie informacji o typie](viewing-type-information.md)|Opisuje <xref:System.Type> klasę i zawiera przykłady kodu, które ilustrują sposób użycia <xref:System.Type> z różnymi klasami odbicia w celu uzyskania informacji na temat konstruktorów, metod, pól, właściwości i zdarzeń.|
