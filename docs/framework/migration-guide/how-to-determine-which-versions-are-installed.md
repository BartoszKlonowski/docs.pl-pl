---
title: Określanie, które wersje programu .NET Framework są zainstalowane
description: Użyj kodu, regedit.exe lub programu PowerShell, aby wykryć, które wersje .NET Framework są zainstalowane na komputerze, badając rejestr systemu Windows.
ms.date: 02/03/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining version
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
ms.openlocfilehash: b4c5b6911a4be4f9ac156b600646c649549f88f8
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438139"
---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a>Instrukcje: Określanie, które wersje .NET Framework są zainstalowane

Użytkownicy mogą [instalować](../install/index.md) i uruchamiać wiele wersji .NET Framework na swoich komputerach. Podczas opracowywania lub wdrażania aplikacji może być konieczne, aby wiedzieć, które wersje .NET Framework są zainstalowane na komputerze użytkownika. Rejestr zawiera listę wersji .NET Framework zainstalowanych na komputerze.

.NET Framework składa się z dwóch głównych składników, które są osobno dla wersji:

- Zestaw zestawów, które są kolekcjami typów i zasobów zapewniających funkcje dla aplikacji. .NET Framework i zestawy mają ten sam numer wersji. Na przykład .NET Framework wersje obejmują 4,5, 4.6.1 i 4.7.2.

- Środowisko uruchomieniowe języka wspólnego (CLR), które zarządza kodem aplikacji i go wykonuje. Jedna wersja środowiska CLR obsługuje zazwyczaj wiele wersji .NET Framework. Na przykład środowisko CLR w wersji 4.0.30319. *XXXXX* , gdzie *XXXXX* jest mniejszy niż 42000, obsługuje .NET Framework wersji 4 do 4.5.2. Wersja środowiska CLR o wartości większej lub równej 4.0.30319.42000 obsługuje wersje .NET Framework począwszy od .NET Framework 4,6.

Narzędzia obsługiwane przez społeczność są dostępne, aby pomóc w wykrywaniu, które wersje .NET Framework są zainstalowane:

- [https://github.com/jmalarcon/DotNetVersions](https://github.com/jmalarcon/DotNetVersions)

  Narzędzie wiersza polecenia .NET Framework 2,0.

- [https://github.com/EliteLoser/DotNetVersionLister](https://github.com/EliteLoser/DotNetVersionLister)

  Moduł programu PowerShell 2,0.

Aby uzyskać informacje dotyczące wykrywania zainstalowanych aktualizacji dla każdej wersji .NET Framework, zobacz [How to: Określanie, które aktualizacje .NET Framework są zainstalowane](how-to-determine-which-net-framework-updates-are-installed.md).

## <a name="detect-net-framework-45-and-later-versions"></a>Wykryj .NET Framework 4,5 i nowsze wersje

Wersja .NET Framework (4,5 lub nowsza) zainstalowana na komputerze jest wymieniona w rejestrze w **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ NET Framework Setup \\ NDP \\ v4 \\**. Jeśli brakuje **pełnego** podklucza, to .NET Framework 4,5 lub nowsze nie są zainstalowane.

> [!NOTE]
> Podklucz **instalacji programu .NET Framework** w ścieżce rejestru *nie* zaczyna się od kropki.

Wartość REG_DWORD **wydania** w rejestrze reprezentuje wersję zainstalowanej .NET Framework.

<a name="version_table"></a>

| Wersja programu .NET Framework | Wartość **wydania** |
| ---------------------- | -------------------------- |
| .NET Framework 4.5     | Wszystkie systemy operacyjne Windows: 378389 |
| .NET Framework 4.5.1   | W systemach Windows 8.1 i Windows Server 2012 R2:378675<br />We wszystkich innych systemach operacyjnych Windows: 378758 |
| .NET Framework 4.5.2   | Wszystkie systemy operacyjne Windows: 379893 |
| Program .NET Framework 4.6     | W systemie Windows 10:393295<br />We wszystkich innych systemach operacyjnych Windows: 393297 |
| .NET Framework 4.6.1   | W systemach aktualizacji systemu Windows 10 listopad: 394254<br />We wszystkich innych systemach operacyjnych Windows (w tym Windows 10): 394271 |
| .NET Framework 4.6.2   | W rocznicowej aktualizacji systemu Windows 10 i Windows Server 2016:394802<br />Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 394806 |
|  .NET Framework 4.7     | Aktualizacja systemu Windows 10 dla twórców: 460798<br />Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 460805 |
| .NET Framework 4.7.1   | W przypadku aktualizacji systemu Windows 10 dla twórców i systemu Windows Server w wersji 1709:461308<br/>Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 461310 |
|  .NET Framework 4.7.2   | W systemie Windows 10 kwiecień 2018 Update i Windows Server w wersji 1803:461808<br/>We wszystkich systemach operacyjnych Windows innych niż Windows 10 kwiecień 2018 Update i Windows Server w wersji 1803:461814 |
|  .NET Framework 4.8     | W systemie Windows 10 maja 2019 Update i aktualizacja Windows 10 listopad 2019:528040<br/>Aktualizacje systemu Windows 10 maja 2020 Update i Windows 10 października 2020:528372<br/>Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 528049 |

### <a name="minimum-version"></a>Minimalna wersja

Aby określić, czy jest dostępna *minimalna* wersja .NET Framework, sprawdź, czy wartość **wydania** REG_DWORD, która jest większa lub równa odpowiadającej wartości wymienionej w poniższej tabeli. Na przykład, jeśli aplikacja działa w .NET Framework 4,8 lub nowszej wersji, należy sprawdzić, czy w **wersji** REG_DWORD wartość jest *większa niż lub równa* 528040.

| Wersja programu .NET Framework | Wartość minimalna |
| ---------------------- | ------------- |
| .NET Framework 4.5     | 378389 |
| .NET Framework 4.5.1   | 378675 |
| .NET Framework 4.5.2   | 379893 |
| Program .NET Framework 4.6     | 393295 |
| .NET Framework 4.6.1   | 394254 |
| .NET Framework 4.6.2   | 394802 |
|  .NET Framework 4.7     | 460798 |
| .NET Framework 4.7.1   | 461308 |
|  .NET Framework 4.7.2   | 461808 |
|  .NET Framework 4.8     | 528040 |

### <a name="use-registry-editor"></a>Korzystanie z edytora rejestru

01. Z menu **Start** wybierz polecenie **Uruchom**, wpisz polecenie *regedit*, a następnie wybierz przycisk **OK**.

   (Musisz mieć poświadczenia administracyjne, aby uruchomić regedit).

01. W Edytorze rejestru Otwórz następujący podklucz: **HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\**. Jeśli **pełny** podklucz nie jest obecny, nie masz zainstalowanego .NET Framework 4,5 lub nowszego.

01. Sprawdź, czy REG_DWORD wpis o nazwie **Release**. Jeśli istnieje, jest zainstalowana .NET Framework 4,5 lub nowsza. Jego wartość odnosi się do określonej wersji .NET Framework. Na przykład, wartość wpisu **zlecenia** to 528040, który jest kluczem wydania dla .NET Framework 4,8.

   ![Wpis rejestru dla .NET Framework 4,5](./media/clr-installdir.png )

### <a name="use-powershell-to-check-for-a-minimum-version"></a>Sprawdzanie minimalnej wersji przy użyciu programu PowerShell

Użyj poleceń programu PowerShell, aby sprawdzić wartość wpisu **Release** w **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ NET Framework Setup \\ NDP \\ v4 \\ Full** podklucza.

W poniższych przykładach Sprawdź wartość wpisu **Zwolnij** , aby określić, czy .NET Framework 4.6.2 czy nowsza. Ten kod zwraca `True` , jeśli jest zainstalowany i `False` w przeciwnym razie.

```powershell
(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
```

### <a name="query-the-registry-using-code"></a>Tworzenie zapytań dotyczących rejestru przy użyciu kodu

01. Użyj <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> metod i, <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> Aby uzyskać dostęp do **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\** w rejestrze systemu Windows.

    > [!IMPORTANT]
    > Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej. Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** . Na przykład podklucz rejestru dla .NET Framework 4,5 to **HKEY_LOCAL_MACHINE \\ Software \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Full**.

01. Sprawdź wartość REG_DWORD **wydania** , aby określić zainstalowaną wersję. Aby można było przesłać dalej, sprawdź, czy wartość jest większa niż lub równa wartości wymienionej w [tabeli wersji .NET Framework](#version_table).

Poniższy przykład sprawdza wartość wpisu **Release** w rejestrze, aby znaleźć zainstalowane wersje .NET Framework 4.5-4.8:

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="2":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="2":::

Przykład wyświetla dane wyjściowe podobne do następujących:

```output
.NET Framework Version: 4.6.1
```

Ten przykład jest zgodny z zalecaną metodą sprawdzania wersji:

- Sprawdza, czy wartość wpisu **wydania** jest *większa niż lub równa* wartości znanych kluczy wydania.
- Sprawdza w kolejności od najnowszej wersji do najwcześniejszej wersji.

## <a name="detect-net-framework-10-through-40"></a>Wykryj .NET Framework 1,0 do 4,0

Każda wersja .NET Framework od 1,1 do 4,0 jest wyświetlana jako podklucz w **HKEY_LOCAL_MACHINE \\ oprogramowaniu \\ Microsoft \\ .NET Framework Setup \\ NDP**. Poniższa tabela zawiera listę ścieżek do poszczególnych wersji .NET Framework. W przypadku większości wersji **istnieje REG_DWORD wartość** , aby wskazać, że `1` Ta wersja jest zainstalowana. W tych podkluczach istnieje również **wersja** REG_SZ wartość, która zawiera ciąg wersji.

> [!NOTE]
> Podklucz **instalacji programu .NET Framework** w ścieżce rejestru *nie* zaczyna się od kropki.

| Wersja struktury  | Podklucz rejestru | Wartość |
| ------------------ | --------------- | ----- |
| 1,0                | **HKLM \\ oprogramowanie \\ Microsoft \\ . NETFramework \\ Policy \\ v 1.0 \\ 3705**     | **Zainstaluj** program REG_SZ równa się `1` |
| 1,1                | **HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 1.1.4322**   | **Zainstaluj** program REG_DWORD równa się `1` |
| 2,0                | **HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 2.0.50727**  | **Zainstaluj** program REG_DWORD równa się `1` |
| 3.0                | **HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.0 \\ Setup** | **InstallSuccess** REG_DWORD równa się `1` |
| 3,5                | **HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**        | **Zainstaluj** program REG_DWORD równa się `1` |
| 4,0 profil klienta | **HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Client**  | **Zainstaluj** program REG_DWORD równa się `1` |
| pełny profil 4,0   | **HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Full**    | **Zainstaluj** program REG_DWORD równa się `1` |

> [!IMPORTANT]
> Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej. Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** . Na przykład podklucz rejestru dla .NET Framework 3,5 jest **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**.

Zwróć uwagę, że ścieżka rejestru do podklucza .NET Framework 1,0 różni się od innych.

### <a name="use-registry-editor-older-framework-versions"></a>Użyj edytora rejestru (starsze wersje Framework)

01. Z menu **Start** wybierz polecenie **Uruchom**, wpisz polecenie *regedit*, a następnie wybierz przycisk **OK**.

    Musisz mieć poświadczenia administracyjne, aby uruchomić regedit.

01. Otwórz podklucz pasujący do wersji, którą chcesz sprawdzić. Skorzystaj z tabeli w sekcji [wykrywanie .NET Framework 1,0 do 4,0](#detect-net-framework-10-through-40) .

    Na poniższej ilustracji przedstawiono podklucz i jego wartość **wersji** dla .NET Framework 3,5.

    ![Wpis rejestru dla .NET Framework 3,5.](./media/net-4-and-earlier.png ".NET Framework 3,5 i wcześniejsze wersje")

### <a name="query-the-registry-using-code-older-framework-versions"></a>Wykonywanie zapytania dotyczącego rejestru przy użyciu kodu (starsze wersje Framework)

Użyj <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> klasy, aby uzyskać HKEY_LOCAL_MACHINE dostęp do podklucza **\\ \\ NDP oprogramowania Microsoft \\ .NET Framework Instalatora \\** w rejestrze systemu Windows.

> [!IMPORTANT]
> Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej. Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** . Na przykład podklucz rejestru dla .NET Framework 3,5 jest **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**.

Poniższy przykład umożliwia znalezienie zainstalowanych wersji .NET Framework 1-4:

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="1":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="1":::

W przykładzie przedstawiono dane wyjściowe podobne do następujących:

```output
v2.0.50727  2.0.50727.4927  SP2
v3.0  3.0.30729.4926  SP2
v3.5  3.5.30729.4926  SP1
v4.0
  Client  4.0.0.0
```

## <a name="find-clr-versions"></a>Znajdź wersje środowiska CLR

.NET Framework środowisko CLR zainstalowane z .NET Framework jest używane oddzielnie. Istnieją dwa sposoby wykrywania wersji .NET Framework CLR:

- **Narzędzie Clrver.exe**

  Użyj [Narzędzia wersji środowiska CLR (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) , aby określić, które wersje środowiska CLR są zainstalowane na komputerze. Otwórz [wiersz polecenia dla deweloperów dla programu Visual Studio](../tools/developer-command-prompt-for-vs.md) i wprowadź `clrver` .

  Przykładowe dane wyjściowe:

  ```console
  Versions installed on the machine:
  v2.0.50727
  v4.0.30319
  ```

- **`Environment`Klasa**

  > [!IMPORTANT]
  > W przypadku .NET Framework 4,5 i nowszych wersji nie należy używać <xref:System.Environment.Version%2A?displayProperty=nameWithType> właściwości do wykrywania wersji środowiska CLR. Zamiast tego należy wykonać zapytanie dotyczące rejestru zgodnie z opisem w artykule [wykrywanie .NET Framework 4,5 i nowszych wersji](#detect-net-framework-45-and-later-versions).

  1. Zbadaj <xref:System.Environment.Version?displayProperty=nameWithType> Właściwość w celu pobrania <xref:System.Version> obiektu.

     Zwrócony `System.Version` obiekt identyfikuje wersję środowiska uruchomieniowego, które aktualnie wykonuje kod. Nie zwraca wersji zestawu ani innych wersji środowiska uruchomieniowego, które mogły zostać zainstalowane na komputerze.

     W przypadku .NET Framework w wersji 4, 4,5, 4.5.1 i 4.5.2 ciąg reprezentujący zwracanego <xref:System.Version> obiektu ma postać 4.0.30319.*XXXXX*, gdzie *XXXXX* jest mniejszy niż 42000. W przypadku .NET Framework 4,6 i nowszych wersje ma postać 4.0.30319.42000.

  1. Po utworzeniu obiektu **wersji** wykonaj zapytanie w następujący sposób:

     - Aby uzyskać informacje o głównym identyfikatorze wydania (na przykład *4* dla wersji 4,0), użyj <xref:System.Version.Major%2A?displayProperty=nameWithType> właściwości.

     - W przypadku pomocniczego identyfikatora wydania (na przykład *0* w przypadku wersji 4,0) należy użyć <xref:System.Version.Minor%2A?displayProperty=nameWithType> właściwości.

     - Dla całego ciągu wersji (na przykład *4.0.30319.18010*) Użyj <xref:System.Version.ToString%2A?displayProperty=nameWithType> metody. Ta metoda zwraca pojedynczą wartość odzwierciedlającą wersję środowiska uruchomieniowego, które wykonuje kod. Nie zwraca wersji zestawu ani innych wersji środowiska uruchomieniowego, które mogą być zainstalowane na komputerze.

  W poniższym przykładzie zastosowano <xref:System.Environment.Version%2A?displayProperty=nameWithType> Właściwość w celu pobrania informacji o wersji środowiska CLR:

  ```csharp
  Console.WriteLine($"Version: {Environment.Version}");
  ```

  ```vb
  Console.WriteLine($"Version: {Environment.Version}")
  ```

  W przykładzie przedstawiono dane wyjściowe podobne do następujących:

  ```output
  Version: 4.0.30319.18010
  ```

## <a name="see-also"></a>Zobacz także

- [Instrukcje: Określanie, które aktualizacje .NET Framework są zainstalowane](how-to-determine-which-net-framework-updates-are-installed.md)
- [Zainstaluj .NET Framework dla deweloperów](../install/guide-for-developers.md)
- [.NET Framework wersje i zależności](versions-and-dependencies.md)
