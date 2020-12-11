---
title: Tworzenie i zgłaszanie wyjątków — Przewodnik programowania w języku C#
description: Dowiedz się więcej na temat tworzenia i zgłaszania wyjątków. Wyjątki są używane do wskazywania, że wystąpił błąd podczas uruchamiania programu.
ms.date: 12/09/2020
helpviewer_keywords:
- catching exceptions [C#]
- throwing exceptions [C#]
- exceptions [C#], creating
- exceptions [C#], throwing
ms.assetid: 6bbba495-a115-4c6d-90cc-1f4d7b5f39e2
ms.openlocfilehash: a6998c5b274736b290460808ad4c7cb22be7ebf6
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110211"
---
# <a name="creating-and-throwing-exceptions-c-programming-guide"></a>Tworzenie i zgłaszanie wyjątków (Przewodnik programowania w języku C#)

Wyjątki są używane do wskazywania, że wystąpił błąd podczas uruchamiania programu. Obiekty wyjątków opisujące błąd są tworzone, a następnie *generowane* za pomocą słowa kluczowego [throw](../../language-reference/keywords/throw.md) . Środowisko uruchomieniowe następnie wyszukuje najbardziej zgodny program obsługi wyjątków.

Programiści powinni zgłosić wyjątki, gdy spełnione są co najmniej jeden z następujących warunków:

- Metoda nie może ukończyć zdefiniowanej funkcji. Na przykład jeśli parametr do metody ma nieprawidłową wartość:
  :::code language="csharp" source="snippets/exceptions/Program.cs" ID="CantComplete":::
- Nieodpowiednie wywołanie do obiektu jest wykonywane na podstawie stanu obiektu. Przykładem może być próba zapisu w pliku tylko do odczytu. W przypadkach, w których stan obiektu nie zezwala na operację, zgłoś wystąpienie <xref:System.InvalidOperationException> obiektu lub obiekt na podstawie wartości pochodnych tej klasy. Poniższy kod jest przykładem metody, która zgłasza <xref:System.InvalidOperationException> obiekt:
  :::code language="csharp" source="snippets/exceptions/ProgramLog.cs" ID="ProgramLog":::
- Gdy argument metody powoduje wyjątek. W takim przypadku należy przechwycić oryginalny wyjątek i <xref:System.ArgumentException> utworzyć wystąpienie. Oryginalny wyjątek powinien zostać przesłany do konstruktora <xref:System.ArgumentException> jako <xref:System.Exception.InnerException%2A> parametr:
  :::code language="csharp" source="snippets/exceptions/Program.cs" ID="InvalidArg":::

Wyjątki zawierają właściwość o nazwie <xref:System.Exception.StackTrace%2A> . Ten ciąg zawiera nazwę metod w bieżącym stosie wywołań, wraz z nazwą pliku i numerem wiersza, dla których zgłoszono wyjątek dla każdej metody. <xref:System.Exception.StackTrace%2A>Obiekt jest tworzony automatycznie przez środowisko uruchomieniowe języka wspólnego (CLR) z punktu `throw` instrukcji, aby wyjątki musiały zostać zgłoszone od punktu, w którym ma zostać rozpoczęte śledzenie stosu.

Wszystkie wyjątki zawierają właściwość o nazwie <xref:System.Exception.Message%2A> . Ten ciąg powinien być ustawiony na wyjaśnienie przyczyny wyjątku. Informacje, które są wrażliwe na zabezpieczenia, nie powinny być umieszczane w tekście komunikatu. Oprócz <xref:System.Exception.Message%2A> , <xref:System.ArgumentException> zawiera właściwość o nazwie <xref:System.ArgumentException.ParamName%2A> , która powinna być ustawiona na nazwę argumentu, który spowodował zgłoszenie wyjątku. W metodzie ustawiającej właściwość <xref:System.ArgumentException.ParamName%2A> powinna być ustawiona na `value` .

Metody publiczne i chronione umożliwiają zgłaszanie wyjątków za każdym razem, gdy nie mogą ukończyć ich zamierzonych funkcji. Zgłoszona Klasa wyjątku to najbardziej konkretny wyjątek, który pasuje do warunków błędu. Te wyjątki powinny być udokumentowane jako część funkcji klasy, a klasy pochodne lub aktualizacje oryginalnej klasy powinny zachować takie samo zachowanie w celu zapewnienia zgodności z poprzednimi wersjami.

## <a name="things-to-avoid-when-throwing-exceptions"></a>Rzeczy, które należy unikać podczas zgłaszania wyjątków

Poniższa lista zawiera wskazówki, które należy unikać podczas zgłaszania wyjątków:

- Nie należy używać wyjątków, aby zmienić przepływ programu w ramach zwykłego wykonania. Użyj wyjątków, aby zgłosić i obsłużyć błędy.
- Wyjątki nie powinny być zwracane jako wartość zwracana lub parametr zamiast zgłaszania.
- Nie zgłaszaj <xref:System.Exception?displayProperty=nameWithType> , <xref:System.SystemException?displayProperty=nameWithType> , <xref:System.NullReferenceException?displayProperty=nameWithType> lub <xref:System.IndexOutOfRangeException?displayProperty=nameWithType> celowo z własnego kodu źródłowego.
- Nie należy tworzyć wyjątków, które mogą być zgłaszane w trybie debugowania, ale nie w trybie wydania. Aby zidentyfikować błędy czasu wykonywania w fazie opracowywania, należy zamiast tego użyć potwierdzenia debugowania.

## <a name="defining-exception-classes"></a>Definiowanie klas wyjątków

Programy mogą zgłosić wstępnie zdefiniowaną klasę wyjątku w <xref:System> przestrzeni nazw (chyba że wcześniej zanotowano) lub utworzyć własne klasy wyjątków, wyprowadzając z <xref:System.Exception> . Klasy pochodne powinny definiować co najmniej cztery konstruktory: jeden konstruktor bez parametrów, taki, który ustawia właściwość Message, a drugi ustawia <xref:System.Exception.Message%2A> <xref:System.Exception.InnerException%2A> właściwości i. Czwarty Konstruktor jest używany do serializacji wyjątku. Nowe klasy wyjątków powinny być możliwe do serializacji. Na przykład:

:::code language="csharp" source="snippets/exceptions/InvalidDepartmentException.cs" id="DefineExceptionClass":::

Dodaj nowe właściwości do klasy wyjątku, gdy udostępniane dane są przydatne do rozpoznawania wyjątku. Jeśli do klasy wyjątku pochodnego zostaną dodane nowe właściwości, `ToString()` należy je zastąpić, aby zwracały dodane informacje.

## <a name="c-language-specification"></a>Specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz [wyjątki](~/_csharplang/spec/exceptions.md) i [instrukcje throw](~/_csharplang/spec/statements.md#the-throw-statement) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction). Specyfikacja języka jest ostatecznym źródłem informacji o składni i użyciu języka C#.

## <a name="see-also"></a>Zobacz też

- [Hierarchia wyjątków](../../../standard/exceptions/index.md)
