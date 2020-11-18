---
title: Właściwości i klasy wyjątków
ms.date: 03/30/2017
helpviewer_keywords:
- exceptions, Exception class
- Exception class
ms.assetid: e2e1f8c4-e7b4-467d-9a66-13c90861221d
ms.openlocfilehash: 459dc15f136c98d4b889a420dbd863b16aca747c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828208"
---
# <a name="exception-class-and-properties"></a>Właściwości i klasy wyjątków

<xref:System.Exception>Klasa jest klasą bazową, z której są dziedziczone wyjątki. Na przykład <xref:System.InvalidCastException> Hierarchia klas jest następująca:

<xref:System.Object>\
&nbsp;&nbsp;<xref:System.Exception>\
&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.SystemException>\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.InvalidCastException>

<xref:System.Exception>Klasa ma następujące właściwości, które ułatwiają zrozumienie wyjątku.

| Nazwa właściwości | Opis |
| ------------- | ----------- |
| <xref:System.Exception.Data> | <xref:System.Collections.IDictionary>Zawiera dowolne dane w parach klucz-wartość. |
| <xref:System.Exception.HelpLink> | Może zawierać adres URL (lub nazwę URN) do pliku pomocy, który zawiera szczegółowe informacje o przyczynie wyjątku. |
| <xref:System.Exception.InnerException> | Ta właściwość może służyć do tworzenia i zachowywania serii wyjątków podczas obsługi wyjątków. Można go użyć do utworzenia nowego wyjątku, który zawiera wcześniej przechwycone wyjątki. Oryginalny wyjątek może być przechwytywany przez drugi wyjątek we <xref:System.Exception.InnerException> właściwości, co pozwala na kod, który obsługuje drugi wyjątek do badania dodatkowych informacji. Załóżmy na przykład, że masz metodę, która odbiera argument, który jest niepoprawnie sformatowany.  Kod próbuje odczytać argument, ale jest zgłaszany wyjątek. Metoda przechwytuje wyjątek i zgłasza <xref:System.FormatException> . Aby poprawić zdolność obiektu wywołującego do ustalenia przyczyny zgłoszenia wyjątku, czasami jest to konieczne w przypadku metody przechwytywania wyjątku zgłoszonego przez procedurę pomocnika, a następnie zgłosić wyjątek, który wystąpił. Można utworzyć nowy i bardziej zrozumiały wyjątek, gdzie odwołanie do wyjątku wewnętrznego można ustawić na oryginalny wyjątek. Ten bardziej zrozumiały wyjątek może następnie zostać zgłoszony do obiektu wywołującego. Należy pamiętać, że za pomocą tej funkcji można utworzyć serię połączonych wyjątków kończących się na wyjątek, który został wygenerowany jako pierwszy. |
| <xref:System.Exception.Message> | Zawiera szczegółowe informacje o przyczynie wyjątku.
| <xref:System.Exception.Source> | Pobiera lub ustawia nazwę aplikacji lub obiekt, który powoduje błąd. |
| <xref:System.Exception.StackTrace>| Zawiera ślad stosu, którego można użyć do określenia, gdzie wystąpił błąd. Ślad stosu zawiera nazwę pliku źródłowego i numer wiersza programu, jeśli dostępne są informacje debugowania. |

Większość klas, które dziedziczą z programu, <xref:System.Exception> nie implementuje dodatkowych elementów członkowskich ani nie zapewnia dodatkowych funkcji; są one po prostu dziedziczone z <xref:System.Exception> . W związku z tym najważniejsze informacje dotyczące wyjątku można znaleźć w hierarchii klas wyjątków, nazwę wyjątku i informacje zawarte w wyjątku.

Zalecamy wygenerowanie i przechwycenie tylko obiektów, które pochodzą z <xref:System.Exception> , ale można zgłosić dowolny obiekt pochodzący z <xref:System.Object> klasy jako wyjątek. Należy zauważyć, że nie wszystkie języki obsługują generowanie i przechwytywanie obiektów, które nie pochodzą od <xref:System.Exception> .
  
## <a name="see-also"></a>Zobacz także

- [Wyjątki](index.md)
