---
title: Miganie diodą LED
description: Dowiedz się, jak migać diody LED przy użyciu bibliotek programu .NET IoT.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: 07a050c0655f9cae3d7f2b924c0dd07ac1c6c0b9
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590063"
---
# <a name="blink-an-led"></a>Miganie diodą LED

Numery PIN operacji we/wy ogólnego przeznaczenia (GPIO) mogą być kontrolowane indywidualnie. Jest to przydatne do kontrolowania diod LED, przekaźników i innych urządzeń stanowych. W tym temacie będziesz używać platformy .NET i pinów interfejsu GPIO Raspberry Pi, aby obsługiwać diody LED i wielokrotnie migać.

## <a name="prerequisites"></a>Wymagania wstępne

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- dioda LED 5 mm
- Ω opornik 330
- Breadboard
- Przewody skoku
- Tablica zagadnień Raspberry Pi GPIO (opcjonalne/zalecane)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

[!INCLUDE [ensure-ssh](../includes/ensure-ssh.md)]

## <a name="prepare-the-hardware"></a>Przygotowanie sprzętu

Użyj składników sprzętowych, aby skompilować obwód, jak przedstawiono na poniższym diagramie:

:::image type="content" source="../media/rpi-led_bb-thumb.png" alt-text="Diagram Fritzing pokazujący obwód z diodą LED i opornikiem" lightbox="../media/rpi-led_bb.png":::

Na powyższym obrazie przedstawiono następujące połączenia:

- Program GPIO 18 do diody LED (dłuższy, pozytywny potencjalny klient)
- Wywodzij katodę (krótszy, negatywny potencjalny klient) do 330 Ω (jeden koniec)
- 330 Ω (inne zakończenie) do ziemi

[!INCLUDE [tutorial-rpi-gpio](../includes/tutorial-rpi-gpio.md)]

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Tworzenie aplikacji

Wykonaj następujące kroki w preferowanym środowisku programistycznym:

1. Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md). Nadaj mu nazwę *BlinkTutorial*.

    ```dotnetcli
    dotnet new console -o BlinkTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Zastąp zawartość pliku *Program.cs* następującym kodem:

    :::code language="csharp" source="~/iot-samples/tutorials/BlinkTutorial/Program.cs" :::

    Powyższy kod ma następujące działanie:

    - [Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `GpioController` . `using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.
    - Kod pin GPIO 18 jest otwarty dla danych wyjściowych
    - `while`Pętla jest uruchamiana w nieskończoność. Każda iteracja:
        1. Zapisuje wartość do numeru pin GPIO 18. Jeśli `ledOn` ma wartość true, zapisuje `PinValue.High` (włączone). W przeciwnym razie zapisuje `PinValue.Low` .
        1. Uśpienie 1000 ms.
        1. Włącza lub wyłącza wartość `ledOn` .

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.

    ```bash
    ./BlinkTutorial
    ```

    Dioda LED miga i w każdej sekundzie.

1. Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.

Gratulacje! Użyto interfejsu GPIO do migania diody LED.

## <a name="get-the-source-code"></a>Uzyskiwanie kodu źródłowego

Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/BlinkTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się, jak odczytać warunki środowiska z czujnika](../tutorials/temp-sensor.md)
