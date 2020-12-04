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
# <a name="quickstart---use-net-to-drive-a-raspberry-pi-sense-hat"></a>Szybki Start — korzystanie z platformy .NET na potrzeby wykrywania Raspberry Pi

[Hat](https://www.raspberrypi.org/products/sense-hat/) Raspberry Pi jest tablicą <span class="docon docon-navigate-external x-hidden-focus"></span> dodatków dla Raspberry Pi. Program zmysł HAT jest wyposażony w macierz LED 8 × 8, a następnie joystick z pięcioma przyciskami i zawiera następujące czujniki:

- Żyroskop
- Akcelerometr
- Magnetometr
- Temperatura
- Ciśnienie atmosferyczne
- Wilgotność

Ten przewodnik Szybki Start używa platformy .NET do pobierania wartości czujników z czujnika wykrywania, reagowania na dane wejściowe joysticka i na dysku macierzy LED.

## <a name="prerequisites"></a>Wymagania wstępne

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- Wykrywanie sensu

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="run-the-quickstart"></a>Uruchamianie przewodnika Szybki Start

Dołącz HAT wykrywania do Raspberry Pi. Z poziomu monitu bash na Raspberry Pi (lokalne lub zdalne) Uruchom następujące polecenie:

```bash
. <(wget -q -O - https://aka.ms/dotnet-iot-sensehat-quickstart)
```

Polecenie pobiera i uruchamia skrypt. Skrypt:

- Instaluje zestaw .NET SDK.
- Klonuje repozytorium GitHub, które zawiera projekt wykrywania HAT z przewodnikiem Szybki Start.
- Kompiluje projekt.
- Uruchamia projekt.

Zwróć uwagę na dane wyjściowe konsoli, ponieważ są wyświetlane dane czujnika. W macierzy LED jest wyświetlany żółty piksel w polu niebieski. Trzymanie joysticka w dowolnym kierunku przesuwa żółty piksel w tym kierunku. Kliknięcie przycisku środkowy joystick powoduje zmianę tła z niebieski na czerwony.

## <a name="get-the-source-code"></a>Uzyskiwanie kodu źródłowego

Źródło tego przewodnika Szybki Start jest [dostępne w serwisie GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/quickstarts/SenseHat.Quickstart). <span class="docon docon-navigate-external x-hidden-focus"></span>

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się, jak korzystać z Ogólnego przeznaczenia danych wejściowych/wyjściowych w celu migania DIODy](../tutorials/blink-led.md)
