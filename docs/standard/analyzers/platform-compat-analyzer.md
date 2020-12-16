---
title: Analizator zgodności platformy
description: Analizator Roslyn, który może pomóc w wykrywaniu problemów ze zgodnością platformy w aplikacjach i bibliotekach dla wielu platform.
author: buyaa-n
ms.date: 09/17/2020
ms.openlocfilehash: 427a2d8ae61a82699e5cf0987fcd1c5a45152cac
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97594920"
---
# <a name="platform-compatibility-analyzer"></a>Analizator zgodności platformy

Prawdopodobnie przesłuchasz motto "jeden .NET": pojedynczej, ujednoliconej platformy do tworzenia aplikacji dowolnego typu. Zestaw SDK programu .NET 5,0 zawiera ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin i ML.NET, a także doda obsługę większej liczby platform w czasie. Program .NET 5,0 dokłada starań, aby zapewnić środowisko, w którym nie trzeba mieć powodów dotyczących różnych wersji platformy .NET, ale nie próbuje w pełni abstrakcji bazowego systemu operacyjnego. Nadal będziesz mieć możliwość wywoływania interfejsów API specyficznych dla platformy, na przykład P/Invoke, WinRT lub powiązań Xamarin dla systemów iOS i Android.

Jednak używanie interfejsów API specyficznych dla platformy na składniku oznacza, że kod nie działa już na wszystkich platformach. Potrzebujemy sposobu na wykrycie tego rozwiązania w czasie projektowania, aby deweloperzy mogli uzyskać diagnostykę, gdy przypadkowo używają interfejsów API specyficznych dla platformy. Aby osiągnąć ten cel, w programie .NET 5,0 wprowadzono [analizatora zgodności platformy](../../fundamentals/code-analysis/quality-rules/ca1416.md) i uzupełniające się interfejsy API, które ułatwiają deweloperom identyfikowanie i Używanie interfejsów API specyficznych dla platformy w miarę potrzeb.

Nowe interfejsy API obejmują:

- <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> Dodawanie adnotacji do interfejsów API jako specyficznych dla platformy i <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> Dodawanie adnotacji do interfejsów API jako nieobsługiwanych w określonym systemie operacyjnym. Te atrybuty mogą opcjonalnie zawierać numer wersji i zostały już zastosowane do niektórych interfejsów API specyficznych dla platformy w podstawowych bibliotekach platformy .NET.
- `Is<Platform>()` i `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` metody statyczne w <xref:System.OperatingSystem?displayProperty=nameWithType> klasie w celu bezpiecznego wywoływania interfejsów API specyficznych dla platformy. Na przykład <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> może służyć do ochrony wywołania interfejsu API specyficznego dla systemu Windows, a <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType> () może służyć do ochrony wywołania interfejsu API specyficznego dla systemu Windows. Zapoznaj się z tymi [przykładami](#guard-platform-specific-apis-with-guard-methods) , jak te metody mogą być używane jako osłony odwołań do interfejsów API specyficznych dla platformy.

> [!TIP]
> Analizator zgodności platformy uaktualnia i zastępuje funkcję [odnajdywania problemów między platformami](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) w [analizatorze interfejsu API platformy .NET](../../standard/analyzers/api-analyzer.md).

## <a name="prerequisites"></a>Wymagania wstępne

Analizator zgodności platformy jest jednym z Roslynjących analiz jakości kodu. Począwszy od wersji .NET 5.0 te analizatory są [uwzględnione w zestawie .NET SDK](../../fundamentals/code-analysis/overview.md). Analizator zgodności platformy jest domyślnie włączony tylko w przypadku projektów docelowych `net5.0` lub nowszych. Można [go jednak włączyć](../../fundamentals/code-analysis/quality-rules/ca1416.md#configure-code-to-analyze) dla projektów przeznaczonych dla innych platform.

## <a name="how-the-analyzer-determines-platform-dependency"></a>Jak Analizator określa zależność platformy

- **Nieprzypisany interfejs API** jest uznawany za działający na **wszystkich platformach systemu operacyjnego**.
- Interfejs API oznaczony jako with `[SupportedOSPlatform("platform")]` jest traktowany jako przenośny tylko w określonym systemie operacyjnym `platform` .
  - Ten atrybut można zastosować wiele razy, aby wskazać **obsługę wielu platform** ( `[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]` ).
  - Analizator wyświetli **Ostrzeżenie** , jeśli do interfejsów API specyficznych dla platformy są przywoływane bez odpowiedniego **kontekstu platformy**:
    - **Ostrzega** , jeśli projekt nie jest celem obsługiwanej platformy (na przykład wywołania interfejsu API określonego dla systemu Windows i obiektów docelowych projektu `<TargetFramework>net5.0-ios14.0</TargetFramework>` ).
    - **Ostrzega** , jeśli projekt jest przeznaczony do wielowymiarowego ( `<TargetFramework>net5.0</TargetFramework>` ).
    - **Nie ostrzega** o tym, czy w ramach projektu, który jest przeznaczony dla określonych **platform** (na przykład dla wywołania interfejsu API określonego dla systemu Windows i elementów docelowych projektu), jest przywoływany interfejs API specyficzny dla platformy `<TargetFramework>net5.0-windows</TargetFramework>` .
    - **Nie ostrzega** , jeśli wywołanie interfejsu API specyficzne dla platformy jest chronione przez odpowiednie metody sprawdzania platformy (na przykład `if(OperatingSystem.IsWindows())` ).
    - **Nie ostrzega** , jeśli interfejs API specyficzny dla platformy jest przywoływany z tego samego kontekstu specyficznego dla platformy (**połączenie jest również przypisane** do `[SupportedOSPlatform("platform")` ).
- Interfejs API oznaczony za pomocą `[UnsupportedOSPlatform("platform")]` jest uznawany za nieobsługiwany tylko w określonym systemie operacyjnym, `platform` ale jest obsługiwany przez wszystkie inne platformy.
  - Ten atrybut może być stosowany wiele razy z różnymi platformami, na przykład `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]` .
  - Analizator generuje **Ostrzeżenie** tylko wtedy, gdy `platform` jest skuteczny dla witryny wywołania:
    - **Ostrzega** , jeśli projekt jest przeznaczony dla platformy, która jest przypisana jako nieobsługiwana (na przykład jeśli interfejs API jest przypisany do `[UnsupportedOSPlatform("windows")]` i dla obiektów docelowych lokacji wywołania `<TargetFramework>net5.0-windows</TargetFramework>` ).
    - **Ostrzega** o tym, czy projekt jest przeznaczony do wielowymiarowego i `platform` znajduje się w domyślnej grupie elementów programu [ `<SupportedPlatform>` MSBuild](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) , czy też `platform` jest zawarty ręcznie w `MSBuild` \<SupportedPlatform> grupie Items:

      ```XML
      <ItemGroup>
          <SupportedPlatform Include="platform" />
      </ItemGroup>
      ```

    - **Nie ostrzega** w przypadku kompilowania aplikacji, która nie jest przeznaczona dla nieobsługiwanej platformy lub ma wiele obiektów docelowych, a platforma nie jest uwzględniona w domyślnej grupie elementów programu [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) .
- Oba atrybuty mogą być tworzone z numerami wersji lub bez nich w ramach nazwy platformy.
  - Numery wersji są `major.minor[.build[.revision]]` `major.minor` wymagane, a `build` `revision` części i są opcjonalne. Na przykład "system Windows 7.0" wskazuje system Windows w wersji 7,0, ale "Windows" jest interpretowany jako Windows 0,0.

Aby uzyskać więcej informacji, zobacz [przykłady działania atrybutów i ich przyczyny](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).

### <a name="advanced-scenarios-for-combining-attributes"></a>Zaawansowane scenariusze łączenia atrybutów

- Jeśli istnieją kombinacje `[SupportedOSPlatform]` i `[UnsupportedOSPlatform]` atrybuty, wszystkie atrybuty są pogrupowane według identyfikatora platformy systemu operacyjnego:
  - **Tylko obsługiwana lista**. Jeśli najniższa wersja dla każdej platformy systemu operacyjnego jest `[SupportedOSPlatform]` atrybutem, interfejs API jest uznawany za obsługiwany przez wymienione platformy i nieobsługiwany przez wszystkie inne platformy. Atrybuty opcjonalne `[UnsupportedOSPlatform]` dla każdej platformy mogą mieć tylko wyższą wersję minimalnej obsługiwanej wersji, co oznacza, że interfejs API zostanie usunięty od określonej wersji.

    ```csharp
    // The API only supported on Windows 8.0 and later, not supported for all other.
    // The API is removed/unsupported from version 10.0.19041.0.
    [SupportedOSPlatform("windows8.0")]
    [UnsupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows80SupportFromCertainVersion();
    ```

  - **Nieobsługiwana lista**. Jeśli najniższa wersja dla każdej platformy systemu operacyjnego jest `[UnsupportedOSPlatform]` atrybutem, interfejs API jest uznawany za nieobsługiwany przez wymienione platformy i obsługiwany przez wszystkie inne platformy. Lista może mieć `[SupportedOSPlatform]` atrybut o tej samej platformie, ale wyższej wersji, co oznacza, że interfejs API jest obsługiwany w tej wersji.

    ```csharp
    // The API was unsupported on Windows until version 10.0.19041.0.
    // The API is considered supported everywhere else without constraints.
    [UnsupportedOSPlatform("windows")]
    [SupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows8UnsupportFromWindows10();
    ```

  - **Niespójna lista**. Jeśli najniższa wersja dla niektórych platform jest inna niż w przypadku `[SupportedOSPlatform]` `[UnsupportedOSPlatform]` innych platform, jest uważana za niespójną, co nie jest obsługiwane w przypadku analizatora.
  - Jeśli najmniejsze wersje `[SupportedOSPlatform]` i `[UnsupportedOSPlatform]` atrybuty są równe, Analizator traktuje platformę jako część **obsługiwanej listy**.
- Atrybuty platformy można stosować do typów, elementów członkowskich (metod, pól, właściwości i zdarzeń) i zestawów z różnymi nazwami lub wersjami platform.
  - Atrybuty zastosowane na najwyższym poziomie `target` mają wpływ na wszystkie jej składowe i typy.
  - Atrybuty na poziomie podrzędnym są stosowane tylko wtedy, gdy są zgodne z regułą "adnotacje potomne mogą zawęzić obsługę platform, ale nie mogą ich poszerzyć".
    - Gdy element nadrzędny ma **obsługiwaną tylko** listę, a następnie podrzędne atrybuty elementu członkowskiego nie można dodać nowej obsługi platformy, ponieważ spowodowałoby to rozszerzenie obsługi nadrzędnej. Obsługę nowej platformy można dodać tylko do samego siebie. Ale element podrzędny może mieć `Supported` atrybut dla tej samej platformy z nowszymi wersjami, co zawęża pomoc techniczną. Ponadto element podrzędny może mieć `Unsupported` atrybut o tej samej platformie, co umożliwia również zawężenie obsługi nadrzędnej.
    - Gdy element nadrzędny ma **nieobsługiwaną** listę, wówczas atrybuty elementu członkowskiego podrzędnego mogą dodać obsługę nowej platformy, ponieważ powoduje to zawężenie obsługi nadrzędnej. Ale nie może mieć `Supported` atrybutu dla tej samej platformy, co element nadrzędny, ponieważ rozszerza obsługę elementu nadrzędnego. Obsługę tej samej platformy można dodać tylko do elementu nadrzędnego, w którym `Unsupported` zastosowano oryginalny atrybut.
  - Jeśli `[SupportedOSPlatform("platformVersion")]` zastosowano więcej niż jeden raz dla interfejsu API o tej samej `platform` nazwie, Analizator traktuje tylko ten element z minimalną wersją.
  - Jeśli `[UnsupportedOSPlatform("platformVersion")]` zastosowano więcej niż dwa razy dla interfejsu API o tej samej `platform` nazwie, Analizator uwzględnia tylko dwa z najwcześniejszymi wersjami.

  > [!NOTE]
  > Nie oczekuje się, że interfejs API, który był obsługiwany początkowo, ale nie jest obsługiwany (usunięty) w nowszej wersji.

### <a name="examples-of-how-the-attributes-work-and-what-diagnostics-they-produce"></a>Przykłady działania atrybutów i ich diagnostyki

  ```csharp
  // An API supported only on Windows.
  [SupportedOSPlatform("Windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  public void Caller()
  {
      WindowsOnlyApi(); // warns: 'WindowsOnlyApi' is supported on 'windows'

      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Windows'
      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Linux'
      SupportedOnWindowsAndLinuxOnly();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 8.0 and later
      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // for same platform analyzer only warn for the latest version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  public void Caller2()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'android'

      // warns:'StartedWindowsSupportFromVersion8' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFromVersion8' is supported on 'windows' 8.0 and later
      StartedWindowsSupportFromVersion8();

      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is supported on 'windows' 8.0 and later
      // even there were 3 diagnostics found analyzer warn only for the first 2.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

## <a name="handle-reported-warnings"></a>Obsługa ostrzeżeń raportowanych

Zalecanym sposobem postępowania z tą diagnostyką jest upewnienie się, że interfejsy API specyficzne dla platformy są wywoływane tylko w przypadku uruchamiania na odpowiedniej platformie. Poniżej przedstawiono opcje, których można użyć do rozwiązywania ostrzeżeń; Wybierz opcję, która jest najbardziej odpowiednia dla danej sytuacji:

- **Ochrona wywołania**. Można to osiągnąć, warunkowo wywołując kod w czasie wykonywania. Sprawdź, czy pracujesz w żądanym `Platform` miejscu przy użyciu jednej z metod sprawdzania platformy, na przykład `OperatingSystem.Is<Platform>()` lub `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` .

- **Oznacz lokację wywołania jako specyficzną dla platformy**. Możesz także oznaczyć własne interfejsy API jako charakterystyczne dla danej platformy, co skutecznie tylko przekazuje wymagania do obiektów wywołujących. Oznacz zawierającą metodę lub typ lub cały zestaw z tymi samymi atrybutami, co odwołanie zależne od platformy. [Przykłady](#mark-call-site-as-platform-specific).

- **Potwierdź witrynę wywołania przy użyciu sprawdzenia platformy**. Jeśli nie chcesz obciążać dodatkowej `if` instrukcji w czasie wykonywania, użyj <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> . [Przykład](#assert-the-call-site-with-platform-check).

- **Usuń kod**. Na ogół nie jest to potrzebne, ponieważ oznacza to utratę wierności, gdy kod jest używany przez użytkowników systemu Windows. W przypadku, gdy istnieje alternatywa dla wielu platform, najlepiej jest ją używać w przypadku interfejsów API specyficznych dla platformy.

- **Pomiń ostrzeżenie**. Możesz również po prostu pominąć ostrzeżenie za pośrednictwem wpisu EditorConfig lub `#pragma warning disable ca1416` . Jednak ta opcja powinna być ostatnią możliwością w przypadku korzystania z interfejsów API specyficznych dla platformy.

### <a name="guard-platform-specific-apis-with-guard-methods"></a>Ochrona interfejsów API specyficznych dla platformy przy użyciu metod Guard

Nazwa platformy metody Guard powinna być zgodna z nazwą platformy interfejsu API zależnej od platformy wywołującej. Jeśli ciąg platformy wywołującego interfejsu API zawiera wersję:

- Dla `[SupportedOSPlatform("platformVersion")]` atrybutu platforma metody Guard `version` powinna być większa lub równa platformie wywołującej `Version` .
- Dla `[UnsupportedOSPlatform("platformVersion")]` atrybutu platforma metody Guard `version` powinna być mniejsza lub równa platformie wywołującej `Version` .

  ```csharp
  public void CallingSupportedOnlyApis() // Allow list calls
  {
      if (OperatingSystem.IsWindows())
      {
          WindowsOnlyApi(); // will not warn
      }

      if (OperatingSystem.IsLinux())
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn, within one of the supported context
      }

      // Can use &&, || logical operators to guard combined attributes
      if (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10.0.19041)))
      {
          ApiSupportedFromWindows8UnsupportFromWindows10();
      }

      if (OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903))
      {
          AssemblySupportedOnWindowsApiSupportedFromWindows10(); // Only need to check latest supported version
      }
  }

  public void CallingUnsupportedApis()
  {
      if (!OperatingSystem.IsAndroid())
      {
          DoesNotWorkOnAndroid(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || OperatingSystem.IsWindowsVersionAtLeast(8))
      {
          StartedWindowsSupportFromVersion8(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || // supported all other platforms
         (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903)))
      {
          StartedWindowsSupportFrom8UnsupportedFrom10(); // will not warn
      }
  }
  ```

- Jeśli musisz zabezpieczyć kod, którego dotyczy `netstandard` lub `netcoreapp` gdzie nowe <xref:System.OperatingSystem> interfejsy API nie są dostępne, <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> można użyć interfejsu API i będzie on przestrzegany przez analizator. Ale nie jest tak zoptymalizowany jak nowe interfejsy API dodane w programie <xref:System.OperatingSystem> . Jeśli platforma nie jest obsługiwana w <xref:System.Runtime.InteropServices.OSPlatform> strukturze, można wywołać metodę <xref:System.Runtime.InteropServices.OSPlatform.Create(System.String)?displayProperty=nameWithType> i przekazać ją do nazwy platformy, która również odnosi się do analizatora.

  ```csharp
  public void CallingSupportedOnlyApis()
  {
      if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn
      }

      if (RuntimeInformation.IsOSPlatform(OSPlatform.Create("browser")))
      {
          ApiOnlySupportedOnBrowser(); // call of browser specific API
      }
  }
  ```

### <a name="mark-call-site-as-platform-specific"></a>Oznacz lokację wywołania jako specyficzną dla platformy

Nazwy platform powinny być zgodne z interfejsem API zależnym od platformy wywołującej. Jeśli ciąg platformy zawiera wersję:

- Dla `[SupportedOSPlatform("platformVersion")]` atrybutu platforma lokacji wywołania `version` powinna być większa lub równa platformie wywołującej `Version`
- Dla `[UnsupportedOSPlatform("platformVersion")]` atrybutu platforma lokacji wywołania `version` powinna być mniejsza lub równa platformie wywołującej `Version`

  ```csharp
  // an API supported only on Windows.
  [SupportedOSPlatform("windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  [SupportedOSPlatform("windows8.0")] // call site attributed Windows 8.0 or above.
  public void Caller()
  {
      WindowsOnlyApi(); // will not warn as call site is for Windows.

      // will not warn as call site is for Windows.
      SupportedOnWindowsAndLinuxOnly();

      // will not warn for the API's [SupportedOSPlatform("windows8.0")] attribute.
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // as the call site version is lower than calling version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows11.0")] // call site attributed with windows 11.0 or above.
  public void Caller2()
  {
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // will not warn as call site version higher than calling API.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")] // call site supports Windows from version 8.0 to 10.0.19041.0.
  public void Caller3()
  {
      // will not warn as caller has exact same attributes.
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // As call site stopped support from that version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on Android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  [UnsupportedOSPlatform("windows")] // Caller no support Windows for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'Android'.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }

  [UnsupportedOSPlatform("windows")]
  [UnsupportedOSPlatform("android")] // Caller not support Windows and Android for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // will not warn as call site not supports Android.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

### <a name="assert-the-call-site-with-platform-check"></a>Zapoznaj się z sprawdzeniem połączenia z platformą

Jako warunek dla programu można również użyć wszystkich testów warunkowych użytych w [przykładach funkcji ochrony platformy](#guard-platform-specific-apis-with-guard-methods) <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> .

  ```csharp
  // An API supported only on Linux.
  [SupportedOSPlatform("linux")]
  public void LinuxOnlyApi() { }

  public void Caller()
  {
      Debug.Assert(OperatingSystem.IsLinux());

      LinuxOnlyApi(); // will not warn
  }
  ```

## <a name="see-also"></a>Zobacz także

- [Nazwy platformy docelowej w programie .NET 5](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)
- [Dodawanie adnotacji do interfejsów API specyficznych dla platformy i wykrywanie ich użycia](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-checks/platform-checks.md)
- [Dodawanie adnotacji do interfejsów API jako nieobsługiwanych na określonych platformach](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-exclusion/platform-exclusion.md)
- [Analizator zgodności platformy CA1416](../../fundamentals/code-analysis/quality-rules/ca1416.md)
- [Analizator interfejsów API platformy .NET](../../standard/analyzers/api-analyzer.md)
