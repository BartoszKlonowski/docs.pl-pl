---
title: <remove>, element dla webRequestModules (ustawienia sieci)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- remove element, webRequestModules
- webRequestModules, remove element
- <remove> element, webRequestModules
- <webRequestModules>, remove element
ms.assetid: dd84d2fe-2f4f-457a-9d3c-441d0d21cc10
ms.openlocfilehash: 65e8b1f2088015b86d4f981f07875d236a11a617
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91176191"
---
# <a name="remove-element-for-webrequestmodules-network-settings"></a>\<remove>, element dla webRequestModules (ustawienia sieci)

Usuwa niestandardowy moduł żądania sieci Web z aplikacji.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<webRequestModules>**](webrequestmodules-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**
  
## <a name="syntax"></a>Składnia  
  
```xml  
<remove
  prefix="URI prefix"
/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|**Atrybut**|**Opis**|  
|-------------------|---------------------|  
|`prefix`|Prefiks identyfikatora URI dla żądań obsłużonych przez ten moduł żądania sieci Web.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|**Postaci**|**Opis**|  
|-----------------|---------------------|  
|[webRequestModules](webrequestmodules-element-network-settings.md)|Określa moduły, które mają być używane do żądania informacji z hostów sieciowych.|  
  
## <a name="remarks"></a>Uwagi  

 `remove`Element usuwa zarejestrowany moduł żądania sieci Web dla określonego prefiksu URI.  
  
 Wartość `prefix` atrybutu powinna być wiodącymi znakami prawidłowego identyfikatora URI — na przykład " `http` " lub " `http://www.contoso.com` ".  
  
## <a name="configuration-files"></a>Pliki konfiguracji  

 Tego elementu można użyć w pliku konfiguracyjnym aplikacji lub pliku konfiguracji komputera (Machine.config).  
  
## <a name="example"></a>Przykład  

Poniższy przykład usuwa istniejący moduł żądania sieci Web dla protokołu HTTP, a następnie rejestruje nowy niestandardowy moduł żądania sieci Web dla żądań HTTP `www.contoso.com` .
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <remove prefix="http">  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Net.WebRequest>
- [Schemat ustawień sieciowych](index.md)
