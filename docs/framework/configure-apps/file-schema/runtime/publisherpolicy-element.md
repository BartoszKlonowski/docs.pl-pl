---
title: <publisherPolicy> Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/publisherPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/publisherPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#publisherPolicy
helpviewer_keywords:
- publisherPolicy element
- container tags, <publisherPolicy> element
- <publisherPolicy> element
ms.assetid: 4613407e-d0a8-4ef2-9f81-a6acb9fdc7d4
ms.openlocfilehash: bd6ab1123ef3f84f7e8a06b25ce48aed37e4bef7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91195262"
---
# <a name="publisherpolicy-element"></a>\<publisherPolicy> Element

Określa, czy środowisko uruchomieniowe stosuje zasady wydawcy.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<dependentAssembly>**](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<publisherPolicy>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<publisherPolicy apply="yes|no"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`apply`|Określa, czy mają być stosowane zasady wydawcy.|  
  
## <a name="apply-attribute"></a>Zastosuj atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`yes`|Stosuje zasady wydawcy. Jest to ustawienie domyślne.|  
|`no`|Nie stosuje zasad wydawcy.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`assemblyBinding`|Zawiera informacje o przekierowaniu wersji zestawu i lokalizacji zestawów.|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`dependentAssembly`|Hermetyzuje zasady powiązań oraz lokalizację zestawu dla każdego zestawu. Użyj jednego `<dependentAssembly>` elementu dla każdego zestawu.|  
|`runtime`|Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.|  
  
## <a name="remarks"></a>Uwagi  

 Gdy dostawca składnika zwalnia nową wersję zestawu, dostawca może uwzględnić zasady wydawcy, aby aplikacje używające starej wersji używały teraz nowej wersji. Aby określić, czy zastosować zasady wydawcy dla określonego zestawu, umieść **\<publisherPolicy>** element w **\<dependentAssembly>** elemencie.  
  
 Ustawieniem domyślnym dla atrybutu **apply** jest **tak**. Ustawienie atrybutu **Zastosuj** do **nie** zastępuje żadnych poprzednich ustawień **tak** dla zestawu.  
  
 Aby aplikacja jawnie ignorował zasady wydawcy przy użyciu [\<publisherPolicy apply="no"/>](publisherpolicy-element.md) elementu w pliku konfiguracyjnym aplikacji, wymagane jest uprawnienie. Uprawnienie jest udzielane przez ustawienie <xref:System.Security.Permissions.SecurityPermissionFlag> flagi na <xref:System.Security.Permissions.SecurityPermission> . Aby uzyskać więcej informacji, zobacz [uprawnienia zabezpieczeń przekierowania powiązania zestawu](../../assembly-binding-redirection-security-permission.md).  
  
## <a name="example"></a>Przykład  

 Poniższy przykład powoduje wyłączenie zasad wydawcy dla zestawu `myAssembly` .  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                                    publicKeyToken="32ab4ba45e0a69a1"  
                                    culture="neutral" />  
            <publisherPolicy apply="no"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
- [Sposoby lokalizowania zestawów przez środowisko uruchomieniowe](../../../deployment/how-the-runtime-locates-assemblies.md)
- [Przekierowywanie wersji zestawu](../../redirect-assembly-versions.md)
