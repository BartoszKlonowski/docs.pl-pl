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
# <a name="display-text-on-an-lcd"></a><span data-ttu-id="ff113-103">Wyświetlanie tekstu na wyświetlaczu LCD</span><span class="sxs-lookup"><span data-stu-id="ff113-103">Display text on an LCD</span></span>

<span data-ttu-id="ff113-104">Wyświetlacze LCD są przydatne do wyświetlania informacji bez potrzeby monitora zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="ff113-104">LCD character displays are useful for displaying information without the need for an external monitor.</span></span> <span data-ttu-id="ff113-105">Popularne wyświetlacze LCD mogą być połączone bezpośrednio z numerami PIN interfejsu GPIO, ale takie podejście wymaga użycia maksymalnie 10 numerów PIN interfejsu GPIO.</span><span class="sxs-lookup"><span data-stu-id="ff113-105">Common LCD character displays can be connected directly to the GPIO pins, but such an approach requires the use of up to 10 GPIO pins.</span></span> <span data-ttu-id="ff113-106">W scenariuszach, które wymagają połączenia z kombinacją urządzeń, rozgłosowanie tak dużej ilości nagłówka GPIO do wyświetlania znaków jest często niepraktyczne.</span><span class="sxs-lookup"><span data-stu-id="ff113-106">For scenarios that require connecting to a combination of devices, devoting so much of the GPIO header to a character display is often impractical.</span></span>

<span data-ttu-id="ff113-107">Wielu producentów sprzedaje 20x4 LCD z zintegrowanym ekspanderem GPIO.</span><span class="sxs-lookup"><span data-stu-id="ff113-107">Many manufacturers sell 20x4 LCD character displays with an integrated GPIO expander.</span></span> <span data-ttu-id="ff113-108">Wyświetlacz znaku łączy się bezpośrednio z ekspanderem GPIO, który następnie łączy się z Raspberry Pi za pośrednictwem protokołu szeregowego obwodu Inter-Integrated (I2C).</span><span class="sxs-lookup"><span data-stu-id="ff113-108">The character display connects directly to the GPIO expander, which then connects to the Raspberry Pi via the Inter-Integrated Circuit (I2C) serial protocol.</span></span>

<span data-ttu-id="ff113-109">W tym temacie zostanie użyty program .NET do wyświetlania tekstu na ekranie wyświetlacza LCD przy użyciu ekspandera I2C.</span><span class="sxs-lookup"><span data-stu-id="ff113-109">In this topic, you will use .NET to display text on an LCD character display using an I2C GPIO expander.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff113-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff113-110">Prerequisites</span></span>

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- <span data-ttu-id="ff113-111">[20x4 wyświetlacz LCD z interfejsem I2C](https://www.bing.com/images/search?q=20x4+lcd+display+with+i2c)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="ff113-111">[20x4 LCD Character Display with I2C interface](https://www.bing.com/images/search?q=20x4+lcd+display+with+i2c) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
- <span data-ttu-id="ff113-112">Przewody skoku</span><span class="sxs-lookup"><span data-stu-id="ff113-112">Jumper wires</span></span>
- <span data-ttu-id="ff113-113">Breadboard (opcjonalne/zalecane)</span><span class="sxs-lookup"><span data-stu-id="ff113-113">Breadboard (optional/recommended)</span></span>
- <span data-ttu-id="ff113-114">Tablica zagadnień Raspberry Pi GPIO (opcjonalne/zalecane)</span><span class="sxs-lookup"><span data-stu-id="ff113-114">Raspberry Pi GPIO breakout board (optional/recommended)</span></span>
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

> [!NOTE]
> <span data-ttu-id="ff113-115">Istnieje wielu producentów wyświetlaczy LCD.</span><span class="sxs-lookup"><span data-stu-id="ff113-115">There are many manufacturers of LCD character displays.</span></span> <span data-ttu-id="ff113-116">Większość projektów jest identyczna, a producent nie powinien dokonywać żadnych różnic w działaniu.</span><span class="sxs-lookup"><span data-stu-id="ff113-116">Most designs are identical, and the manufacturer shouldn't make any difference to the functionality.</span></span> <span data-ttu-id="ff113-117">Ten samouczek został opracowany z myślą o [wykrytym LCD2004](https://www.sunfounder.com/lcd2004-module.html) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="ff113-117">For reference, this tutorial was developed with the [SunFounder LCD2004](https://www.sunfounder.com/lcd2004-module.html) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="prepare-the-hardware"></a><span data-ttu-id="ff113-118">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="ff113-118">Prepare the hardware</span></span>

<span data-ttu-id="ff113-119">Aby połączyć cztery pinezki w ekspanderze I2C GPIO z Raspberry Pi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff113-119">Use jumper wires to connect the four pins on the I2C GPIO expander to the Raspberry Pi as follows:</span></span>

- <span data-ttu-id="ff113-120">GND na ziemię</span><span class="sxs-lookup"><span data-stu-id="ff113-120">GND to ground</span></span>
- <span data-ttu-id="ff113-121">VCC do 5V</span><span class="sxs-lookup"><span data-stu-id="ff113-121">VCC to 5V</span></span>
- <span data-ttu-id="ff113-122">SDA do SDA (GPIO 2)</span><span class="sxs-lookup"><span data-stu-id="ff113-122">SDA to SDA (GPIO 2)</span></span>
- <span data-ttu-id="ff113-123">SCL do SCL (GPIO 3)</span><span class="sxs-lookup"><span data-stu-id="ff113-123">SCL to SCL (GPIO 3)</span></span>

<span data-ttu-id="ff113-124">W razie potrzeby zapoznaj się z następującymi ilustracjami:</span><span class="sxs-lookup"><span data-stu-id="ff113-124">Refer to the following figures as needed:</span></span>

| <span data-ttu-id="ff113-125">Interfejs I2C (z tyłu ekranu)</span><span class="sxs-lookup"><span data-stu-id="ff113-125">I2C interface (back of display)</span></span> | <span data-ttu-id="ff113-126">Raspberry Pi GPIO</span><span class="sxs-lookup"><span data-stu-id="ff113-126">Raspberry Pi GPIO</span></span> |
|---------------------------------|-------------------|
| :::image type="content" source="../media/character-display-i2c-thumb.png" alt-text="Obraz z tyłu wyświetlania znaków przedstawiający Ekspander I2C GPIO." lightbox="../media/character-display-i2c.png"::: | :::image type="content" source="../media/gpio-pinout-diagram-thumb.png" alt-text="Diagram przedstawiający pinout nagłówka GPIO Raspberry Pi. Obraz przedstawiający Raspberry Pi Foundation." lightbox="../media/gpio-pinout-diagram.png":::<br /><span data-ttu-id="ff113-129">[Obraz przedstawiający Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="ff113-129">[Image courtesy Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>
 |

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a><span data-ttu-id="ff113-130">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ff113-130">Create the app</span></span>

<span data-ttu-id="ff113-131">Wykonaj następujące kroki w preferowanym środowisku programistycznym:</span><span class="sxs-lookup"><span data-stu-id="ff113-131">Complete the following steps in your preferred development environment:</span></span>

1. <span data-ttu-id="ff113-132">Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ff113-132">Create a new .NET Console App using either the [.NET CLI](../../core/tools/dotnet-new.md) or [Visual Studio](../../core/tutorials/with-visual-studio.md).</span></span> <span data-ttu-id="ff113-133">Nadaj mu nazwę *LcdTutorial*.</span><span class="sxs-lookup"><span data-stu-id="ff113-133">Name it *LcdTutorial*.</span></span>

    ```dotnetcli
    dotnet new console -o LcdTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. <span data-ttu-id="ff113-134">Zastąp zawartość pliku *Program.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="ff113-134">Replace the contents of *Program.cs* with the following code:</span></span>

    :::code language="csharp" source="~/iot-samples/tutorials/LcdTutorial/Program.cs" :::

    <span data-ttu-id="ff113-135">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="ff113-135">In the preceding code:</span></span>

    - <span data-ttu-id="ff113-136">[Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `I2cDevice` przez wywoływanie `I2cDevice.Create` i przekazanie nowego `I2cConnectionSettings` przy użyciu `busId` `deviceAddress` parametrów i.</span><span class="sxs-lookup"><span data-stu-id="ff113-136">A [using declaration](../../csharp/whats-new/csharp-8.md#using-declarations) creates an instance of `I2cDevice` by calling `I2cDevice.Create` and passing in a new `I2cConnectionSettings` with the `busId` and `deviceAddress` parameters.</span></span> <span data-ttu-id="ff113-137">`I2cDevice`Reprezentuje to magistralę I2C.</span><span class="sxs-lookup"><span data-stu-id="ff113-137">This `I2cDevice` represents the I2C bus.</span></span> <span data-ttu-id="ff113-138">`using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.</span><span class="sxs-lookup"><span data-stu-id="ff113-138">The `using` declaration ensures the object is disposed and hardware resources are released properly.</span></span>

        > [!WARNING]
        > <span data-ttu-id="ff113-139">Adres urządzenia dla ekspandera GPIO zależy od układu używanego przez producenta.</span><span class="sxs-lookup"><span data-stu-id="ff113-139">The device address for the GPIO expander depends on the chip used by the manufacturer.</span></span> <span data-ttu-id="ff113-140">Rozszerzenia interfejsu GPIO wyposażone w PCF8574 używają adresu `0x27` , podczas gdy korzystają z PCF8574A wiórów `0x3F` .</span><span class="sxs-lookup"><span data-stu-id="ff113-140">GPIO expanders equipped with a PCF8574 use the address `0x27`, while those using PCF8574A chips use `0x3F`.</span></span> <span data-ttu-id="ff113-141">Zapoznaj się z dokumentacją wyświetlacza LCD.</span><span class="sxs-lookup"><span data-stu-id="ff113-141">Consult your LCD's documentation.</span></span>

    - <span data-ttu-id="ff113-142">Inna `using` Deklaracja tworzy wystąpienie `Pcf8574` i przekazuje do `I2cDevice` konstruktora.</span><span class="sxs-lookup"><span data-stu-id="ff113-142">Another `using` declaration creates an instance of `Pcf8574` and passes the `I2cDevice` into the constructor.</span></span> <span data-ttu-id="ff113-143">To wystąpienie reprezentuje Ekspander interfejsu GPIO.</span><span class="sxs-lookup"><span data-stu-id="ff113-143">This instance represents the GPIO expander.</span></span>
    - <span data-ttu-id="ff113-144">Inna `using` Deklaracja tworzy wystąpienie `Lcd2004` do reprezentowania wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="ff113-144">Another `using` declaration creates an instance of `Lcd2004` to represent the display.</span></span> <span data-ttu-id="ff113-145">Kilka parametrów są przekazywane do konstruktora opisującego ustawienia, które mają być używane do komunikacji z ekspanderem GPIO.</span><span class="sxs-lookup"><span data-stu-id="ff113-145">Several parameters are passed to the constructor describing the settings to use to communicate with the GPIO expander.</span></span> <span data-ttu-id="ff113-146">Ekspander GPIO jest przekazaniem jako `controller` parametr.</span><span class="sxs-lookup"><span data-stu-id="ff113-146">The GPIO expander is passed as the `controller` parameter.</span></span>
    - <span data-ttu-id="ff113-147">`while`Pętla jest uruchamiana w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="ff113-147">A `while` loop runs indefinitely.</span></span> <span data-ttu-id="ff113-148">Każda iteracja:</span><span class="sxs-lookup"><span data-stu-id="ff113-148">Each iteration:</span></span>
        1. <span data-ttu-id="ff113-149">Czyści ekran.</span><span class="sxs-lookup"><span data-stu-id="ff113-149">Clears the display.</span></span>
        1. <span data-ttu-id="ff113-150">Ustawia położenie kursora do pierwszej pozycji w bieżącym wierszu.</span><span class="sxs-lookup"><span data-stu-id="ff113-150">Sets the cursor position to the first position on the current line.</span></span>
        1. <span data-ttu-id="ff113-151">Zapisuje bieżący czas do wyświetlania w bieżącym położeniu kursora.</span><span class="sxs-lookup"><span data-stu-id="ff113-151">Writes the current time to the display at the current cursor position.</span></span>
        1. <span data-ttu-id="ff113-152">Wykonuje iterację bieżącego licznika wiersza.</span><span class="sxs-lookup"><span data-stu-id="ff113-152">Iterates the current line counter.</span></span>
        1. <span data-ttu-id="ff113-153">Uśpienie 1000 ms.</span><span class="sxs-lookup"><span data-stu-id="ff113-153">Sleeps 1000 ms.</span></span>

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. <span data-ttu-id="ff113-154">Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="ff113-154">Run the app on the Raspberry Pi by switching to the deployment directory and running the executable.</span></span>

    ```bash
    ./LcdTutorial
    ```

    <span data-ttu-id="ff113-155">Obserwuj wyświetlacz wyświetlacza LCD jako bieżący czas wyświetlania w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="ff113-155">Observe the LCD character display as the current time displays on each line.</span></span>

    > [!TIP]
    > <span data-ttu-id="ff113-156">Jeśli ekran jest widoczny, ale nie widzisz żadnego tekstu, spróbuj dopasować numer kontrastu na odwrocie ekranu.</span><span class="sxs-lookup"><span data-stu-id="ff113-156">If the display is lit but you don't see any text, try adjusting the contrast dial on the back of the display.</span></span>

1. <span data-ttu-id="ff113-157">Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="ff113-157">Terminate the program by pressing <kbd>Ctrl+C</kbd>.</span></span>

<span data-ttu-id="ff113-158">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ff113-158">Congratulations!</span></span> <span data-ttu-id="ff113-159">Wyświetlasz tekst na wyświetlaczu LCD przy użyciu interfejsu I2C i ekspandera GPIO!</span><span class="sxs-lookup"><span data-stu-id="ff113-159">You've displayed text on an LCD using a I2C and a GPIO expander!</span></span>

## <a name="get-the-source-code"></a><span data-ttu-id="ff113-160">Uzyskiwanie kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="ff113-160">Get the source code</span></span>

<span data-ttu-id="ff113-161">Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/LcdTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="ff113-161">The source for this tutorial is [available on GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/LcdTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff113-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff113-162">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff113-163">Dowiedz się, jak korzystać z Ogólnego przeznaczenia danych wejściowych/wyjściowych w celu migania DIODy</span><span class="sxs-lookup"><span data-stu-id="ff113-163">Learn to use General Purpose Input/Output to blink an LED</span></span>](../tutorials/blink-led.md)
