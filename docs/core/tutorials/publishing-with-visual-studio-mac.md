---
title: Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac
description: Dowiedz się, jak za pomocą Visual Studio dla komputerów Mac utworzyć zestaw plików, które są konieczne do uruchomienia aplikacji platformy .NET.
ms.date: 11/30/2020
ms.openlocfilehash: 88f143011b19ca8eda6610803c894e619d06a635
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599192"
---
# <a name="tutorial-publish-a-net-console-application-using-visual-studio-for-mac"></a><span data-ttu-id="66c04-103">Samouczek: publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="66c04-103">Tutorial: Publish a .NET console application using Visual Studio for Mac</span></span>

<span data-ttu-id="66c04-104">W tym samouczku pokazano, jak opublikować aplikację konsolową, tak aby inni użytkownicy mogli ją uruchomić.</span><span class="sxs-lookup"><span data-stu-id="66c04-104">This tutorial shows how to publish a console app so that other users can run it.</span></span> <span data-ttu-id="66c04-105">Publikowanie tworzy zestaw plików, które są konieczne do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-105">Publishing creates the set of files that are needed to run your application.</span></span> <span data-ttu-id="66c04-106">Aby wdrożyć pliki, skopiuj je na maszynę docelową.</span><span class="sxs-lookup"><span data-stu-id="66c04-106">To deploy the files, copy them to the target machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66c04-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="66c04-107">Prerequisites</span></span>

- <span data-ttu-id="66c04-108">Ten samouczek współpracuje z aplikacją konsolową utworzoną w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="66c04-108">This tutorial works with the console app that you create in [Create a .NET console application using Visual Studio for Mac](with-visual-studio-mac.md).</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="66c04-109">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="66c04-109">Publish the app</span></span>

1. <span data-ttu-id="66c04-110">Rozpocznij Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="66c04-110">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="66c04-111">Otwórz projekt HelloWorld, który został utworzony w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="66c04-111">Open the HelloWorld project that you created in [Create a .NET console application using Visual Studio for Mac](with-visual-studio-mac.md).</span></span>

1. <span data-ttu-id="66c04-112">Upewnij się, że program Visual Studio kompiluje wydaną wersję aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-112">Make sure that Visual Studio is building the Release version of your application.</span></span> <span data-ttu-id="66c04-113">W razie potrzeby zmień ustawienie konfiguracji kompilacji na pasku narzędzi z **Debuguj** na **Release**.</span><span class="sxs-lookup"><span data-stu-id="66c04-113">If necessary, change the build configuration setting on the toolbar from **Debug** to **Release**.</span></span>

   :::image type="content" source="media/publishing-with-visual-studio-mac/toolbar-release.png" alt-text="Program Visual Studio Toolbar z wybraną kompilacją wydania":::

1. <span data-ttu-id="66c04-115">Z menu głównego wybierz polecenie **Kompiluj**  >  **Publikuj do folderu.**...</span><span class="sxs-lookup"><span data-stu-id="66c04-115">From the main menu, choose **Build** > **Publish to Folder...**.</span></span>

   :::image type="content" source="media/publishing-with-visual-studio-mac/publish-context-menu.png" alt-text="Menu kontekstowe publikacji programu Visual Studio":::

1. <span data-ttu-id="66c04-117">W oknie dialogowym **Publikowanie do folderu** wybierz pozycję **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="66c04-117">In the **Publish to Folder** dialog, select **Publish**.</span></span>

   :::image type="content" source="media/publishing-with-visual-studio-mac/publish-to-folder-dialog.png" alt-text="Okno dialogowe publikowania do folderu programu Visual Studio":::

   <span data-ttu-id="66c04-119">Zostanie otwarty folder publikowanie zawierający pliki, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="66c04-119">The publish folder opens, showing the files that were created.</span></span>

   :::image type="content" source="media/publishing-with-visual-studio-mac/publish-folder.png" alt-text="folder publikacji":::

1. <span data-ttu-id="66c04-121">Wybierz ikonę koła zębatego, a następnie wybierz pozycję **Kopiuj "Publikuj" jako nazwę ścieżki** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="66c04-121">Select the gear icon, and select **Copy "publish" as Pathname** from the context menu.</span></span>

   :::image type="content" source="media/publishing-with-visual-studio-mac/copy-path.png" alt-text="Kopiuj ścieżkę do folderu publikowania":::

## <a name="inspect-the-files"></a><span data-ttu-id="66c04-123">Inspekcja plików</span><span class="sxs-lookup"><span data-stu-id="66c04-123">Inspect the files</span></span>

<span data-ttu-id="66c04-124">Proces publikowania tworzy wdrożenie zależne od platformy, które jest typem wdrożenia, gdzie opublikowana aplikacja jest uruchamiana na komputerze, na którym zainstalowano środowisko uruchomieniowe platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="66c04-124">The publishing process creates a framework-dependent deployment, which is a type of deployment where the published application runs on a machine that has the .NET runtime installed.</span></span> <span data-ttu-id="66c04-125">Użytkownicy mogą uruchamiać opublikowaną aplikację, uruchamiając `dotnet HelloWorld.dll` polecenie z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="66c04-125">Users can run the published app by running the `dotnet HelloWorld.dll` command from a command prompt.</span></span>

<span data-ttu-id="66c04-126">Jak widać na poprzedniej ilustracji, opublikowane dane wyjściowe zawierają następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="66c04-126">As the preceding image shows, the published output includes the following files:</span></span>

* <span data-ttu-id="66c04-127">*HelloWorld.deps.jsna*</span><span class="sxs-lookup"><span data-stu-id="66c04-127">*HelloWorld.deps.json*</span></span>

  <span data-ttu-id="66c04-128">Jest to plik zależności środowiska uruchomieniowego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-128">This is the application's runtime dependencies file.</span></span> <span data-ttu-id="66c04-129">Definiuje składniki platformy .NET i biblioteki (w tym bibliotekę dołączaną dynamicznie, która zawiera aplikację) potrzebną do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-129">It defines the .NET components and the libraries (including the dynamic link library that contains your application) needed to run the app.</span></span> <span data-ttu-id="66c04-130">Aby uzyskać więcej informacji, zobacz [pliki konfiguracji środowiska uruchomieniowego](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="66c04-130">For more information, see [Runtime configuration files](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md).</span></span>

* <span data-ttu-id="66c04-131">*HelloWorld.dll*</span><span class="sxs-lookup"><span data-stu-id="66c04-131">*HelloWorld.dll*</span></span>

   <span data-ttu-id="66c04-132">Jest to [zależna od platformy wersja wdrożenia](../deploying/deploy-with-cli.md#framework-dependent-deployment) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-132">This is the [framework-dependent deployment](../deploying/deploy-with-cli.md#framework-dependent-deployment) version of the application.</span></span> <span data-ttu-id="66c04-133">Aby wykonać tę bibliotekę dołączaną dynamicznie, wprowadź `dotnet HelloWorld.dll` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="66c04-133">To execute this dynamic link library, enter `dotnet HelloWorld.dll` at a command prompt.</span></span> <span data-ttu-id="66c04-134">Ta metoda uruchamiania aplikacji działa na dowolnej platformie, na której zainstalowano środowisko uruchomieniowe platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="66c04-134">This method of running the app works on any platform that has the .NET runtime installed.</span></span>

* <span data-ttu-id="66c04-135">*HelloWorld. pdb* (opcjonalnie dla wdrożenia)</span><span class="sxs-lookup"><span data-stu-id="66c04-135">*HelloWorld.pdb* (optional for deployment)</span></span>

   <span data-ttu-id="66c04-136">Jest to plik symboli debugowania.</span><span class="sxs-lookup"><span data-stu-id="66c04-136">This is the debug symbols file.</span></span> <span data-ttu-id="66c04-137">Nie musisz wdrażać tego pliku wraz z aplikacją, chociaż należy je zapisać w zdarzeniu, które trzeba debugować opublikowaną wersję aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-137">You aren't required to deploy this file along with your application, although you should save it in the event that you need to debug the published version of your application.</span></span>

* <span data-ttu-id="66c04-138">*HelloWorld.runtimeconfig.jsna*</span><span class="sxs-lookup"><span data-stu-id="66c04-138">*HelloWorld.runtimeconfig.json*</span></span>

   <span data-ttu-id="66c04-139">To jest plik konfiguracji czasu wykonywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66c04-139">This is the application's run-time configuration file.</span></span> <span data-ttu-id="66c04-140">Identyfikuje wersję platformy .NET, w której aplikacja została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="66c04-140">It identifies the version of .NET that your application was built to run on.</span></span> <span data-ttu-id="66c04-141">Możesz również dodać do niej opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="66c04-141">You can also add configuration options to it.</span></span> <span data-ttu-id="66c04-142">Aby uzyskać więcej informacji, zobacz [Ustawienia konfiguracji środowiska uruchomieniowego .NET](../run-time-config/index.md#runtimeconfigjson).</span><span class="sxs-lookup"><span data-stu-id="66c04-142">For more information, see [.NET run-time configuration settings](../run-time-config/index.md#runtimeconfigjson).</span></span>

## <a name="run-the-published-app"></a><span data-ttu-id="66c04-143">Uruchom opublikowaną aplikację</span><span class="sxs-lookup"><span data-stu-id="66c04-143">Run the published app</span></span>

1. <span data-ttu-id="66c04-144">Otwórz Terminal i przejdź do folderu *Publikowanie* .</span><span class="sxs-lookup"><span data-stu-id="66c04-144">Open a terminal and navigate to the *publish* folder.</span></span> <span data-ttu-id="66c04-145">W tym celu wprowadź, `cd` a następnie wklej wcześniej skopiowaną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="66c04-145">To do that, enter `cd` and then paste the path that you copied earlier.</span></span> <span data-ttu-id="66c04-146">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="66c04-146">For example:</span></span>

   ```console
   cd ~/Projects/HelloWorld/HelloWorld/bin/Release/net5.0/publish/
   ```

1. <span data-ttu-id="66c04-147">Uruchom aplikację za pomocą `dotnet` polecenia:</span><span class="sxs-lookup"><span data-stu-id="66c04-147">Run the app by using the `dotnet` command:</span></span>

   1. <span data-ttu-id="66c04-148">Wprowadź `dotnet HelloWorld.dll` i naciśnij klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="66c04-148">Enter `dotnet HelloWorld.dll` and press <kbd>enter</kbd>.</span></span>

   1. <span data-ttu-id="66c04-149">Wprowadź nazwę w odpowiedzi na monit, a następnie naciśnij dowolny klawisz, aby wyjść.</span><span class="sxs-lookup"><span data-stu-id="66c04-149">Enter a name in response to the prompt, and press any key to exit.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66c04-150">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="66c04-150">Additional resources</span></span>

- [<span data-ttu-id="66c04-151">Wdrażanie aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="66c04-151">.NET application deployment</span></span>](../deploying/index.md)

## <a name="next-steps"></a><span data-ttu-id="66c04-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="66c04-152">Next steps</span></span>

<span data-ttu-id="66c04-153">W tym samouczku opublikowano aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="66c04-153">In this tutorial, you published a console app.</span></span> <span data-ttu-id="66c04-154">W następnym samouczku utworzysz bibliotekę klas.</span><span class="sxs-lookup"><span data-stu-id="66c04-154">In the next tutorial, you create a class library.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66c04-155">Tworzenie biblioteki .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="66c04-155">Create a .NET library using Visual Studio for Mac</span></span>](library-with-visual-studio-mac.md)
