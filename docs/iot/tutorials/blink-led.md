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
# <a name="blink-an-led"></a><span data-ttu-id="f53fb-103">Miganie diodą LED</span><span class="sxs-lookup"><span data-stu-id="f53fb-103">Blink an LED</span></span>

<span data-ttu-id="f53fb-104">Numery PIN operacji we/wy ogólnego przeznaczenia (GPIO) mogą być kontrolowane indywidualnie.</span><span class="sxs-lookup"><span data-stu-id="f53fb-104">General-purpose I/O (GPIO) pins can be controlled individually.</span></span> <span data-ttu-id="f53fb-105">Jest to przydatne do kontrolowania diod LED, przekaźników i innych urządzeń stanowych.</span><span class="sxs-lookup"><span data-stu-id="f53fb-105">This is useful for controlling LEDs, relays, and other stateful devices.</span></span> <span data-ttu-id="f53fb-106">W tym temacie będziesz używać platformy .NET i pinów interfejsu GPIO Raspberry Pi, aby obsługiwać diody LED i wielokrotnie migać.</span><span class="sxs-lookup"><span data-stu-id="f53fb-106">In this topic, you will use .NET and your Raspberry Pi's GPIO pins to power an LED and blink it repeatedly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f53fb-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f53fb-107">Prerequisites</span></span>

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- <span data-ttu-id="f53fb-108">dioda LED 5 mm</span><span class="sxs-lookup"><span data-stu-id="f53fb-108">5 mm LED</span></span>
- <span data-ttu-id="f53fb-109">Ω opornik 330</span><span class="sxs-lookup"><span data-stu-id="f53fb-109">330 Ω resistor</span></span>
- <span data-ttu-id="f53fb-110">Breadboard</span><span class="sxs-lookup"><span data-stu-id="f53fb-110">Breadboard</span></span>
- <span data-ttu-id="f53fb-111">Przewody skoku</span><span class="sxs-lookup"><span data-stu-id="f53fb-111">Jumper wires</span></span>
- <span data-ttu-id="f53fb-112">Tablica zagadnień Raspberry Pi GPIO (opcjonalne/zalecane)</span><span class="sxs-lookup"><span data-stu-id="f53fb-112">Raspberry Pi GPIO breakout board (optional/recommended)</span></span>
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

[!INCLUDE [ensure-ssh](../includes/ensure-ssh.md)]

## <a name="prepare-the-hardware"></a><span data-ttu-id="f53fb-113">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="f53fb-113">Prepare the hardware</span></span>

<span data-ttu-id="f53fb-114">Użyj składników sprzętowych, aby skompilować obwód, jak przedstawiono na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="f53fb-114">Use the hardware components to build the circuit as depicted in the following diagram:</span></span>

:::image type="content" source="../media/rpi-led_bb-thumb.png" alt-text="Diagram Fritzing pokazujący obwód z diodą LED i opornikiem" lightbox="../media/rpi-led_bb.png":::

<span data-ttu-id="f53fb-116">Na powyższym obrazie przedstawiono następujące połączenia:</span><span class="sxs-lookup"><span data-stu-id="f53fb-116">The image above depicts the following connections:</span></span>

- <span data-ttu-id="f53fb-117">Program GPIO 18 do diody LED (dłuższy, pozytywny potencjalny klient)</span><span class="sxs-lookup"><span data-stu-id="f53fb-117">GPIO 18 to LED anode (longer, positive lead)</span></span>
- <span data-ttu-id="f53fb-118">Wywodzij katodę (krótszy, negatywny potencjalny klient) do 330 Ω (jeden koniec)</span><span class="sxs-lookup"><span data-stu-id="f53fb-118">LED cathode (shorter, negative lead) to 330 Ω resistor (either end)</span></span>
- <span data-ttu-id="f53fb-119">330 Ω (inne zakończenie) do ziemi</span><span class="sxs-lookup"><span data-stu-id="f53fb-119">330 Ω resistor (other end) to ground</span></span>

[!INCLUDE [tutorial-rpi-gpio](../includes/tutorial-rpi-gpio.md)]

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a><span data-ttu-id="f53fb-120">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f53fb-120">Create the app</span></span>

<span data-ttu-id="f53fb-121">Wykonaj następujące kroki w preferowanym środowisku programistycznym:</span><span class="sxs-lookup"><span data-stu-id="f53fb-121">Complete the following steps in your preferred development environment:</span></span>

1. <span data-ttu-id="f53fb-122">Utwórz nową aplikację konsolową platformy .NET przy użyciu [interfejsu wiersza polecenia platformy .NET](../../core/tools/dotnet-new.md) lub [programu Visual Studio](../../core/tutorials/with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f53fb-122">Create a new .NET Console App using either the [.NET CLI](../../core/tools/dotnet-new.md) or [Visual Studio](../../core/tutorials/with-visual-studio.md).</span></span> <span data-ttu-id="f53fb-123">Nadaj mu nazwę *BlinkTutorial*.</span><span class="sxs-lookup"><span data-stu-id="f53fb-123">Name it *BlinkTutorial*.</span></span>

    ```dotnetcli
    dotnet new console -o BlinkTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. <span data-ttu-id="f53fb-124">Zastąp zawartość pliku *Program.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="f53fb-124">Replace the contents of *Program.cs* with the following code:</span></span>

    :::code language="csharp" source="~/iot-samples/tutorials/BlinkTutorial/Program.cs" :::

    <span data-ttu-id="f53fb-125">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="f53fb-125">In the preceding code:</span></span>

    - <span data-ttu-id="f53fb-126">[Deklaracja using](../../csharp/whats-new/csharp-8.md#using-declarations) tworzy wystąpienie `GpioController` .</span><span class="sxs-lookup"><span data-stu-id="f53fb-126">A [using declaration](../../csharp/whats-new/csharp-8.md#using-declarations) creates an instance of `GpioController`.</span></span> <span data-ttu-id="f53fb-127">`using`Deklaracja gwarantuje, że obiekt jest usuwany, a zasoby sprzętowe są prawidłowo wydane.</span><span class="sxs-lookup"><span data-stu-id="f53fb-127">The `using` declaration ensures the object is disposed and hardware resources are released properly.</span></span>
    - <span data-ttu-id="f53fb-128">Kod pin GPIO 18 jest otwarty dla danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="f53fb-128">GPIO pin 18 is opened for output</span></span>
    - <span data-ttu-id="f53fb-129">`while`Pętla jest uruchamiana w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="f53fb-129">A `while` loop runs indefinitely.</span></span> <span data-ttu-id="f53fb-130">Każda iteracja:</span><span class="sxs-lookup"><span data-stu-id="f53fb-130">Each iteration:</span></span>
        1. <span data-ttu-id="f53fb-131">Zapisuje wartość do numeru pin GPIO 18.</span><span class="sxs-lookup"><span data-stu-id="f53fb-131">Writes a value to GPIO pin 18.</span></span> <span data-ttu-id="f53fb-132">Jeśli `ledOn` ma wartość true, zapisuje `PinValue.High` (włączone).</span><span class="sxs-lookup"><span data-stu-id="f53fb-132">If `ledOn` is true, it writes `PinValue.High` (on).</span></span> <span data-ttu-id="f53fb-133">W przeciwnym razie zapisuje `PinValue.Low` .</span><span class="sxs-lookup"><span data-stu-id="f53fb-133">Otherwise, it writes `PinValue.Low`.</span></span>
        1. <span data-ttu-id="f53fb-134">Uśpienie 1000 ms.</span><span class="sxs-lookup"><span data-stu-id="f53fb-134">Sleeps 1000 ms.</span></span>
        1. <span data-ttu-id="f53fb-135">Włącza lub wyłącza wartość `ledOn` .</span><span class="sxs-lookup"><span data-stu-id="f53fb-135">Toggles the value of `ledOn`.</span></span>

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. <span data-ttu-id="f53fb-136">Uruchom aplikację na Raspberry Pi, przełączając się do katalogu wdrożenia i uruchamiając plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="f53fb-136">Run the app on the Raspberry Pi by switching to the deployment directory and running the executable.</span></span>

    ```bash
    ./BlinkTutorial
    ```

    <span data-ttu-id="f53fb-137">Dioda LED miga i w każdej sekundzie.</span><span class="sxs-lookup"><span data-stu-id="f53fb-137">The LED blinks off and on every second.</span></span>

1. <span data-ttu-id="f53fb-138">Przerwij program, naciskając <kbd>klawisze CTRL + C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="f53fb-138">Terminate the program by pressing <kbd>Ctrl+C</kbd>.</span></span>

<span data-ttu-id="f53fb-139">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f53fb-139">Congratulations!</span></span> <span data-ttu-id="f53fb-140">Użyto interfejsu GPIO do migania diody LED.</span><span class="sxs-lookup"><span data-stu-id="f53fb-140">You've used GPIO to blink an LED.</span></span>

## <a name="get-the-source-code"></a><span data-ttu-id="f53fb-141">Uzyskiwanie kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="f53fb-141">Get the source code</span></span>

<span data-ttu-id="f53fb-142">Źródło dla tego samouczka jest [dostępne w witrynie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/BlinkTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="f53fb-142">The source for this tutorial is [available on GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/BlinkTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f53fb-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f53fb-143">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f53fb-144">Dowiedz się, jak odczytać warunki środowiska z czujnika</span><span class="sxs-lookup"><span data-stu-id="f53fb-144">Learn how to read environmental conditions from a sensor</span></span>](../tutorials/temp-sensor.md)
