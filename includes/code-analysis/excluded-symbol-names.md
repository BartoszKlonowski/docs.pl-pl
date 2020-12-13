---
ms.openlocfilehash: 83644b9205d650da68c910095dd1d22a14940c44
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97366848"
---
### <a name="exclude-specific-symbols"></a>Wyklucz określone symbole

Z analizy można wykluczyć określone symbole, takie jak typy i metody. Na przykład aby określić, że reguła nie powinna być uruchamiana na żadnym kodzie w typach o nazwie `MyType` , Dodaj następującą parę klucz-wartość do pliku *editorconfig* w projekcie:

```ini
dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType
```

Dozwolone formaty nazw symboli w wartości opcji (oddzielone przez `|` ):

- Tylko nazwa symbolu (zawiera wszystkie symbole z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw).
- W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings)symbolu. Każda nazwa symbolu wymaga prefiksu rodzaju symboli, takiego jak `M:` dla metod, `T:` dla typów i `N:` dla przestrzeni nazw.
- `.ctor` dla konstruktorów i `.cctor` dla konstruktorów statycznych.

Przykłady:

| Wartość opcji | Podsumowanie |
| --- | --- |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType` | Dopasowuje wszystkie symbole o nazwie `MyType` . |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType1|MyType2` | Dopasowuje wszystkie symbole o nazwie `MyType1` lub `MyType2` . |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = M:NS.MyType.MyMethod(ParamType)` | Dopasowuje określoną metodę `MyMethod` z określonym w pełni kwalifikowanym podpisem. |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = M:NS1.MyType1.MyMethod1(ParamType)|M:NS2.MyType2.MyMethod2(ParamType)` | Dopasowuje określone metody `MyMethod1` i `MyMethod2` z odpowiednimi w pełni kwalifikowanymi podpisami. |
