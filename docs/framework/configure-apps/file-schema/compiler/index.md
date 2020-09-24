---
title: Schemat ustawień kompilatora i dostawcy języka
ms.date: 03/30/2017
helpviewer_keywords:
- configuration settings [.NET Framework], compilers
- compiler configuration elements, schema
- compiler configuration elements
- language providers
- compiler configuration settings, schema
- configuration schema [.NET Framework], compiler settings
- language providers, settings schema
- compiler configuration settings
ms.assetid: c020b139-8699-4f0d-9ac9-70d0c5b2a8c8
ms.openlocfilehash: 457e90c92530e04070575e42e3fc282ce45b3d03
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153953"
---
# <a name="compiler-and-language-provider-settings-schema"></a>Schemat ustawień kompilatora i dostawcy języka

Ustawienia kompilatora i dostawcy języka określają elementy konfiguracji kompilatora dla dostępnych dostawców języka. Każdy element konfiguracji kompilatora określa nazwę typu dostawcy kodu, parametry kompilatora, obsługiwane nazwy języków i obsługiwane rozszerzenia plików.  
  
.NET Framework definiuje początkowe ustawienia kompilatora w pliku konfiguracji komputera (Machine.config). Deweloperzy i dostawcy kompilatora mogą dodać ustawienia konfiguracji dla nowej <xref:System.CodeDom.Compiler.CodeDomProvider> implementacji. Użyj <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> metody, aby programowo wyliczyć dostawcę języka i ustawienia konfiguracji kompilatora na komputerze.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.codedom>**](system-codedom-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<compilers>**](compilers-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<compiler>**](compiler-element.md)
  
|Element|Opis|  
|-------------|-----------------|  
|[\<system.codedom>](system-codedom-element.md)|Określa ustawienia konfiguracji kompilatora dla dostępnych dostawców języka.|  
|[\<compilers>](compilers-element.md)|Kontener dla elementów konfiguracji kompilatora; zawiera zero lub więcej [\<compiler>](compiler-element.md) elementów.|  
|[\<compiler>](compiler-element.md)|Określa atrybuty konfiguracji kompilatora dla dostawcy języka.|  
  
## <a name="example"></a>Przykład  

 Poniższy przykład ilustruje typowy element konfiguracji kompilatora.  
  
```xml  
<configuration>  
   <system.codedom>  
     <compilers>  
       <!-- zero or more compiler elements -->  
       <compiler  
          language="c#;cs;csharp"  
          extension=".cs"  
          type="Microsoft.CSharp.CSharpCodeProvider, System, Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
          compilerOptions=""  
          warningLevel="1" />  
     </compilers>  
   </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [Schemat pliku konfiguracji](../index.md)
- [\<compiler> Postaci](compiler-element.md)
