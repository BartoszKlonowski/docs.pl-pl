---
title: Środowisko deweloperskie dla aplikacji platformy Docker
description: Poznaj najważniejsze opcje narzędzia deweloperskiego, które obsługują cykl życia platformy Docker.
ms.date: 02/15/2019
ms.openlocfilehash: 0f71ffa5e6870f45908e4def6577120a17ec744c
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295302"
---
# <a name="development-environment-for-docker-apps"></a><span data-ttu-id="1e1b7-103">Środowisko deweloperskie dla aplikacji platformy Docker</span><span class="sxs-lookup"><span data-stu-id="1e1b7-103">Development environment for Docker apps</span></span>

## <a name="development-tools-choices-ide-or-editor"></a><span data-ttu-id="1e1b7-104">Opcje narzędzi programistycznych: IDE lub Edytor</span><span class="sxs-lookup"><span data-stu-id="1e1b7-104">Development tools choices: IDE or editor</span></span>

<span data-ttu-id="1e1b7-105">Niezależnie od tego, czy wolisz pełną i wydajną platformę IDE, czy też Edytor uproszczony i Agile, firma Microsoft połączyła się z tworzeniem aplikacji platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-105">No matter if you prefer a full and powerful IDE or a lightweight and agile editor, Microsoft has you covered when it comes to developing Docker applications.</span></span>

### <a name="visual-studio-code-and-docker-cli-cross-platform-tools-for-mac-linux-and-windows"></a><span data-ttu-id="1e1b7-106">Visual Studio Code i interfejs wiersza polecenia platformy Docker (narzędzia dla wielu platform dla systemów Mac, Linux i Windows)</span><span class="sxs-lookup"><span data-stu-id="1e1b7-106">Visual Studio Code and Docker CLI (cross-platform tools for Mac, Linux, and Windows)</span></span>

<span data-ttu-id="1e1b7-107">Jeśli wolisz lekki Edytor Międzyplatformowy obsługujący dowolny język programowania, możesz użyć Visual Studio Code i interfejsu wiersza polecenia platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-107">If you prefer a lightweight, cross-platform editor supporting any development language, you can use Visual Studio Code and Docker CLI.</span></span> <span data-ttu-id="1e1b7-108">Te produkty zapewniają proste, a jeszcze niezawodne środowisko, które ma kluczowe znaczenie dla usprawnienia przepływu pracy dewelopera.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-108">These products provide a simple yet robust experience, which is critical for streamlining the developer workflow.</span></span> <span data-ttu-id="1e1b7-109">Instalując "Docker for Mac" lub "Docker for Windows" (środowisko programistyczne), deweloperzy platformy Docker mogą używać jednego interfejsu wiersza polecenia platformy Docker do kompilowania aplikacji dla systemu Windows lub Linux (środowisko uruchomieniowe).</span><span class="sxs-lookup"><span data-stu-id="1e1b7-109">By installing "Docker for Mac" or "Docker for Windows" (development environment), Docker developers can use a single Docker CLI to build apps for both Windows or Linux (runtime environment).</span></span> <span data-ttu-id="1e1b7-110">Dodatkowo Visual Studio Code obsługuje rozszerzenia dla platformy Docker z technologią IntelliSense dla wieloetapowe dockerfile oraz zadania skrótów do uruchamiania poleceń platformy Docker z edytora.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-110">Plus, Visual Studio Code supports extensions for Docker with IntelliSense for Dockerfiles and shortcut-tasks to run Docker commands from the editor.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1e1b7-111">Aby pobrać Visual Studio Code, przejdź do <https://code.visualstudio.com/download>.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-111">To download Visual Studio Code, go to <https://code.visualstudio.com/download>.</span></span>
>
> <span data-ttu-id="1e1b7-112">Aby pobrać platformę Docker dla komputerów Mac i Windows <https://www.docker.com/products/docker>, przejdź do.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-112">To download Docker for Mac and Windows, go to <https://www.docker.com/products/docker>.</span></span>

### <a name="visual-studio-with-docker-tools-windows-development-machine"></a><span data-ttu-id="1e1b7-113">Visual Studio z narzędziami platformy Docker (komputer deweloperski systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="1e1b7-113">Visual Studio with Docker Tools (Windows development machine)</span></span>

<span data-ttu-id="1e1b7-114">Zalecamy używanie programu Visual Studio 2017 (lub nowszego) z włączonymi wbudowanymi narzędziami platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-114">We recommend you use Visual Studio 2017 (or later) with the built-in Docker Tools enabled.</span></span> <span data-ttu-id="1e1b7-115">Za pomocą programu Visual Studio można opracowywać, uruchamiać i weryfikować aplikacje bezpośrednio w wybranym środowisku platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-115">With Visual Studio, you can develop, run, and validate your applications directly in the chosen Docker environment.</span></span> <span data-ttu-id="1e1b7-116">Naciśnij klawisz F5, aby debugować aplikację (pojedynczy kontener lub wiele kontenerów) bezpośrednio na hoście platformy Docker lub naciśnij klawisze CTRL + F5, aby edytować i odświeżyć aplikację bez konieczności ponownego kompilowania kontenera.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-116">Press F5 to debug your application (single container or multiple containers) directly in a Docker host, or press Ctrl+F5 to edit and refresh your app without having to rebuild the container.</span></span> <span data-ttu-id="1e1b7-117">Jest to najprostszy i najbardziej zaawansowany wybór dla deweloperów systemu Windows do tworzenia kontenerów platformy Docker dla systemu Linux lub Windows.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-117">It's the simplest and most powerful choice for Windows developers to create Docker containers for Linux or Windows.</span></span>

### <a name="visual-studio-for-mac-mac-development-machine"></a><span data-ttu-id="1e1b7-118">Visual Studio dla komputerów Mac (komputer deweloperski dla komputerów Mac)</span><span class="sxs-lookup"><span data-stu-id="1e1b7-118">Visual Studio for Mac (Mac development machine)</span></span>

<span data-ttu-id="1e1b7-119">Podczas tworzenia aplikacji opartych na platformie Docker można użyć [Visual Studio dla komputerów Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) .</span><span class="sxs-lookup"><span data-stu-id="1e1b7-119">You can use [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) when developing Docker-based applications.</span></span> <span data-ttu-id="1e1b7-120">Visual Studio dla komputerów Mac oferuje bogatsze środowisko IDE w porównaniu do Visual Studio Code dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-120">Visual Studio for Mac offers a richer IDE when compared to Visual Studio Code for Mac.</span></span>

## <a name="language-and-framework-choices"></a><span data-ttu-id="1e1b7-121">Wybór języka i struktury</span><span class="sxs-lookup"><span data-stu-id="1e1b7-121">Language and framework choices</span></span>

<span data-ttu-id="1e1b7-122">Aplikacje platformy Docker można opracowywać przy użyciu narzędzi firmy Microsoft z większością nowoczesnych języków.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-122">You can develop Docker applications using Microsoft tools with most modern languages.</span></span> <span data-ttu-id="1e1b7-123">Poniżej znajduje się lista wstępna, ale nie jest ograniczona do niej:</span><span class="sxs-lookup"><span data-stu-id="1e1b7-123">The following is an initial list, but you're not limited to it:</span></span>

- <span data-ttu-id="1e1b7-124">.NET Core i ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1e1b7-124">.NET Core and ASP.NET Core</span></span>
- <span data-ttu-id="1e1b7-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="1e1b7-125">Node.js</span></span>
- <span data-ttu-id="1e1b7-126">Z rzeczywistym użyciem</span><span class="sxs-lookup"><span data-stu-id="1e1b7-126">Go</span></span>
- <span data-ttu-id="1e1b7-127">Java</span><span class="sxs-lookup"><span data-stu-id="1e1b7-127">Java</span></span>
- <span data-ttu-id="1e1b7-128">Ruby</span><span class="sxs-lookup"><span data-stu-id="1e1b7-128">Ruby</span></span>
- <span data-ttu-id="1e1b7-129">Python</span><span class="sxs-lookup"><span data-stu-id="1e1b7-129">Python</span></span>

<span data-ttu-id="1e1b7-130">W zasadzie można użyć dowolnego nowoczesnego języka obsługiwanego przez platformę Docker w systemie Linux lub Windows.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-130">Basically, you can use any modern language supported by Docker in Linux or Windows.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="1e1b7-131">[Poprzedni](deploy-azure-kubernetes-service.md)Następny
>[](docker-apps-inner-loop-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="1e1b7-131">[Previous](deploy-azure-kubernetes-service.md)
[Next](docker-apps-inner-loop-workflow.md)</span></span>