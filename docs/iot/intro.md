---
title: Tworzenie aplikacji dla urządzeń IoT przy użyciu bibliotek .NET IoT
description: Dowiedz się, w jaki sposób można używać platformy .NET do kompilowania aplikacji dla urządzeń i scenariuszy IoT.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: overview
ms.prod: dotnet
ms.openlocfilehash: c3d05ec5b05780f91404c3c27e91bcd602b0faeb
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "96589983"
---
# <a name="develop-apps-for-iot-devices-with-the-net-iot-libraries"></a><span data-ttu-id="fb23c-103">Tworzenie aplikacji dla urządzeń IoT przy użyciu bibliotek .NET IoT</span><span class="sxs-lookup"><span data-stu-id="fb23c-103">Develop apps for IoT devices with the .NET IoT Libraries</span></span>

<span data-ttu-id="fb23c-104">Platforma .NET działa na różnych platformach i architekturach.</span><span class="sxs-lookup"><span data-stu-id="fb23c-104">.NET runs on a variety of platforms and architectures.</span></span> <span data-ttu-id="fb23c-105">Obsługiwane są popularne tablice Internetu rzeczy (IoT), takie jak Raspberry Pi i Hummingboard.</span><span class="sxs-lookup"><span data-stu-id="fb23c-105">Common Internet of things (IoT) boards, such as Raspberry Pi and Hummingboard, are supported.</span></span> <span data-ttu-id="fb23c-106">Aplikacje IoT zwykle współpracują z wyspecjalizowanym sprzętem, takim jak czujniki, Przetworniki analogowo-cyfrowe i urządzenia LCD.</span><span class="sxs-lookup"><span data-stu-id="fb23c-106">IoT apps typically interact with specialized hardware, such as sensors, analog-to-digital converters, and LCD devices.</span></span> <span data-ttu-id="fb23c-107">Biblioteki IoT platformy .NET umożliwiają korzystanie z tych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="fb23c-107">The .NET IoT Libraries enable these scenarios.</span></span>

## <a name="video-overview"></a><span data-ttu-id="fb23c-108">Omówienie wideo</span><span class="sxs-lookup"><span data-stu-id="fb23c-108">Video overview</span></span>

<!--markdownlint-disable MD034 -->
> [!VIDEO https://channel9.msdn.com/Series/IoT-101/Intro-to-IOT-with-NET-Core-1-of-9/player]

## <a name="libraries"></a><span data-ttu-id="fb23c-109">Biblioteki</span><span class="sxs-lookup"><span data-stu-id="fb23c-109">Libraries</span></span>

<span data-ttu-id="fb23c-110">Biblioteki IoT platformy .NET składają się z dwóch pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="fb23c-110">The .NET IoT Libraries are composed of two NuGet packages:</span></span>

- <span data-ttu-id="fb23c-111">[System. Device. GPIO](https://www.nuget.org/packages/System.Device.Gpio/)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-111">[System.Device.Gpio](https://www.nuget.org/packages/System.Device.Gpio/) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
- <span data-ttu-id="fb23c-112">[IoT. Device. bindings](https://www.nuget.org/packages/Iot.Device.Bindings/)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-112">[Iot.Device.Bindings](https://www.nuget.org/packages/Iot.Device.Bindings/) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>

### <a name="systemdevicegpio"></a><span data-ttu-id="fb23c-113">System. Device. GPIO</span><span class="sxs-lookup"><span data-stu-id="fb23c-113">System.Device.Gpio</span></span>

<span data-ttu-id="fb23c-114">`System.Device.Gpio` Program obsługuje różne protokoły umożliwiające współpracę z numerami sprzętu niskiego poziomu w celu sterowania urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="fb23c-114">`System.Device.Gpio` supports a variety of protocols for interacting with low-level hardware pins to control devices.</span></span> <span data-ttu-id="fb23c-115">Są one następujące:</span><span class="sxs-lookup"><span data-stu-id="fb23c-115">These include:</span></span>

- <span data-ttu-id="fb23c-116">We/wy ogólnego przeznaczenia (GPIO)</span><span class="sxs-lookup"><span data-stu-id="fb23c-116">General-purpose I/O (GPIO)</span></span>
- <span data-ttu-id="fb23c-117">Obwód Inter-Integrated (I2C)</span><span class="sxs-lookup"><span data-stu-id="fb23c-117">Inter-Integrated Circuit (I2C)</span></span>
- <span data-ttu-id="fb23c-118">Interfejs urządzeń peryferyjnych (SPI)</span><span class="sxs-lookup"><span data-stu-id="fb23c-118">Serial Peripheral Interface (SPI)</span></span>
- <span data-ttu-id="fb23c-119">Modulacja szerokości impulsu (PWM)</span><span class="sxs-lookup"><span data-stu-id="fb23c-119">Pulse Width Modulation (PWM)</span></span>
- <span data-ttu-id="fb23c-120">Port szeregowy</span><span class="sxs-lookup"><span data-stu-id="fb23c-120">Serial port</span></span>

### <a name="iotdevicebindings"></a><span data-ttu-id="fb23c-121">IoT. Device. bindings</span><span class="sxs-lookup"><span data-stu-id="fb23c-121">Iot.Device.Bindings</span></span>

<span data-ttu-id="fb23c-122">`Iot.Device.Bindings`Pakiet:</span><span class="sxs-lookup"><span data-stu-id="fb23c-122">The `Iot.Device.Bindings` package:</span></span>

* <span data-ttu-id="fb23c-123">Zawiera [powiązania urządzeń](https://github.com/dotnet/iot/blob/master/src/devices/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> w celu usprawnienia tworzenia aplikacji przez Zawijanie systemu. Device. GPIO.</span><span class="sxs-lookup"><span data-stu-id="fb23c-123">Contains [device bindings](https://github.com/dotnet/iot/blob/master/src/devices/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> to streamline app development by wrapping System.Device.Gpio.</span></span>
* <span data-ttu-id="fb23c-124">Jest obsługiwana przez społeczność i ciągle dodawane są dodatkowe powiązania.</span><span class="sxs-lookup"><span data-stu-id="fb23c-124">Is community-supported, and additional bindings are added continually.</span></span>

<span data-ttu-id="fb23c-125">Często używane powiązania urządzeń obejmują:</span><span class="sxs-lookup"><span data-stu-id="fb23c-125">Commonly used device bindings include:</span></span>

- <span data-ttu-id="fb23c-126">[CharacterLcd — wyświetlacz z wyświetlaczem LCD](https://github.com/dotnet/iot/tree/master/src/devices/CharacterLcd)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-126">[CharacterLcd - LCD character display](https://github.com/dotnet/iot/tree/master/src/devices/CharacterLcd) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
- <span data-ttu-id="fb23c-127">[SN74HC595-8-bitowy rejestr Shift](https://github.com/dotnet/iot/tree/master/src/devices/Sn74hc595)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-127">[SN74HC595 - 8-bit shift register](https://github.com/dotnet/iot/tree/master/src/devices/Sn74hc595) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
- <span data-ttu-id="fb23c-128">[BrickPi3](https://github.com/dotnet/iot/tree/master/src/devices/BrickPi3)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-128">[BrickPi3](https://github.com/dotnet/iot/tree/master/src/devices/BrickPi3) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
- <span data-ttu-id="fb23c-129">[Sterownik macierzy LED Max7219](https://github.com/dotnet/iot/tree/master/src/devices/Max7219)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-129">[Max7219 - LED Matrix driver](https://github.com/dotnet/iot/tree/master/src/devices/Max7219) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
- <span data-ttu-id="fb23c-130">[RGBLedMatrix — macierz LED RGB](https://github.com/dotnet/iot/tree/master/src/devices/RGBLedMatrix)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-130">[RGBLedMatrix - RGB LED Matrix](https://github.com/dotnet/iot/tree/master/src/devices/RGBLedMatrix) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="fb23c-131">Obsługiwane systemy operacyjne</span><span class="sxs-lookup"><span data-stu-id="fb23c-131">Supported operating systems</span></span>

<span data-ttu-id="fb23c-132">`System.Device.Gpio` jest obsługiwany w większości wersji systemu Linux, które obsługują ARM/ARM64 i Windows 10 IoT Core.</span><span class="sxs-lookup"><span data-stu-id="fb23c-132">`System.Device.Gpio` is supported on most versions of Linux that support ARM/ARM64 and Windows 10 IoT Core.</span></span>

> [!TIP]
> <span data-ttu-id="fb23c-133">Zaleca się używanie systemu operacyjnego Raspberry Pi, [Raspberry Pi](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> (dawniej raspbian).  </span><span class="sxs-lookup"><span data-stu-id="fb23c-133">For Raspberry Pi, [Raspberry Pi OS](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)  <span class="docon docon-navigate-external x-hidden-focus"></span> (formerly Raspbian) is recommended.</span></span>

## <a name="supported-hardware-platforms"></a><span data-ttu-id="fb23c-134">Obsługiwane platformy sprzętowe</span><span class="sxs-lookup"><span data-stu-id="fb23c-134">Supported hardware platforms</span></span>

<span data-ttu-id="fb23c-135">`System.Device.Gpio` jest zgodny z większością platform pojedynczej tablicy.</span><span class="sxs-lookup"><span data-stu-id="fb23c-135">`System.Device.Gpio` is compatible with most single-board platforms.</span></span> <span data-ttu-id="fb23c-136">Zalecane platformy to Raspberry Pi (2 i nowsze) i Hummingboard.</span><span class="sxs-lookup"><span data-stu-id="fb23c-136">Recommended platforms are Raspberry Pi (2 and greater) and Hummingboard.</span></span> <span data-ttu-id="fb23c-137">Inne platformy znane do zgodności to BeagleBoard i ODROID.</span><span class="sxs-lookup"><span data-stu-id="fb23c-137">Other platforms known to be compatible are BeagleBoard and ODROID.</span></span>

<span data-ttu-id="fb23c-138">Platformy komputerowe są obsługiwane za pośrednictwem mostka USB do funkcji WWH/I2C.</span><span class="sxs-lookup"><span data-stu-id="fb23c-138">PC platforms are supported via the use of a USB to SPI/I2C bridge.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb23c-139">Platforma .NET nie jest obsługiwana na urządzeniach z architekturą ARMv6, w tym Raspberry Pi i Raspberry Pi przed Raspberry Pi 2.</span><span class="sxs-lookup"><span data-stu-id="fb23c-139">.NET is not supported on ARMv6 architecture devices, including Raspberry Pi Zero and Raspberry Pi devices prior to Raspberry Pi 2.</span></span>

## <a name="resources"></a><span data-ttu-id="fb23c-140">Zasoby</span><span class="sxs-lookup"><span data-stu-id="fb23c-140">Resources</span></span>

- <span data-ttu-id="fb23c-141">[Biblioteki IoT platformy .NET w witrynie GitHub](https://github.com/dotnet/iot)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="fb23c-141">[.NET IoT Libraries on Github](https://github.com/dotnet/iot) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>
