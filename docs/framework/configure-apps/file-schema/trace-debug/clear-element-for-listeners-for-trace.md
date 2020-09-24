---
title: <clear> Element dla <listeners> elementu <trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear
helpviewer_keywords:
- clear element for <listeners> for <trace>
- <clear> element for <listeners> for <trace>
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
ms.openlocfilehash: 2d301d588e33b0eea4164a6bf62dedd7b0c450ec
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91149273"
---
# <a name="clear-element-for-listeners-for-trace"></a><span data-ttu-id="9f90b-102">\<clear> Element dla \<listeners> elementu \<trace></span><span class="sxs-lookup"><span data-stu-id="9f90b-102">\<clear> Element for \<listeners> for \<trace></span></span>

<span data-ttu-id="9f90b-103">Czyści `Listeners` kolekcję do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9f90b-103">Clears the `Listeners` collection for trace.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**

## <a name="syntax"></a><span data-ttu-id="9f90b-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9f90b-104">Syntax</span></span>  
  
```xml  
<clear/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="9f90b-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="9f90b-105">Attributes and Elements</span></span>  

 <span data-ttu-id="9f90b-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="9f90b-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="9f90b-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="9f90b-107">Attributes</span></span>  

 <span data-ttu-id="9f90b-108">Brak.</span><span class="sxs-lookup"><span data-stu-id="9f90b-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="9f90b-109">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="9f90b-109">Child Elements</span></span>  

 <span data-ttu-id="9f90b-110">Brak.</span><span class="sxs-lookup"><span data-stu-id="9f90b-110">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="9f90b-111">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="9f90b-111">Parent Elements</span></span>  
  
|<span data-ttu-id="9f90b-112">Element</span><span class="sxs-lookup"><span data-stu-id="9f90b-112">Element</span></span>|<span data-ttu-id="9f90b-113">Opis</span><span class="sxs-lookup"><span data-stu-id="9f90b-113">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="9f90b-114">Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9f90b-114">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`system.diagnostics`|<span data-ttu-id="9f90b-115">Określa detektory śledzenia, które zbierają, przechowują i rozsyłają komunikaty oraz poziom, w którym ustawiono przełącznik śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9f90b-115">Specifies trace listeners that collect, store, and route messages and the level where a trace switch is set.</span></span>|  
|`trace`|<span data-ttu-id="9f90b-116">Zawiera detektory, które zbierają, przechowują i rozsyłają komunikaty śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9f90b-116">Contains listeners that collect, store, and route tracing messages.</span></span>|  
|`listeners`|<span data-ttu-id="9f90b-117">Zawiera detektory, które zbierają, przechowują i rozsyłają komunikaty.</span><span class="sxs-lookup"><span data-stu-id="9f90b-117">Contains listeners that collect, store, and route messages.</span></span> <span data-ttu-id="9f90b-118">Odbiorniki kierują dane wyjściowe śledzenia do odpowiedniego obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="9f90b-118">Listeners direct the tracing output to an appropriate target.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9f90b-119">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9f90b-119">Remarks</span></span>  

 <span data-ttu-id="9f90b-120">`<clear>`Element usuwa wszystkie odbiorniki z `Listeners` kolekcji w celu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9f90b-120">The `<clear>` element removes all listeners from the `Listeners` collection for trace.</span></span> <span data-ttu-id="9f90b-121">Możesz użyć `<clear>` elementu przed użyciem `<add>` elementu, aby mieć pewność, że w kolekcji nie ma żadnych innych aktywnych odbiorników.</span><span class="sxs-lookup"><span data-stu-id="9f90b-121">You can use the `<clear>` element before using the `<add>` element to be certain there are no other active listeners in the collection.</span></span>  
  
 <span data-ttu-id="9f90b-122">Możesz wyczyścić `Listeners` kolekcję programowo, wywołując <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> metodę we <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> właściwości ( `System.Diagnostics.Trace.Listeners.Clear()` ).</span><span class="sxs-lookup"><span data-stu-id="9f90b-122">You can clear the `Listeners` collection programmatically by calling the <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> method on the <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> property (`System.Diagnostics.Trace.Listeners.Clear()`).</span></span>  
  
 <span data-ttu-id="9f90b-123">Tego elementu można użyć w pliku konfiguracji komputera (Machine.config) i pliku konfiguracyjnym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9f90b-123">This element can be used in the machine configuration file (Machine.config) and the application configuration file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9f90b-124">`<clear>`Element usuwa <xref:System.Diagnostics.DefaultTraceListener> z `Listeners` kolekcji, zmieniając zachowanie <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> metod,, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> i <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="9f90b-124">The `<clear>` element removes the <xref:System.Diagnostics.DefaultTraceListener> from the `Listeners` collection, altering the behavior of the <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType>, and <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> methods.</span></span> <span data-ttu-id="9f90b-125">Wywołanie `Assert` metody lub `Fail` zwykle powoduje wyświetlenie okna komunikatu.</span><span class="sxs-lookup"><span data-stu-id="9f90b-125">Calling an `Assert` or `Fail` method normally results in the display of a message box.</span></span> <span data-ttu-id="9f90b-126">Jednak okno komunikatu nie jest wyświetlane, jeśli <xref:System.Diagnostics.DefaultTraceListener> nie znajduje się w `Listeners` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9f90b-126">However, the message box is not displayed if the <xref:System.Diagnostics.DefaultTraceListener> is not in the `Listeners` collection.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9f90b-127">Przykład</span><span class="sxs-lookup"><span data-stu-id="9f90b-127">Example</span></span>  

 <span data-ttu-id="9f90b-128">Poniższy przykład pokazuje, jak używać `<clear>` elementu przed użyciem `<add>` elementu, aby dodać odbiornik `console` do `Listeners` kolekcji w celu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9f90b-128">The following example shows how to use the `<clear>` element before using the `<add>` element to add the listener `console` to the `Listeners` collection for trace.</span></span>  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <clear/>  
        <add name="console"
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"
            initializeData="Error" />  
        </add>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a><span data-ttu-id="9f90b-129">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9f90b-129">See also</span></span>

- <xref:System.Diagnostics.Trace.Listeners%2A>
- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.TraceSource>
- [<span data-ttu-id="9f90b-130">Schemat ustawień śledzenia i debugowania</span><span class="sxs-lookup"><span data-stu-id="9f90b-130">Trace and Debug Settings Schema</span></span>](index.md)
- [\<remove>](remove-element-for-listeners-for-trace.md)
- [<span data-ttu-id="9f90b-131">Obiekty nasłuchujące śledzenia</span><span class="sxs-lookup"><span data-stu-id="9f90b-131">Trace Listeners</span></span>](../../../debug-trace-profile/trace-listeners.md)
