---
title: Kontenery, obrazy i rejestry platformy Docker
description: Poznaj rolę klucza, którą rejestry odgrywają ogólnie w programie Docker w celu wdrożenia aplikacji.
ms.date: 08/06/2020
ms.openlocfilehash: 2ff6cf76b35777546b6e653d477a029296f8e496
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915245"
---
# <a name="docker-containers-images-and-registries"></a>Kontenery, obrazy i rejestry platformy Docker

W przypadku korzystania z platformy Docker można utworzyć aplikację lub usługę oraz spakować ją wraz z jej zależnościami na obraz kontenera. Obraz jest statyczną reprezentacją aplikacji lub usługi oraz jej konfiguracji i zależności.

Aby uruchomić aplikację lub usługę, zostanie utworzone wystąpienie obrazu aplikacji w celu utworzenia kontenera, który będzie działać na hoście platformy Docker. Kontenery są wstępnie testowane w środowisku deweloperskim lub komputerze.

Obrazy są przechowywane w rejestrze, który działa jako biblioteka obrazów. W przypadku wdrażania w programie Orchestrator w środowisku produkcyjnym potrzebny jest rejestr. Platforma Docker utrzymuje rejestr publiczny za pośrednictwem narzędzia [Docker Hub](https://hub.docker.com/). inni dostawcy dostarczają rejestry dla różnych kolekcji obrazów, w tym [Azure Container Registry](https://azure.microsoft.com/services/container-registry/). Alternatywnie przedsiębiorstwa mogą lokalnie korzystać z prywatnego rejestru dla własnych obrazów platformy Docker.

Rysunek 1-4 pokazuje, jak obrazy i rejestry w Docker odnoszą się do innych składników. Przedstawiono w nim także oferty wielu rejestrów od dostawców.

![Diagram przedstawiający podstawową taksonomię w platformie Docker.](./media/docker-containers-images-and-registries/taxonomy-docker-terms-concepts.png)

**Rysunek 1-4**. Taksonomia warunków i koncepcji platformy Docker

Rejestr jest taki jak Bookshelf, gdzie obrazy są przechowywane i dostępne do kompilowania w celu tworzenia kontenerów do uruchamiania usług lub aplikacji sieci Web. Istnieją prywatne rejestry platformy Docker lokalnie i w chmurze publicznej. Usługa Docker Hub jest rejestrem publicznym obsługiwanym przez platformę Docker oraz z zaufanym rejestrem platformy Docker rozwiązanie klasy korporacyjnej, platforma Azure oferuje Azure Container Registry. AWS, Google i inne również mają rejestry kontenerów.

Umieszczając obrazy w rejestrze, można przechowywać statyczne i niezmienne bity aplikacji, w tym wszystkie ich zależności, na poziomie platformy. Następnie można zainstalować i wdrożyć obrazy w wielu środowiskach, a tym samym zapewnić spójną jednostkę wdrożenia.

Prywatne rejestry obrazów, hostowane lokalnie lub w chmurze, są zalecane w przypadku:

- Obrazy nie mogą być udostępniane publicznie z powodu poufności.

- Potrzebujesz minimalnych opóźnień sieci między obrazami i wybranym środowiskiem wdrażania. Na przykład jeśli środowisko produkcyjne jest platformą Azure, prawdopodobnie chcesz przechowywać obrazy w [Azure Container Registry](https://azure.microsoft.com/services/container-registry/) tak, aby opóźnienie sieci było minimalne. W podobny sposób, jeśli środowisko produkcyjne działa lokalnie, w tej samej sieci lokalnej może być dostępny lokalny rejestr platformy Docker.

>[!div class="step-by-step"]
>[Poprzedni](docker-terminology.md) 
> [Dalej](road-to-modern-applications-based-on-containers.md)
