---
title: <PreferComInsteadOfManagedRemoting> Element
ms.date: 03/30/2017
helpviewer_keywords:
- <PreferComInsteadOfManagedRemoting> element
- PreferComInsteadOfManagedRemoting element
ms.assetid: a279a42a-c415-4e79-88cf-64244ebda613
ms.openlocfilehash: 2fb0d94f91d28f9d9d4f247411d273f786f7b63b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91195288"
---
# <a name="prefercominsteadofmanagedremoting-element"></a>\<PreferComInsteadOfManagedRemoting> Element

Określa, czy środowisko uruchomieniowe będzie używać międzyoperacyjności modelu COM zamiast komunikacji zdalnej dla wszystkich wywołań między domenami aplikacji.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<PreferComInsteadOfManagedRemoting>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<PreferComInsteadOfManagedRemoting enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`enabled`|Atrybut wymagany.<br /><br /> Wskazuje, czy środowisko uruchomieniowe będzie używać międzyoperacyjności modelu COM zamiast komunikacji zdalnej między granicami domeny aplikacji.|  
  
## <a name="enabled-attribute"></a>Atrybut włączony  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`false`|Środowisko uruchomieniowe będzie używać komunikacji zdalnej między granicami domeny aplikacji. Jest to opcja domyślna.|  
|`true`|Środowisko uruchomieniowe będzie używać międzyoperacyjności modelu COM między granicami domeny aplikacji.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`runtime`|Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.|  
  
## <a name="remarks"></a>Uwagi  

 Po ustawieniu `enabled` atrybutu na `true` , środowisko uruchomieniowe zachowuje się w następujący sposób:  
  
- Środowisko uruchomieniowe nie wywołuje [IUnknown:: QueryInterface](/windows/win32/api/unknwn/nf-unknwn-iunknown-queryinterface(q)) dla interfejsu [IManagedObject](../../../unmanaged-api/hosting/imanagedobject-interface.md) , gdy interfejs [IUnknown](/windows/win32/api/unknwn/nn-unknwn-iunknown) przechodzi do domeny za pomocą interfejsu com. Zamiast tego konstruuje [otokę w czasie wykonywania](../../../../standard/native-interop/runtime-callable-wrapper.md) (RCW) wokół obiektu.  
  
- Środowisko uruchomieniowe zwraca E_NOINTERFACE, gdy odbierze `QueryInterface` wywołanie dla interfejsu [IManagedObject](../../../unmanaged-api/hosting/imanagedobject-interface.md) dla dowolnej [otoki](../../../../standard/native-interop/com-callable-wrapper.md) CCW (com), która została utworzona w tej domenie.  
  
 Te dwa zachowania zapewniają, że wszystkie wywołania przez interfejsy COM między obiektami zarządzanymi między domenami aplikacji korzystają z międzyoperacyjności modelu COM i modelu COM zamiast komunikacji zdalnej.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak określić, że środowisko uruchomieniowe ma używać międzyoperacyjności modelu COM w granicach izolacji:  
  
```xml  
<configuration>  
  <runtime>  
    <PreferComInsteadOfManagedRemoting enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
