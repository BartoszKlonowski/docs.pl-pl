---
title: 'Instrukcje: Wywoływanie funkcji definiowanych przez model jako metod obiektu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 33bae8a8-4ed8-4a1f-85d1-c62ff288cc61
ms.openlocfilehash: 5e5ae2fd838a34d7f665b23a14db2a599367e801
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197797"
---
# <a name="how-to-call-model-defined-functions-as-object-methods"></a>Instrukcje: Wywoływanie funkcji definiowanych przez model jako metod obiektu

W tym temacie opisano sposób wywoływania funkcji zdefiniowanej przez model jako metody na <xref:System.Data.Objects.ObjectContext> obiekcie lub jako metody statycznej klasy niestandardowej. *Funkcja zdefiniowana przez model* jest funkcją zdefiniowaną w modelu koncepcyjnym. Procedury w temacie opisują sposób wywołania tych funkcji bezpośrednio zamiast wywoływania ich z LINQ to Entities zapytań. Aby uzyskać informacje o wywoływaniu funkcji zdefiniowanych przez model w zapytaniach LINQ to Entities, zobacz [How to: Call defined model Functions in zapytania](how-to-call-model-defined-functions-in-queries.md).  
  
 Niezależnie od tego, czy wywoływana jest funkcja zdefiniowana przez model jako <xref:System.Data.Objects.ObjectContext> Metoda, czy jako metoda statyczna klasy niestandardowej, należy najpierw zmapować metodę do funkcji zdefiniowanej przez model przy użyciu <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> . Jednak podczas definiowania metody <xref:System.Data.Objects.ObjectContext> klasy należy użyć <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> właściwości, aby uwidocznić dostawcę LINQ, podczas gdy definiujemy metodę statyczną dla klasy niestandardowej, należy użyć <xref:System.Linq.IQueryable.Provider%2A> właściwości, aby uwidocznić dostawcę LINQ. Aby uzyskać więcej informacji, zobacz przykłady, które postępują zgodnie z poniższymi procedurami.  
  
 Poniższe procedury zapewniają konspekt wysokiego poziomu na potrzeby wywoływania funkcji zdefiniowanej przez model jako metody na <xref:System.Data.Objects.ObjectContext> obiekcie oraz jako metody statycznej klasy niestandardowej. Poniższe przykłady zawierają więcej szczegółów na temat kroków w procedurach. W procedurach przyjęto założenie, że zdefiniowano funkcję w modelu koncepcyjnym. Aby uzyskać więcej informacji, zobacz [How to: define Custom Functions w modelu koncepcyjnym](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).  
  
### <a name="to-call-a-model-defined-function-as-a-method-on-an-objectcontext-object"></a>Wywoływanie funkcji zdefiniowanej przez model jako metody obiektu ObjectContext  
  
1. Dodaj plik źródłowy, aby zwiększyć klasę częściową pochodną <xref:System.Data.Objects.ObjectContext> klasy, automatycznie wygenerowaną przez narzędzia Entity Framework. Zdefiniowanie klasy zastępczej środowiska CLR w osobnym pliku źródłowym uniemożliwi utratę zmian po ponownym wygenerowanym pliku.  
  
2. Dodaj do klasy metodę środowiska uruchomieniowego języka wspólnego (CLR) <xref:System.Data.Objects.ObjectContext> , która wykonuje następujące czynności:  
  
    - Mapuje do funkcji zdefiniowanej w modelu koncepcyjnym. Aby zmapować metodę, należy zastosować <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> do metody. Należy zauważyć, <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> że <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> Parametry i atrybutu są nazwą przestrzeni nazw modelu koncepcyjnego i nazwą funkcji w modelu koncepcyjnym. Rozpoznawanie nazw funkcji dla LINQ jest rozróżniana wielkość liter.  
  
    - Zwraca wyniki <xref:System.Linq.IQueryProvider.Execute%2A> metody, która jest zwracana przez <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> Właściwość.  
  
3. Wywołaj metodę jako element członkowski w wystąpieniu <xref:System.Data.Objects.ObjectContext> klasy.  
  
### <a name="to-call-a-model-defined-function-as-static-method-on-a-custom-class"></a>Wywoływanie funkcji zdefiniowanej przez model jako metody statycznej w klasie niestandardowej  
  
1. Dodaj klasę do aplikacji za pomocą metody statycznej, która wykonuje następujące czynności:  
  
    - Mapuje do funkcji zdefiniowanej w modelu koncepcyjnym. Aby zmapować metodę, należy zastosować <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> do metody. Należy zauważyć, <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> że <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> Parametry i atrybutu są nazwą przestrzeni nazw modelu koncepcyjnego i nazwą funkcji w modelu koncepcyjnym.  
  
    - Akceptuje <xref:System.Linq.IQueryable> argument.  
  
    - Zwraca wyniki <xref:System.Linq.IQueryProvider.Execute%2A> metody, która jest zwracana przez <xref:System.Linq.IQueryable.Provider%2A> Właściwość.  
  
2. Wywołaj metodę jako składową metodę statyczną w klasie niestandardowej  
  
## <a name="example"></a>Przykład  

 **Wywoływanie funkcji zdefiniowanej przez model jako metody dla obiektu ObjectContext**  
  
 Poniższy przykład ilustruje sposób wywołania funkcji zdefiniowanej przez model jako metody w <xref:System.Data.Objects.ObjectContext> obiekcie. W przykładzie zastosowano [model sprzedaży AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  
 Rozważmy poniższe funkcje modelu koncepcyjnego, które zwracają przychód produktu dla określonego produktu. (Aby uzyskać informacje na temat dodawania funkcji do modelu koncepcyjnego, zobacz [How to: define Custom Functions w modelu koncepcyjnym](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))).  
  
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  

## <a name="example"></a>Przykład  

 Poniższy kod dodaje metodę do `AdventureWorksEntities` klasy, która jest mapowana na powyższą funkcję modelu koncepcyjnego.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## <a name="example"></a>Przykład  

 Poniższy kod wywołuje metodę powyżej, aby wyświetlić przychód produktu dla określonego produktu:  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład ilustruje sposób wywoływania funkcji zdefiniowanej przez model, która zwraca kolekcję (jako <xref:System.Linq.IQueryable%601> obiekt). Rozważmy poniższe funkcje modelu koncepcyjnego, które zwracają wszystkie `SalesOrderDetails` dla danego identyfikatora produktu.  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## <a name="example"></a>Przykład  

 Poniższy kod dodaje metodę do `AdventureWorksEntities` klasy, która jest mapowana na powyższą funkcję modelu koncepcyjnego.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## <a name="example"></a>Przykład  

 Poniższy kod wywołuje metodę. Zwróć uwagę, że zwrócone <xref:System.Linq.IQueryable%601> zapytanie jest bardziej udoskonalane w celu zwrócenia sum wierszy dla każdego z nich `SalesOrderDetail` .  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## <a name="example"></a>Przykład  

 **Wywoływanie funkcji zdefiniowanej przez model jako metody statycznej w klasie niestandardowej**  
  
 W następnym przykładzie pokazano sposób wywołania funkcji zdefiniowanej przez model jako metody statycznej klasy niestandardowej. W przykładzie zastosowano [model sprzedaży AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  
> [!NOTE]
> W przypadku wywołania funkcji zdefiniowanej przez model jako metody statycznej klasy niestandardowej funkcja zdefiniowana przez model musi akceptować kolekcję i zwracać agregację wartości w kolekcji.  
  
 Rozważmy poniższe funkcje modelu koncepcyjnego zwracające przychód produktu dla kolekcji SalesOrderDetail. (Aby uzyskać informacje na temat dodawania funkcji do modelu koncepcyjnego, zobacz [How to: define Custom Functions w modelu koncepcyjnym](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))).  
  
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]
  
## <a name="example"></a>Przykład  

 Poniższy kod dodaje klasę do aplikacji, która zawiera statyczną metodę, która jest mapowana na powyższą funkcję modelu koncepcyjnego.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## <a name="example"></a>Przykład  

 Poniższy kod wywołuje metodę powyżej, aby wyświetlić przychód produktu dla kolekcji SalesOrderDetail:  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## <a name="see-also"></a>Zobacz też

- [Plik. edmx — Omówienie](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [Zapytania w składniku LINQ to Entities](queries-in-linq-to-entities.md)
- [Wywoływanie funkcji w zapytaniach składnika LINQ to Entities](calling-functions-in-linq-to-entities-queries.md)
