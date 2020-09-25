---
title: <trace> Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace
- http://schemas.microsoft.com/.NetConfiguration/v2.0#trace
helpviewer_keywords:
- <trace> element
- listeners
- trace element
- trace listener, <trace> element
ms.assetid: 7931c942-63c1-47c3-a045-9d9de3cacdbf
ms.openlocfilehash: 617b42a0be2be272a78b33be997cce632d1c6dcb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198928"
---
# <a name="trace-element"></a>\<trace> Element

Zawiera detektory, które zbierają, przechowują i rozsyłają komunikaty śledzenia.  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<trace>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<trace autoflush="true|false"
       indentsize="indent value"  
       useGlobalLock="true| false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`autoflush`|Atrybut opcjonalny.<br /><br /> Określa, czy odbiorniki śledzenia automatycznie opróżniają bufor wyjściowy po każdej operacji zapisu.|  
|`indentsize`|Atrybut opcjonalny.<br /><br /> Określa liczbę spacji do wcięcia.|  
|`useGlobalLock`|Atrybut opcjonalny.<br /><br /> Wskazuje, czy globalna blokada powinna być używana.|  
  
## <a name="autoflush-attribute"></a>AutoFlush — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`false`|Nie opróżnia bufora wyjściowego. Jest to opcja domyślna.|  
|`true`|Automatycznie opróżnia bufor wyjściowy.|  
  
## <a name="usegloballock-attribute"></a>useGlobalLock — Atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`false`|Nie używa blokady globalnej, jeśli odbiornik jest bezpieczny wątkowo; w przeciwnym razie używa blokady globalnej.|  
|`true`|Używa blokady globalnej niezależnie od tego, czy odbiornik jest bezpieczny wątkowo. Jest to opcja domyślna.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<listeners>](listeners-element-for-trace.md)|Określa odbiornik, który zbiera, przechowuje i kieruje komunikaty.|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`system.diagnostics`|Określa detektory śledzenia, które zbierają, przechowują i rozsyłają komunikaty oraz poziom, w którym ustawiono przełącznik śledzenia.|  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak użyć elementu, `<trace>` Aby dodać odbiornik `MyListener` do `Listeners` kolekcji. `MyListener` tworzy plik o nazwie `MyListener.log` i zapisuje dane wyjściowe do pliku. `useGlobalLock`Atrybut jest ustawiony na `false` , co powoduje, że globalna blokada nie zostanie użyta, jeśli odbiornik śledzenia jest bezpieczny wątkowo. `autoflush`Atrybut jest ustawiony na `true` , co powoduje, że odbiornik śledzenia ma zapisywać do pliku bez względu na to, czy <xref:System.Diagnostics.Trace.Flush%2A?displayProperty=nameWithType> Metoda jest wywoływana. `indentsize`Atrybut jest ustawiony na 0 (zero), co powoduje, że odbiornik ma wcięcie zerowej spacji, gdy <xref:System.Diagnostics.Trace.Indent%2A?displayProperty=nameWithType> wywoływana jest metoda.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace useGlobalLock="false" autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- [Schemat ustawień śledzenia i debugowania](index.md)
