---
title: Przegląd zabezpieczeń automatyzacji interfejsu użytkownika
description: Zapoznaj się z omówieniem modelu zabezpieczeń automatyzacji interfejsu użytkownika firmy Microsoft. Zrozumienie kontroli konta użytkownika, zadań wymagających wyższych uprawnień i plików manifestu.
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, security model
- security model, UI Automation
ms.assetid: 1d853695-973c-48ae-b382-4132ae702805
ms.openlocfilehash: d483f282db8ce8e5653d6d83361fa44df05f63f5
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163141"
---
# <a name="ui-automation-security-overview"></a>Przegląd zabezpieczeń automatyzacji interfejsu użytkownika

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).

W tym omówieniu opisano model zabezpieczeń programu [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] w systemie Windows Vista.

<a name="User_Account_Control"></a>

## <a name="user-account-control"></a>Kontrola konta użytkownika

Bezpieczeństwo jest głównym fokusem systemu Windows Vista i wśród innowacji jest możliwość, aby użytkownicy mogli uruchamiać jako użytkownicy ze standardem (nie będącymi administratorami) bez konieczności blokowania uruchamiania aplikacji i usług, które wymagają wyższego poziomu uprawnień.

W systemie Windows Vista większość aplikacji jest dostarczana z tokenem standardowym lub administracyjnym. Jeśli aplikacja nie może być zidentyfikowana jako aplikacja administracyjna, domyślnie jest uruchamiana jako aplikacja standardowa. Aby można było uruchomić aplikację zidentyfikowaną jako administracyjna, system Windows Vista monituje użytkownika o zgodę na uruchomienie aplikacji jako podniesienia uprawnień. Monit o zgodę jest domyślnie wyświetlany, nawet jeśli użytkownik jest członkiem lokalnej grupy administratorów, ponieważ Administratorzy są uruchamiani jako użytkownicy standardowi do momentu, gdy aplikacja lub składnik systemowy, który wymaga poświadczeń administracyjnych, żąda uprawnień do uruchomienia.

<a name="Tasks_Requiring_Higher_Privileges"></a>

## <a name="tasks-requiring-higher-privileges"></a>Zadania wymagające wyższych uprawnień

Gdy użytkownik próbuje wykonać zadanie, które wymaga uprawnień administracyjnych, w systemie Windows Vista zostanie wyświetlone okno dialogowe z prośbą o zgodę na kontynuowanie przez użytkownika. To okno dialogowe jest chronione przed procesami komunikacji, dzięki czemu złośliwe oprogramowanie nie może symulować danych wejściowych użytkownika. Podobnie nie można uzyskać dostępu do ekranu logowania pulpitu przez inne procesy.

Klienci automatyzacji interfejsu użytkownika muszą komunikować się z innymi procesami, ale niektóre z nich są prawdopodobnie uruchomione na wyższym poziomie uprawnień. Klienci mogą również potrzebować dostępu do okien dialogowych systemu, które nie są zwykle widoczne dla innych procesów. W związku z tym [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klienci muszą być Zaufani przez system i muszą mieć specjalne uprawnienia.

Aby mieć zaufanie do komunikacji z aplikacjami działającymi na wyższym poziomie uprawnień, aplikacje muszą być podpisane.

<a name="Manifest_Files"></a>

## <a name="manifest-files"></a>Pliki manifestu

Aby uzyskać dostęp do interfejsu użytkownika chronionego systemu, aplikacje muszą być skompilowane przy użyciu pliku manifestu, który zawiera `uiAccess` atrybut w `requestedExecutionLevel` tagu w następujący sposób:

```xml
<trustInfo xmlns="urn:schemas-microsoft-com:asm.v3">
  <security>
    <requestedPrivileges>
      <requestedExecutionLevel
        level="highestAvailable"
        uiAccess="true" />
    </requestedPrivileges>
  </security>
</trustInfo>
```

Wartość `level` atrybutu w tym kodzie jest tylko przykładem.

`uiAccess`Domyślnie ma wartość "false"; oznacza to, że jeśli atrybut zostanie pominięty lub nie ma manifestu dla zestawu, aplikacja nie będzie w stanie uzyskać dostępu do chronionego interfejsu użytkownika.
