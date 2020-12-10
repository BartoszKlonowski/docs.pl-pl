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
# <a name="appsettings-element-for-configuration"></a>\<appSettings>, element dla \<configuration>

Zawiera niestandardowe ustawienia aplikacji. Jest to wstępnie zdefiniowana sekcja konfiguracji udostępniona przez .NET Framework.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;**\<appSettings>**

## <a name="syntax"></a>Składnia

```xml
<appSettings>
  <!-- Elements to add, clear, or remove configuration settings -->
</appSettings>
```

## <a name="attribute"></a>Atrybut

|           | Opis |
| --------- | ----------- |
| **rozszerzeniem**  | Atrybut opcjonalny.<br><br>Określa ścieżkę względną do pliku zewnętrznego zawierającego niestandardowe ustawienia konfiguracji aplikacji. Określony plik zawiera ten sam rodzaj ustawień, które są określone w **\<add>** , **\<remove>** , i **\<clear>** i używa tego samego formatu pary klucz/wartość, co te elementy.<br><br>Określona ścieżka jest względna w stosunku do głównego pliku konfiguracji. W przypadku aplikacji Windows Forms jest to folder binarny (na przykład */bin/debug*), a nie lokalizacja pliku konfiguracji aplikacji. W przypadku aplikacji formularzy sieci Web ścieżka jest określana względem katalogu głównego aplikacji, w którym znajduje się plik *web.config* .<br><br>Środowisko uruchomieniowe ignoruje atrybut, jeśli nie można znaleźć określonego pliku. |

## <a name="parent-element"></a>Element nadrzędny

|     | Opis |
| --- | ----------- |
| [**\<configuration>** Postaci](../configuration-element.md) | Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework. |

## <a name="child-elements"></a>Elementy podrzędne

|     | Opis |
| --- | ----------- |
| [**\<add>**](add-element-for-appsettings.md) | Dodaje niestandardowe ustawienie aplikacji. |
| [**\<clear>**](clear-element-for-appsettings.md) | Czyści wszystkie wcześniej zdefiniowane ustawienia aplikacji. |
| [**\<remove>**](remove-element-for-appsettings.md) | Usuwa poprzednio zdefiniowane ustawienie aplikacji. |

## <a name="remarks"></a>Uwagi

**\<appSettings>** Element przechowuje niestandardowe informacje o konfiguracji aplikacji, takie jak parametry połączenia bazy danych, ścieżki plików, adresy URL usług sieci Web XML lub inne niestandardowe informacje o konfiguracji dla aplikacji. Pary klucz/wartość określone w **\<appSettings>** elemencie są dostępne w kodzie przy użyciu <xref:System.Configuration.ConfigurationSettings> klasy.

Można użyć atrybutu **pliku** w **\<appSettings>** elemencie *Web.config* i plików konfiguracji aplikacji. Ten atrybut określa plik konfiguracji, który zawiera dodatkowe ustawienia lub zastępuje ustawienia określone w **\<appSettings>** elemencie. Atrybut **pliku** może być używany w scenariuszach tworzenia zespołu kontroli źródła, na przykład gdy użytkownik chce zastąpić ustawienia projektu określone w pliku konfiguracyjnym aplikacji.

Pliki konfiguracyjne określone przez atrybut **pliku** muszą mieć węzeł główny, **\<appSettings>** a nie **\<configuration>** .

## <a name="example"></a>Przykład

W poniższym przykładzie przedstawiono zewnętrzny plik ustawień aplikacji (*custom.config*) definiujący niestandardowe ustawienie aplikacji:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="MyCustomSetting" value="MyCustomSettingValue" />
</appSettings>
```

Poniższy przykład przedstawia plik konfiguracji aplikacji, który używa ustawienia w pliku ustawień zewnętrznych i ustawia własne ustawienie aplikacji:

```xml
<configuration>
  <appSettings file="custom.config">
    <add key="ApplicationName" value="MyApplication" />
  </appSettings>
</configuration>
```

## <a name="configuration-file"></a>Plik konfiguracji

Tego elementu można użyć w pliku konfiguracyjnym aplikacji, pliku konfiguracji komputera (*Machine.config*) i plikach *Web.config* , które nie znajdują się na poziomie katalogu aplikacji.

## <a name="see-also"></a>Zobacz także

- [Schemat pliku konfiguracji dla .NET Framework](../index.md)
