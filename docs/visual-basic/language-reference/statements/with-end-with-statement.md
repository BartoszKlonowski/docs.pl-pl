---
title: With...End With, instrukcja
ms.date: 07/20/2015
f1_keywords:
- vb.With
helpviewer_keywords:
- With keyword [Visual Basic]
- loop structures [Visual Basic], and With...End With statements
- execution [Visual Basic], on object
- instructions, repeating
- With...End With statements [Visual Basic]
- With statement [Visual Basic]
- With statement [Visual Basic], nesting
- objects [Visual Basic], accessing
- With block
- End keyword [Visual Basic], With...End With statements
ms.assetid: 340d5fbb-4f43-48ec-a024-80843c137817
ms.openlocfilehash: 50f3bd0c6e96254274b429794901e2e4ac719ad0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401384"
---
# <a name="withend-with-statement-visual-basic"></a>With...End With — Instrukcja (Visual Basic)

Wykonuje szereg instrukcji, które wielokrotnie odwołują się do pojedynczego obiektu lub struktury, dzięki czemu instrukcje mogą używać uproszczonej składni podczas uzyskiwania dostępu do członków obiektu lub struktury.  W przypadku użycia struktury można odczytać tylko wartości elementów członkowskich lub wywołać metody, a w przypadku próby przypisania wartości do elementów członkowskich struktury używanej w instrukcji należy uzyskać błąd `With...End With` .

## <a name="syntax"></a>Składnia

```vb
With objectExpression
    [ statements ]
End With
```

## <a name="parts"></a>Części

|Termin|Definicja|
|---|---|
|`objectExpression`|Wymagany. Wyrażenie, które zostaje oszacowane do obiektu. Wyrażenie może być dowolnie złożone i jest sprawdzane tylko raz. Wyrażenie może być dowolnego typu danych, w tym typów podstawowych.|
|`statements`|Opcjonalny. Jedna lub więcej instrukcji między `With` i `End With` , które mogą odwoływać się do elementów członkowskich obiektu, który jest produkowany przez `objectExpression` ocenę.|
|`End With`|Wymagany. Kończy definicję `With` bloku.|

## <a name="remarks"></a>Uwagi

Za pomocą `With...End With` , można wykonać serię instrukcji dla określonego obiektu bez podawania nazwy obiektu wiele razy. W `With` bloku instrukcji można określić element członkowski obiektu, rozpoczynając od kropki, tak jakby `With` obiekt instrukcji poprzedzał go.

Na przykład aby zmienić wiele właściwości dla pojedynczego obiektu, umieść instrukcje przypisania właściwości wewnątrz `With...End With` bloku, odwołując się do obiektu tylko raz, a nie raz dla każdego przypisania właściwości.

Jeśli kod uzyskuje dostęp do tego samego obiektu w wielu instrukcjach, uzyskasz następujące korzyści przy użyciu `With` instrukcji:

- Nie musisz szacować złożonego wyrażenia wiele razy ani przypisywać wyniku do zmiennej tymczasowej, aby odwołać się do jego członków wiele razy.

- Kod staje się bardziej czytelny dzięki eliminacji powtarzających się wyrażeń kwalifikujących.

Typem danych `objectExpression` może być dowolna klasa lub typ struktury, a nawet Visual Basic typ podstawowy, taki jak `Integer` .  Jeśli `objectExpression` wynikiem jest coś innego niż obiekt, można odczytać tylko wartości swoich elementów członkowskich lub wywołać metody, a w przypadku próby przypisania wartości do elementów członkowskich struktury użytej w instrukcji zostanie wyświetlony komunikat o błędzie `With...End With` .  Jest to ten sam błąd, który można uzyskać w przypadku wywołania metody, która zwróciła strukturę i od razu uzyskuje dostęp do elementu członkowskiego wyniku funkcji, na przykład `GetAPoint().x = 1` .  Problem w obu przypadkach jest taki, że struktura istnieje tylko na stosie wywołań i nie ma żadnego sposobu, aby członek zmodyfikowanej struktury w takich sytuacjach mógł pisać do takich lokalizacji, żeby inny kod w programie mógł obserwować zmiany.

Ten `objectExpression` element jest obliczany raz, po umieszczeniu w bloku. Nie można ponownie przypisać elementu `objectExpression` z wewnątrz `With` bloku.

W `With` bloku można uzyskać dostęp do metod i właściwości tylko określonego obiektu bez ich kwalifikowania. Możesz użyć metod i właściwości innych obiektów, ale musisz je zakwalifikować z ich nazwami obiektów.

Można umieścić jedną `With...End With` instrukcję w innej. Zagnieżdżone `With...End With` instrukcje mogą być mylące, jeśli obiekty, do których odwołuje się nie są jasne z kontekstu. Musisz podać w pełni kwalifikowane odwołanie do obiektu znajdującego się w bloku zewnętrznym, `With` gdy odwołanie do obiektu następuje w `With` bloku wewnętrznym.

Nie można rozgałęzić `With` bloku instrukcji spoza bloku.

Instrukcje są wykonywane tylko raz, chyba że blok zawiera pętlę. Możesz zagnieździć różne rodzaje struktur sterujących. Aby uzyskać więcej informacji, zobacz [struktury formantów zagnieżdżonych](../../programming-guide/language-features/control-flow/nested-control-structures.md).

> [!NOTE]
> Możesz `With` również użyć słowa kluczowego w inicjatorach obiektów. Aby uzyskać więcej informacji i przykładów, zobacz [Inicjatory obiektów: typy nazwane i anonimowe](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md) oraz [Typy anonimowe](../../programming-guide/language-features/objects-and-classes/anonymous-types.md).
>
> Jeśli używasz `With` bloku tylko do inicjowania właściwości lub pól obiektu, który został właśnie utworzony, rozważ użycie inicjatora obiektów.

## <a name="example"></a>Przykład

W poniższym przykładzie każdy `With` blok wykonuje serię instrukcji na pojedynczym obiekcie.

[!code-vb[VbVbalrWithStatement#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrwithstatement/vb/mainwindow.xaml.vb#2)]

## <a name="example"></a>Przykład

Poniższy przykład zagnieżdża `With…End With` instrukcje. W instrukcji zagnieżdżonej `With` składnia odwołuje się do obiektu wewnętrznego.

[!code-vb[VbVbalrWithStatement#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrwithstatement/vb/mainwindow.xaml.vb#1)]

## <a name="see-also"></a>Zobacz też

- <xref:System.Collections.Generic.List%601>
- [Zagnieżdżone struktury sterujące](../../programming-guide/language-features/control-flow/nested-control-structures.md)
- [Inicjatory obiektów: typy nazwane i anonimowe](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [Typy anonimowe](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)
