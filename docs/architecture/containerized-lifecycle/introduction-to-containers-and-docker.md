---
title: Wprowadzenie do kontenerów i platformy Docker
description: Zapoznaj się z ogólnymi omówieniem głównych korzyści płynących z używania platformy Docker.
ms.date: 04/15/2020
ms.openlocfilehash: 79b4752ef4d2f0aa6199414aea5cf4ef357c86d3
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915955"
---
# <a name="introduction-to-containers-and-docker"></a>Wprowadzenie do kontenerów i platformy Docker

*Kontenerach to podejście do tworzenia oprogramowania, w którym aplikacja lub usługa, jej zależności i jej konfiguracja (Abstrakcja jako pliki manifestu wdrożenia) są pakowane razem jako obraz kontenera. Następnie można przetestować aplikację kontenerową jako jednostkę i wdrożyć ją jako wystąpienie obrazu kontenera w systemie operacyjnym hosta (OS).*

Podobnie jak kontenery wysyłkowe umożliwiają transport towarów przez wysyłkę, szkolenie lub ciężarówkę niezależnie od ładunku, kontenery oprogramowania działają jako standardowa jednostka wdrażania oprogramowania, która może zawierać inny kod i zależności. Konteneryzowania oprogramowanie w ten sposób umożliwia deweloperom i specjalistom IT wdrażanie ich w różnych środowiskach z niewielkim modyfikacją lub bez niej.

Kontenery izolują również aplikacje od siebie w udostępnionym systemie operacyjnym. Aplikacje kontenerowe działają na hoście kontenera, który z kolei jest uruchamiany w systemie operacyjnym (Linux lub Windows). W związku z tym kontenery mają znacznie mniejsze rozmiary niż obrazy maszyn wirtualnych.

Każdy kontener może uruchamiać całą aplikację sieci Web lub usługę, jak pokazano na rysunku 1-1. W tym przykładzie Host platformy Docker jest hostem kontenera, a APP1, APP2, Svc1 i Svc2 są kontenerami aplikacjami lub usługami.

![Diagram przedstawiający cztery kontenery działające na maszynie wirtualnej lub serwerze.](./media/introduction-to-containers-and-docker/multiple-containers-single-host.png)

**Rysunek 1-1**. Wiele kontenerów uruchomionych na hoście kontenera

Inną korzyścią, jaką można uzyskać od kontenerach, jest skalowalność. Możesz szybko skalować w poziomie, tworząc nowe kontenery dla krótkoterminowych zadań. Z punktu widzenia aplikacji Tworzenie wystąpienia obrazu (Tworzenie kontenera) jest podobne do tworzenia wystąpienia procesu, takiego jak usługa lub aplikacja sieci Web. Niemniej jednak w przypadku uruchamiania wielu wystąpień tego samego obrazu na wielu serwerach hosta, zazwyczaj każdy kontener (wystąpienie obrazu) można uruchomić na innym serwerze hosta lub maszynie wirtualnej w różnych domenach błędów.

W krótkim czasie kontenery oferują zalety izolacji, przenośności, elastyczności, skalowalności i kontroli całego przepływu pracy cyklu życia aplikacji. Najważniejsze korzyści to izolacja środowiska zapewniana między tworzeniem i Ops.

>[!div class="step-by-step"]
>[Poprzedni](index.md) 
> [Dalej](what-is-docker.md)
