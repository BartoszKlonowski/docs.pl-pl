---
title: Napisz prosty program równoległy używający metody Parallel. ForEach
description: W tym artykule dowiesz się, jak włączyć równoległość danych w programie .NET. Napisz pętlę Parallel. ForEach dla dowolnego źródła danych IEnumerable lub IEnumerable <T> .
ms.date: 02/14/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- foreach, parallel version
- parallel programming, foreach
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
ms.openlocfilehash: e4f67f6fbe5a79e925ecd6aaec3f833704cda38c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94825419"
---
# <a name="how-to-write-a-simple-parallelforeach-loop"></a>Instrukcje: zapisywanie prostej pętli Parallel. ForEach

Ten przykład pokazuje, jak używać <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> pętli, aby włączyć równoległość danych dla dowolnego <xref:System.Collections.IEnumerable?displayProperty=nameWithType> <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> źródła danych lub.

> [!NOTE]
> Ta dokumentacja używa wyrażeń lambda do definiowania delegatów w PLINQ. Jeśli nie znasz wyrażeń lambda w języku C# lub Visual Basic, zobacz [lambda Expressions in PLINQ and TPL](lambda-expressions-in-plinq-and-tpl.md).

## <a name="example"></a>Przykład

W tym przykładzie założono, że masz kilka plików jpg w folderze *C:\Users\Public\Pictures\Sample obrazy* i utworzysz nowy podfolder o nazwie *zmodyfikowano*. Gdy uruchamiasz ten przykład, obraca każdy obraz jpg w *przykładowych* obrazach i zapisuje je do *zmodyfikowania*. W razie potrzeby można zmodyfikować dwie ścieżki.

[!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
[!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]

<xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>Pętla działa jak <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> pętla. Pętla jest partycją źródłową kolekcji i planuje prace na wielu wątkach na podstawie środowiska systemowego. Im więcej procesorów w systemie, tym szybsze jest uruchamianie metody równoległej. W przypadku niektórych kolekcji źródłowych pętla sekwencyjna może być szybsza, w zależności od rozmiaru źródła i rodzaju pracy wykonywanej przez pętlę. Aby uzyskać więcej informacji o wydajności, zobacz [potencjalne pułapek w zakresie danych i równoległości zadań](potential-pitfalls-in-data-and-task-parallelism.md).

Aby uzyskać więcej informacji na temat pętli równoległych, zobacz [How to: Write a Simple Parallel. for](how-to-write-a-simple-parallel-for-loop.md).

Aby użyć <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> z kolekcją nieogólną, można użyć <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> metody rozszerzenia, aby skonwertować kolekcję do kolekcji ogólnej, jak pokazano w następującym przykładzie:

[!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
[!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]

Można również użyć równoległego LINQ (PLINQ) do zrównoleglanie przetwarzania <xref:System.Collections.Generic.IEnumerable%601> źródeł danych. PLINQ umożliwia użycie deklaracyjnej składni zapytań, aby wyrazić zachowanie pętli. Aby uzyskać więcej informacji, zobacz [Parallel LINQ (PLINQ)](introduction-to-plinq.md).

## <a name="compile-and-run-the-code"></a>Kompiluj i uruchamiaj kod

Można skompilować kod jako aplikację konsolową dla .NET Framework lub jako aplikację konsolową dla platformy .NET Core.

W programie Visual Studio istnieją szablony aplikacji konsoli w języku C# Visual Basic i .NET Core.

W wierszu polecenia można użyć poleceń interfejs wiersza polecenia platformy .NET Core (na przykład `dotnet new console` lub `dotnet new console -lang vb` ) lub można utworzyć plik i użyć kompilatora wiersza polecenia dla aplikacji .NET Framework.

W przypadku projektu .NET Core należy odwołać się do pakietu NuGet **System. Drawing. Common** . W programie Visual Studio Użyj Menedżera pakietów NuGet, aby zainstalować pakiet. Alternatywnie można dodać odwołanie do pakietu w \* pliku. csproj lub \* . vbproj:

```xml
<ItemGroup>
     <PackageReference Include="System.Drawing.Common" Version="4.5.1" />
</ItemGroup>
```

Aby uruchomić aplikację konsolową .NET Core z wiersza polecenia, należy użyć `dotnet run` z folderu, który zawiera aplikację.

Aby uruchomić aplikację konsolową z poziomu programu Visual Studio, naciśnij klawisz **F5**.

## <a name="see-also"></a>Zobacz także

- [Równoległość danych](data-parallelism-task-parallel-library.md)
- [Programowanie równoległe](index.md)
- [Równoległe LINQ (PLINQ)](introduction-to-plinq.md)
