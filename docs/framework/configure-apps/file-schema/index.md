---
title: Schemat pliku konfiguracji dla .NET Framework
ms.date: 05/01/2017
helpviewer_keywords:
- .NET Framework application configuration, configuration schema
- machine configuration files
- application configuration files, schema
- app.config files, schema
- schema configuration settings
- schemas, configuration settings
- enterprisesec.config files
- well-formed XML
- enterprisesec configuration files
- security.config files
- security [.NET Framework], configuration files
- application development [.NET Framework], schema
- XML tags
- container tags
- machine.config files
- configuration schema [.NET Framework]
- configuration settings [.NET Framework], applications
- configuration file reference [.NET Framework]
ms.assetid: 69003d39-dc8a-460c-a6be-e6d93e690b38
ms.openlocfilehash: ab6f12be01899f5b7e54a7ec2d9675d502d88bc3
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555136"
---
# <a name="configuration-file-schema-for-the-net-framework"></a><span data-ttu-id="a9bec-102">Schemat pliku konfiguracji dla .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a9bec-102">Configuration file schema for the .NET Framework</span></span>

<span data-ttu-id="a9bec-103">Pliki konfiguracji to standardowe pliki XML, których można użyć do zmiany ustawień i ustawienia zasad dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-103">Configuration files are standard XML files that you can use to change settings and set policies for your apps.</span></span> <span data-ttu-id="a9bec-104">Schemat konfiguracji .NET Framework składa się z elementów, których można użyć w plikach konfiguracji w celu sterowania zachowaniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-104">The .NET Framework configuration schema consists of elements that you can use in configuration files to control the behavior of your apps.</span></span> <span data-ttu-id="a9bec-105">Spis treści tej sekcji odzwierciedla hierarchię schematu dla uruchamiania, środowiska uruchomieniowego, sieci i innych typów ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-105">The table of contents for this section reflects the schema hierarchy for startup, runtime, network, and other types of configuration settings.</span></span>

<span data-ttu-id="a9bec-106">Aby uzyskać informacje o typach, formacie i lokalizacji plików konfiguracji, zobacz [Konfigurowanie aplikacji](../index.md).</span><span class="sxs-lookup"><span data-stu-id="a9bec-106">For information about the types, format, and location of configuration files, see [Configure apps](../index.md).</span></span> <span data-ttu-id="a9bec-107">Zapoznaj się z plikiem XML, jeśli chcesz bezpośrednio edytować pliki konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-107">Familiarize yourself with XML if you want to edit the configuration files directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9bec-108">W przypadku tagów i atrybutów XML w plikach konfiguracji rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="a9bec-108">XML tags and attributes in configuration files are case-sensitive.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="a9bec-109">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="a9bec-109">In this section</span></span>

<span data-ttu-id="a9bec-110">[**\<configuration>** Postaci](configuration-element.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-110">[**\<configuration>** Element](configuration-element.md)</span></span>\
<span data-ttu-id="a9bec-111">Element najwyższego poziomu dla wszystkich plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-111">The top-level element for all configuration files.</span></span>

<span data-ttu-id="a9bec-112">[**\<assemblyBinding>** Postaci](assemblybinding-element-for-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-112">[**\<assemblyBinding>** Element](assemblybinding-element-for-configuration.md)</span></span>\
<span data-ttu-id="a9bec-113">Określa zasady powiązań zestawów na poziomie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-113">Specifies assembly binding policy at the configuration level.</span></span>

<span data-ttu-id="a9bec-114">[**\<linkedConfiguration>** Postaci](linkedconfiguration-element.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-114">[**\<linkedConfiguration>** Element](linkedconfiguration-element.md)</span></span>\
<span data-ttu-id="a9bec-115">Określa plik konfiguracji, który ma zostać uwzględniony.</span><span class="sxs-lookup"><span data-stu-id="a9bec-115">Specifies a configuration file to include.</span></span>

<span data-ttu-id="a9bec-116">[Schemat ustawień uruchamiania](./startup/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-116">[Startup Settings Schema](./startup/index.md)</span></span>\
<span data-ttu-id="a9bec-117">Elementy określające wersję środowiska uruchomieniowego języka wspólnego do użycia.</span><span class="sxs-lookup"><span data-stu-id="a9bec-117">Elements that specify which version of the common language runtime to use.</span></span>

<span data-ttu-id="a9bec-118">[Schemat ustawień środowiska uruchomieniowego](./runtime/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-118">[Runtime Settings Schema](./runtime/index.md)</span></span>\
<span data-ttu-id="a9bec-119">Elementy, które konfigurują powiązanie zestawu i zachowanie środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="a9bec-119">Elements that configure assembly binding and runtime behavior.</span></span>

<span data-ttu-id="a9bec-120">[Schemat ustawień sieciowych](./network/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-120">[Network Settings Schema](./network/index.md)</span></span>\
<span data-ttu-id="a9bec-121">Elementy, które określają, w jaki sposób .NET Framework nawiązuje połączenie z Internetem.</span><span class="sxs-lookup"><span data-stu-id="a9bec-121">Elements that specify how the .NET Framework connects to the internet.</span></span>

<span data-ttu-id="a9bec-122">[Schemat ustawień kryptografii](./cryptography/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-122">[Cryptography Settings Schema](./cryptography/index.md)</span></span>\
<span data-ttu-id="a9bec-123">Elementy, które mapują przyjazne nazwy algorytmów na klasy implementujące algorytmy kryptografii.</span><span class="sxs-lookup"><span data-stu-id="a9bec-123">Elements that map friendly algorithm names to classes that implement cryptography algorithms.</span></span>

<span data-ttu-id="a9bec-124">[Schemat sekcji konfiguracji](configuration-sections-schema.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-124">[Configuration Sections Schema](configuration-sections-schema.md)</span></span>\
<span data-ttu-id="a9bec-125">Elementy służące do tworzenia i używania sekcji konfiguracyjnych ustawień niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="a9bec-125">Elements used to create and use configuration sections for custom settings.</span></span>

<span data-ttu-id="a9bec-126">[Schemat ustawień śledzenia i debugowania](./trace-debug/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-126">[Trace and Debug Settings Schema](./trace-debug/index.md)</span></span>\
<span data-ttu-id="a9bec-127">Elementy, które określają przełączniki śledzenia i odbiorniki.</span><span class="sxs-lookup"><span data-stu-id="a9bec-127">Elements that specify trace switches and listeners.</span></span>

<span data-ttu-id="a9bec-128">[Schemat ustawień kompilatora i dostawcy języka](./compiler/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-128">[Compiler and Language Provider Settings Schema](./compiler/index.md)</span></span>\
<span data-ttu-id="a9bec-129">Elementy, które określają konfigurację kompilatora dla dostępnych dostawców języka.</span><span class="sxs-lookup"><span data-stu-id="a9bec-129">Elements that specify compiler configuration for available language providers.</span></span>

<span data-ttu-id="a9bec-130">[Schemat ustawień aplikacji](application-settings-schema.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-130">[Application Settings Schema](application-settings-schema.md)</span></span>\
<span data-ttu-id="a9bec-131">Elementy, które umożliwiają aplikacji Windows Forms lub ASP.NET przechowywanie i pobieranie ustawień zakresu aplikacji i zakresu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a9bec-131">Elements that enable a Windows Forms or ASP.NET application to store and retrieve application-scoped and user-scoped settings.</span></span>

<span data-ttu-id="a9bec-132">[Schemat ustawień aplikacji](./appsettings/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-132">[App Settings Schema](./appsettings/index.md)</span></span>\
<span data-ttu-id="a9bec-133">Zawiera niestandardowe ustawienia aplikacji, takie jak ścieżki plików, adresy URL usług sieci Web XML lub inne niestandardowe informacje o konfiguracji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9bec-133">Contains custom application settings, such as file paths, XML Web service URLs, or any other custom configuration information for an application.</span></span>

<span data-ttu-id="a9bec-134">[Schemat ustawień sieci Web](./web/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-134">[Web Settings Schema](./web/index.md)</span></span>\
<span data-ttu-id="a9bec-135">Elementy służące do konfigurowania sposobu działania ASP.NET z aplikacją hosta, taką jak usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="a9bec-135">Elements for configuring how ASP.NET works with a host application such as IIS.</span></span> <span data-ttu-id="a9bec-136">Używane w plikach *Aspnet.config* .</span><span class="sxs-lookup"><span data-stu-id="a9bec-136">Used in *Aspnet.config* files.</span></span>

<span data-ttu-id="a9bec-137">[Schemat konfiguracji Windows Forms](winforms/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-137">[Windows Forms Configuration Schema](winforms/index.md)</span></span>\
<span data-ttu-id="a9bec-138">Wszystkie elementy w sekcji Konfiguracja aplikacji Windows Forms, w tym takie, jak takie dostosowania, jak obsługa wielomonitorów i wysokiej rozdzielczości DPI.</span><span class="sxs-lookup"><span data-stu-id="a9bec-138">All elements in the Windows Forms application configuration section, which includes customizations such as multi-monitor and high-DPI support.</span></span>

<span data-ttu-id="a9bec-139">[Schemat konfiguracji WCF](./wcf/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-139">[WCF Configuration Schema](./wcf/index.md)</span></span>\
<span data-ttu-id="a9bec-140">Wszystkie elementy, które umożliwiają skonfigurowanie usługi WCF i aplikacji klienckich.</span><span class="sxs-lookup"><span data-stu-id="a9bec-140">All elements that enable you to configure WCF service and client applications.</span></span>

<span data-ttu-id="a9bec-141">[Składnia dyrektywy WCF](./wcf-directive/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-141">[WCF Directive Syntax](./wcf-directive/index.md)</span></span>\
<span data-ttu-id="a9bec-142">Opisuje `@ServiceHost` dyrektywę, która definiuje atrybuty specyficzne dla strony używane przez kompilator SVC.</span><span class="sxs-lookup"><span data-stu-id="a9bec-142">Describes the `@ServiceHost` directive, which defines page-specific attributes used by the .svc compiler.</span></span>

<span data-ttu-id="a9bec-143">[Schemat konfiguracji WIF](windows-identity-foundation/index.md)</span><span class="sxs-lookup"><span data-stu-id="a9bec-143">[WIF Configuration Schema](windows-identity-foundation/index.md)</span></span>\
<span data-ttu-id="a9bec-144">Wszystkie elementy schematu konfiguracji Windows Identity Foundation (WIF).</span><span class="sxs-lookup"><span data-stu-id="a9bec-144">All elements of the Windows Identity Foundation (WIF) configuration schema.</span></span>

## <a name="related-sections"></a><span data-ttu-id="a9bec-145">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="a9bec-145">Related sections</span></span>

<span data-ttu-id="a9bec-146">[Schemat ustawień komunikacji zdalnej](/previous-versions/dotnet/netframework-4.0/z415cf9a(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="a9bec-146">[Remoting Settings Schema](/previous-versions/dotnet/netframework-4.0/z415cf9a(v=vs.100))</span></span>\
<span data-ttu-id="a9bec-147">Opisuje elementy, które konfigurują aplikacje klienta i serwera, które implementują komunikację zdalną.</span><span class="sxs-lookup"><span data-stu-id="a9bec-147">Describes the elements that configure client and server applications that implement remoting.</span></span>

<span data-ttu-id="a9bec-148">[Schemat ustawień ASP.NET](/previous-versions/dotnet/netframework-4.0/b5ysx397(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="a9bec-148">[ASP.NET Settings Schema](/previous-versions/dotnet/netframework-4.0/b5ysx397(v=vs.100))</span></span>\
<span data-ttu-id="a9bec-149">Opisuje elementy kontrolujące zachowanie aplikacji sieci Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a9bec-149">Describes the elements that control the behavior of ASP.NET Web applications.</span></span>

<span data-ttu-id="a9bec-150">[Schemat ustawień usług sieci Web](/previous-versions/dotnet/netframework-4.0/cctwteet(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="a9bec-150">[Web Services Settings Schema](/previous-versions/dotnet/netframework-4.0/cctwteet(v=vs.100))</span></span>\
<span data-ttu-id="a9bec-151">Opisuje elementy kontrolujące zachowanie usług sieci Web ASP.NET i ich klientów.</span><span class="sxs-lookup"><span data-stu-id="a9bec-151">Describes the elements that control the behavior of ASP.NET Web services and their clients.</span></span>

<span data-ttu-id="a9bec-152">[Konfigurowanie aplikacji .NET Framework](/previous-versions/dotnet/netframework-4.0/kza1yk3a(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="a9bec-152">[Configuring .NET Framework Apps](/previous-versions/dotnet/netframework-4.0/kza1yk3a(v=vs.100))</span></span>\
<span data-ttu-id="a9bec-153">Opisuje sposób konfigurowania zabezpieczeń, powiązań zestawów i komunikacji zdalnej w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a9bec-153">Describes how to configure security, assembly binding, and remoting in the .NET Framework.</span></span>
