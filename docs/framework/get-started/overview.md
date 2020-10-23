---
title: Omówienie platformy .NET Framework
description: Zapoznaj się z omówieniem .NET Framework, który jest technologią, która obsługuje Kompilowanie i uruchamianie aplikacji systemu Windows i usług sieci Web.
ms.date: 10/21/2020
helpviewer_keywords:
- application development [.NET Framework]
- common language runtime
- common language runtime, about
- common language runtime, overview
ms.assetid: 29848c96-fc36-462d-8072-ba223a40b697
ms.openlocfilehash: 75b2e94b93eabdbf8a6a40f38c1b12a8caddd98a
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471747"
---
# <a name="overview-of-net-framework"></a>Omówienie platformy .NET Framework

.NET Framework to technologia, która obsługuje tworzenie i uruchamianie aplikacji i usług sieci Web systemu Windows. .NET Framework zaprojektowano w celu spełnienia następujących celów:

- Zapewnianie spójnego, zorientowanego obiektowo środowiska programowania, niezależnie od tego, czy kod obiektu jest przechowywany i wykonywany lokalnie, wykonywany lokalnie, ale w sieci Web, czy wykonywany zdalnie.

- Podaj środowisko wykonywania kodu, które:

  - Minimalizuje konflikty wdrażania oprogramowania i przechowywania wersji.

  - Promuje bezpieczne wykonywanie kodu, w tym kod utworzony przez nieznaną lub częściowo zaufaną stronę trzecią.

  - Eliminuje problemy z wydajnością w środowiskach ze skryptami lub interpretowane.

- Zapewniaj spójność dla deweloperów w różnych typach aplikacji, takich jak aplikacje oparte na systemie Windows i aplikacje oparte na sieci Web.

- Kompiluj całą komunikację z normami branżowymi, aby upewnić się, że kod oparty na .NET Framework integruje się z jakimkolwiek innym kodem.

[!INCLUDE [net-framework-future](../../../includes/net-framework-future.md)]

.NET Framework składa się ze środowiska uruchomieniowego języka wspólnego (CLR) i biblioteki klas .NET Framework. Środowisko uruchomieniowe języka wspólnego jest podstawą .NET Framework. Należy traktować środowisko uruchomieniowe jako agenta, który zarządza kodem w czasie wykonywania, zapewniającym podstawowe usługi, takie jak zarządzanie pamięcią, zarządzanie wątkami i komunikacja zdalna, a także wymuszanie ścisłego bezpieczeństwa typów i inne formy dokładności kodu, które promują bezpieczeństwo i niezawodność. W rzeczywistości koncepcja zarządzania kodem jest podstawową zasadą środowiska uruchomieniowego. Kod przeznaczony dla środowiska uruchomieniowego jest znany jako kod zarządzany, podczas gdy kod, który nie jest celem środowiska uruchomieniowego, jest znany jako kod niezarządzany. Biblioteka klas to kompleksowa, zorientowana obiektowo Kolekcja typów wielokrotnego użytku, które służą do opracowywania aplikacji w oparciu o tradycyjne aplikacje wiersza polecenia lub graficznego interfejsu użytkownika (GUI) do aplikacji na podstawie najnowszych innowacji zapewnianych przez ASP.NET, takich jak formularze sieci Web i usługi sieci Web XML.

.NET Framework mogą być hostowane przez niezarządzane składniki, które ładują środowisko uruchomieniowe języka wspólnego do swoich procesów i inicjują wykonywanie kodu zarządzanego, tworząc w ten sposób środowisko oprogramowania korzystające z funkcji zarządzanych i niezarządzanych. Program .NET Framework nie tylko zawiera kilka hostów środowiska uruchomieniowego, ale również obsługuje opracowywanie hostów środowiska uruchomieniowego innych firm.

Na przykład ASP.NET hostuje środowisko uruchomieniowe w celu zapewnienia skalowalnego środowiska po stronie serwera dla kodu zarządzanego. ASP.NET działa bezpośrednio w środowisku uruchomieniowym w celu włączenia aplikacji ASP.NET i usług sieci Web XML, które zostały omówione w dalszej części tego artykułu.

Internet Explorer to przykład niezarządzanej aplikacji, która hostuje środowisko uruchomieniowe (w postaci rozszerzenia typu MIME). Korzystanie z programu Internet Explorer do hostowania środowiska uruchomieniowego umożliwia osadzanie składników zarządzanych lub formantów Windows Forms w dokumentach HTML. Hosting środowiska uruchomieniowego w ten sposób sprawia, że zarządzany kod mobilny jest możliwy, ale z znaczącymi ulepszeniami, które są dostępne tylko w przypadku ofert z kodem zarządzanym, takich jak wykonywanie częściowo zaufane i izolowany magazyn plików.

Na poniższej ilustracji przedstawiono relacje środowiska uruchomieniowego języka wspólnego i biblioteki klas z aplikacjami oraz do całego systemu. Ilustracja pokazuje również, jak kod zarządzany działa w ramach większej architektury.

![Zrzut ekranu pokazujący, jak kod zarządzany działa w ramach większej architektury.](./media/overview/language-runtime-class-library-relationship.gif)

W poniższych sekcjach opisano najważniejsze funkcje .NET Framework bardziej szczegółowo.

## <a name="features-of-the-common-language-runtime"></a>Funkcje środowiska uruchomieniowego języka wspólnego

Środowisko uruchomieniowe języka wspólnego zarządza pamięcią, wykonywaniem wątków, wykonywaniem kodu, weryfikacją bezpieczeństwa kodu, kompilacją i innymi usługami systemowymi. Te funkcje są wewnętrzne dla kodu zarządzanego, który jest uruchamiany w środowisku uruchomieniowym języka wspólnego.

W odniesieniu do zabezpieczeń zarządzane składniki są przyznawane różnym stopniu zaufania, w zależności od różnych czynników, które obejmują ich źródła (takie jak Internet, Sieć przedsiębiorstwa lub komputer lokalny). Oznacza to, że zarządzany składnik może lub może nie być w stanie wykonywać operacji dostępu do plików, operacji dostępu do rejestru ani innych poufnych funkcji, nawet jeśli jest używany w tej samej aktywnej aplikacji.

Środowisko uruchomieniowe wymusza również niezawodność kodu przez implementację infrastruktury ścisłej weryfikacji typu i kodu o nazwie system typu wspólnego (CTS). CTS gwarantuje, że cały kod zarządzany jest własny opis. Różne kompilatory języka firmy Microsoft i innych firm generują kod zarządzany, który jest zgodny z CTS. Oznacza to, że kod zarządzany może zużywać inne zarządzane typy i wystąpienia, jednocześnie jednocześnie wymuszające wierność i bezpieczeństwo typów.

Ponadto zarządzane środowisko uruchomieniowe programu eliminuje wiele typowych problemów z oprogramowaniem. Na przykład środowisko uruchomieniowe automatycznie obsługuje układ obiektu i zarządza odwołaniami do obiektów, zwalniając je, gdy nie są już używane. To automatyczne zarządzanie pamięcią rozwiązuje dwa najczęstsze błędy aplikacji, przecieki pamięci i nieprawidłowe odwołania do pamięci.

Środowisko uruchomieniowe przyspiesza również produktywność deweloperów. Na przykład programiści piszą aplikacje w ich języku programistycznym, ale w pełni wykorzystują środowisko uruchomieniowe, bibliotekę klas oraz składniki pisane w innych językach przez innych deweloperów. Każdy dostawca kompilatora, który wybiera cel środowiska uruchomieniowego, może to zrobić. Kompilatory języka, które są przeznaczone dla .NET Framework sprawiają, że funkcje .NET Framework są dostępne dla istniejącego kodu pisanego w tym języku, znacznie przyspieszają proces migracji istniejących aplikacji.

Środowisko uruchomieniowe jest przeznaczone dla oprogramowania w przyszłości, ale również obsługuje oprogramowanie z dzisiaj i wczoraj. Współdziałanie między kodem zarządzanym i niezarządzanym pozwala deweloperom nadal korzystać z niezbędnych składników COM i bibliotek DLL.

Środowisko uruchomieniowe zostało zaprojektowane w celu zwiększenia wydajności. Chociaż środowisko uruchomieniowe języka wspólnego udostępnia wiele standardowych usług czasu wykonywania, kod zarządzany nigdy nie jest interpretowany. Funkcja, która nazywa kompilację just-in-Time (JIT), umożliwia uruchamianie całego kodu zarządzanego w języku macierzystym systemu, w którym jest wykonywane. W tym czasie Menedżer pamięci usuwa możliwości fragmentacji pamięci i zwiększa ilość pamięci w odwołaniu, aby zwiększyć wydajność.

Na koniec środowisko uruchomieniowe może być hostowane przez aplikacje po stronie serwera, takie jak Microsoft SQL Server i Internet Information Services (IIS). Ta infrastruktura umożliwia korzystanie z kodu zarządzanego do pisania logiki biznesowej, przy jednoczesnym zachowaniu najwyższej wydajności najlepszych serwerów przedsiębiorstwa, które obsługują hosting w czasie wykonywania.

## <a name="net-framework-class-library"></a>Biblioteka klas programu .NET Framework

Biblioteka klas .NET Framework jest kolekcją typów wielokrotnego użytku, które są ściśle zintegrowane ze środowiskiem uruchomieniowym języka wspólnego. Biblioteka klas jest zorientowana obiektowo, dostarczając typy, z których pochodzi własny kod zarządzany. To nie tylko ułatwia używanie typów .NET Framework, ale również skraca czas związany z uczeniem nowych funkcji .NET Framework. Ponadto składniki innych firm integrują się bezproblemowo z klasami w .NET Framework.

Na przykład klasy kolekcji .NET Framework implementują zestaw interfejsów do tworzenia własnych klas kolekcji. Klasy kolekcji mieszają się bezproblemowo z klasami w .NET Framework.

Zgodnie z oczekiwaniami z biblioteki klas zorientowanej obiektowo typy .NET Framework umożliwiają wykonywanie wielu typowych zadań programistycznych, takich jak zarządzanie ciągami, zbieranie danych, łączność z bazami danych i dostęp do plików. Oprócz tych typowych zadań Biblioteka klas zawiera typy, które obsługują różne wyspecjalizowane scenariusze programistyczne. Za pomocą .NET Framework można opracowywać następujące typy aplikacji i usług:

- Aplikacje konsolowe. Zobacz [Kompilowanie aplikacji konsolowych](../../standard/building-console-apps.md).

- Aplikacje GUI systemu Windows (Windows Forms). Zobacz [Windows Forms](/dotnet/desktop/winforms/).

- Aplikacje Windows Presentation Foundation (WPF). Zobacz [Windows Presentation Foundation](/dotnet/desktop/wpf/).

- Aplikacje ASP.NET. Zobacz [aplikacje sieci Web za pomocą ASP.NET](../develop-web-apps-with-aspnet.md).

- Usługi systemu Windows. Zobacz [wprowadzenie do aplikacji usług systemu Windows](../windows-services/introduction-to-windows-service-applications.md).

- Aplikacje zorientowane na usługę korzystające z Windows Communication Foundation (WCF). Zobacz [aplikacje zorientowane na usługę za pomocą programu WCF](../wcf/index.md).

- Aplikacje obsługujące przepływy pracy korzystające z Windows Workflow Foundation (WF). Zobacz [Windows Workflow Foundation](../windows-workflow-foundation/index.md).

Klasy Windows Forms to kompleksowy zestaw typów wielokrotnego użytku, które znacznie upraszczają tworzenie interfejsu GUI systemu Windows. Jeśli piszesz aplikację formularza sieci Web ASP.NET, możesz użyć klas formularzy sieci Web.

## <a name="see-also"></a>Zobacz też

- [Wymagania systemowe](system-requirements.md)
- [Przewodnik instalacji](../install/index.md)
- [Podręcznik programowania](../development-guide.md)
- [Narzędzia](../tools/index.md)
- [Przykłady i samouczki dotyczące platformy .NET](../../samples-and-tutorials/index.md)
- [Przeglądarka interfejsów API platformy .NET](../../../api/index.md)
