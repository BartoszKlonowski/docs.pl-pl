---
title: Wyświetlanie tekstu na wyświetlaczu LCD
description: Dowiedz się, jak wyświetlać znaki w ciekłym wyświetlaczu Crystal przy użyciu bibliotek .NET IoT.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: d4c3e373207e23877903491871f4d09e11000c1a
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590052"
---
<!--markdownlint-disable DOCSMD011 -->
# <a name="display-text-on-an-lcd"></a>Wyświetlanie tekstu na wyświetlaczu LCD

Wyświetlacze LCD są przydatne do wyświetlania informacji bez potrzeby monitora zewnętrznego. Popularne wyświetlacze LCD mogą być połączone bezpośrednio z numerami PIN interfejsu GPIO, ale takie podejście wymaga użycia maksymalnie 10 numerów PIN interfejsu GPIO. W scenariuszach, które wymagają połączenia z kombinacją urządzeń, rozgłosowanie tak dużej ilości nagłówka GPIO do wyświetlania znaków jest często niepraktyczne.

Wielu producentów sprzedaje 20x4 LCD z zintegrowanym ekspanderem GPIO. Wyświetlacz znaku łączy się bezpośrednio z ekspanderem GPIO, który następnie łączy się z Raspberry Pi za pośrednictwem protokołu szeregowego obwodu Inter-Integrated (I2C).

W tym temacie zostanie użyty program .NET do wyświetlania tekstu na ekranie wyświetlacza LCD przy użyciu ekspandera I2C.

## <a name="prerequisites"></a>Wymagania wstępne

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- [20x4 wyświetlacz LCD z interfejsem I2C](https://www.bing.com/images/search?q=20x4+lcd+display+with+i2c)<span class="docon docon-navigate-external x-hidden-focus"></span>
- Przewody skoku
- Breadboard (opcjonalne/zalecane)
- Tablica zagadnień Raspberry Pi GPIO (opcjonalne/zalecane)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

> [!NOTE]
> Istnieje wielu producentów wyświetlaczy LCD. Większość projektów jest identyczna, a producent nie powinien dokonywać żadnych różnic w działaniu. Ten samouczek został opracowany z myślą o [wykrytym LCD2004](https://www.sunfounder.com/lcd2004-module.html) <span class="docon docon-navigate-external x-hidden-focus"></span> .

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="prepare-the-hardware"></a>Przygotowanie sprzętu

Aby połączyć cztery pinezki w ekspanderze I2C GPIO z Raspberry Pi w następujący sposób:

- GND na ziemię
- VCC do 5V
- SDA do SDA (GPIO 2)
- SCL do SCL (GPIO 3)

W razie potrzeby zapoznaj się z następującymi ilustracjami:

| Interfejs I2C (z tyłu ekranu) | Raspberry Pi GPIO |
|---------------------------------|-------------------|
| :::image type="content" source="../media/character-display-i2c-thumb.png" alt-text="Obraz z tyłu wyświetlania znaków przedstawiający Ekspander I2C GPIO." lightbox="../media/character-display-i2c.png"::: | :::image type="content" source="../media/gpio-pinout-diagram-thumb.png" alt-text="Diagram przedstawiający pinout nagłówka GPIO Raspberry Pi. Obraz przedstawiający Raspberry Pi Foundation." lightbox="../media/gpio-pinout-diagram.png":::<br />[Obraz przedstawiający Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/) <span class="docon docon-navigate-external x-hidden-focus"></span> .
 |

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Tworzenie aplikacji

Wykonaj następujące kroki w preferowanym środowisku programistycznym:

1. Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md). Nadaj mu nazwę *LcdTutorial*.

    ```dotnetcli
    dotnet new console -o LcdTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Zastąp zawartość pliku *Program.cs* następującym kodem:

    :::code language="csharp" source="~/iot-samples/tutorials/LcdTutorial/Program.cs" :::

    Powyższy kod ma następujące działanie:

    - [Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `I2cDevice` przez wywoływanie `I2cDevice.Create` i przekazanie nowego `I2cConnectionSettings` przy użyciu `busId` `deviceAddress` parametrów i. `I2cDevice`Reprezentuje to magistralę I2C. `using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.

        > [!WARNING]
        > Adres urządzenia dla ekspandera GPIO zależy od układu używanego przez producenta. Rozszerzenia interfejsu GPIO wyposażone w PCF8574 używają adresu `0x27` , podczas gdy korzystają z PCF8574A wiórów `0x3F` . Zapoznaj się z dokumentacją wyświetlacza LCD.

    - Inna `using` Deklaracja tworzy wystąpienie `Pcf8574` i przekazuje do `I2cDevice` konstruktora. To wystąpienie reprezentuje Ekspander interfejsu GPIO.
    - Inna `using` Deklaracja tworzy wystąpienie `Lcd2004` do reprezentowania wyświetlania. Kilka parametrów są przekazywane do konstruktora opisującego ustawienia, które mają być używane do komunikacji z ekspanderem GPIO. Ekspander GPIO jest przekazaniem jako `controller` parametr.
    - `while`Pętla jest uruchamiana w nieskończoność. Każda iteracja:
        1. Czyści ekran.
        1. Ustawia położenie kursora do pierwszej pozycji w bieżącym wierszu.
        1. Zapisuje bieżący czas do wyświetlania w bieżącym położeniu kursora.
        1. Wykonuje iterację bieżącego licznika wiersza.
        1. Uśpienie 1000 ms.

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.

    ```bash
    ./LcdTutorial
    ```

    Obserwuj wyświetlacz wyświetlacza LCD jako bieżący czas wyświetlania w każdym wierszu.

    > [!TIP]
    > Jeśli ekran jest widoczny, ale nie widzisz żadnego tekstu, spróbuj dopasować numer kontrastu na odwrocie ekranu.

1. Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.

Gratulacje! Wyświetlasz tekst na wyświetlaczu LCD przy użyciu interfejsu I2C i ekspandera GPIO!

## <a name="get-the-source-code"></a>Uzyskiwanie kodu źródłowego

Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/LcdTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się, jak korzystać z Ogólnego przeznaczenia danych wejściowych/wyjściowych w celu migania DIODy](../tutorials/blink-led.md)
