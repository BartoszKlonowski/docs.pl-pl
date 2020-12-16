---
ms.openlocfilehash: 4125df1d64fe7f3f2eb1eb4a821ed46c8270c95f
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97531845"
---
### <a name="exclude-specific-types-and-their-derived-types"></a><span data-ttu-id="86bfa-101">Wyklucz określone typy i ich typy pochodne</span><span class="sxs-lookup"><span data-stu-id="86bfa-101">Exclude specific types and their derived types</span></span>

<span data-ttu-id="86bfa-102">Można wykluczyć określone typy i ich typy pochodne z analizy.</span><span class="sxs-lookup"><span data-stu-id="86bfa-102">You can exclude specific types and their derived types from analysis.</span></span> <span data-ttu-id="86bfa-103">Na przykład, aby określić, że reguła nie powinna być uruchamiana na żadnej metodzie w typach o nazwach `MyType` i ich typach pochodnych, Dodaj następującą parę klucz-wartość do pliku *editorconfig* w projekcie:</span><span class="sxs-lookup"><span data-stu-id="86bfa-103">For example, to specify that the rule should not run on any methods within types named `MyType` and their derived types, add the following key-value pair to an *.editorconfig* file in your project:</span></span>

```ini
dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = MyType
```

<span data-ttu-id="86bfa-104">Dozwolone formaty nazw symboli w wartości opcji (oddzielone przez `|` ):</span><span class="sxs-lookup"><span data-stu-id="86bfa-104">Allowed symbol name formats in the option value (separated by `|`):</span></span>

- <span data-ttu-id="86bfa-105">Tylko nazwa typu (obejmuje wszystkie typy z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw).</span><span class="sxs-lookup"><span data-stu-id="86bfa-105">Type name only (includes all types with the name, regardless of the containing type or namespace).</span></span>
- <span data-ttu-id="86bfa-106">W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings)symbolu z opcjonalnym `T:` prefiksem.</span><span class="sxs-lookup"><span data-stu-id="86bfa-106">Fully qualified names in the symbol's [documentation ID format](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings), with an optional `T:` prefix.</span></span>

<span data-ttu-id="86bfa-107">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="86bfa-107">Examples:</span></span>

| <span data-ttu-id="86bfa-108">Wartość opcji</span><span class="sxs-lookup"><span data-stu-id="86bfa-108">Option Value</span></span> | <span data-ttu-id="86bfa-109">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="86bfa-109">Summary</span></span> |
| --- | --- |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = MyType` | <span data-ttu-id="86bfa-110">Dopasowuje wszystkie typy o nazwach `MyType` i wszystkich typach pochodnych.</span><span class="sxs-lookup"><span data-stu-id="86bfa-110">Matches all types named `MyType` and all of their derived types.</span></span> |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = MyType1|MyType2` | <span data-ttu-id="86bfa-111">Dopasowuje wszystkie typy o nazwach `MyType1` lub `MyType2` i wszystkich typach pochodnych.</span><span class="sxs-lookup"><span data-stu-id="86bfa-111">Matches all types named either `MyType1` or `MyType2` and all of their derived types.</span></span> |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = M:NS.MyType` | <span data-ttu-id="86bfa-112">Dopasowuje określony typ `MyType` z określoną w pełni kwalifikowaną nazwą i wszystkimi typami pochodnymi.</span><span class="sxs-lookup"><span data-stu-id="86bfa-112">Matches specific type `MyType` with given fully qualified name and all of its derived types.</span></span> |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = M:NS1.MyType1|M:NS2.MyType2` | <span data-ttu-id="86bfa-113">Dopasowuje określone typy `MyType1` i `MyType2` z odpowiednimi w pełni kwalifikowanymi nazwami i wszystkimi typami pochodnymi.</span><span class="sxs-lookup"><span data-stu-id="86bfa-113">Matches specific types `MyType1` and `MyType2` with the respective fully qualified names, and all of their derived types.</span></span> |
