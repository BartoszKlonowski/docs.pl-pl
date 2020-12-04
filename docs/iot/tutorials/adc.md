---
title: Odczytywanie wartości z przetwornika analogowo-cyfrowego
description: Dowiedz się, jak odczytywać zmienne wartości napięcia przy użyciu konwertera Analog-to-Digital.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: eda6d8980d256c8063f2bfe1e051b0cb90b587ad
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590059"
---
<!--markdownlint-disable DOCSMD011 -->
# <a name="read-values-from-an-analog-to-digital-converter"></a>Odczytywanie wartości z przetwornika analogowo-cyfrowego

Konwerter analogowo-cyfrowy (ADC) to urządzenie, które może odczytywać wartość napięcia wejściowego sygnału analogowego i przekształcić ją w wartość cyfrową. ADCs są używane do odczytywania wartości z thermistors, potencjometrów i innych urządzeń, które zmieniają odporność na podstawie określonych warunków.

W tym temacie użyjesz platformy .NET do odczytu wartości z ADC w miarę modulacji napięcia wejściowego z potencjometrem.

## <a name="prerequisites"></a>Wymagania wstępne

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- [MCP3008](https://www.microchip.com/wwwproducts/MCP3008) <span class="docon docon-navigate-external x-hidden-focus"></span> konwerter analogowo-cyfrowy
- Potencjometr z trzema numerami PIN
- Breadboard
- Przewody skoku
- Tablica zagadnień Raspberry Pi GPIO (opcjonalne/zalecane)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

[!INCLUDE [prepare-pi-spi](../includes/prepare-pi-spi.md)]

## <a name="prepare-the-hardware"></a>Przygotowanie sprzętu

Użyj składników sprzętowych, aby skompilować obwód, jak przedstawiono na poniższym diagramie:

:::image type="content" source="../media/rpi-trimpot_spi-thumb.png" alt-text="Diagram Fritzing przedstawiający obwód z MCP3008 ADC i potencjometr" lightbox="../media/rpi-trimpot_spi.png":::

MCP3008 używa interfejsu szeregowego urządzenia peryferyjnego (SPI) do komunikacji. Poniżej przedstawiono połączenia z MCP3008 do Raspberry Pi i Potencjometr:

- Od<sub>DD</sub> do 3.3 v (pokazane na czerwono)
- V<sub>ref</sub> do 3.3 v (czerwony)
- AGND na ziemię (czerń)
- CLK do SCLK (pomarańczowy)
- D<sub>do</sub> miso (pomarańczowy)
- D<sub>w</sub> do mosi (pomarańczowy)
- CS/SHDN do CE0 (zielony)
- DGND na ziemię (czerń)
- CH0 do zmiennej (środkowej) numeru PIN na potencjometr (żółty)

Dostarczaj 3.3 V i ziemi do zewnętrznych pinów na potencjometr. Zamówienie jest nieważne.

W razie potrzeby zapoznaj się z poniższymi diagramami pinout:

| MCP3008  | Raspberry Pi GPIO |
|----------|-------------------|
| :::image type="content" source="../media/mcp3008-diagram-thumb.png" alt-text="Diagram przedstawiający pinout MCP3008" lightbox="../media/mcp3008-diagram.png"::: | :::image type="content" source="../media/gpio-pinout-diagram-thumb.png" alt-text="Diagram przedstawiający pinout nagłówka GPIO Raspberry Pi. Obraz przedstawiający Raspberry Pi Foundation." lightbox="../media/gpio-pinout-diagram.png":::<br />[Obraz przedstawiający Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/).
 |

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Tworzenie aplikacji

Wykonaj następujące kroki w preferowanym środowisku programistycznym:

1. Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md). Nadaj mu nazwę *AdcTutorial*.

    ```dotnetcli
    dotnet new console -o AdcTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Zastąp zawartość pliku *Program.cs* następującym kodem:

    :::code language="csharp" source="~/iot-samples/tutorials/AdcTutorial/Program.cs" :::

    Powyższy kod ma następujące działanie:

    - `hardwareSpiSettings` jest ustawiony na nowe wystąpienie `SpiConnectionSettings` . Konstruktor ustawia `busId` parametr na 0, a `chipSelectLine` parametr na 0.
    - [Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `SpiDevice` przez wywołanie `SpiDevice.Create` i przekazanie `hardwareSpiSettings` . `SpiDevice`Reprezentuje magistralę WWH. `using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.
    - Inna `using` Deklaracja tworzy wystąpienie `Mcp3008` i przekazuje do `SpiDevice` konstruktora.
    - `while`Pętla jest uruchamiana w nieskończoność. Każda iteracja:
        1. Odczytuje wartość CH0 na ADC, wywołując metodę `mcp.Read(0)` .
        1. Dzieli wartość na 10,24. MCP3008 jest 10-bitowym ADC, co oznacza, że zwraca 1024 możliwych wartości z zakresu 0-1023. Dzielenie wartości przez 10,24 reprezentuje wartość procentową.
        1. Zaokrągla wartość do najbliższej liczby całkowitej.
        1. Zapisuje wartość do konsoli sformatowaną jako wartość procentowa.
        1. Uśpienie 500 ms.

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.

    ```bash
    ./AdcTutorial
    ```

    Obserwuj dane wyjściowe podczas obracania tarczy. Jest to spowodowane różnicą napięcia podanego w CH0 na ADC. ADC porównuje napięcie wejściowe z CH0 do napięcia odniesienia dostarczonego do<sub>odwołania</sub> V w celu wygenerowania wartości.

1. Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.

Gratulacje! Indeks SPI jest używany do odczytywania wartości z konwertera Analog-to-Digital.

## <a name="get-the-source-code"></a>Uzyskiwanie kodu źródłowego

Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/AdcTutorial). <span class="docon docon-navigate-external x-hidden-focus"></span>

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się, jak korzystać z Ogólnego przeznaczenia danych wejściowych/wyjściowych w celu migania DIODy](../tutorials/blink-led.md)
