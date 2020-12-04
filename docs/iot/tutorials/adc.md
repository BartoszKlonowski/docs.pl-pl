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
# <a name="read-values-from-an-analog-to-digital-converter"></a><span data-ttu-id="84518-103">Odczytywanie wartości z przetwornika analogowo-cyfrowego</span><span class="sxs-lookup"><span data-stu-id="84518-103">Read values from an analog-to-digital converter</span></span>

<span data-ttu-id="84518-104">Konwerter analogowo-cyfrowy (ADC) to urządzenie, które może odczytywać wartość napięcia wejściowego sygnału analogowego i przekształcić ją w wartość cyfrową.</span><span class="sxs-lookup"><span data-stu-id="84518-104">An analog-to-digital converter (ADC) is a device that can read an analog input voltage value and convert it into a digital value.</span></span> <span data-ttu-id="84518-105">ADCs są używane do odczytywania wartości z thermistors, potencjometrów i innych urządzeń, które zmieniają odporność na podstawie określonych warunków.</span><span class="sxs-lookup"><span data-stu-id="84518-105">ADCs are used for reading values from thermistors, potentiometers, and other devices that change resistance based on certain conditions.</span></span>

<span data-ttu-id="84518-106">W tym temacie użyjesz platformy .NET do odczytu wartości z ADC w miarę modulacji napięcia wejściowego z potencjometrem.</span><span class="sxs-lookup"><span data-stu-id="84518-106">In this topic, you will use .NET to read values from an ADC as you modulate the input voltage with a potentiometer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84518-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="84518-107">Prerequisites</span></span>

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- <span data-ttu-id="84518-108">[MCP3008](https://www.microchip.com/wwwproducts/MCP3008) <span class="docon docon-navigate-external x-hidden-focus"></span> konwerter analogowo-cyfrowy</span><span class="sxs-lookup"><span data-stu-id="84518-108">[MCP3008](https://www.microchip.com/wwwproducts/MCP3008) <span class="docon docon-navigate-external x-hidden-focus"></span> analog-to-digital converter</span></span>
- <span data-ttu-id="84518-109">Potencjometr z trzema numerami PIN</span><span class="sxs-lookup"><span data-stu-id="84518-109">Three-pin potentiometer</span></span>
- <span data-ttu-id="84518-110">Breadboard</span><span class="sxs-lookup"><span data-stu-id="84518-110">Breadboard</span></span>
- <span data-ttu-id="84518-111">Przewody skoku</span><span class="sxs-lookup"><span data-stu-id="84518-111">Jumper wires</span></span>
- <span data-ttu-id="84518-112">Tablica zagadnień Raspberry Pi GPIO (opcjonalne/zalecane)</span><span class="sxs-lookup"><span data-stu-id="84518-112">Raspberry Pi GPIO breakout board (optional/recommended)</span></span>
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

[!INCLUDE [prepare-pi-spi](../includes/prepare-pi-spi.md)]

## <a name="prepare-the-hardware"></a><span data-ttu-id="84518-113">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="84518-113">Prepare the hardware</span></span>

<span data-ttu-id="84518-114">Użyj składników sprzętowych, aby skompilować obwód, jak przedstawiono na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="84518-114">Use the hardware components to build the circuit as depicted in the following diagram:</span></span>

:::image type="content" source="../media/rpi-trimpot_spi-thumb.png" alt-text="Diagram Fritzing przedstawiający obwód z MCP3008 ADC i potencjometr" lightbox="../media/rpi-trimpot_spi.png":::

<span data-ttu-id="84518-116">MCP3008 używa interfejsu szeregowego urządzenia peryferyjnego (SPI) do komunikacji.</span><span class="sxs-lookup"><span data-stu-id="84518-116">The MCP3008 uses Serial Peripheral Interface (SPI) to communicate.</span></span> <span data-ttu-id="84518-117">Poniżej przedstawiono połączenia z MCP3008 do Raspberry Pi i Potencjometr:</span><span class="sxs-lookup"><span data-stu-id="84518-117">The following are the connections from the MCP3008 to the Raspberry Pi and potentiometer:</span></span>

- <span data-ttu-id="84518-118">Od<sub>DD</sub> do 3.3 v (pokazane na czerwono)</span><span class="sxs-lookup"><span data-stu-id="84518-118">V<sub>DD</sub> to 3.3V (shown in red)</span></span>
- <span data-ttu-id="84518-119">V<sub>ref</sub> do 3.3 v (czerwony)</span><span class="sxs-lookup"><span data-stu-id="84518-119">V<sub>REF</sub> to 3.3V (red)</span></span>
- <span data-ttu-id="84518-120">AGND na ziemię (czerń)</span><span class="sxs-lookup"><span data-stu-id="84518-120">AGND to ground (black)</span></span>
- <span data-ttu-id="84518-121">CLK do SCLK (pomarańczowy)</span><span class="sxs-lookup"><span data-stu-id="84518-121">CLK to SCLK (orange)</span></span>
- <span data-ttu-id="84518-122">D<sub>do</sub> miso (pomarańczowy)</span><span class="sxs-lookup"><span data-stu-id="84518-122">D<sub>OUT</sub> to MISO (orange)</span></span>
- <span data-ttu-id="84518-123">D<sub>w</sub> do mosi (pomarańczowy)</span><span class="sxs-lookup"><span data-stu-id="84518-123">D<sub>IN</sub> to MOSI (orange)</span></span>
- <span data-ttu-id="84518-124">CS/SHDN do CE0 (zielony)</span><span class="sxs-lookup"><span data-stu-id="84518-124">CS/SHDN to CE0 (green)</span></span>
- <span data-ttu-id="84518-125">DGND na ziemię (czerń)</span><span class="sxs-lookup"><span data-stu-id="84518-125">DGND to ground (black)</span></span>
- <span data-ttu-id="84518-126">CH0 do zmiennej (środkowej) numeru PIN na potencjometr (żółty)</span><span class="sxs-lookup"><span data-stu-id="84518-126">CH0 to variable (middle) pin on potentiometer (yellow)</span></span>

<span data-ttu-id="84518-127">Dostarczaj 3.3 V i ziemi do zewnętrznych pinów na potencjometr.</span><span class="sxs-lookup"><span data-stu-id="84518-127">Supply 3.3V and ground to the outer pins on the potentiometer.</span></span> <span data-ttu-id="84518-128">Zamówienie jest nieważne.</span><span class="sxs-lookup"><span data-stu-id="84518-128">Order is unimportant.</span></span>

<span data-ttu-id="84518-129">W razie potrzeby zapoznaj się z poniższymi diagramami pinout:</span><span class="sxs-lookup"><span data-stu-id="84518-129">Refer to the following pinout diagrams as needed:</span></span>

| <span data-ttu-id="84518-130">MCP3008</span><span class="sxs-lookup"><span data-stu-id="84518-130">MCP3008</span></span>  | <span data-ttu-id="84518-131">Raspberry Pi GPIO</span><span class="sxs-lookup"><span data-stu-id="84518-131">Raspberry Pi GPIO</span></span> |
|----------|-------------------|
| :::image type="content" source="../media/mcp3008-diagram-thumb.png" alt-text="Diagram przedstawiający pinout MCP3008" lightbox="../media/mcp3008-diagram.png"::: | :::image type="content" source="../media/gpio-pinout-diagram-thumb.png" alt-text="Diagram przedstawiający pinout nagłówka GPIO Raspberry Pi. Obraz przedstawiający Raspberry Pi Foundation." lightbox="../media/gpio-pinout-diagram.png":::<br /><span data-ttu-id="84518-134">[Obraz przedstawiający Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/).</span><span class="sxs-lookup"><span data-stu-id="84518-134">[Image courtesy Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/).</span></span>
 |

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a><span data-ttu-id="84518-135">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="84518-135">Create the app</span></span>

<span data-ttu-id="84518-136">Wykonaj następujące kroki w preferowanym środowisku programistycznym:</span><span class="sxs-lookup"><span data-stu-id="84518-136">Complete the following steps in your preferred development environment:</span></span>

1. <span data-ttu-id="84518-137">Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="84518-137">Create a new .NET Console App using either the [.NET CLI](../../core/tools/dotnet-new.md) or [Visual Studio](../../core/tutorials/with-visual-studio.md).</span></span> <span data-ttu-id="84518-138">Nadaj mu nazwę *AdcTutorial*.</span><span class="sxs-lookup"><span data-stu-id="84518-138">Name it *AdcTutorial*.</span></span>

    ```dotnetcli
    dotnet new console -o AdcTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. <span data-ttu-id="84518-139">Zastąp zawartość pliku *Program.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="84518-139">Replace the contents of *Program.cs* with the following code:</span></span>

    :::code language="csharp" source="~/iot-samples/tutorials/AdcTutorial/Program.cs" :::

    <span data-ttu-id="84518-140">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="84518-140">In the preceding code:</span></span>

    - <span data-ttu-id="84518-141">`hardwareSpiSettings` jest ustawiony na nowe wystąpienie `SpiConnectionSettings` .</span><span class="sxs-lookup"><span data-stu-id="84518-141">`hardwareSpiSettings` is set to a new instance of `SpiConnectionSettings`.</span></span> <span data-ttu-id="84518-142">Konstruktor ustawia `busId` parametr na 0, a `chipSelectLine` parametr na 0.</span><span class="sxs-lookup"><span data-stu-id="84518-142">The constructor sets the `busId` parameter to 0 and the `chipSelectLine` parameter to 0.</span></span>
    - <span data-ttu-id="84518-143">[Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `SpiDevice` przez wywołanie `SpiDevice.Create` i przekazanie `hardwareSpiSettings` .</span><span class="sxs-lookup"><span data-stu-id="84518-143">A [using declaration](../../csharp/whats-new/csharp-8.md#using-declarations) creates an instance of `SpiDevice` by calling `SpiDevice.Create` and passing in `hardwareSpiSettings`.</span></span> <span data-ttu-id="84518-144">`SpiDevice`Reprezentuje magistralę WWH.</span><span class="sxs-lookup"><span data-stu-id="84518-144">This `SpiDevice` represents the SPI bus.</span></span> <span data-ttu-id="84518-145">`using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.</span><span class="sxs-lookup"><span data-stu-id="84518-145">The `using` declaration ensures the object is disposed and hardware resources are released properly.</span></span>
    - <span data-ttu-id="84518-146">Inna `using` Deklaracja tworzy wystąpienie `Mcp3008` i przekazuje do `SpiDevice` konstruktora.</span><span class="sxs-lookup"><span data-stu-id="84518-146">Another `using` declaration creates an instance of `Mcp3008` and passes the `SpiDevice` into the constructor.</span></span>
    - <span data-ttu-id="84518-147">`while`Pętla jest uruchamiana w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="84518-147">A `while` loop runs indefinitely.</span></span> <span data-ttu-id="84518-148">Każda iteracja:</span><span class="sxs-lookup"><span data-stu-id="84518-148">Each iteration:</span></span>
        1. <span data-ttu-id="84518-149">Odczytuje wartość CH0 na ADC, wywołując metodę `mcp.Read(0)` .</span><span class="sxs-lookup"><span data-stu-id="84518-149">Reads the value of CH0 on the ADC by calling `mcp.Read(0)`.</span></span>
        1. <span data-ttu-id="84518-150">Dzieli wartość na 10,24.</span><span class="sxs-lookup"><span data-stu-id="84518-150">Divides the value by 10.24.</span></span> <span data-ttu-id="84518-151">MCP3008 jest 10-bitowym ADC, co oznacza, że zwraca 1024 możliwych wartości z zakresu 0-1023.</span><span class="sxs-lookup"><span data-stu-id="84518-151">The MCP3008 is a 10-bit ADC, which means it returns 1024 possible values ranging 0-1023.</span></span> <span data-ttu-id="84518-152">Dzielenie wartości przez 10,24 reprezentuje wartość procentową.</span><span class="sxs-lookup"><span data-stu-id="84518-152">Dividing the value by 10.24 represents the value as a percentage.</span></span>
        1. <span data-ttu-id="84518-153">Zaokrągla wartość do najbliższej liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="84518-153">Rounds the value to the nearest integer.</span></span>
        1. <span data-ttu-id="84518-154">Zapisuje wartość do konsoli sformatowaną jako wartość procentowa.</span><span class="sxs-lookup"><span data-stu-id="84518-154">Writes the value to the console formatted as a percentage.</span></span>
        1. <span data-ttu-id="84518-155">Uśpienie 500 ms.</span><span class="sxs-lookup"><span data-stu-id="84518-155">Sleeps 500 ms.</span></span>

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. <span data-ttu-id="84518-156">Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="84518-156">Run the app on the Raspberry Pi by switching to the deployment directory and running the executable.</span></span>

    ```bash
    ./AdcTutorial
    ```

    <span data-ttu-id="84518-157">Obserwuj dane wyjściowe podczas obracania tarczy.</span><span class="sxs-lookup"><span data-stu-id="84518-157">Observe the output as you rotate the potentiometer dial.</span></span> <span data-ttu-id="84518-158">Jest to spowodowane różnicą napięcia podanego w CH0 na ADC.</span><span class="sxs-lookup"><span data-stu-id="84518-158">This is due to the potentiometer varying the voltage supplied to CH0 on the ADC.</span></span> <span data-ttu-id="84518-159">ADC porównuje napięcie wejściowe z CH0 do napięcia odniesienia dostarczonego do<sub>odwołania</sub> V w celu wygenerowania wartości.</span><span class="sxs-lookup"><span data-stu-id="84518-159">The ADC compares the input voltage on CH0 to the reference voltage supplied to V<sub>REF</sub> to generate a value.</span></span>

1. <span data-ttu-id="84518-160">Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="84518-160">Terminate the program by pressing <kbd>Ctrl+C</kbd>.</span></span>

<span data-ttu-id="84518-161">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="84518-161">Congratulations!</span></span> <span data-ttu-id="84518-162">Indeks SPI jest używany do odczytywania wartości z konwertera Analog-to-Digital.</span><span class="sxs-lookup"><span data-stu-id="84518-162">You've used SPI to read values from an analog-to-digital converter.</span></span>

## <a name="get-the-source-code"></a><span data-ttu-id="84518-163">Uzyskiwanie kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="84518-163">Get the source code</span></span>

<span data-ttu-id="84518-164">Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/AdcTutorial).</span><span class="sxs-lookup"><span data-stu-id="84518-164">The source for this tutorial is [available on GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/AdcTutorial).</span></span> <span class="docon docon-navigate-external x-hidden-focus"></span>

## <a name="next-steps"></a><span data-ttu-id="84518-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84518-165">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="84518-166">Dowiedz się, jak korzystać z Ogólnego przeznaczenia danych wejściowych/wyjściowych w celu migania DIODy</span><span class="sxs-lookup"><span data-stu-id="84518-166">Learn to use General Purpose Input/Output to blink an LED</span></span>](../tutorials/blink-led.md)
