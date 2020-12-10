---
title: <appSettings>, element dla <configuration>
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings
helpviewer_keywords:
- appSettings Element
- <appSettings> Element
ms.assetid: 39694cc4-6b84-45a6-9329-385a0d8b48fe
ms.openlocfilehash: 66260d15768781b7fa3d9397b8e8a7d9ad68ab95
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009797"
---
# <a name="appsettings-element-for-configuration"></a><span data-ttu-id="733ac-102">\<appSettings>, element dla \<configuration></span><span class="sxs-lookup"><span data-stu-id="733ac-102">\<appSettings> element for \<configuration></span></span>

<span data-ttu-id="733ac-103">Zawiera niestandardowe ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-103">Contains custom application settings.</span></span> <span data-ttu-id="733ac-104">Jest to wstępnie zdefiniowana sekcja konfiguracji udostępniona przez .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="733ac-104">This is a predefined configuration section provided by the .NET Framework.</span></span>

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;**\<appSettings>**

## <a name="syntax"></a><span data-ttu-id="733ac-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="733ac-105">Syntax</span></span>

```xml
<appSettings>
  <!-- Elements to add, clear, or remove configuration settings -->
</appSettings>
```

## <a name="attribute"></a><span data-ttu-id="733ac-106">Atrybut</span><span class="sxs-lookup"><span data-stu-id="733ac-106">Attribute</span></span>

|           | <span data-ttu-id="733ac-107">Opis</span><span class="sxs-lookup"><span data-stu-id="733ac-107">Description</span></span> |
| --------- | ----------- |
| <span data-ttu-id="733ac-108">**rozszerzeniem**</span><span class="sxs-lookup"><span data-stu-id="733ac-108">**file**</span></span>  | <span data-ttu-id="733ac-109">Atrybut opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="733ac-109">Optional attribute.</span></span><br><br><span data-ttu-id="733ac-110">Określa ścieżkę względną do pliku zewnętrznego zawierającego niestandardowe ustawienia konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-110">Specifies a relative path to an external file containing custom application configuration settings.</span></span> <span data-ttu-id="733ac-111">Określony plik zawiera ten sam rodzaj ustawień, które są określone w **\<add>** , **\<remove>** , i **\<clear>** i używa tego samego formatu pary klucz/wartość, co te elementy.</span><span class="sxs-lookup"><span data-stu-id="733ac-111">The specified file contains the same kind of settings that are specified in the **\<add>**, **\<remove>**, and **\<clear>** elements and uses the same key/value pair format as those elements.</span></span><br><br><span data-ttu-id="733ac-112">Określona ścieżka jest względna w stosunku do głównego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="733ac-112">The path specified is relative to the main configuration file.</span></span> <span data-ttu-id="733ac-113">W przypadku aplikacji Windows Forms jest to folder binarny (na przykład */bin/debug*), a nie lokalizacja pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-113">For a Windows Forms application, this is the binary folder (such as */bin/debug*), not the location of the application configuration file.</span></span> <span data-ttu-id="733ac-114">W przypadku aplikacji formularzy sieci Web ścieżka jest określana względem katalogu głównego aplikacji, w którym znajduje się plik *web.config* .</span><span class="sxs-lookup"><span data-stu-id="733ac-114">For Web Forms applications, the path is relative to the application root, where the *web.config* file is located.</span></span><br><br><span data-ttu-id="733ac-115">Środowisko uruchomieniowe ignoruje atrybut, jeśli nie można znaleźć określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="733ac-115">The runtime ignores the attribute if the specified file can't be found.</span></span> |

## <a name="parent-element"></a><span data-ttu-id="733ac-116">Element nadrzędny</span><span class="sxs-lookup"><span data-stu-id="733ac-116">Parent element</span></span>

|     | <span data-ttu-id="733ac-117">Opis</span><span class="sxs-lookup"><span data-stu-id="733ac-117">Description</span></span> |
| --- | ----------- |
| [<span data-ttu-id="733ac-118">**\<configuration>** Postaci</span><span class="sxs-lookup"><span data-stu-id="733ac-118">**\<configuration>** Element</span></span>](../configuration-element.md) | <span data-ttu-id="733ac-119">Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="733ac-119">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span> |

## <a name="child-elements"></a><span data-ttu-id="733ac-120">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="733ac-120">Child elements</span></span>

|     | <span data-ttu-id="733ac-121">Opis</span><span class="sxs-lookup"><span data-stu-id="733ac-121">Description</span></span> |
| --- | ----------- |
| [**\<add>**](add-element-for-appsettings.md) | <span data-ttu-id="733ac-122">Dodaje niestandardowe ustawienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-122">Adds a custom application setting.</span></span> |
| [**\<clear>**](clear-element-for-appsettings.md) | <span data-ttu-id="733ac-123">Czyści wszystkie wcześniej zdefiniowane ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-123">Clears all previously defined application settings.</span></span> |
| [**\<remove>**](remove-element-for-appsettings.md) | <span data-ttu-id="733ac-124">Usuwa poprzednio zdefiniowane ustawienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-124">Removes a previously defined application setting.</span></span> |

## <a name="remarks"></a><span data-ttu-id="733ac-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="733ac-125">Remarks</span></span>

<span data-ttu-id="733ac-126">**\<appSettings>** Element przechowuje niestandardowe informacje o konfiguracji aplikacji, takie jak parametry połączenia bazy danych, ścieżki plików, adresy URL usług sieci Web XML lub inne niestandardowe informacje o konfiguracji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-126">The **\<appSettings>** element stores custom application configuration information, such as database connection strings, file paths, XML Web service URLs, or any other custom configuration information for an application.</span></span> <span data-ttu-id="733ac-127">Pary klucz/wartość określone w **\<appSettings>** elemencie są dostępne w kodzie przy użyciu <xref:System.Configuration.ConfigurationSettings> klasy.</span><span class="sxs-lookup"><span data-stu-id="733ac-127">The key/value pairs specified in the **\<appSettings>** element are accessed in code using the <xref:System.Configuration.ConfigurationSettings> class.</span></span>

<span data-ttu-id="733ac-128">Można użyć atrybutu **pliku** w **\<appSettings>** elemencie *Web.config* i plików konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-128">You can use the **file** attribute in the **\<appSettings>** element of the *Web.config* and application configuration files.</span></span> <span data-ttu-id="733ac-129">Ten atrybut określa plik konfiguracji, który zawiera dodatkowe ustawienia lub zastępuje ustawienia określone w **\<appSettings>** elemencie.</span><span class="sxs-lookup"><span data-stu-id="733ac-129">This attribute specifies a configuration file that provides additional settings or overrides the settings specified in the **\<appSettings>** element.</span></span> <span data-ttu-id="733ac-130">Atrybut **pliku** może być używany w scenariuszach tworzenia zespołu kontroli źródła, na przykład gdy użytkownik chce zastąpić ustawienia projektu określone w pliku konfiguracyjnym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-130">The **file** attribute can be used in source control team development scenarios, such as when a user wants to override the project settings specified in an application configuration file.</span></span>

<span data-ttu-id="733ac-131">Pliki konfiguracyjne określone przez atrybut **pliku** muszą mieć węzeł główny, **\<appSettings>** a nie **\<configuration>** .</span><span class="sxs-lookup"><span data-stu-id="733ac-131">Configuration files specified by the **file** attribute must have a root node of **\<appSettings>** rather than **\<configuration>**.</span></span>

## <a name="example"></a><span data-ttu-id="733ac-132">Przykład</span><span class="sxs-lookup"><span data-stu-id="733ac-132">Example</span></span>

<span data-ttu-id="733ac-133">W poniższym przykładzie przedstawiono zewnętrzny plik ustawień aplikacji (*custom.config*) definiujący niestandardowe ustawienie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="733ac-133">The following example shows an external application settings file (*custom.config*) that defines a custom application setting:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="MyCustomSetting" value="MyCustomSettingValue" />
</appSettings>
```

<span data-ttu-id="733ac-134">Poniższy przykład przedstawia plik konfiguracji aplikacji, który używa ustawienia w pliku ustawień zewnętrznych i ustawia własne ustawienie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="733ac-134">The following example shows an application configuration file that consumes the setting in the external settings file and sets an application setting of its own:</span></span>

```xml
<configuration>
  <appSettings file="custom.config">
    <add key="ApplicationName" value="MyApplication" />
  </appSettings>
</configuration>
```

## <a name="configuration-file"></a><span data-ttu-id="733ac-135">Plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="733ac-135">Configuration file</span></span>

<span data-ttu-id="733ac-136">Tego elementu można użyć w pliku konfiguracyjnym aplikacji, pliku konfiguracji komputera (*Machine.config*) i plikach *Web.config* , które nie znajdują się na poziomie katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="733ac-136">This element can be used in the application configuration file, machine configuration file (*Machine.config*), and *Web.config* files that are not at the application directory level.</span></span>

## <a name="see-also"></a><span data-ttu-id="733ac-137">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="733ac-137">See also</span></span>

- [<span data-ttu-id="733ac-138">Schemat pliku konfiguracji dla .NET Framework</span><span class="sxs-lookup"><span data-stu-id="733ac-138">Configuration file schema for the .NET Framework</span></span>](../index.md)
