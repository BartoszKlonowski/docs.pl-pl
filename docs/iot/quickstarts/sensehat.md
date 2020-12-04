---
title: Szybki Start — korzystanie z platformy .NET na potrzeby wykrywania Raspberry Pi
description: Rozpocznij pracę z bibliotekami .NET IoT w ciągu 5 minut, korzystając z funkcji wykrywania, tablicy dodatków dla Raspberry Pi.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: quickstart
ms.prod: dotnet
ms.openlocfilehash: 09e0c46a08e08a2021a9dffe214d3d62d6fb8ec5
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "96589980"
---
# <a name="quickstart---use-net-to-drive-a-raspberry-pi-sense-hat"></a><span data-ttu-id="85e41-103">Szybki Start — korzystanie z platformy .NET na potrzeby wykrywania Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="85e41-103">Quickstart - Use .NET to drive a Raspberry Pi Sense HAT</span></span>

<span data-ttu-id="85e41-104">[Hat](https://www.raspberrypi.org/products/sense-hat/) Raspberry Pi jest tablicą <span class="docon docon-navigate-external x-hidden-focus"></span> dodatków dla Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="85e41-104">The Raspberry Pi [Sense HAT](https://www.raspberrypi.org/products/sense-hat/) <span class="docon docon-navigate-external x-hidden-focus"></span> is an add-on board for Raspberry Pi.</span></span> <span data-ttu-id="85e41-105">Program zmysł HAT jest wyposażony w macierz LED 8 × 8, a następnie joystick z pięcioma przyciskami i zawiera następujące czujniki:</span><span class="sxs-lookup"><span data-stu-id="85e41-105">The Sense HAT is equipped with an 8×8 RGB LED matrix, a five-button joystick, and includes the following sensors:</span></span>

- <span data-ttu-id="85e41-106">Żyroskop</span><span class="sxs-lookup"><span data-stu-id="85e41-106">Gyroscope</span></span>
- <span data-ttu-id="85e41-107">Akcelerometr</span><span class="sxs-lookup"><span data-stu-id="85e41-107">Accelerometer</span></span>
- <span data-ttu-id="85e41-108">Magnetometr</span><span class="sxs-lookup"><span data-stu-id="85e41-108">Magnetometer</span></span>
- <span data-ttu-id="85e41-109">Temperatura</span><span class="sxs-lookup"><span data-stu-id="85e41-109">Temperature</span></span>
- <span data-ttu-id="85e41-110">Ciśnienie atmosferyczne</span><span class="sxs-lookup"><span data-stu-id="85e41-110">Barometric pressure</span></span>
- <span data-ttu-id="85e41-111">Wilgotność</span><span class="sxs-lookup"><span data-stu-id="85e41-111">Humidity</span></span>

<span data-ttu-id="85e41-112">Ten przewodnik Szybki Start używa platformy .NET do pobierania wartości czujników z czujnika wykrywania, reagowania na dane wejściowe joysticka i na dysku macierzy LED.</span><span class="sxs-lookup"><span data-stu-id="85e41-112">This quickstart uses .NET to retrieve sensor values from the Sense HAT, respond to joystick input, and drive the LED matrix.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85e41-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="85e41-113">Prerequisites</span></span>

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- <span data-ttu-id="85e41-114">Wykrywanie sensu</span><span class="sxs-lookup"><span data-stu-id="85e41-114">Sense HAT</span></span>

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="run-the-quickstart"></a><span data-ttu-id="85e41-115">Uruchamianie przewodnika Szybki Start</span><span class="sxs-lookup"><span data-stu-id="85e41-115">Run the quickstart</span></span>

<span data-ttu-id="85e41-116">Dołącz HAT wykrywania do Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="85e41-116">Attach the Sense HAT to your Raspberry Pi.</span></span> <span data-ttu-id="85e41-117">Z poziomu monitu bash na Raspberry Pi (lokalne lub zdalne) Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="85e41-117">From a Bash prompt on the Raspberry Pi (local or remote), run the following command:</span></span>

```bash
. <(wget -q -O - https://aka.ms/dotnet-iot-sensehat-quickstart)
```

<span data-ttu-id="85e41-118">Polecenie pobiera i uruchamia skrypt.</span><span class="sxs-lookup"><span data-stu-id="85e41-118">The command downloads and runs a script.</span></span> <span data-ttu-id="85e41-119">Skrypt:</span><span class="sxs-lookup"><span data-stu-id="85e41-119">The script:</span></span>

- <span data-ttu-id="85e41-120">Instaluje zestaw .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="85e41-120">Installs the .NET SDK.</span></span>
- <span data-ttu-id="85e41-121">Klonuje repozytorium GitHub, które zawiera projekt wykrywania HAT z przewodnikiem Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="85e41-121">Clones a GitHub repository that includes the Sense HAT quickstart project.</span></span>
- <span data-ttu-id="85e41-122">Kompiluje projekt.</span><span class="sxs-lookup"><span data-stu-id="85e41-122">Builds the project.</span></span>
- <span data-ttu-id="85e41-123">Uruchamia projekt.</span><span class="sxs-lookup"><span data-stu-id="85e41-123">Runs the project.</span></span>

<span data-ttu-id="85e41-124">Zwróć uwagę na dane wyjściowe konsoli, ponieważ są wyświetlane dane czujnika.</span><span class="sxs-lookup"><span data-stu-id="85e41-124">Observe the console output as sensor data is displayed.</span></span> <span data-ttu-id="85e41-125">W macierzy LED jest wyświetlany żółty piksel w polu niebieski.</span><span class="sxs-lookup"><span data-stu-id="85e41-125">The LED matrix displays a yellow pixel on a field of blue.</span></span> <span data-ttu-id="85e41-126">Trzymanie joysticka w dowolnym kierunku przesuwa żółty piksel w tym kierunku.</span><span class="sxs-lookup"><span data-stu-id="85e41-126">Holding the joystick in any direction moves the yellow pixel in that direction.</span></span> <span data-ttu-id="85e41-127">Kliknięcie przycisku środkowy joystick powoduje zmianę tła z niebieski na czerwony.</span><span class="sxs-lookup"><span data-stu-id="85e41-127">Clicking the center joystick button causes the background to switch from blue to red.</span></span>

## <a name="get-the-source-code"></a><span data-ttu-id="85e41-128">Uzyskiwanie kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="85e41-128">Get the source code</span></span>

<span data-ttu-id="85e41-129">Źródło tego przewodnika Szybki Start jest [dostępne w serwisie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/quickstarts/SenseHat.Quickstart).</span><span class="sxs-lookup"><span data-stu-id="85e41-129">The source for this quickstart is [available on GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/quickstarts/SenseHat.Quickstart).</span></span> <span class="docon docon-navigate-external x-hidden-focus"></span>

## <a name="next-steps"></a><span data-ttu-id="85e41-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85e41-130">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="85e41-131">Dowiedz się, jak korzystać z Ogólnego przeznaczenia danych wejściowych/wyjściowych w celu migania DIODy</span><span class="sxs-lookup"><span data-stu-id="85e41-131">Learn to use General Purpose Input/Output to blink an LED</span></span>](../tutorials/blink-led.md)
