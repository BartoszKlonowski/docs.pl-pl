---
title: On Error, instrukcja
ms.date: 07/20/2015
f1_keywords:
- vb.OnError
helpviewer_keywords:
- Visual Basic code, control flow
- Resume Next statement [Visual Basic]
- errors [Visual Basic], trapping
- error handling, On Error statement
- Next statement [Visual Basic], On Error
- control flow [Visual Basic], branching
- Error keyword [Visual Basic]
- execution [Visual Basic], conditional
- Resume statement [Visual Basic], and On Error statement
- Error statement [Visual Basic], and On Error statement
- GoTo statement [Visual Basic], and On Error statement
- branching [Visual Basic], on error
- conditional statements [Visual Basic], On Error
- On Error statement [Visual Basic], syntax
- On keyword [Visual Basic]
- run-time errors [Visual Basic], handling
- On Error statement [Visual Basic]
ms.assetid: ff947930-fb84-40cf-bd66-1ea219561d5c
ms.openlocfilehash: 7e007d59292fc577c0c8927766423ba6f7896a71
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873190"
---
# <a name="on-error-statement-visual-basic"></a>On Error — Instrukcja (Visual Basic)

Włącza procedurę obsługi błędów i określa lokalizację procedury w ramach procedury; można również użyć, aby wyłączyć procedurę obsługi błędu. `On Error`Instrukcja jest używana w obsłudze błędów bez struktury i może być używana zamiast strukturalnej obsługi wyjątków. [Strukturalna obsługa wyjątków](../../../standard/exceptions/index.md) jest wbudowana w platformę .NET, jest zwykle wydajniejsza i dlatego jest zalecana w przypadku obsługi błędów środowiska uruchomieniowego w aplikacji.

 Bez obsługi błędów lub obsługi wyjątków, wystąpi błąd w czasie wykonywania, który jest krytyczny: wyświetlany jest komunikat o błędzie, a wykonywanie jest zatrzymywane.

> [!NOTE]
> `Error`Słowo kluczowe jest również używane w [instrukcji Error](error-statement.md), która jest obsługiwana w celu zapewnienia zgodności z poprzednimi wersjami.

## <a name="syntax"></a>Składnia

```vb
On Error { GoTo [ line | 0 | -1 ] | Resume Next }
```

## <a name="parts"></a>Części

|Termin|Definicja|
|---|---|
|`GoTo` *line*|Włącza procedurę obsługi błędów, która zaczyna się w wierszu określonym w wymaganym argumencie *wiersza* . Argument *wiersza* to dowolna etykieta wiersza lub numer wiersza. Jeśli wystąpi błąd w czasie wykonywania, należy kontrolować gałęzie do określonego wiersza, co sprawia, że program obsługi błędów jest aktywny. Określony wiersz musi znajdować się w tej samej procedurze co `On Error` instrukcja lub wystąpił błąd w czasie kompilacji.|
|`GoTo 0`|Wyłącza włączony program obsługi błędów w bieżącej procedurze i resetuje go do `Nothing` .|
|`GoTo -1`|Wyłącza włączony wyjątek w bieżącej procedurze i resetuje go do `Nothing` .|
|`Resume Next`|Określa, że gdy wystąpi błąd w czasie wykonywania, formant przechodzi do instrukcji bezpośrednio po instrukcji, w której wystąpił błąd, a wykonywanie jest kontynuowane z tego punktu. Użyj tego formularza, a nie `On Error GoTo` podczas uzyskiwania dostępu do obiektów.|

## <a name="remarks"></a>Uwagi

> [!NOTE]
> Zalecamy używanie obsługi wyjątków strukturalnych w kodzie wszędzie tam, gdzie to możliwe, zamiast używania obsługi wyjątków niestrukturalnych i `On Error` instrukcji. Aby uzyskać więcej informacji, zobacz [try... Catch... Finally — instrukcja](try-catch-finally-statement.md).

 Procedura obsługi błędów "Enabled" jest taka, która jest włączona przez `On Error` instrukcję. Procedura obsługi błędów "Active" jest włączoną obsługą, która jest w trakcie obsługi błędu.

 Jeśli wystąpi błąd, gdy program obsługi błędów jest aktywny (między wystąpieniem błędu a `Resume` , `Exit Sub` ,, `Exit Function` lub `Exit Property` instrukcji), procedura obsługi błędów bieżącej procedury nie może obsłużyć błędu. Kontrolka powraca do procedury wywołującej.
  
 Jeśli procedura wywoływania ma włączoną procedurę obsługi błędów, została aktywowana, aby obsłużyć błąd. Jeśli procedura obsługi błędów procedury wywołującej jest również aktywna, kontrola przechodzi z powrotem przez poprzednie procedury wywołujące do momentu, gdy zostanie znaleziona funkcja obsługi błędów, ale nieaktywna. Jeśli nie zostanie znaleziona taka procedura obsługi błędów, błąd jest krytyczny w punkcie, w którym faktycznie wystąpił.
  
 Za każdym razem, gdy program obsługi błędów przekazuje kontrolę z powrotem do procedury wywołującej, ta procedura jest bieżącą procedurą. Gdy błąd zostanie obsłużony przez procedurę obsługi błędów w procedurze, wykonanie jest wznawiane w bieżącej procedurze w punkcie wydzielonym przez `Resume` instrukcję.
  
> [!NOTE]
> Procedura obsługi błędu nie jest `Sub` procedurą ani `Function` procedurą. Jest to sekcja kodu oznaczona przez etykietę wiersza lub numer wiersza.
  
## <a name="number-property"></a>Number — właściwość

 Procedury obsługi błędów są zależne od wartości `Number` właściwości `Err` obiektu, aby określić przyczynę błędu. Procedura powinna testować lub zapisywać odpowiednie wartości właściwości w `Err` obiekcie przed wystąpieniem innego błędu lub przed wykonaniem procedury, która może spowodować wystąpienie błędu. Wartości właściwości w `Err` obiekcie odzwierciedlają tylko ostatni błąd. Komunikat o błędzie skojarzony z `Err.Number` jest zawarty w `Err.Description` .  
  
## <a name="throw-statement"></a>Throw — Instrukcja  

 Błąd, który jest wywoływany za pomocą `Err.Raise` metody ustawia `Exception` Właściwość na nowo utworzone wystąpienie <xref:System.Exception> klasy. Aby można było obsługiwać wywoływanie wyjątków pochodnych typów wyjątków, `Throw` instrukcja jest obsługiwana w języku. Przyjmuje jeden parametr, który jest wystąpieniem wyjątku, które ma zostać zgłoszone. W poniższym przykładzie pokazano, jak te funkcje mogą być używane z istniejącą obsługą obsługi wyjątków:

 [!code-vb[VbVbalrErrorHandling#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#17)]  
  
 Zwróć uwagę, że `On Error GoTo` instrukcja Zalewka wszystkich błędów, niezależnie od klasy wyjątku.
  
## <a name="on-error-resume-next"></a>Przy wznowieniu błędu dalej

 `On Error Resume Next` powoduje, że wykonanie instrukcji kontynuuje się bezpośrednio po instrukcji, która spowodowała błąd czasu wykonywania, lub instrukcji zaraz po ostatnim wywołaniu procedury zawierającej `On Error Resume Next` instrukcję. Ta instrukcja umożliwia kontynuowanie wykonywania pomimo błędu czasu wykonywania. Można umieścić procedurę obsługi błędów, w której wystąpił błąd, zamiast przenoszenia kontroli do innej lokalizacji w ramach procedury. `On Error Resume Next`Instrukcja stanie się nieaktywna, gdy wywoływana jest inna procedura, więc należy wykonać `On Error Resume Next` instrukcję w każdej nazwie procedury, jeśli chcesz, aby Wbudowana obsługa błędów w tej procedurze.
  
> [!NOTE]
> `On Error Resume Next`Konstrukcja może być preferowana w `On Error GoTo` przypadku obsługi błędów generowanych podczas uzyskiwania dostępu do innych obiektów. `Err`Po każdej interakcji z obiektem jest usuwana niejednoznaczność informacji o obiekcie, do którego miał dostęp kod. Możesz mieć pewność, który obiekt został umieszczony w kodzie błędu `Err.Number` , a także który obiekt pierwotnie wygenerował błąd (obiekt określony w `Err.Source` ).

## <a name="on-error-goto-0"></a>W przypadku błędu GoTo 0

 `On Error GoTo 0` wyłącza obsługę błędów w bieżącej procedurze. Nie określa wiersz 0 jako początku kodu obsługi błędu, nawet jeśli procedura zawiera numer 1. Bez `On Error GoTo 0` instrukcji procedura obsługi błędów jest automatycznie wyłączona, gdy procedura zostanie zakończona.

## <a name="on-error-goto--1"></a>W przypadku błędu GoTo-1

 `On Error GoTo -1` wyłącza wyjątek w bieżącej procedurze. Nie określa wiersz-1 jako początku kodu obsługi błędu, nawet jeśli procedura zawiera numer wiersza-1. Bez `On Error GoTo -1` instrukcji, wyjątek jest automatycznie wyłączany, gdy procedura zostanie zakończona.

 Aby zapobiec uruchamianiu kodu obsługi błędów, gdy nie wystąpił błąd, należy umieścić `Exit Sub` `Exit Function` instrukcję,, lub `Exit Property` bezpośrednio przed procedurą obsługi błędów, tak jak w poniższym fragmencie:

 [!code-vb[VbVbalrErrorHandling#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#18)]

 W tym miejscu kod obsługi błędu następuje po `Exit Sub` instrukcji i poprzedza `End Sub` instrukcję, aby oddzielić ją od przepływu procedury. Kod obsługi błędów można umieścić w dowolnym miejscu w procedurze.

## <a name="untrapped-errors"></a>Błędy niezalewkowane

 Błędy niezalewkowane w obiektach są zwracane do aplikacji kontrolującej, gdy obiekt jest uruchomiony jako plik wykonywalny. W środowisku programistycznym błędy niezalewkowane są zwracane do aplikacji kontrolującej tylko wtedy, gdy są ustawione odpowiednie opcje. Zapoznaj się z dokumentacją aplikacji hosta, aby zapoznać się z opisem opcji, które należy ustawić podczas debugowania, sposobie ich ustawiania oraz o tym, czy host może tworzyć klasy.

 Jeśli utworzysz obiekt, który uzyskuje dostęp do innych obiektów, spróbuj obsłużyć wszelkie nieobsłużone błędy, które przechodzą z powrotem. Jeśli nie jest to możliwe, zamapuj kody błędów w `Err.Number` jeden z własnych błędów, a następnie Przekaż je z powrotem do wywołującego obiektu. Należy określić błąd, dodając kod błędu do `VbObjectError` stałej. Na przykład jeśli kod błędu to 1052, przypisz go w następujący sposób:

 [!code-vb[VbVbalrErrorHandling#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#19)]

> [!CAUTION]
> Błędy systemowe podczas wywołań bibliotek dołączanych dynamicznie (dll) systemu Windows nie powodują wymuszania wyjątków i nie można ich zalewkować przy użyciu nadlewek Visual Basic błędów. Podczas wywoływania funkcji DLL, należy sprawdzić każdą wartość zwracaną dla sukcesu lub niepowodzenia (zgodnie ze specyfikacją interfejsu API), a w przypadku niepowodzenia Sprawdź wartość we `Err` `LastDLLError` właściwości obiektu.

## <a name="example"></a>Przykład

 Ten przykład najpierw używa `On Error GoTo` instrukcji, aby określić lokalizację procedury obsługi błędów w ramach procedury. W przykładzie próba podzielenia przez zero spowoduje wygenerowanie błędu o numerze 6. Błąd jest obsługiwany w procedurze obsługi błędów, a następnie formant jest zwracany do instrukcji, która spowodowała błąd. `On Error GoTo 0`Instrukcja powoduje wyłączenie zalewkowania błędów. Następnie `On Error Resume Next` instrukcja jest używana do opóźniania zalewkowania błędów, dzięki czemu kontekst dla błędu generowanego przez następną instrukcję może być znany dla niektórych. Należy pamiętać, że `Err.Clear` służy do czyszczenia `Err` właściwości obiektu po obsłudze błędu.

 [!code-vb[VbVbalrErrorHandling#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#20)]

## <a name="requirements"></a>Wymagania

 **Przestrzeń nazw:** [Microsoft. VisualBasic](../runtime-library-members.md)

 **Zestaw:** Biblioteka środowiska uruchomieniowego Visual Basic (w Microsoft.VisualBasic.dll)

## <a name="see-also"></a>Zobacz też

- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Number%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Description%2A>
- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [End — instrukcja](end-statement.md)
- [Exit, instrukcja](exit-statement.md)
- [Resume — Instrukcja](resume-statement.md)
- [Komunikaty o błędach](../error-messages/index.md)
- [Try...Catch...Finally, instrukcja](try-catch-finally-statement.md)
