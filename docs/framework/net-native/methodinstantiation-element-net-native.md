---
title: <MethodInstantiation> — Element (.NET Native)
ms.date: 03/30/2017
ms.assetid: a3355d78-2a88-4109-8521-830d7cae260a
ms.openlocfilehash: e247db05f8442d4fcfddbf03b5eb8955b8ff425a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250960"
---
# <a name="methodinstantiation-element-net-native"></a>\<MethodInstantiation> — Element (.NET Native)

Stosuje zasady odbicia środowiska uruchomieniowego do skonstruowanej metody ogólnej.  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<MethodInstantiation Name="method_name"  
                     Signature="method_signature"  
                     Arguments="method_arguments"  
                     Browse="policy_type"  
                     Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Typ atrybutu|Opis|  
|---------------|--------------------|-----------------|  
|`Name`|Ogólne|Atrybut wymagany. Określa nazwę metody.|  
|`Signature`|Ogólne|Atrybut opcjonalny. Określa nazwane parametry metody. Wiele parametrów nazwanych są oddzielone przecinkami. Ten `Signature` atrybut jest używany do odróżniania przeciążonych metod.|  
|`Arguments`|Ogólne|Atrybut wymagany. Określa argumenty typu ogólnego. Jeśli istnieją wiele argumentów, są one oddzielone przecinkami.|  
|`Browse`|Odbicie|Atrybut opcjonalny. Kontroluje wykonywanie zapytań dotyczących informacji na temat lub wyliczanie metody, ale nie włącza żadnego dynamicznego wywołania w czasie wykonywania.|  
|`Dynamic`|Odbicie|Atrybut opcjonalny. Kontroluje dostęp środowiska uruchomieniowego do konstruktora lub metody w celu włączenia programowania dynamicznego. Te zasady zapewniają, że element członkowski może być wywoływany dynamicznie w czasie wykonywania.|  
  
## <a name="name-attribute"></a>Atrybut nazwy  
  
|Wartość|Opis|  
|-----------|-----------------|  
|*method_name*|Nazwa metody. Typ metody jest zdefiniowany przez [\<Type>](type-element-net-native.md) element nadrzędny lub [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .|  
  
## <a name="signature-attribute"></a>Atrybut podpisu  
  
|Wartość|Opis|  
|-----------|-----------------|  
|*method_signature*|Określa nazwane parametry metody. Jeśli istnieją wiele parametrów, są one oddzielone przecinkami.|  
  
## <a name="arguments-attribute"></a>Arguments — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|*method_arguments*|Określa argumenty typu ogólnego. Jeśli istnieją wiele argumentów, są one oddzielone przecinkami. Każdy argument musi składać się z w pełni kwalifikowanej nazwy typu.|  
  
## <a name="all-other-attributes"></a>Wszystkie inne atrybuty  
  
|Wartość|Opis|  
|-----------|-----------------|  
|*policy_setting*|Ustawienie, które ma zostać zastosowane do tego typu zasad dla metody. Możliwe wartości to `Auto` , `Excluded` , `Included` , i `Required` . Aby uzyskać więcej informacji, zobacz [Ustawienia zasad dyrektywy środowiska uruchomieniowego](runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|Stosuje zasady odbicia do typu i wszystkich jego elementów członkowskich.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Stosuje zasady odbicia do skonstruowanego typu ogólnego i wszystkich jego członków.|  
  
## <a name="remarks"></a>Uwagi  

 `<MethodInstantiation>`Element zastępuje zasady odbicia środowiska uruchomieniowego odpowiadającej jej otwartej metody ogólnej.  
  
## <a name="see-also"></a>Zobacz też

- [Dokumentacja pliku konfiguracji dyrektyw środowiska uruchomieniowego (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Elementy dyrektyw środowiska uruchomieniowego](runtime-directive-elements.md)
- [Ustawienia zasad dyrektyw środowiska uruchomieniowego](runtime-directive-policy-settings.md)
- [\<Method> Postaci](method-element-net-native.md)
