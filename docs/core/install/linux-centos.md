---
title: Instalowanie platformy .NET w systemie CentOS — .NET
description: Przedstawiono różne sposoby instalowania zestawu .NET SDK i środowiska uruchomieniowego .NET w systemie CentOS.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.openlocfilehash: b2ed62d024c6f0d78a4ec64693f1dafeabd8f47b
ms.sourcegitcommit: c38bf879a2611ff46aacdd529b9f2725f93e18a9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "94594635"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-centos"></a>Zainstaluj zestaw .NET SDK lub środowisko uruchomieniowe .NET w systemie CentOS

Platforma .NET jest obsługiwana w systemie CentOS. W tym artykule opisano sposób instalowania programu .NET w systemie CentOS.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a>Obsługiwane dystrybucje

Poniższa tabela zawiera listę obecnie obsługiwanych wersji platformy .NET w systemach CentOS 7 i CentOS 8. Te wersje pozostają obsługiwane, dopóki wersja [platformy .NET nie osiągnie końca obsługi](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) lub wersja CentOS nie jest już obsługiwana.

- ✔️ wskazuje, że wersja programu CentOS lub .NET jest nadal obsługiwana.
- ❌Wskazuje, że wersja programu CentOS lub .NET nie jest obsługiwana w tej wersji CentOS.
- Gdy wersja programu CentOS i wersja platformy .NET mają ✔️, obsługiwane są kombinacje systemów operacyjnych i .NET.

| CentOS                   | .NET Core 2.1 | .NET Core 3,1 | .NET 5,0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](#centos-8-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [7](#centos-7-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Następujące wersje platformy .NET nie są już obsługiwane. Pliki do pobrania dla tych nadal są publikowane:

- 3.0
- 2.2
- 2,0

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="how-to-install-other-versions"></a>Jak zainstalować inne wersje

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="centos-8-"></a>CentOS 8 ✔️

> [!TIP]
> Program .NET 5,0 nie jest jeszcze dostępny w repozytoriach pakietów domyślnych, ale .NET Core 3,1 to. Aby zainstalować program .NET Core 3,1, użyj `dnf install` polecenia z odpowiednim pakietem, takim jak `aspnetcore-runtime-3.1` lub `dotnet-sdk-3.1` . Poniższe instrukcje dotyczą programu .NET 5,0.

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/8/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-dnf-install-50](includes/linux-install-50-dnf.md)]

## <a name="centos-7-"></a>CentOS ✔️ 7

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-50](includes/linux-install-50-yum.md)]

## <a name="troubleshoot-the-package-manager"></a>Rozwiązywanie problemów z menedżerem pakietów

Ta sekcja zawiera informacje o typowych błędach, które mogą wystąpić podczas instalowania programu .NET przy użyciu Menedżera pakietów.

### <a name="unable-to-find-package"></a>Nie można znaleźć pakietu

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

### <a name="failed-to-fetch"></a>Nie można pobrać

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a>Przystawki

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a>Zależności

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="scripted-install"></a>Instalacja z skryptami

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a>Instalacja ręczna

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a>Następne kroki

- [Samouczek: Tworzenie aplikacji konsolowej za pomocą zestawu .NET SDK przy użyciu Visual Studio Code](../tutorials/with-visual-studio-code.md)
