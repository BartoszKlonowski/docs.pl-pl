---
title: Odczytywanie warunków środowiska z czujnika
description: Dowiedz się, jak odczytywać termperature, ciśnienie atmosferyczne i wilgotność za pomocą bibliotek .NET IoT.
author: camsoper
ms.author: casoper
ms.date: 11/14/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: 1270e7629e9afc12b1d76d260d4b8b51428f1040
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590064"
---
# <a name="read-environmental-conditions-from-a-sensor"></a>Odczytywanie warunków środowiska z czujnika

Jednym z najpopularniejszych scenariuszy dotyczących urządzeń IoT jest wykrywanie warunków środowiskowych. Różne czujniki są dostępne do monitorowania temperatury, wilgotności, ciśnienia atmosferycznego i nie tylko.

W tym temacie zostanie użyty program .NET do odczytywania warunków środowiskowych z czujnika.

## <a name="prerequisites"></a>Wymagania wstępne

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- [BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout) <span class="docon docon-navigate-external x-hidden-focus"></span> wilgotność/ciśnienie atmosferyczne/czujnik temperatury zagadnień
- Przewody skoku
- Breadboard (opcjonalnie)
- Tablica Raspberry Pi GPIO zagadnień (opcjonalnie)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

> [!IMPORTANT]
> Istnieje wielu producentów BME280 podgrupach. Większość projektów jest podobna, a producent nie powinien dokonywać żadnych różnic w działaniu. Ten samouczek próbuje uwzględnić odmiany. Upewnij się, że BME280 zagadnień zawiera interfejs obwodu Inter-Integrated (I2C).

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="prepare-the-hardware"></a>Przygotowanie sprzętu

Użyj składników sprzętowych, aby skompilować obwód, jak przedstawiono na poniższym diagramie:

:::image type="content" source="../media/rpi-bmp280_i2c-thumb.png" alt-text="Diagram Fritzing przedstawiający połączenie z tablicy Raspberry Pi z BME280 zagadnień" lightbox="../media/rpi-bmp280_i2c.png":::

Poniżej przedstawiono połączenia z Raspberry Pi do BME280 zagadnień:

- 3.3 v do VIN *lub* 3v3 (pokazane na czerwono)
- Od podstaw do GND (czarny)
- SDA (GPIO 2) do SDI *lub* SDA (Blue)
- SCL (GPIO 3) do SCK *lub* SCL (pomarańczowy)

[!INCLUDE [tutorial-rpi-gpio](../includes/tutorial-rpi-gpio.md)]

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Tworzenie aplikacji

Wykonaj następujące kroki w preferowanym środowisku programistycznym:

1. Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md). Nadaj mu nazwę *SensorTutorial*.

    ```dotnetcli
    dotnet new console -o SensorTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Zastąp zawartość pliku *Program.cs* następującym kodem:

    :::code language="csharp" source="~/iot-samples/tutorials/SensorTutorial/Program.cs" :::

    Powyższy kod ma następujące działanie:

    - `i2cSettings` jest ustawiony na nowe wystąpienie `I2cConnectionSettings` . Konstruktor ustawia `busId` parametr na wartość 1, a `deviceAddress` parametr na `Bme280.DefaultI2cAddress` .

        > [!IMPORTANT]
        > Niektórzy producenci BME280 zagadnień używają dodatkowej wartości adresu. Dla tych urządzeń Użyj `Bme280.SecondaryI2cAddress` .

    - [Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `I2cDevice` przez wywołanie `I2cDevice.Create` i przekazanie `i2cSettings` . `I2cDevice`Reprezentuje to magistralę I2C. `using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.
    - Inna `using` Deklaracja tworzy wystąpienie `Bme280` do reprezentowania czujnika. Wartość `I2cDevice` jest przenoszona w konstruktorze.
    - Czas wymagany do wykonania pomiarów przez mikroukład przy użyciu bieżących ustawień (domyślnych) układu jest pobierany przez wywołanie `GetMeasurementDuration` .
    - `while`Pętla jest uruchamiana w nieskończoność. Każda iteracja:
        1. Czyści konsolę.
        1. Ustawia tryb mocy na `Bmx280PowerMode.Forced` . Powoduje to wymuszenie przeprowadzenia jednej miary przez mikroukład, przechowanie wyników, a następnie uśpienie.
        1. Odczytuje wartości temperatury, ciśnienia, wilgotności i wysokości.

            > [!NOTE]
            > Wysokość jest obliczana na podstawie powiązania urządzenia. To Przeciążenie `TryReadAltitude` ma zastosowanie do wygenerowania szacunku poziomu średniego.

        1. Zapisuje bieżące warunki środowiska w konsoli programu.
        1. Uśpienie 1000 ms.

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.

    ```bash
    ./SensorTutorial
    ```

    Obserwuj dane wyjściowe czujnika w konsoli programu.

1. Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.

Gratulacje! Użyto I2C do odczytu wartości z czujnika ciśnienia temperatury/wilgotności/atmosferycznego!

## <a name="get-the-source-code"></a>Uzyskiwanie kodu źródłowego

Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/SensorTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się, jak wyświetlać tekst na wyświetlaczu LCD](../tutorials/lcd-display.md)
