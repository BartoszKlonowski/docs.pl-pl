---
title: Adoptowanie programu Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 49ba71e2-9468-4082-84c5-cf8daf95e34a
ms.openlocfilehash: 40a2eac1e282640f0df70a7eca16e3b2401c0764
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546011"
---
# <a name="adopt-windows-communication-foundation"></a>Przyjmowanie Windows Communication Foundation

Przy użyciu programu Windows Communication Foundation (WCF) można korzystać z nowego programowania, jednocześnie utrzymując istniejące aplikacje opracowane za pomocą ASP.NET. Ponieważ WCF jest to najbardziej odpowiedni wybór w celu ułatwienia komunikacji z aplikacjami skompilowanymi przy użyciu .NET Framework w dowolnym scenariuszu, może służyć jako standardowe narzędzie do rozwiązywania różnorodnych problemów z komunikacją w taki sposób, że ASP.NET nie.

Nowe aplikacje WCF można wdrożyć na tych samych komputerach, co istniejące usługi sieci Web ASP.NET. Jeśli istniejące usługi sieci Web ASP.NET używają wersji .NET Framework starszej niż 2,0, można użyć narzędzia rejestracji programu ASP.NET IIS, aby selektywnie wdrożyć .NET Framework 2,0 w aplikacjach IIS, w których mają być hostowane nowe aplikacje WCF. To narzędzie jest udokumentowane w [ASP.NET narzędzia rejestracji programu IIS (Aspnet_regiis.exe)](/previous-versions/dotnet/netframework-3.5/k6h9cz8h(v=vs.90))i ma interfejs użytkownika wbudowany w konsolę zarządzania usług IIS 6,0.

Programu WCF można użyć do dodawania nowych funkcji do istniejących usług sieci Web ASP.NET przez dodanie usług WCF skonfigurowanych do uruchamiania w trybie zgodności ASP.NET do istniejących aplikacji usługi sieci Web ASP.NET w usługach IIS. Ze względu na tryb zgodności ASP.NET, kod dla nowych usług WCF ma dostęp do tych samych informacji o stanie aplikacji, co istniejący kod ASP.NET, przy użyciu <xref:System.Web.HttpContext> klasy. Aplikacje mogą również współużytkować te same biblioteki klas.

Klienci programu WCF mogą korzystać z usług sieci Web ASP.NET. Usługi WCF skonfigurowane przy użyciu programu <xref:System.ServiceModel.BasicHttpBinding> mogą być używane przez klientów usługi sieci Web ASP.NET. Usługi sieci Web ASP.NET mogą współistnieć z aplikacjami WCF, a funkcja WCF może być nawet używana do dodawania funkcji do istniejących usług sieci Web ASP.NET. Ze względu na wszystkie te sposoby, w których można używać usług sieci Web WCF i ASP.NET, można migrować usługi sieci Web ASP.NET do WCF tylko wtedy, gdy wymagane są funkcje udostępniane przez program WCF, a nie ASP.NET usług sieci Web.

Nawet w kilku przypadkach, gdy jest to konieczne, migrowanie kodu z jednej technologii do innej jest rzadko poprawnym rozwiązaniem. Przyczyną przyjęcia nowej technologii jest spełnienie nowych wymagań, które nie mogą zostać spełnione przy użyciu wcześniejszej technologii, a w takim przypadku należy zaprojektować nowe rozwiązanie w celu spełnienia nowo rozwiniętego zestawu wymagań. Nowy projekt korzyści ze środowiska pracy z istniejącym systemem i od mądry uzyskanych od momentu zaprojektowania tego systemu. Nowy projekt może również używać pełnych możliwości nowych technologii zamiast odtwarzania starego projektu na nowej platformie. Po prototypie najważniejszych elementów nowego projektu, łatwiej będzie ponownie wykorzystać kod z istniejącego systemu w nowym.

## <a name="see-also"></a>Zobacz także

- [Instrukcje: pobieranie metadanych i implementowanie zgodnej usługi](how-to-retrieve-metadata-and-implement-a-compliant-service.md)
