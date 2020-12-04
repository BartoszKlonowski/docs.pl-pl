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
# <a name="develop-apps-for-iot-devices-with-the-net-iot-libraries"></a>Tworzenie aplikacji dla urządzeń IoT przy użyciu bibliotek .NET IoT

Platforma .NET działa na różnych platformach i architekturach. Obsługiwane są popularne tablice Internetu rzeczy (IoT), takie jak Raspberry Pi i Hummingboard. Aplikacje IoT zwykle współpracują z wyspecjalizowanym sprzętem, takim jak czujniki, Przetworniki analogowo-cyfrowe i urządzenia LCD. Biblioteki IoT platformy .NET umożliwiają korzystanie z tych scenariuszy.

## <a name="video-overview"></a>Omówienie wideo

<!--markdownlint-disable MD034 -->
> [!VIDEO https://channel9.msdn.com/Series/IoT-101/Intro-to-IOT-with-NET-Core-1-of-9/player]

## <a name="libraries"></a>Biblioteki

Biblioteki IoT platformy .NET składają się z dwóch pakietów NuGet:

- [System. Device. GPIO](https://www.nuget.org/packages/System.Device.Gpio/)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [IoT. Device. bindings](https://www.nuget.org/packages/Iot.Device.Bindings/)<span class="docon docon-navigate-external x-hidden-focus"></span>

### <a name="systemdevicegpio"></a>System. Device. GPIO

`System.Device.Gpio` Program obsługuje różne protokoły umożliwiające współpracę z numerami sprzętu niskiego poziomu w celu sterowania urządzeniami. Są one następujące:

- We/wy ogólnego przeznaczenia (GPIO)
- Obwód Inter-Integrated (I2C)
- Interfejs urządzeń peryferyjnych (SPI)
- Modulacja szerokości impulsu (PWM)
- Port szeregowy

### <a name="iotdevicebindings"></a>IoT. Device. bindings

`Iot.Device.Bindings`Pakiet:

* Zawiera [powiązania urządzeń](https://github.com/dotnet/iot/blob/master/src/devices/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> w celu usprawnienia tworzenia aplikacji przez Zawijanie systemu. Device. GPIO.
* Jest obsługiwana przez społeczność i ciągle dodawane są dodatkowe powiązania.

Często używane powiązania urządzeń obejmują:

- [CharacterLcd — wyświetlacz z wyświetlaczem LCD](https://github.com/dotnet/iot/tree/master/src/devices/CharacterLcd)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [SN74HC595-8-bitowy rejestr Shift](https://github.com/dotnet/iot/tree/master/src/devices/Sn74hc595)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [BrickPi3](https://github.com/dotnet/iot/tree/master/src/devices/BrickPi3)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [Sterownik macierzy LED Max7219](https://github.com/dotnet/iot/tree/master/src/devices/Max7219)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [RGBLedMatrix — macierz LED RGB](https://github.com/dotnet/iot/tree/master/src/devices/RGBLedMatrix)<span class="docon docon-navigate-external x-hidden-focus"></span>

## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne

`System.Device.Gpio` jest obsługiwany w większości wersji systemu Linux, które obsługują ARM/ARM64 i Windows 10 IoT Core.

> [!TIP]
> Zaleca się używanie systemu operacyjnego Raspberry Pi, [Raspberry Pi](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> (dawniej raspbian).  

## <a name="supported-hardware-platforms"></a>Obsługiwane platformy sprzętowe

`System.Device.Gpio` jest zgodny z większością platform pojedynczej tablicy. Zalecane platformy to Raspberry Pi (2 i nowsze) i Hummingboard. Inne platformy znane do zgodności to BeagleBoard i ODROID.

Platformy komputerowe są obsługiwane za pośrednictwem mostka USB do funkcji WWH/I2C.

> [!IMPORTANT]
> Platforma .NET nie jest obsługiwana na urządzeniach z architekturą ARMv6, w tym Raspberry Pi i Raspberry Pi przed Raspberry Pi 2.

## <a name="resources"></a>Zasoby

- [Biblioteki IoT platformy .NET w witrynie GitHub](https://github.com/dotnet/iot)<span class="docon docon-navigate-external x-hidden-focus"></span>
