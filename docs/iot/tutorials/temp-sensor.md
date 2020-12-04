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
# <a name="read-environmental-conditions-from-a-sensor"></a><span data-ttu-id="b6c2d-103">Odczytywanie warunków środowiska z czujnika</span><span class="sxs-lookup"><span data-stu-id="b6c2d-103">Read environmental conditions from a sensor</span></span>

<span data-ttu-id="b6c2d-104">Jednym z najpopularniejszych scenariuszy dotyczących urządzeń IoT jest wykrywanie warunków środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-104">One of the most common scenarios for IoT devices is detection of environmental conditions.</span></span> <span data-ttu-id="b6c2d-105">Różne czujniki są dostępne do monitorowania temperatury, wilgotności, ciśnienia atmosferycznego i nie tylko.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-105">A variety of sensors are available to monitor temperature, humidity, barometric pressure, and more.</span></span>

<span data-ttu-id="b6c2d-106">W tym temacie zostanie użyty program .NET do odczytywania warunków środowiskowych z czujnika.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-106">In this topic, you will use .NET to read environmental conditions from a sensor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6c2d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b6c2d-107">Prerequisites</span></span>

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- <span data-ttu-id="b6c2d-108">[BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout) <span class="docon docon-navigate-external x-hidden-focus"></span> wilgotność/ciśnienie atmosferyczne/czujnik temperatury zagadnień</span><span class="sxs-lookup"><span data-stu-id="b6c2d-108">[BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout) <span class="docon docon-navigate-external x-hidden-focus"></span> humidity/barometric pressure/temperature sensor breakout</span></span>
- <span data-ttu-id="b6c2d-109">Przewody skoku</span><span class="sxs-lookup"><span data-stu-id="b6c2d-109">Jumper wires</span></span>
- <span data-ttu-id="b6c2d-110">Breadboard (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="b6c2d-110">Breadboard (optional)</span></span>
- <span data-ttu-id="b6c2d-111">Tablica Raspberry Pi GPIO zagadnień (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="b6c2d-111">Raspberry Pi GPIO breakout board (optional)</span></span>
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

> [!IMPORTANT]
> <span data-ttu-id="b6c2d-112">Istnieje wielu producentów BME280 podgrupach.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-112">There are many manufacturers of BME280 breakouts.</span></span> <span data-ttu-id="b6c2d-113">Większość projektów jest podobna, a producent nie powinien dokonywać żadnych różnic w działaniu.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-113">Most designs are similar, and the manufacturer shouldn't make any difference to the functionality.</span></span> <span data-ttu-id="b6c2d-114">Ten samouczek próbuje uwzględnić odmiany.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-114">This tutorial attempts to account for variations.</span></span> <span data-ttu-id="b6c2d-115">Upewnij się, że BME280 zagadnień zawiera interfejs obwodu Inter-Integrated (I2C).</span><span class="sxs-lookup"><span data-stu-id="b6c2d-115">Ensure your BME280 breakout includes an Inter-Integrated Circuit (I2C) interface.</span></span>

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="prepare-the-hardware"></a><span data-ttu-id="b6c2d-116">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="b6c2d-116">Prepare the hardware</span></span>

<span data-ttu-id="b6c2d-117">Użyj składników sprzętowych, aby skompilować obwód, jak przedstawiono na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="b6c2d-117">Use the hardware components to build the circuit as depicted in the following diagram:</span></span>

:::image type="content" source="../media/rpi-bmp280_i2c-thumb.png" alt-text="Diagram Fritzing przedstawiający połączenie z tablicy Raspberry Pi z BME280 zagadnień" lightbox="../media/rpi-bmp280_i2c.png":::

<span data-ttu-id="b6c2d-119">Poniżej przedstawiono połączenia z Raspberry Pi do BME280 zagadnień:</span><span class="sxs-lookup"><span data-stu-id="b6c2d-119">The following are the connections from the Raspberry Pi to the BME280 breakout:</span></span>

- <span data-ttu-id="b6c2d-120">3.3 v do VIN *lub* 3v3 (pokazane na czerwono)</span><span class="sxs-lookup"><span data-stu-id="b6c2d-120">3.3V to VIN *OR* 3V3 (shown in red)</span></span>
- <span data-ttu-id="b6c2d-121">Od podstaw do GND (czarny)</span><span class="sxs-lookup"><span data-stu-id="b6c2d-121">Ground to GND (black)</span></span>
- <span data-ttu-id="b6c2d-122">SDA (GPIO 2) do SDI *lub* SDA (Blue)</span><span class="sxs-lookup"><span data-stu-id="b6c2d-122">SDA (GPIO 2) to SDI *OR* SDA (blue)</span></span>
- <span data-ttu-id="b6c2d-123">SCL (GPIO 3) do SCK *lub* SCL (pomarańczowy)</span><span class="sxs-lookup"><span data-stu-id="b6c2d-123">SCL (GPIO 3) to SCK *OR* SCL (orange)</span></span>

[!INCLUDE [tutorial-rpi-gpio](../includes/tutorial-rpi-gpio.md)]

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a><span data-ttu-id="b6c2d-124">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b6c2d-124">Create the app</span></span>

<span data-ttu-id="b6c2d-125">Wykonaj następujące kroki w preferowanym środowisku programistycznym:</span><span class="sxs-lookup"><span data-stu-id="b6c2d-125">Complete the following steps in your preferred development environment:</span></span>

1. <span data-ttu-id="b6c2d-126">Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b6c2d-126">Create a new .NET Console App using either the [.NET CLI](../../core/tools/dotnet-new.md) or [Visual Studio](../../core/tutorials/with-visual-studio.md).</span></span> <span data-ttu-id="b6c2d-127">Nadaj mu nazwę *SensorTutorial*.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-127">Name it *SensorTutorial*.</span></span>

    ```dotnetcli
    dotnet new console -o SensorTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. <span data-ttu-id="b6c2d-128">Zastąp zawartość pliku *Program.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="b6c2d-128">Replace the contents of *Program.cs* with the following code:</span></span>

    :::code language="csharp" source="~/iot-samples/tutorials/SensorTutorial/Program.cs" :::

    <span data-ttu-id="b6c2d-129">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="b6c2d-129">In the preceding code:</span></span>

    - <span data-ttu-id="b6c2d-130">`i2cSettings` jest ustawiony na nowe wystąpienie `I2cConnectionSettings` .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-130">`i2cSettings` is set to a new instance of `I2cConnectionSettings`.</span></span> <span data-ttu-id="b6c2d-131">Konstruktor ustawia `busId` parametr na wartość 1, a `deviceAddress` parametr na `Bme280.DefaultI2cAddress` .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-131">The constructor sets the `busId` parameter to 1 and the `deviceAddress` parameter to `Bme280.DefaultI2cAddress`.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="b6c2d-132">Niektórzy producenci BME280 zagadnień używają dodatkowej wartości adresu.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-132">Some BME280 breakout manufacturers use the secondary address value.</span></span> <span data-ttu-id="b6c2d-133">Dla tych urządzeń Użyj `Bme280.SecondaryI2cAddress` .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-133">For those devices, use `Bme280.SecondaryI2cAddress`.</span></span>

    - <span data-ttu-id="b6c2d-134">[Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `I2cDevice` przez wywołanie `I2cDevice.Create` i przekazanie `i2cSettings` .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-134">A [using declaration](../../csharp/whats-new/csharp-8.md#using-declarations) creates an instance of `I2cDevice` by calling `I2cDevice.Create` and passing in `i2cSettings`.</span></span> <span data-ttu-id="b6c2d-135">`I2cDevice`Reprezentuje to magistralę I2C.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-135">This `I2cDevice` represents the I2C bus.</span></span> <span data-ttu-id="b6c2d-136">`using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-136">The `using` declaration ensures the object is disposed and hardware resources are released properly.</span></span>
    - <span data-ttu-id="b6c2d-137">Inna `using` Deklaracja tworzy wystąpienie `Bme280` do reprezentowania czujnika.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-137">Another `using` declaration creates an instance of `Bme280` to represent the sensor.</span></span> <span data-ttu-id="b6c2d-138">Wartość `I2cDevice` jest przenoszona w konstruktorze.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-138">The `I2cDevice` is passed in the constructor.</span></span>
    - <span data-ttu-id="b6c2d-139">Czas wymagany do wykonania pomiarów przez mikroukład przy użyciu bieżących ustawień (domyślnych) układu jest pobierany przez wywołanie `GetMeasurementDuration` .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-139">The time required for the chip to take measurements with the chip's current (default) settings is retrieved by calling `GetMeasurementDuration`.</span></span>
    - <span data-ttu-id="b6c2d-140">`while`Pętla jest uruchamiana w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-140">A `while` loop runs indefinitely.</span></span> <span data-ttu-id="b6c2d-141">Każda iteracja:</span><span class="sxs-lookup"><span data-stu-id="b6c2d-141">Each iteration:</span></span>
        1. <span data-ttu-id="b6c2d-142">Czyści konsolę.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-142">Clears the console.</span></span>
        1. <span data-ttu-id="b6c2d-143">Ustawia tryb mocy na `Bmx280PowerMode.Forced` .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-143">Sets the power mode to `Bmx280PowerMode.Forced`.</span></span> <span data-ttu-id="b6c2d-144">Powoduje to wymuszenie przeprowadzenia jednej miary przez mikroukład, przechowanie wyników, a następnie uśpienie.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-144">This forces the chip to perform one measurement, store the results, and then sleep.</span></span>
        1. <span data-ttu-id="b6c2d-145">Odczytuje wartości temperatury, ciśnienia, wilgotności i wysokości.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-145">Reads the values for temperature, pressure, humidity, and altitude.</span></span>

            > [!NOTE]
            > <span data-ttu-id="b6c2d-146">Wysokość jest obliczana na podstawie powiązania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-146">Altitude is calculated by the device binding.</span></span> <span data-ttu-id="b6c2d-147">To Przeciążenie `TryReadAltitude` ma zastosowanie do wygenerowania szacunku poziomu średniego.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-147">This overload of `TryReadAltitude` uses mean sea level pressure to generate an estimate.</span></span>

        1. <span data-ttu-id="b6c2d-148">Zapisuje bieżące warunki środowiska w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-148">Writes the current environmental conditions to the console.</span></span>
        1. <span data-ttu-id="b6c2d-149">Uśpienie 1000 ms.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-149">Sleeps 1000 ms.</span></span>

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. <span data-ttu-id="b6c2d-150">Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-150">Run the app on the Raspberry Pi by switching to the deployment directory and running the executable.</span></span>

    ```bash
    ./SensorTutorial
    ```

    <span data-ttu-id="b6c2d-151">Obserwuj dane wyjściowe czujnika w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-151">Observe the sensor output in the console.</span></span>

1. <span data-ttu-id="b6c2d-152">Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="b6c2d-152">Terminate the program by pressing <kbd>Ctrl+C</kbd>.</span></span>

<span data-ttu-id="b6c2d-153">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="b6c2d-153">Congratulations!</span></span> <span data-ttu-id="b6c2d-154">Użyto I2C do odczytu wartości z czujnika ciśnienia temperatury/wilgotności/atmosferycznego!</span><span class="sxs-lookup"><span data-stu-id="b6c2d-154">You've used I2C to read values from a temperature/humidity/barometric pressure sensor!</span></span>

## <a name="get-the-source-code"></a><span data-ttu-id="b6c2d-155">Uzyskiwanie kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="b6c2d-155">Get the source code</span></span>

<span data-ttu-id="b6c2d-156">Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/SensorTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="b6c2d-156">The source for this tutorial is [available on GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/SensorTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6c2d-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6c2d-157">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6c2d-158">Dowiedz się, jak wyświetlać tekst na wyświetlaczu LCD</span><span class="sxs-lookup"><span data-stu-id="b6c2d-158">Learn how to display text on an LCD</span></span>](../tutorials/lcd-display.md)
