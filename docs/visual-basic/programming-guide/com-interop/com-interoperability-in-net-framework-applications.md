---
title: Współdziałanie COM w aplikacjach .NET Framework
ms.date: 07/20/2015
helpviewer_keywords:
- interoperability, COM and .NET Framework objects
- COM interop [Visual Basic]
- shared components
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
ms.openlocfilehash: 377958a21886fe0257633ea19417f9a19bd51ff3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396872"
---
# <a name="com-interoperability-in-net-framework-applications-visual-basic"></a>Współdziałanie COM w aplikacjach .NET Framework (Visual Basic)

Jeśli chcesz używać obiektów COM i .NET Framework obiektów w tej samej aplikacji, musisz rozwiązać różnice w sposobie, w jaki obiekty istnieją w pamięci. Obiekt .NET Framework znajduje się w pamięci zarządzanej — pamięci kontrolowanej przez środowisko uruchomieniowe języka wspólnego — i może być przenoszony przez środowisko uruchomieniowe w razie konieczności. Obiekt COM znajduje się w pamięci niezarządzanej i nie powinien być przenoszony do innej lokalizacji pamięci. Program Visual Studio i .NET Framework udostępniają narzędzia do kontrolowania interakcji z tymi zarządzanymi i niezarządzanymi składnikami. Aby uzyskać więcej informacji o kodzie zarządzanym, zobacz [środowisko uruchomieniowe języka wspólnego](../../../standard/clr.md).

Oprócz używania obiektów COM w aplikacjach .NET, warto również użyć Visual Basic do opracowania obiektów dostępnych z kodu niezarządzanego za pośrednictwem modelu COM.

Linki na tej stronie zawierają szczegóły dotyczące interakcji między obiektami COM i .NET Framework.

## <a name="related-sections"></a>Sekcje pokrewne

| | |
|---------|---------|
| [Międzyoperacyjność modelu COM](index.md) | Zawiera łącza do tematów obejmujących współdziałanie COM w Visual Basic, w tym obiekty COM, formanty ActiveX, biblioteki DLL Win32, obiekty zarządzane i dziedziczenie obiektów COM. |
| [Współdziałanie z kodem niezarządzanym](../../../framework/interop/index.md) | Krótki opis niektórych problemów z interakcją między zarządzanym i niezarządzanym kodem i zawiera linki do dalszych badań. |
| [Otoki COM](../../../standard/native-interop/com-wrappers.md) | Omawia wywoływane otoki środowiska uruchomieniowego, które umożliwiają kodowi zarządzanemu wywoływanie metod COM, i możliwe do wywołania otok COM, które umożliwiają klientom COM wywoływanie metod obiektu .NET. |
| [Zaawansowana współdziałanie COM](../../../framework/interop/index.md) | Zawiera łącza do tematów obejmujących współdziałanie modelu COM w odniesieniu do otok, wyjątków, dziedziczenia, wątkowości, zdarzeń, konwersji i organizowania. |
| [Tlbimp. exe (Importer biblioteki typów)](../../../framework/tools/tlbimp-exe-type-library-importer.md) | Omawia narzędzie, za pomocą którego można skonwertować definicje typów Znalezione w bibliotece typów modelu COM do równoważnych definicji w zestawie środowiska uruchomieniowego języka wspólnego. |
