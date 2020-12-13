---
ms.openlocfilehash: 83644b9205d650da68c910095dd1d22a14940c44
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97366848"
---
### <a name="exclude-specific-symbols"></a><span data-ttu-id="0ec1e-101">Wyklucz określone symbole</span><span class="sxs-lookup"><span data-stu-id="0ec1e-101">Exclude specific symbols</span></span>

<span data-ttu-id="0ec1e-102">Z analizy można wykluczyć określone symbole, takie jak typy i metody.</span><span class="sxs-lookup"><span data-stu-id="0ec1e-102">You can exclude specific symbols, such as types and methods, from analysis.</span></span> <span data-ttu-id="0ec1e-103">Na przykład aby określić, że reguła nie powinna być uruchamiana na żadnym kodzie w typach o nazwie `MyType` , Dodaj następującą parę klucz-wartość do pliku *editorconfig* w projekcie:</span><span class="sxs-lookup"><span data-stu-id="0ec1e-103">For example, to specify that the rule should not run on any code within types named `MyType`, add the following key-value pair to an *.editorconfig* file in your project:</span></span>

```ini
dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType
```

<span data-ttu-id="0ec1e-104">Dozwolone formaty nazw symboli w wartości opcji (oddzielone przez `|` ):</span><span class="sxs-lookup"><span data-stu-id="0ec1e-104">Allowed symbol name formats in the option value (separated by `|`):</span></span>

- <span data-ttu-id="0ec1e-105">Tylko nazwa symbolu (zawiera wszystkie symbole z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw).</span><span class="sxs-lookup"><span data-stu-id="0ec1e-105">Symbol name only (includes all symbols with the name, regardless of the containing type or namespace).</span></span>
- <span data-ttu-id="0ec1e-106">W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings)symbolu.</span><span class="sxs-lookup"><span data-stu-id="0ec1e-106">Fully qualified names in the symbol's [documentation ID format](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings).</span></span> <span data-ttu-id="0ec1e-107">Każda nazwa symbolu wymaga prefiksu rodzaju symboli, takiego jak `M:` dla metod, `T:` dla typów i `N:` dla przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0ec1e-107">Each symbol name requires a symbol-kind prefix, such as `M:` for methods, `T:` for types, and `N:` for namespaces.</span></span>
- <span data-ttu-id="0ec1e-108">`.ctor` dla konstruktorów i `.cctor` dla konstruktorów statycznych.</span><span class="sxs-lookup"><span data-stu-id="0ec1e-108">`.ctor` for constructors and `.cctor` for static constructors.</span></span>

<span data-ttu-id="0ec1e-109">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="0ec1e-109">Examples:</span></span>

| <span data-ttu-id="0ec1e-110">Wartość opcji</span><span class="sxs-lookup"><span data-stu-id="0ec1e-110">Option Value</span></span> | <span data-ttu-id="0ec1e-111">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0ec1e-111">Summary</span></span> |
| --- | --- |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType` | <span data-ttu-id="0ec1e-112">Dopasowuje wszystkie symbole o nazwie `MyType` .</span><span class="sxs-lookup"><span data-stu-id="0ec1e-112">Matches all symbols named `MyType`.</span></span> |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType1|MyType2` | <span data-ttu-id="0ec1e-113">Dopasowuje wszystkie symbole o nazwie `MyType1` lub `MyType2` .</span><span class="sxs-lookup"><span data-stu-id="0ec1e-113">Matches all symbols named either `MyType1` or `MyType2`.</span></span> |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = M:NS.MyType.MyMethod(ParamType)` | <span data-ttu-id="0ec1e-114">Dopasowuje określoną metodę `MyMethod` z określonym w pełni kwalifikowanym podpisem.</span><span class="sxs-lookup"><span data-stu-id="0ec1e-114">Matches specific method `MyMethod` with the specified fully qualified signature.</span></span> |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = M:NS1.MyType1.MyMethod1(ParamType)|M:NS2.MyType2.MyMethod2(ParamType)` | <span data-ttu-id="0ec1e-115">Dopasowuje określone metody `MyMethod1` i `MyMethod2` z odpowiednimi w pełni kwalifikowanymi podpisami.</span><span class="sxs-lookup"><span data-stu-id="0ec1e-115">Matches specific methods `MyMethod1` and `MyMethod2` with the respective fully qualified signatures.</span></span> |
