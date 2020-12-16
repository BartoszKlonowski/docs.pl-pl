---
ms.openlocfilehash: 4125df1d64fe7f3f2eb1eb4a821ed46c8270c95f
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97531845"
---
### <a name="exclude-specific-types-and-their-derived-types"></a>Wyklucz określone typy i ich typy pochodne

Można wykluczyć określone typy i ich typy pochodne z analizy. Na przykład, aby określić, że reguła nie powinna być uruchamiana na żadnej metodzie w typach o nazwach `MyType` i ich typach pochodnych, Dodaj następującą parę klucz-wartość do pliku *editorconfig* w projekcie:

```ini
dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = MyType
```

Dozwolone formaty nazw symboli w wartości opcji (oddzielone przez `|` ):

- Tylko nazwa typu (obejmuje wszystkie typy z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw).
- W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings)symbolu z opcjonalnym `T:` prefiksem.

Przykłady:

| Wartość opcji | Podsumowanie |
| --- | --- |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = MyType` | Dopasowuje wszystkie typy o nazwach `MyType` i wszystkich typach pochodnych. |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = MyType1|MyType2` | Dopasowuje wszystkie typy o nazwach `MyType1` lub `MyType2` i wszystkich typach pochodnych. |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = M:NS.MyType` | Dopasowuje określony typ `MyType` z określoną w pełni kwalifikowaną nazwą i wszystkimi typami pochodnymi. |
|`dotnet_code_quality.CAXXXX.excluded_type_names_with_derived_types = M:NS1.MyType1|M:NS2.MyType2` | Dopasowuje określone typy `MyType1` i `MyType2` z odpowiednimi w pełni kwalifikowanymi nazwami i wszystkimi typami pochodnymi. |
