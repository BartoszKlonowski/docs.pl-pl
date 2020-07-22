---
title: 'Instrukcje: Badanie i tworzenie wystąpień typów ogólnych za pomocą odbicia'
description: Zobacz, jak sprawdzić i utworzyć wystąpienia typów ogólnych z odbiciem. Użyj właściwości IsGenericType, IsGenericParameter i GenericParameterPosition.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection, generic types
- generics [.NET Framework], reflection
ms.assetid: f93b03b0-1778-43fc-bc6d-35983d210e74
ms.openlocfilehash: b57a0ed0c809da442dc9fcf202ad364060971f80
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/21/2020
ms.locfileid: "86865102"
---
# <a name="how-to-examine-and-instantiate-generic-types-with-reflection"></a>Instrukcje: Badanie i tworzenie wystąpień typów ogólnych za pomocą odbicia
Informacje o typach ogólnych są uzyskiwane w taki sam sposób jak informacje o innych typach: przez badanie <xref:System.Type> obiektu, który reprezentuje typ ogólny. Różnica między zasadami polega na tym, że typ ogólny ma listę <xref:System.Type> obiektów reprezentujących parametry typu ogólnego. Pierwsza procedura w tej sekcji bada typy ogólne.  
  
 Można utworzyć <xref:System.Type> obiekt reprezentujący skonstruowany typ według argumentów typu powiązania do parametrów typu definicji typu ogólnego. Druga procedura pokazuje to.  
  
### <a name="to-examine-a-generic-type-and-its-type-parameters"></a>Aby przejrzeć typ ogólny i jego parametry typu  
  
1. Pobierz wystąpienie <xref:System.Type> reprezentujące typ ogólny. W poniższym kodzie, typ jest uzyskiwany przy użyciu operatora języka C# `typeof` ( `GetType` w Visual Basic, `typeid` w Visual C++). Zapoznaj się z <xref:System.Type> tematem klasy, aby poznać inne sposoby pobierania <xref:System.Type> obiektu. Należy zauważyć, że w pozostałej części tej procedury typ jest zawarty w parametrze metody o nazwie `t` .  
  
     [!code-cpp[HowToGeneric#2](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#2)]
     [!code-csharp[HowToGeneric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#2)]
     [!code-vb[HowToGeneric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#2)]  
  
2. Użyj <xref:System.Type.IsGenericType%2A> właściwości, aby określić, czy typ jest ogólny, i Użyj <xref:System.Type.IsGenericTypeDefinition%2A> właściwości, aby określić, czy typ jest definicją typu ogólnego.  
  
     [!code-cpp[HowToGeneric#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#3)]
     [!code-csharp[HowToGeneric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#3)]
     [!code-vb[HowToGeneric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#3)]  
  
3. Pobierz tablicę zawierającą argumenty typu ogólnego przy użyciu <xref:System.Type.GetGenericArguments%2A> metody.  
  
     [!code-cpp[HowToGeneric#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#4)]
     [!code-csharp[HowToGeneric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#4)]
     [!code-vb[HowToGeneric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#4)]  
  
4. Dla każdego argumentu typu należy określić, czy jest to parametr typu (na przykład w definicji typu ogólnego) czy typ, który został określony dla parametru typu (na przykład w typie konstruowanym), przy użyciu <xref:System.Type.IsGenericParameter%2A> właściwości.  
  
     [!code-cpp[HowToGeneric#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#5)]
     [!code-csharp[HowToGeneric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#5)]
     [!code-vb[HowToGeneric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#5)]  
  
5. W systemie typów parametr typu ogólnego jest reprezentowany przez wystąpienie klasy <xref:System.Type> , podobnie jak typy zwykłe. Poniższy kod wyświetla nazwę i położenie parametru <xref:System.Type> obiektu, który reprezentuje parametr typu ogólnego. Pozycja parametru to uproszczone informacje. jest on bardziej interesujący podczas badania parametru typu, który został użyty jako argument typu innego typu ogólnego.  
  
     [!code-cpp[HowToGeneric#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#6)]
     [!code-csharp[HowToGeneric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#6)]
     [!code-vb[HowToGeneric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#6)]  
  
6. Określanie ograniczenia typu podstawowego i ograniczeń interfejsu parametru typu ogólnego przy użyciu <xref:System.Type.GetGenericParameterConstraints%2A> metody w celu uzyskania wszystkich ograniczeń w pojedynczej tablicy. Ograniczenia nie są gwarantowane w żadnej określonej kolejności.  
  
     [!code-cpp[HowToGeneric#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#7)]
     [!code-csharp[HowToGeneric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#7)]
     [!code-vb[HowToGeneric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#7)]  
  
7. Użyj <xref:System.Type.GenericParameterAttributes%2A> właściwości, aby odnaleźć specjalne ograniczenia dla parametru typu, na przykład wymagając, aby był typem referencyjnym. Właściwość zawiera również wartości, które reprezentują wariancję, która może być maskowany, jak pokazano w poniższym kodzie.  
  
     [!code-cpp[HowToGeneric#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#8)]
     [!code-csharp[HowToGeneric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#8)]
     [!code-vb[HowToGeneric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#8)]  
  
8. Specjalne atrybuty ograniczenia są flagami, a ta sama flaga ( <xref:System.Reflection.GenericParameterAttributes.None?displayProperty=nameWithType> ), która reprezentuje żadne specjalne ograniczenia, również nie reprezentuje kowariancji lub kontrawariancja. W ten sposób, aby testować dla dowolnego z tych warunków, należy użyć odpowiedniej maski. W takim przypadku należy użyć <xref:System.Reflection.GenericParameterAttributes.SpecialConstraintMask?displayProperty=nameWithType> do izolowania specjalnych flag ograniczeń.  
  
     [!code-cpp[HowToGeneric#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#9)]
     [!code-csharp[HowToGeneric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#9)]
     [!code-vb[HowToGeneric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#9)]  
  
## <a name="constructing-an-instance-of-a-generic-type"></a>Konstruowanie wystąpienia typu ogólnego  
 Typ ogólny jest podobny do szablonu. Nie można tworzyć wystąpień tego elementu, chyba że określono typy rzeczywiste dla parametrów typu ogólnego. Aby to zrobić w czasie wykonywania, przy użyciu odbicia wymaga <xref:System.Type.MakeGenericType%2A> metody.  
  
#### <a name="to-construct-an-instance-of-a-generic-type"></a>Aby skonstruować wystąpienie typu ogólnego  
  
1. Pobierz <xref:System.Type> obiekt, który reprezentuje typ ogólny. Poniższy kod pobiera typ ogólny <xref:System.Collections.Generic.Dictionary%602> na dwa różne sposoby: przy użyciu <xref:System.Type.GetType%28System.String%29?displayProperty=nameWithType> przeciążenia metody z ciągiem opisującym typ oraz przez wywołanie <xref:System.Type.GetGenericTypeDefinition%2A> metody dla konstruowanego typu `Dictionary\<String, Example>` ( `Dictionary(Of String, Example)` w Visual Basic). <xref:System.Type.MakeGenericType%2A>Metoda wymaga definicji typu ogólnego.  
  
     [!code-cpp[HowToGeneric#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#10)]
     [!code-csharp[HowToGeneric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#10)]
     [!code-vb[HowToGeneric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#10)]  
  
2. Skonstruuj tablicę argumentów typu, które mają zostać zastąpione dla parametrów typu. Tablica musi zawierać poprawną liczbę <xref:System.Type> obiektów w tej samej kolejności, w jakiej występują na liście parametrów typu. W tym przypadku klucz (pierwszy typ parametru) jest typu <xref:System.String> , a wartości w słowniku są wystąpieniami klasy o nazwie `Example` .  
  
     [!code-cpp[HowToGeneric#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#11)]
     [!code-csharp[HowToGeneric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#11)]
     [!code-vb[HowToGeneric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#11)]  
  
3. Wywołaj <xref:System.Type.MakeGenericType%2A> metodę, aby powiązać argumenty typu z parametrami typu i skonstruować typ.  
  
     [!code-cpp[HowToGeneric#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#12)]
     [!code-csharp[HowToGeneric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#12)]
     [!code-vb[HowToGeneric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#12)]  
  
4. Użyj <xref:System.Activator.CreateInstance%28System.Type%29> przeciążenia metody, aby utworzyć obiekt typu złożonego. Poniższy kod przechowuje dwa wystąpienia `Example` klasy w obiekcie będącym wynikiem `Dictionary<String, Example>` .  
  
     [!code-cpp[HowToGeneric#13](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#13)]
     [!code-csharp[HowToGeneric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#13)]
     [!code-vb[HowToGeneric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#13)]  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kodu definiuje metodę, `DisplayGenericType` Aby przeanalizować definicje typów ogólnych i skonstruowane typy używane w kodzie i wyświetlić ich informacje. `DisplayGenericType`Metoda pokazuje, jak używać <xref:System.Type.IsGenericType%2A> właściwości, i <xref:System.Type.IsGenericParameter%2A> <xref:System.Type.GenericParameterPosition%2A> i <xref:System.Type.GetGenericArguments%2A> metody.  
  
 W przykładzie zdefiniowano również `DisplayGenericParameter` metodę w celu sprawdzenia parametru typu ogólnego i wyświetlenia jego ograniczeń.  
  
 Przykładowy kod definiuje zestaw typów testów, w tym typ ogólny, który ilustruje ograniczenia parametru typu, i pokazuje, jak wyświetlić informacje o tych typach.  
  
 Przykład tworzy typ z <xref:System.Collections.Generic.Dictionary%602> klasy przez utworzenie tablicy argumentów typu i wywołanie <xref:System.Type.MakeGenericType%2A> metody. Program porównuje <xref:System.Type> obiekt skonstruowany przy użyciu <xref:System.Type.MakeGenericType%2A> z <xref:System.Type> obiektem uzyskanym przy użyciu `typeof` ( `GetType` w Visual Basic), pokazując, że są one takie same. Podobnie program używa <xref:System.Type.GetGenericTypeDefinition%2A> metody do uzyskania definicji typu ogólnego złożonego typu i porównuje go z <xref:System.Type> obiektem reprezentującym <xref:System.Collections.Generic.Dictionary%602> klasę.  
  
 [!code-cpp[HowToGeneric#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#1)]
 [!code-csharp[HowToGeneric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#1)]
 [!code-vb[HowToGeneric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#1)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Type>
- <xref:System.Reflection.MethodInfo>
- [Odbicie i typy ogólne](reflection-and-generic-types.md)
- [Wyświetlanie informacji o typie](viewing-type-information.md)
- [Typy ogólne](../../standard/generics/index.md)
