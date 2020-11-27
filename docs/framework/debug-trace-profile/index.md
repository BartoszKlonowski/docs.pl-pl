---
title: Debugowanie, śledzenie i profilowanie
description: Przeczytaj informacje o debugowaniu, śledzeniu i profilowania w programie .NET. Zobacz artykuły dotyczące debugowania (just-in-Time), śledzenia i Instrumentacji aplikacji oraz nie tylko.
ms.date: 03/30/2017
helpviewer_keywords:
- debugging [.NET Framework]
- .NET Framework application configuration, debugging
- debugging [.NET Framework], .NET Framework application debugging
- troubleshooting applications [.NET Framework], profiling
- application development [.NET Framework], debugging
- .NET Framework application configuration, profiling
- profiling applications
- troubleshooting applications [.NET Framework], debugging
- troubleshooting applications [.NET Framework]
- application development [.NET Framework], profiling
ms.assetid: 4a04863e-2475-46f4-bc3f-3c11510c2a4b
ms.openlocfilehash: 33dd840f4c1421bbff54499af56ab3e147cc694b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272777"
---
# <a name="debugging-tracing-and-profiling"></a>Debugowanie, śledzenie i profilowanie

Aby debugować aplikację .NET Framework, środowisko kompilatora i środowiska uruchomieniowego musi być skonfigurowane tak, aby umożliwić debugerowi dołączenie do aplikacji i tworzenie zarówno symboli, jak i map wierszy, jeśli to możliwe, dla aplikacji i odpowiedniego języka pośredniego firmy Microsoft (MSIL). Po debugowaniu aplikacji zarządzanej można ją profilować w celu zwiększenia wydajności. Profilowanie szacuje i opisuje wiersze kodu źródłowego, które generują najczęściej wykonywany kod, oraz czas ich wykonania.  
  
 Aplikacje .NET Framework są łatwo debugowane przy użyciu programu Visual Studio, który obsługuje wiele szczegółów konfiguracji. Jeśli program Visual Studio nie jest zainstalowany, można przeanalizować i poprawić wydajność aplikacji .NET Framework przy użyciu klas debugowania w <xref:System.Diagnostics> przestrzeni nazw .NET Framework. Ta przestrzeń nazw zawiera <xref:System.Diagnostics.Trace> <xref:System.Diagnostics.Debug> klasy,, i <xref:System.Diagnostics.TraceSource> dla przepływu wykonywania śledzenia oraz <xref:System.Diagnostics.Process> klasy, <xref:System.Diagnostics.EventLog> i <xref:System.Diagnostics.PerformanceCounter> dla profilowania kodu.  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Włączanie debugowania dołączania JIT](enabling-jit-attach-debugging.md)  
 Pokazuje, jak skonfigurować rejestr do JIT — Dołącz aparat debugowania do aplikacji .NET Framework.  
  
 [Ułatwianie debugowania obrazu](making-an-image-easier-to-debug.md)  
 Pokazuje, jak włączyć i zoptymalizować śledzenie JIT, aby ułatwić debugowanie zestawu.  
  
 [Śledzenie i instrumentowanie aplikacji](tracing-and-instrumenting-applications.md)  
 Opisuje, jak monitorować wykonywanie aplikacji w trakcie jej działania oraz jak można przyłączyć ją do wyświetlania, jak to działa, lub czy problem został usunięty.  
  
 [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](diagnosing-errors-with-managed-debugging-assistants.md)  
 Opisuje zarządzane asystentów debugowania (MDA), które są ułatwieniami debugowania, które działają w połączeniu z środowiskiem uruchomieniowym języka wspólnego (CLR) w celu zapewnienia informacji o stanie środowiska uruchomieniowego.  
  
 [Udoskonalanie debugowania za pomocą atrybutów wyświetlania debugera](enhancing-debugging-with-the-debugger-display-attributes.md)  
 Opisuje, w jaki sposób deweloper typu może określić, jaki typ ma wyglądać, gdy zostanie wyświetlony w debugerze.  
  
 [Liczniki wydajności](performance-counters.md)  
 Opisuje liczniki, których można użyć do śledzenia wydajności aplikacji.  
  
## <a name="related-sections"></a>Sekcje pokrewne  

 [Debugowanie aplikacji platformy ASP.NET lub ASP.NET Core w programie Visual Studio](/visualstudio/debugger/how-to-enable-debugging-for-aspnet-applications)  
 Zawiera wymagania wstępne i instrukcje dotyczące debugowania aplikacji ASP.NET podczas tworzenia lub po wdrożeniu.  
  
 [Przewodnik programowania](../development-guide.md)  
 Przewodnik po wszystkich obszarach kluczowych technologii i zadaniach związanych z rozwojem aplikacji, takich jak tworzenie, konfigurowanie, debugowanie, zabezpieczanie i wdrażanie aplikacji, oraz informacje na temat programowania dynamicznego, interoperacyjności, rozszerzalności, zarządzania pamięcią i wątków.
