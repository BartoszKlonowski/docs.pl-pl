---
title: Zagadnienia dotyczące przeciążania procedur
ms.date: 07/20/2015
helpviewer_keywords:
- signatures [Visual Basic], ParamArray arguments
- ParamArray keyword [Visual Basic], parameter arrays
- ParamArray keyword [Visual Basic], arguments and signatures
- function overloading [Visual Basic], implicit overloads for ParamArray
- ParamArray keyword [Visual Basic], signatures
- Visual Basic code, procedures
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], overloading
- parameters [Visual Basic], lists
- function overloading [Visual Basic], typeless programming
- typeless programming
- function overloading [Visual Basic], restrictions
- arguments [Visual Basic], optional
- optional arguments [Visual Basic], overloading
- signatures [Visual Basic], procedure
- parameter lists [Visual Basic]
- parameter arrays [Visual Basic], overloading arguments
- Visual Basic code, parameter lists
- procedure overloading [Visual Basic], considerations
- Option Explicit statement [Visual Basic]
- restrictions [Visual Basic], overloading procedures
- procedures [Visual Basic], parameter lists
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
ms.openlocfilehash: 6197fa4041a22944542b2657e35bc293a6e5c244
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91075060"
---
# <a name="considerations-in-overloading-procedures-visual-basic"></a>Zagadnienia dotyczące przeciążania procedur (Visual Basic)

W przypadku przeciążenia procedury należy użyć innej *sygnatury* dla każdej przeciążonej wersji. Zazwyczaj oznacza to, że każda wersja musi określać inną listę parametrów. Aby uzyskać więcej informacji, zobacz "różne sygnatury" podczas [przeciążania procedur](./procedure-overloading.md).  
  
 Można przeciążyć `Function` procedurę za pomocą `Sub` procedury i na odwrót, pod warunkiem, że mają różne sygnatury. Dwa przeciążenia nie mogą się różnić tylko w tym, że ma wartość zwracaną, a druga nie.  
  
 Można przeciążać Właściwość tak samo jak w przypadku przeciążenia procedury i z tymi samymi ograniczeniami. Nie można jednak przeciążać procedury z właściwością lub odwrotnie.  
  
## <a name="alternatives-to-overloaded-versions"></a>Alternatywy dla przeciążonych wersji  

 Czasami istnieją alternatywy dla przeciążonych wersji, szczególnie gdy obecność argumentów jest opcjonalna lub ich liczba jest zmienna.  
  
 Należy pamiętać, że argumenty opcjonalne nie są koniecznie obsługiwane przez wszystkie języki, a tablice parametrów są ograniczone do Visual Basic. Jeśli piszesz procedurę, która prawdopodobnie zostanie wywołana z kodu napisanego w jednym z kilku różnych języków, przeciążone wersje zapewniają największą elastyczność.  
  
### <a name="overloads-and-optional-arguments"></a>Przeciążenia i opcjonalne argumenty  

 Gdy wywoływany kod może opcjonalnie dostarczyć lub pominąć jeden lub więcej argumentów, można zdefiniować wiele przeciążonych wersji lub użyć parametrów opcjonalnych.  
  
#### <a name="when-to-use-overloaded-versions"></a>Kiedy używać przeciążonych wersji  

 Można rozważyć zdefiniowanie szeregu przeciążonych wersji w następujących przypadkach:  
  
- Logika w kodzie procedury jest znacznie inna w zależności od tego, czy wywoływany kod dostarcza opcjonalny argument, czy nie.  
  
- Kod procedury nie może niezawodnie sprawdzić, czy wywoływany kod dostarczył opcjonalny argument. Dotyczy to na przykład sytuacji, gdy nie istnieje możliwy kandydat dla wartości domyślnej, która nie może zostać dostarczona do kodu wywołującego.  
  
#### <a name="when-to-use-optional-parameters"></a>Kiedy należy używać parametrów opcjonalnych  

 W następujących przypadkach może być preferowany co najmniej jeden parametr opcjonalny:  
  
- Jedyną wymaganą akcją, gdy wywoływany kod nie dostarcza opcjonalnego argumentu, jest ustawienie wartości domyślnej dla parametru. W takim przypadku kod procedury może być mniej skomplikowany w przypadku zdefiniowania jednej wersji z co najmniej jednym `Optional` parametrem.  
  
 Aby uzyskać więcej informacji, zobacz [Parametry opcjonalne](./optional-parameters.md).  
  
### <a name="overloads-and-paramarrays"></a>Przeciążenia i ParamArray  

 Gdy wywoływany kod może przekazać zmienną liczbę argumentów, można zdefiniować wiele przeciążonych wersji lub użyć tablicy parametrów.  
  
#### <a name="when-to-use-overloaded-versions"></a>Kiedy używać przeciążonych wersji  

 Można rozważyć zdefiniowanie szeregu przeciążonych wersji w następujących przypadkach:  
  
- Wiadomo, że wywoływany kod nigdy nie przekazuje więcej niż niewielką liczbę wartości do tablicy parametrów.  
  
- Logika w kodzie procedury jest znacznie inna w zależności od liczby wartości przekazywanych przez wywoływany kod.  
  
- Kod wywołujący może przekazywać wartości różnych typów danych.  
  
#### <a name="when-to-use-a-parameter-array"></a>Kiedy używać tablicy parametrów  

 Są one lepiej obsługiwane przez `ParamArray` parametr w następujących przypadkach:  
  
- Nie można przewidzieć, ile wartości kod wywołujący może być przekazywany do tablicy parametrów i może być dużą liczbą.  
  
- Logika procedury polega na przeprowadzeniu iteracji przez wszystkie wartości, które wywołuje wywoływany kod, wykonując zasadniczo te same operacje na każdej wartości.  
  
 Aby uzyskać więcej informacji, zobacz [tablice parametrów](./parameter-arrays.md).  
  
## <a name="implicit-overloads-for-optional-parameters"></a>Niejawne przeciążenia dla parametrów opcjonalnych  

 Procedura z [opcjonalnym](../../../language-reference/modifiers/optional.md) parametrem jest równoznaczna z dwoma przeciążonymi procedurami, jedną z opcjonalnym parametrem i bez niej. Nie można przeciążyć takiej procedury z listą parametrów odpowiadającą którejkolwiek z nich. Ilustruje to następujące deklaracje.  
  
 [!code-vb[VbVbcnProcedures#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#58)]  
  
 [!code-vb[VbVbcnProcedures#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#60)]  
  
 [!code-vb[VbVbcnProcedures#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#61)]  
  
 W przypadku procedury z więcej niż jednym opcjonalnym parametrem istnieje zestaw niejawnych przeciążeń, które zostały dostarczone przez logikę podobną do tego w poprzednim przykładzie.  
  
## <a name="implicit-overloads-for-a-paramarray-parameter"></a>Niejawne przeciążenia dla parametru ParamArray  

 Kompilator traktuje procedurę z parametrem [ParamArray](../../../language-reference/modifiers/paramarray.md) w celu uzyskania nieskończonej liczby przeciążeń, które różnią się od siebie w wyniku wywołania kodu do tablicy parametrów w następujący sposób:  
  
- Jedno Przeciążenie, gdy wywołujący kod nie dostarcza argumentu do `ParamArray`  
  
- Jedno Przeciążenie, gdy wywołujący kod dostarcza tablicę jednowymiarową `ParamArray` typu elementu  
  
- Dla każdej dodatniej liczby całkowitej jedno Przeciążenie, gdy wywołujący kod dostarcza tę liczbę argumentów, każdy `ParamArray` Typ elementu  
  
 Następujące deklaracje ilustrują te niejawne przeciążenia.  
  
 [!code-vb[VbVbcnProcedures#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#68)]  
  
 [!code-vb[VbVbcnProcedures#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#70)]  
  
 Nie można przeciążyć takiej procedury z listą parametrów, która przyjmuje jednowymiarową tablicę dla tablicy parametrów. Można jednak użyć podpisów innych niejawnych przeciążeń. Ilustruje to następujące deklaracje.  
  
 [!code-vb[VbVbcnProcedures#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#71)]  
  
## <a name="typeless-programming-as-an-alternative-to-overloading"></a>Programowanie beztypu jako alternatywa dla przeciążenia  

 Jeśli chcesz zezwolić, aby kod wywołujący przekaże różne typy danych do parametru, podejście alternatywne to programowanie bez typu. Można ustawić przełącznik sprawdzania typu `Off` z opcją [Strict](../../../language-reference/statements/option-strict-statement.md) lub Option [-optionstrict](../../../reference/command-line-compiler/optionstrict.md) kompilatora. Następnie nie trzeba deklarować typu danych parametru. Jednak takie podejście ma następujące wady w porównaniu z przeciążeniem:  
  
- Programowanie bez typu generuje mniej wydajny kod wykonania.  
  
- Procedura musi testować dla każdego typu danych, który przewiduje przekazanie.  
  
- Kompilator nie może sygnalizować błędu, Jeśli wywołujący kod przekaże typ danych, których procedura nie obsługuje.  
  
## <a name="see-also"></a>Zobacz także

- [Procedury](./index.md)
- [Parametry i argumenty procedur](./procedure-parameters-and-arguments.md)
- [Rozwiązywanie problemów z procedurami](./troubleshooting-procedures.md)
- [Instrukcje: definiowanie wielu wersji procedury](./how-to-define-multiple-versions-of-a-procedure.md)
- [Instrukcje: wywoływanie procedury przeciążenia](./how-to-call-an-overloaded-procedure.md)
- [Instrukcje: przeciążanie procedury korzystającej z parametrów opcjonalnych](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [Porady: przeciążanie procedury wykorzystującej nieokreśloną liczbę parametrów](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [Rozpoznanie przeciążenia](./overload-resolution.md)
- [Przeciążenia](../../../language-reference/modifiers/overloads.md)
