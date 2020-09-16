---
title: <compiler> Element
ms.date: 08/14/2018
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#compiler
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom/compilers/compiler
helpviewer_keywords:
- compiler configuration elements, <compiler> element
- <compiler> element
- compiler configuration attributes
- compiler element
ms.assetid: 7a151659-b803-4c27-b5ce-1c4aa0d5a823
ms.openlocfilehash: 0abbe594754cbd70ec4732a1e7ef98e8e88bf167
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544755"
---
# <a name="compiler-element"></a>\<compiler> Element

Określa atrybuty konfiguracji kompilatora dla dostawcy języka.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.codedom>**](system-codedom-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<compilers>**](compilers-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<compiler>**

## <a name="syntax"></a>Składnia

```xml
<compiler
  language="languageName[;...;...]"
  extension="fileExtension[;...;...]"
  type="typeName, assemblyName"
  warningLevel="number"
  compilerOptions="option1 option2"
/>
```

## <a name="attributes-and-elements"></a>Atrybuty i elementy

W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.

### <a name="attributes"></a>Atrybuty

|Atrybut|Opis|
|---------------|-----------------|
|`compilerOptions`|Atrybut opcjonalny.<br /><br /> Określa dodatkowe argumenty specyficzne dla kompilatora dla kompilacji. Wartości `compilerOptions` atrybutu są zwykle wymienione w temacie Opcje kompilatora dla kompilatora.|
|`extension`|Atrybut wymagany.<br /><br /> Zawiera rozdzieloną średnikami listę rozszerzeń nazw plików używanych przez pliki źródłowe dla dostawcy języka. Na przykład ". cs".|
|`language`|Atrybut wymagany.<br /><br /> Zawiera rozdzieloną średnikami listę nazw języków obsługiwanych przez dostawcę języka. Na przykład "c#; CS; CSharp".|
|`type`|Atrybut wymagany.<br /><br /> Określa nazwę typu dostawcy języka, łącznie z nazwą zestawu zawierającego implementację dostawcy. Nazwa typu musi spełniać wymagania zdefiniowane w ramach [określania w pełni kwalifikowanych nazw typów](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md).|
|`warningLevel`|Atrybut opcjonalny.<br /><br /> Określa domyślny poziom ostrzeżeń kompilatora; Określa poziom, na którym dostawca języka traktuje ostrzeżenia kompilacji jako błędy.|

### <a name="child-elements"></a>Elementy podrzędne

|Element|Opis|
|-------------|-----------------|
|[\<providerOption> Postaci](provideroption-element.md)|Określa atrybuty wersji kompilatora dla dostawcy języka.|

### <a name="parent-elements"></a>Elementy nadrzędne

|Element|Opis|
|-------------|-----------------|
|[\<configuration> Postaci](../configuration-element.md)|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|
|[\<system.codedom> Postaci](system-codedom-element.md)|Określa ustawienia konfiguracji kompilatora dla dostępnych dostawców języka.|
|[\<compilers> Postaci](compilers-element.md)|Kontener dla elementów konfiguracji kompilatora; zawiera zero lub więcej `<compiler>` elementów.|

## <a name="remarks"></a>Uwagi

Każdy `<compiler>` element określa atrybuty konfiguracji kompilatora dla określonego dostawcy języka. Dostawca rozszerza <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> klasę dla określonego języka; `<compiler>` element definiuje ustawienia kompilatora i generatora kodu dla dostawcy języka.

.NET Framework definiuje początkowe ustawienia kompilatora w pliku konfiguracji komputera (Machine.config). Deweloperzy i dostawcy kompilatora mogą dodać ustawienia konfiguracji dla nowej <xref:System.CodeDom.Compiler.CodeDomProvider> implementacji. Użyj <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> metody, aby programowo wyliczyć dostawcę języka i ustawienia konfiguracji kompilatora na komputerze.

Elementy kompilatora w pliku konfiguracyjnym aplikacji lub sieci Web mogą uzupełniać lub zastępować ustawienia w pliku konfiguracji komputera. Jeśli skonfigurowano więcej niż jedną implementację dostawcy dla tej samej nazwy języka lub tego samego rozszerzenia pliku, Ostatnia zgodna konfiguracja zastępuje wszelkich wcześniej skonfigurowanych dostawców dla tej nazwy języka lub rozszerzenia pliku.

## <a name="configuration-file"></a>Plik konfiguracji

Ten element może być używany w pliku konfiguracji komputera i w pliku konfiguracji aplikacji.

## <a name="example"></a>Przykład

Poniższy przykład ilustruje typowy element konfiguracji kompilatora:

```xml
<configuration>
  <system.codedom>
    <compilers>
      <!-- zero or more compiler elements -->
      <compiler
        language="c#;cs;csharp"
        extension=".cs"
        type="Microsoft.CSharp.CSharpCodeProvider, System,
          Version=2.0.3600.0, Culture=neutral,
          PublicKeyToken=b77a5c561934e089"
        compilerOptions="/optimize"
        warningLevel="1" />
    </compilers>
  </system.codedom>
</configuration>
```

## <a name="see-also"></a>Zobacz także

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [Schemat pliku konfiguracji](../index.md)
- [\<compilers> Postaci](compilers-element.md)
- [Określanie w pełni kwalifikowanych nazw typów](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)
- [Element kompilatora dla kompilatorów dla kompilacji (Schemat ustawień ASP.NET)](/previous-versions/dotnet/netframework-4.0/a15ebt6c(v=vs.100))
