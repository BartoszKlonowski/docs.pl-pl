---
title: <configuration>, element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration
helpviewer_keywords:
- <configuration> element
- configuration element
- container tags, <configuration> element
ms.assetid: 2ec1c9dc-2e5c-4ef0-9958-81670ab88449
ms.openlocfilehash: 8f79981a55d0bc9b1cd522e45f5606fda102c72c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544694"
---
# <a name="configuration-element"></a>\<configuration>, element

Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.

**\<configuration>**

## <a name="syntax"></a>Składnia

```xml
<configuration>
  <!-- Configuration settings -->
</configuration>
```

## <a name="attributes"></a>Atrybuty

Brak

## <a name="parent-element"></a>Element nadrzędny

Brak

## <a name="child-elements"></a>Elementy podrzędne

|     | Opis |
| --- | ----------- |
| [**\<assemblyBinding>**](assemblybinding-element-for-configuration.md) | Określa zasady powiązań zestawów na poziomie konfiguracji.|
| [**\<startup>** Schemat ustawień](./startup/index.md) | Wszystkie elementy w schemacie ustawienia uruchamiania. |
| [**\<runtime>** Schemat ustawień](./runtime/index.md) | Wszystkie elementy w schemacie ustawień środowiska uruchomieniowego. |
| [**\<system.runtime.remoting>** Schemat ustawień](/previous-versions/dotnet/netframework-4.0/z415cf9a(v=vs.100)) | Wszystkie elementy w schemacie ustawień usług zdalnych. |
| [**\<system.Net>** Schemat ustawień](./network/index.md) | Wszystkie elementy w schemacie ustawień sieciowych. |
| [**\<cryptographySettings>** Schemat ustawień](./cryptography/index.md) | Wszystkie elementy w schemacie ustawień kryptograficznych. |
| [**\<configuration>** Schemat sekcji](configuration-sections-schema.md) | Wszystkie elementy w schemacie ustawień sekcji konfiguracji. |
| [Schemat ustawień śledzenia i debugowania](./trace-debug/index.md) | Wszystkie elementy w schemacie ustawienia śledzenia i debugowania. |
| [Schemat ustawień konfiguracji ASP.NET](/previous-versions/dotnet/netframework-4.0/b5ysx397(v=vs.100)) | Wszystkie elementy w schemacie konfiguracji ASP.NET, w tym elementy służące do konfigurowania witryn i aplikacji sieci Web ASP.NET. Używane w plikach *Web.config* . |
| [**\<webServices>** Schemat ustawień](/previous-versions/dotnet/netframework-4.0/cctwteet(v=vs.100)) | Wszystkie elementy w schemacie ustawień usług sieci Web. |
| [Schemat ustawień sieci Web](./web/index.md) | Wszystkie elementy w schemacie ustawień sieci Web, w tym elementy służące do konfigurowania sposobu działania programu ASP.NET z aplikacją hosta, taką jak usługi IIS. Używane w plikach *aspnet.config* . |

## <a name="remarks"></a>Uwagi

Każdy plik konfiguracji musi zawierać dokładnie jeden **\<configuration>** element.

## <a name="see-also"></a>Zobacz także

- [Schemat pliku konfiguracji dla .NET Framework](index.md)
