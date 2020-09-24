---
title: Przekierowywanie wersji zestawu
description: Przekieruj odwołania w czasie kompilacji do różnych wersji zestawów .NET, zestawów stron trzecich lub zestawów własnych aplikacji.
ms.date: 03/30/2017
helpviewer_keywords:
- assembly binding, redirection
- redirecting assembly binding to earlier version
- configuration [.NET Framework], applications
- application configuration [.NET Framework]
- assemblies [.NET Framework], binding redirection
ms.assetid: 88fb1a17-6ac9-4b57-8028-193aec1f727c
ms.openlocfilehash: f0db5c32ba12b8e5313ca363e82260d66a7c010f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91166901"
---
# <a name="redirecting-assembly-versions"></a><span data-ttu-id="51afb-103">Przekierowywanie wersji zestawu</span><span class="sxs-lookup"><span data-stu-id="51afb-103">Redirecting Assembly Versions</span></span>

<span data-ttu-id="51afb-104">Odwołania do powiązań w czasie kompilacji można przekierować do zestawów .NET Framework, zestawów stron trzecich lub zestawów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51afb-104">You can redirect compile-time binding references to .NET Framework assemblies, third-party assemblies, or your own app's assemblies.</span></span> <span data-ttu-id="51afb-105">Możesz przekierować aplikację do korzystania z innej wersji zestawu na wiele sposobów: za pomocą zasad wydawcy w pliku konfiguracji aplikacji; lub za pomocą pliku konfiguracji komputera.</span><span class="sxs-lookup"><span data-stu-id="51afb-105">You can redirect your app to use a different version of an assembly in a number of ways: through publisher policy, through an app configuration file; or through the machine configuration file.</span></span> <span data-ttu-id="51afb-106">W tym artykule omówiono sposób działania powiązania zestawu w .NET Framework i sposobu jego konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="51afb-106">This article discusses how assembly binding works in the .NET Framework and how it can be configured.</span></span>

<a name="BKMK_Assemblyunificationanddefaultbinding"></a>

## <a name="assembly-unification-and-default-binding"></a><span data-ttu-id="51afb-107">Ujednolicenie zestawu i powiązanie domyślne</span><span class="sxs-lookup"><span data-stu-id="51afb-107">Assembly unification and default binding</span></span>

 <span data-ttu-id="51afb-108">Powiązania z zestawami .NET Framework czasami są przekierowane przez proces nazywany *dezjednoczeniem zestawu*.</span><span class="sxs-lookup"><span data-stu-id="51afb-108">Bindings to .NET Framework assemblies are sometimes redirected through a process called *assembly unification*.</span></span> <span data-ttu-id="51afb-109">.NET Framework składa się z wersji środowiska uruchomieniowego języka wspólnego oraz o dwóch dziesiątych zestawach .NET Framework tworzących bibliotekę typów.</span><span class="sxs-lookup"><span data-stu-id="51afb-109">The .NET Framework consists of a version of the common language runtime and about two dozen .NET Framework assemblies that make up the type library.</span></span> <span data-ttu-id="51afb-110">Te zestawy .NET Framework są traktowane przez środowisko uruchomieniowe jako pojedynczą jednostkę.</span><span class="sxs-lookup"><span data-stu-id="51afb-110">These .NET Framework assemblies are treated by the runtime as a single unit.</span></span> <span data-ttu-id="51afb-111">Domyślnie po uruchomieniu aplikacji wszystkie odwołania do typów w kodzie wykonywane przez środowisko uruchomieniowe są kierowane do zestawów .NET Framework, które mają ten sam numer wersji, co środowisko uruchomieniowe, które jest ładowane w procesie.</span><span class="sxs-lookup"><span data-stu-id="51afb-111">By default, when an app is launched, all references to types in code run by the runtime are directed to .NET Framework assemblies that have the same version number as the runtime that is loaded in a process.</span></span> <span data-ttu-id="51afb-112">Przekierowania, które występują w tym modelu, są domyślnym zachowaniem środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="51afb-112">The redirections that occur with this model are the default behavior for the runtime.</span></span>

 <span data-ttu-id="51afb-113">Na przykład jeśli aplikacja odwołuje się do typów w przestrzeni nazw System.XML i została skompilowana przy użyciu .NET Framework 4,5, zawiera statyczne odwołania do zestawu System.XML, który jest dostarczany ze środowiskiem uruchomieniowym w wersji 4,5.</span><span class="sxs-lookup"><span data-stu-id="51afb-113">For example, if your app references types in the System.XML namespace and was built by using the .NET Framework 4.5, it contains static references to the System.XML assembly that ships with runtime version 4.5.</span></span> <span data-ttu-id="51afb-114">Jeśli chcesz przekierować odwołanie do powiązania, aby wskazywało zestaw System.XML, który jest dostarczany z .NET Framework 4, możesz umieścić informacje o przekierowaniu w pliku konfiguracyjnym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51afb-114">If you want to redirect the binding reference to point to the System.XML assembly that ship with the .NET Framework 4, you can put redirect information in the app configuration file.</span></span> <span data-ttu-id="51afb-115">Przekierowanie powiązania w pliku konfiguracyjnym dla ujednoliconego zestawu .NET Framework anuluje ujednolicenie tego zestawu.</span><span class="sxs-lookup"><span data-stu-id="51afb-115">A binding redirection in a configuration file for a unified .NET Framework assembly cancels the unification for that assembly.</span></span>

 <span data-ttu-id="51afb-116">Ponadto możesz chcieć ręcznie przekierować powiązanie zestawu dla zestawów innych firm, jeśli jest dostępnych wiele wersji.</span><span class="sxs-lookup"><span data-stu-id="51afb-116">In addition, you may want to manually redirect assembly binding for third-party assemblies if there are multiple versions available.</span></span>

<a name="BKMK_Redirectingassemblyversionsbyusingpublisherpolicy"></a>

## <a name="redirecting-assembly-versions-by-using-publisher-policy"></a><span data-ttu-id="51afb-117">Przekierowywanie wersji zestawu przy użyciu zasad wydawcy</span><span class="sxs-lookup"><span data-stu-id="51afb-117">Redirecting assembly versions by using publisher policy</span></span>

 <span data-ttu-id="51afb-118">Dostawcy zestawów mogą kierować aplikacje do nowszej wersji zestawu, dołączając plik zasad wydawcy z nowym zestawem.</span><span class="sxs-lookup"><span data-stu-id="51afb-118">Vendors of assemblies can direct apps to a newer version of an assembly by including a publisher policy file with the new assembly.</span></span> <span data-ttu-id="51afb-119">Plik zasad wydawcy, który znajduje się w globalnej pamięci podręcznej zestawów, zawiera ustawienia przekierowania zestawu.</span><span class="sxs-lookup"><span data-stu-id="51afb-119">The publisher policy file, which is located in the global assembly cache, contains assembly redirection settings.</span></span>

 <span data-ttu-id="51afb-120">Każda *główna*. wersja *pomocnicza* zestawu ma swój własny plik zasad wydawcy.</span><span class="sxs-lookup"><span data-stu-id="51afb-120">Each *major*.*minor* version of an assembly has its own publisher policy file.</span></span> <span data-ttu-id="51afb-121">Na przykład przekierowania z wersji 2.0.2.222 do 2.0.3.000 i z wersji 2.0.2.321 do wersji 2.0.3.000 oba przechodzą do tego samego pliku, ponieważ są one skojarzone z wersją 2,0.</span><span class="sxs-lookup"><span data-stu-id="51afb-121">For example, redirections from version 2.0.2.222 to 2.0.3.000 and from version 2.0.2.321 to version 2.0.3.000 both go into the same file, because they are associated with version 2.0.</span></span> <span data-ttu-id="51afb-122">Jednak przekierowanie z wersji 3.0.0.999 do wersji 4.0.0.000 przejdzie do pliku w wersji 3.0.999.</span><span class="sxs-lookup"><span data-stu-id="51afb-122">However, a redirection from version 3.0.0.999 to version 4.0.0.000 goes into the file for version 3.0.999.</span></span> <span data-ttu-id="51afb-123">Każda główna wersja .NET Framework ma swój własny plik zasad wydawcy.</span><span class="sxs-lookup"><span data-stu-id="51afb-123">Each major version of the .NET Framework has its own publisher policy file.</span></span>

 <span data-ttu-id="51afb-124">Jeśli plik zasad wydawcy istnieje dla zestawu, środowisko uruchomieniowe sprawdzi ten plik po sprawdzeniu pliku konfiguracji manifestu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51afb-124">If a publisher policy file exists for an assembly, the runtime checks this file after checking the assembly's manifest and app configuration file.</span></span> <span data-ttu-id="51afb-125">Dostawcy powinni używać plików zasad wydawcy tylko wtedy, gdy nowy zestaw jest zgodny z poprzednimi wersjami z przekierowanym zestawem.</span><span class="sxs-lookup"><span data-stu-id="51afb-125">Vendors should use publisher policy files only when the new assembly is backward compatible with the assembly being redirected.</span></span>

 <span data-ttu-id="51afb-126">Zasady wydawcy można ominąć dla aplikacji, określając Ustawienia w pliku konfiguracji aplikacji, zgodnie z opisem w [sekcji pomijanie zasad wydawcy](#bypass_PP).</span><span class="sxs-lookup"><span data-stu-id="51afb-126">You can bypass publisher policy for your app by specifying settings in the app configuration file, as discussed in the [Bypassing publisher policy section](#bypass_PP).</span></span>

<a name="BKMK_Redirectingassemblyversionsattheapplevel"></a>

## <a name="redirecting-assembly-versions-at-the-app-level"></a><span data-ttu-id="51afb-127">Przekierowywanie wersji zestawu na poziomie aplikacji</span><span class="sxs-lookup"><span data-stu-id="51afb-127">Redirecting assembly versions at the app level</span></span>

 <span data-ttu-id="51afb-128">Istnieje kilka różnych technik zmiany zachowania powiązania aplikacji za pomocą pliku konfiguracji aplikacji: można ręcznie edytować plik, można polegać na automatycznym przekierowaniu powiązań lub można określić zachowanie powiązania, pomijając zasady wydawcy.</span><span class="sxs-lookup"><span data-stu-id="51afb-128">There are a few different techniques for changing the binding behavior for your app through the app configuration file: you can manually edit the file, you can rely on automatic binding redirection, or you can specify binding behavior by bypassing publisher policy.</span></span>

### <a name="manually-editing-the-app-config-file"></a><span data-ttu-id="51afb-129">Ręczne edytowanie pliku konfiguracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="51afb-129">Manually editing the app config file</span></span>

 <span data-ttu-id="51afb-130">Możesz ręcznie edytować plik konfiguracji aplikacji, aby rozwiązać problemy z zestawem.</span><span class="sxs-lookup"><span data-stu-id="51afb-130">You can manually edit the app configuration file to resolve assembly issues.</span></span> <span data-ttu-id="51afb-131">Na przykład, jeśli dostawca może wydać nowszą wersję zestawu, którego używa aplikacja bez dostarczania zasad wydawcy, ponieważ nie zapewniają zgodności z poprzednimi wersjami, można skierować aplikację do korzystania z nowszej wersji zestawu, umieszczając informacje o powiązaniu zestawu w pliku konfiguracyjnym aplikacji w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="51afb-131">For example, if a vendor might release a newer version of an assembly that your app uses without supplying a publisher policy, because they do not guarantee backward compatibility, you can direct your app to use the newer version of the assembly by putting assembly binding information in your app's configuration file as follows.</span></span>

```xml
<dependentAssembly>
  <assemblyIdentity name="someAssembly"
    publicKeyToken="32ab4ba45e0a69a1"
    culture="en-us" />
  <bindingRedirect oldVersion="7.0.0.0" newVersion="8.0.0.0" />
</dependentAssembly>
```

### <a name="relying-on-automatic-binding-redirection"></a><span data-ttu-id="51afb-132">Poleganie na automatycznym przekierowaniu powiązań</span><span class="sxs-lookup"><span data-stu-id="51afb-132">Relying on automatic binding redirection</span></span>

<span data-ttu-id="51afb-133">Po utworzeniu aplikacji klasycznej w programie Visual Studio, która jest przeznaczona dla .NET Framework 4.5.1 lub nowszej wersji, aplikacja używa automatycznego przekierowywania powiązań.</span><span class="sxs-lookup"><span data-stu-id="51afb-133">When you create a desktop app in Visual Studio that targets the .NET Framework 4.5.1 or a later version, the app uses automatic binding redirection.</span></span> <span data-ttu-id="51afb-134">Oznacza to, że jeśli dwa składniki odwołują się do różnych wersji tego samego zestawu o silnej nazwie, środowisko uruchomieniowe automatycznie dodaje przekierowanie powiązania do nowszej wersji zestawu w pliku konfiguracji aplikacji wyjściowej (app.config).</span><span class="sxs-lookup"><span data-stu-id="51afb-134">This means that if two components reference different versions of the same strong-named assembly, the runtime automatically adds a binding redirection to the newer version of the assembly in the output app configuration (app.config) file.</span></span> <span data-ttu-id="51afb-135">To przekierowanie zastępuje Montaż zestawu, który może być w innym przypadku.</span><span class="sxs-lookup"><span data-stu-id="51afb-135">This redirection overrides the assembly unification that might otherwise take place.</span></span> <span data-ttu-id="51afb-136">Źródłowy plik app.config nie jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="51afb-136">The source app.config file is not modified.</span></span> <span data-ttu-id="51afb-137">Załóżmy na przykład, że aplikacja bezpośrednio odwołuje się do składnika .NET Framework poza pasmem, ale używa biblioteki innej firmy, która jest przeznaczona dla starszej wersji tego samego składnika.</span><span class="sxs-lookup"><span data-stu-id="51afb-137">For example, let's say that your app directly references an out-of-band .NET Framework component but uses a third-party library that targets an older version of the same component.</span></span> <span data-ttu-id="51afb-138">Podczas kompilowania aplikacji plik konfiguracji aplikacji wyjściowej jest modyfikowany tak, aby zawierał przekierowanie powiązania do nowszej wersji składnika.</span><span class="sxs-lookup"><span data-stu-id="51afb-138">When you compile the app, the output app configuration file is modified to contain a binding redirection to the newer version of the component.</span></span> <span data-ttu-id="51afb-139">W przypadku tworzenia aplikacji sieci Web zostanie wyświetlone ostrzeżenie dotyczące kompilacji dotyczące konfliktu powiązania, co z kolei umożliwia dodanie niezbędnego przekierowania powiązania do źródłowego pliku konfiguracji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="51afb-139">If you create a web app, you receive a build warning regarding the binding conflict, which in turn, gives you the option to add the necessary binding redirect to the source web configuration file.</span></span>

<span data-ttu-id="51afb-140">W przypadku ręcznego dodawania przekierowań powiązań do pliku źródłowego app.config w czasie kompilacji program Visual Studio próbuje ujednolicić zestawy na podstawie dodanych przekierowań powiązań.</span><span class="sxs-lookup"><span data-stu-id="51afb-140">If you manually add binding redirects to the source app.config file, at compile time, Visual Studio tries to unify the assemblies based on the binding redirects you added.</span></span> <span data-ttu-id="51afb-141">Załóżmy na przykład, że wstawisz następujące przekierowanie powiązania dla zestawu:</span><span class="sxs-lookup"><span data-stu-id="51afb-141">For example, let's say you insert the following binding redirect for an assembly:</span></span>

`<bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0" />`

<span data-ttu-id="51afb-142">Jeśli inny projekt w aplikacji odwołuje się do wersji 1.0.0.0 tego samego zestawu, automatyczne przekierowanie powiązań dodaje następujący wpis do pliku wyjściowego app.config, aby aplikacja była ujednolicona w wersji 2.0.0.0 tego zestawu:</span><span class="sxs-lookup"><span data-stu-id="51afb-142">If another project in your app references version 1.0.0.0 of the same assembly, automatic binding redirection adds the following entry to the output app.config file so that the app is unified on version 2.0.0.0 of this assembly:</span></span>

`<bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" />`

<span data-ttu-id="51afb-143">Automatyczne przekierowywanie powiązań można włączyć, jeśli aplikacja jest przeznaczona dla starszych wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="51afb-143">You can enable automatic binding redirection if your app targets older versions of the .NET Framework.</span></span> <span data-ttu-id="51afb-144">To zachowanie domyślne można przesłonić, dostarczając informacje o przekierowaniu powiązań w pliku app.config dla dowolnego zestawu lub wyłączając funkcję przekierowywania powiązań.</span><span class="sxs-lookup"><span data-stu-id="51afb-144">You can override this default behavior by providing binding redirection information in the app.config file for any assembly, or by turning off the binding redirection feature.</span></span> <span data-ttu-id="51afb-145">Aby uzyskać informacje na temat włączania lub wyłączania tej funkcji, zobacz [jak: Włączanie i wyłączanie automatycznego przekierowywania powiązań](how-to-enable-and-disable-automatic-binding-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="51afb-145">For information about how to turn this feature on or off, see [How to: Enable and Disable Automatic Binding Redirection](how-to-enable-and-disable-automatic-binding-redirection.md).</span></span>

<a name="bypass_PP"></a>

### <a name="bypassing-publisher-policy"></a><span data-ttu-id="51afb-146">Pomijanie zasad wydawcy</span><span class="sxs-lookup"><span data-stu-id="51afb-146">Bypassing publisher policy</span></span>

 <span data-ttu-id="51afb-147">W razie potrzeby można zastąpić zasady wydawcy w pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51afb-147">You can override publisher policy in the app configuration file if necessary.</span></span> <span data-ttu-id="51afb-148">Na przykład nowe wersje zestawów, które są zgodne z poprzednimi wersjami, mogą nadal przerwać aplikację.</span><span class="sxs-lookup"><span data-stu-id="51afb-148">For example, new versions of assemblies that claim to be backward compatible can still break an app.</span></span> <span data-ttu-id="51afb-149">Jeśli chcesz obejść zasady wydawcy, Dodaj [\<publisherPolicy>](./file-schema/runtime/publisherpolicy-element.md) element do [\<dependentAssembly>](./file-schema/runtime/dependentassembly-element.md) elementu w pliku konfiguracji aplikacji i ustaw dla atrybutu **Zastosuj** wartość **nie**, który zastępuje wszystkie poprzednie ustawienia **tak** .</span><span class="sxs-lookup"><span data-stu-id="51afb-149">If you want to bypass publisher policy, add a [\<publisherPolicy>](./file-schema/runtime/publisherpolicy-element.md) element to the [\<dependentAssembly>](./file-schema/runtime/dependentassembly-element.md) element in the app configuration file, and set the **apply** attribute to **no**, which overrides any previous **yes** settings.</span></span>

 `<publisherPolicy apply="no" />`

 <span data-ttu-id="51afb-150">Pomiń zasady wydawcy, aby zachować swoją aplikację dla użytkowników, ale upewnij się, że problem został zaraportowany do dostawcy zestawu.</span><span class="sxs-lookup"><span data-stu-id="51afb-150">Bypass publisher policy to keep your app running for your users, but make sure you report the problem to the assembly vendor.</span></span> <span data-ttu-id="51afb-151">Jeśli zestaw ma plik zasad wydawcy, dostawca powinien upewnić się, że zestaw jest zgodny z poprzednimi wersjami, a klienci mogą korzystać z nowej wersji tak jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="51afb-151">If an assembly has a publisher policy file, the vendor should make sure that the assembly is backward compatible and that clients can use the new version as much as possible.</span></span>

<a name="BKMK_Redirectingassemblyversionsatthemachinelevel"></a>

## <a name="redirecting-assembly-versions-at-the-machine-level"></a><span data-ttu-id="51afb-152">Przekierowywanie wersji zestawu na poziomie komputera</span><span class="sxs-lookup"><span data-stu-id="51afb-152">Redirecting assembly versions at the machine level</span></span>

 <span data-ttu-id="51afb-153">Mogą wystąpić sytuacje sytuacje, w których administrator komputera chce, aby wszystkie aplikacje na komputerze korzystały z określonej wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="51afb-153">There might be rare cases when a machine administrator wants all apps on a computer to use a specific version of an assembly.</span></span> <span data-ttu-id="51afb-154">Na przykład administrator może chcieć, aby każda aplikacja korzystała z określonej wersji zestawu, ponieważ ta wersja naprawia lukę w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="51afb-154">For example, the administrator might want every app to use a particular assembly version, because that version fixes a security hole.</span></span> <span data-ttu-id="51afb-155">Jeśli zestaw zostanie przekierowany w pliku konfiguracyjnym maszyny, wszystkie aplikacje na tym komputerze, które używają starej wersji, będą kierowane do korzystania z nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="51afb-155">If an assembly is redirected in the machine's configuration file, all apps on that machine that use the old version will be directed to use the new version.</span></span> <span data-ttu-id="51afb-156">Plik konfiguracji komputera zastępuje plik konfiguracji aplikacji i plik zasad wydawcy.</span><span class="sxs-lookup"><span data-stu-id="51afb-156">The machine configuration file overrides the app configuration file and the publisher policy file.</span></span> <span data-ttu-id="51afb-157">Ten plik znajduje się w katalogu% \ config*instalacji systemu plików wykonywalnych*.</span><span class="sxs-lookup"><span data-stu-id="51afb-157">This file is located in the %*runtime install path*%\Config directory.</span></span> <span data-ttu-id="51afb-158">Zwykle .NET Framework jest instalowany w katalogu%drive%\Windows\Microsoft.NET\Framework.</span><span class="sxs-lookup"><span data-stu-id="51afb-158">Typically, the .NET Framework is installed in the %drive%\Windows\Microsoft.NET\Framework directory.</span></span>

<a name="BKMK_Specifyingassemblybindinginconfigurationfiles"></a>

## <a name="specifying-assembly-binding-in-configuration-files"></a><span data-ttu-id="51afb-159">Określanie powiązania zestawu w plikach konfiguracji</span><span class="sxs-lookup"><span data-stu-id="51afb-159">Specifying assembly binding in configuration files</span></span>

 <span data-ttu-id="51afb-160">Ten sam format XML służy do określania przekierowań powiązań niezależnie od tego, czy znajduje się on w pliku konfiguracji aplikacji, pliku konfiguracji komputera czy pliku zasad wydawcy.</span><span class="sxs-lookup"><span data-stu-id="51afb-160">You use the same XML format to specify binding redirects whether it’s in the app configuration file, the machine configuration file, or the publisher policy file.</span></span> <span data-ttu-id="51afb-161">Aby przekierować jedną wersję zestawu do innej, użyj [\<bindingRedirect>](./file-schema/runtime/bindingredirect-element.md) elementu.</span><span class="sxs-lookup"><span data-stu-id="51afb-161">To redirect one assembly version to another, use the [\<bindingRedirect>](./file-schema/runtime/bindingredirect-element.md) element.</span></span> <span data-ttu-id="51afb-162">Atrybut **oldVersion** może określać jedną wersję zestawu lub zakres wersji.</span><span class="sxs-lookup"><span data-stu-id="51afb-162">The **oldVersion** attribute can specify a single assembly version or a range of versions.</span></span> <span data-ttu-id="51afb-163">Ten `newVersion` atrybut powinien określać jedną wersję.</span><span class="sxs-lookup"><span data-stu-id="51afb-163">The `newVersion` attribute should specify a single version.</span></span>  <span data-ttu-id="51afb-164">Na przykład `<bindingRedirect oldVersion="1.1.0.0-1.2.0.0" newVersion="2.0.0.0"/>` określa, że środowisko uruchomieniowe ma używać wersji 2.0.0.0 zamiast wersji zestawu między 1.1.0.0 i 1.2.0.0.</span><span class="sxs-lookup"><span data-stu-id="51afb-164">For example, `<bindingRedirect oldVersion="1.1.0.0-1.2.0.0" newVersion="2.0.0.0"/>` specifies that the runtime should use version 2.0.0.0 instead of the assembly versions between 1.1.0.0 and 1.2.0.0.</span></span>

 <span data-ttu-id="51afb-165">Poniższy przykład kodu demonstruje różne scenariusze przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="51afb-165">The following code example demonstrates a variety of binding redirect scenarios.</span></span> <span data-ttu-id="51afb-166">W tym przykładzie określono przekierowanie dla zakresu wersji programu `myAssembly` oraz przekierowanie pojedynczego powiązania dla `mySecondAssembly` .</span><span class="sxs-lookup"><span data-stu-id="51afb-166">The example specifies a redirect for a range of versions for `myAssembly`, and a single binding redirect for `mySecondAssembly`.</span></span> <span data-ttu-id="51afb-167">W przykładzie określono również, że plik zasad wydawcy nie przesłania przekierowań powiązań dla programu `myThirdAssembly` .</span><span class="sxs-lookup"><span data-stu-id="51afb-167">The example also specifies that publisher policy file will not override the binding redirects for `myThirdAssembly`.</span></span>

 <span data-ttu-id="51afb-168">Aby powiązać zestaw, należy określić ciąg "urn: schematys-Microsoft-com: ASM. v1" z atrybutem **xmlns** w [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) tagu.</span><span class="sxs-lookup"><span data-stu-id="51afb-168">To bind an assembly, you must specify the string "urn:schemas-microsoft-com:asm.v1" with the **xmlns** attribute in the [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) tag.</span></span>

```xml
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="myAssembly"
          publicKeyToken="32ab4ba45e0a69a1"
          culture="en-us" />
        <!-- Assembly versions can be redirected in app,
          publisher policy, or machine configuration files. -->
        <bindingRedirect oldVersion="1.0.0.0-2.0.0.0" newVersion="3.0.0.0" />
      </dependentAssembly>
      <dependentAssembly>
        <assemblyIdentity name="mySecondAssembly"
          publicKeyToken="32ab4ba45e0a69a1"
          culture="en-us" />
             <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" />
      </dependentAssembly>
      <dependentAssembly>
      <assemblyIdentity name="myThirdAssembly"
        publicKeyToken="32ab4ba45e0a69a1"
        culture="en-us" />
        <!-- Publisher policy can be set only in the app
          configuration file. -->
        <publisherPolicy apply="no" />
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```

### <a name="limiting-assembly--bindings-to-a-specific-version"></a><span data-ttu-id="51afb-169">Ograniczanie powiązań zestawu do określonej wersji</span><span class="sxs-lookup"><span data-stu-id="51afb-169">Limiting assembly  bindings to a specific version</span></span>

 <span data-ttu-id="51afb-170">Można użyć atrybutu **AppliesTo** dla [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) elementu w pliku konfiguracyjnym aplikacji, aby przekierować odwołania do powiązań zestawów do określonej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="51afb-170">You can use the **appliesTo** attribute on the [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) element in an app configuration file to redirect assembly binding references to a specific version of the .NET Framework.</span></span> <span data-ttu-id="51afb-171">Ten opcjonalny atrybut używa numeru wersji .NET Framework, aby wskazać, której wersji dotyczy.</span><span class="sxs-lookup"><span data-stu-id="51afb-171">This optional attribute uses a .NET Framework version number to indicate what version it applies to.</span></span> <span data-ttu-id="51afb-172">Jeśli nie określono atrybutu **AppliesTo** , [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) element ma zastosowanie do wszystkich wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="51afb-172">If no **appliesTo** attribute is specified, the [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) element applies to all versions of the .NET Framework.</span></span>

 <span data-ttu-id="51afb-173">Na przykład aby przekierować powiązanie zestawu dla zestawu .NET Framework 3,5, należy dołączyć następujący kod XML do pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51afb-173">For example, to redirect assembly binding for a .NET Framework 3.5 assembly, you would include the following XML code in your app configuration file.</span></span>

```xml
<runtime>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1"
    appliesTo="v3.5">
    <dependentAssembly>
      <!-- assembly information goes here -->
    </dependentAssembly>
  </assemblyBinding>
</runtime>
```

 <span data-ttu-id="51afb-174">Należy wprowadzić informacje o przekierowaniu w kolejności wersji.</span><span class="sxs-lookup"><span data-stu-id="51afb-174">You should enter redirection information in version order.</span></span> <span data-ttu-id="51afb-175">Na przykład wprowadź informacje o przekierowaniach powiązań zestawów dla zestawów .NET Framework 3,5, a następnie zestawy .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="51afb-175">For example, enter assembly binding redirection information for .NET Framework 3.5 assemblies followed by .NET Framework 4.5 assemblies.</span></span> <span data-ttu-id="51afb-176">Na koniec wprowadź informacje o przekierowaniu powiązań zestawów dla dowolnego przekierowania zestawu .NET Framework, który nie używa atrybutu **AppliesTo** i w związku z tym ma zastosowanie do wszystkich wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="51afb-176">Finally, enter assembly binding redirection information for any .NET Framework assembly redirection that does not use the **appliesTo** attribute and therefore applies to all versions of the .NET Framework.</span></span> <span data-ttu-id="51afb-177">W przypadku konfliktu w przekierowaniu zostanie użyta pierwsza zgodna instrukcja przekierowania w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="51afb-177">If there is a conflict in redirection, the first matching redirection statement in the configuration file is used.</span></span>

 <span data-ttu-id="51afb-178">Na przykład, aby przekierować jedno odwołanie do zestawu .NET Framework 3,5 i innego odwołania do zestawu .NET Framework 4, użyj wzorca pokazanego w poniższym pseudokodzie.</span><span class="sxs-lookup"><span data-stu-id="51afb-178">For example, to redirect one reference to a .NET Framework 3.5 assembly and another reference to a .NET Framework 4 assembly, use the pattern shown in the following pseudocode.</span></span>

```xml
<assemblyBinding xmlns="..." appliesTo="v3.5 ">
  <!--.NET Framework version 3.5 redirects here -->
</assemblyBinding>

<assemblyBinding xmlns="..." appliesTo="v4.0.30319">
  <!--.NET Framework version 4.0 redirects here -->
</assemblyBinding>

<assemblyBinding xmlns="...">
  <!-- redirects meant for all versions of the runtime -->
</assemblyBinding>
```

## <a name="see-also"></a><span data-ttu-id="51afb-179">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="51afb-179">See also</span></span>

- [<span data-ttu-id="51afb-180">Instrukcje: Włączanie i wyłączanie automatycznego przekierowania powiązań</span><span class="sxs-lookup"><span data-stu-id="51afb-180">How to: Enable and Disable Automatic Binding Redirection</span></span>](how-to-enable-and-disable-automatic-binding-redirection.md)
- [<span data-ttu-id="51afb-181">\<bindingRedirect> Postaci</span><span class="sxs-lookup"><span data-stu-id="51afb-181">\<bindingRedirect> Element</span></span>](./file-schema/runtime/bindingredirect-element.md)
- [<span data-ttu-id="51afb-182">Uprawnienie zabezpieczeń przekierowania powiązania zestawu</span><span class="sxs-lookup"><span data-stu-id="51afb-182">Assembly Binding Redirection Security Permission</span></span>](assembly-binding-redirection-security-permission.md)
- [<span data-ttu-id="51afb-183">Zestawy w środowisku .NET</span><span class="sxs-lookup"><span data-stu-id="51afb-183">Assemblies in .NET</span></span>](../../standard/assembly/index.md)
- [<span data-ttu-id="51afb-184">Programowanie za pomocą zestawów</span><span class="sxs-lookup"><span data-stu-id="51afb-184">Programming with Assemblies</span></span>](../../standard/assembly/index.md)
- [<span data-ttu-id="51afb-185">Sposoby lokalizowania zestawów przez środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="51afb-185">How the Runtime Locates Assemblies</span></span>](../deployment/how-the-runtime-locates-assemblies.md)
- [<span data-ttu-id="51afb-186">Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="51afb-186">Configuring Apps</span></span>](index.md)
- [<span data-ttu-id="51afb-187">Schemat ustawień środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="51afb-187">Runtime Settings Schema</span></span>](./file-schema/runtime/index.md)
- [<span data-ttu-id="51afb-188">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="51afb-188">Configuration File Schema</span></span>](./file-schema/index.md)
- [<span data-ttu-id="51afb-189">Instrukcje: Tworzenie zasad wydawcy</span><span class="sxs-lookup"><span data-stu-id="51afb-189">How to: Create a Publisher Policy</span></span>](how-to-create-a-publisher-policy.md)
