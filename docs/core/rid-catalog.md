---
title: Wykaz identyfikatorów środowiska uruchomieniowego platformy .NET Core (RID)
description: Dowiedz się więcej o identyfikatorze środowiska uruchomieniowego (RID) i sposobie używania identyfikatorów RID w programie .NET Core.
ms.date: 12/15/2020
ms.openlocfilehash: f818ab2d503be7960d9eb8450a7dd749766637a6
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633614"
---
# <a name="net-core-rid-catalog"></a>Katalog programu .NET Core RID

Identyfikator RID jest krótki dla *identyfikatora środowiska uruchomieniowego*. Wartości identyfikatorów RID służą do identyfikowania platform docelowych, w których jest uruchamiana aplikacja.
Są one używane przez pakiety .NET do reprezentowania zasobów specyficznych dla platformy w pakietach NuGet. Poniżej przedstawiono przykłady identyfikatorów RID: `linux-x64` , `ubuntu.14.04-x64` , `win7-x64` lub `osx.10.12-x64` .
W przypadku pakietów z natywnymi zależnościami identyfikator RID określa platformy, na których można przywrócić pakiet.

Pojedynczy identyfikator RID można ustawić w `<RuntimeIdentifier>` elemencie pliku projektu. Wiele identyfikatorów RID można zdefiniować jako listę rozdzielaną średnikami w elemencie pliku projektu `<RuntimeIdentifiers>` . Są one również używane przez `--runtime` opcję z następującymi [interfejs wiersza polecenia platformy .NET Core poleceniami](./tools/index.md):

- [dotnet build](./tools/dotnet-build.md)
- [dotnet clean](./tools/dotnet-clean.md)
- [dotnet pack](./tools/dotnet-pack.md)
- [dotnet publish](./tools/dotnet-publish.md)
- [dotnet restore](./tools/dotnet-restore.md)
- [dotnet run](./tools/dotnet-run.md)
- [dotnet store](./tools/dotnet-store.md)

Identyfikatory RID reprezentujące konkretne systemy operacyjne zwykle są zgodne z tym wzorcem: `[os].[version]-[architecture]-[additional qualifiers]` gdzie:

- `[os]` jest monikerem systemu operacyjnego/platformy. Na przykład `ubuntu`.

- `[version]` jest wersją systemu operacyjnego w postaci numeru wersji oddzielonej kropką ( `.` ). Na przykład `15.10`.

  - Wersja nie **powinna** być wersją marketingową, ponieważ często reprezentuje wiele dyskretnych wersji systemu operacyjnego z różnymi obszarami powierzchni interfejsu API platformy.

- `[architecture]` jest architekturą procesora. Na przykład: `x86` , `x64` , `arm` lub `arm64` .

- `[additional qualifiers]` dalsze odróżnienie różnych platform. Na przykład: `aot`.

## <a name="rid-graph"></a>Wykres RID

Wykres RID lub wykres rezerwowy środowiska uruchomieniowego to lista identyfikatorów RID, które są zgodne ze sobą. Identyfikatory RID są zdefiniowane w pakiecie [Microsoft. servicecore. platforms](https://www.nuget.org/packages/Microsoft.NETCore.Platforms/) . Listę obsługiwanych identyfikatorów RID i Graf RID można zobaczyć w [*runtime.js*](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) pliku, który znajduje się w `dotnet/runtime` repozytorium. W tym pliku można zobaczyć, że wszystkie identyfikatory RID, z wyjątkiem podstawowego, zawierają `"#import"` instrukcję. Te instrukcje wskazują zgodne identyfikatory RID.

Gdy pakiet NuGet przywraca pakiety, próbuje znaleźć dokładne dopasowanie dla określonego środowiska uruchomieniowego.
Jeśli dokładne dopasowanie nie zostanie znalezione, pakiet NuGet przeprowadzi ponownie wykres do momentu znalezienia najbliższego zgodnego systemu zgodnie z wykresem RID.

Poniższy przykład jest rzeczywistym wpisem `osx.10.12-x64` identyfikatora RID:

```json
"osx.10.12-x64": {
    "#import": [ "osx.10.12", "osx.10.11-x64" ]
}
```

Powyższy identyfikator RID określa, że `osx.10.12-x64` Importy `osx.10.11-x64` . W związku z tym, gdy pakiet NuGet przywraca pakiety, próbuje znaleźć dokładne dopasowanie dla  `osx.10.12-x64` pakietu. Jeśli NuGet nie może znaleźć określonego środowiska uruchomieniowego, można przywrócić pakiety, które określają `osx.10.11-x64` środowisko uruchomieniowe, na przykład.

Poniższy przykład pokazuje nieco większego wykresu RID, zdefiniowany w *runtime.jsw*  pliku:

```
    win7-x64    win7-x86
       |   \   /    |
       |   win7     |
       |     |      |
    win-x64  |  win-x86
          \  |  /
            win
             |
            any
```

Wszystkie identyfikatory RID ostatecznie zamapują się z powrotem do głównego `any` identyfikatora RID.

Istnieją pewne kwestie dotyczące identyfikatorów RID, które należy wziąć pod uwagę podczas pracy z nimi:

- Nie próbuj analizować identyfikatorów RID, aby pobrać części składnika.
- Nie Kompiluj identyfikatorów RID programowo.
- Użyj identyfikatorów RID, które są już zdefiniowane dla platformy.
- Identyfikatory RID muszą być specyficzne, więc nie założono niczego z rzeczywistej wartości RID.

## <a name="using-rids"></a>Korzystanie z identyfikatorów RID

Aby móc korzystać z identyfikatorów RID, musisz wiedzieć, które istniejące identyfikatory RID istnieją. Nowe wartości są regularnie dodawane do platformy.
Aby uzyskać najnowszą i pełną wersję, zobacz [runtime.jsw](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) pliku w `dotnet/runtime` repozytorium.

Zestaw SDK platformy .NET Core 2,0 wprowadza koncepcję przenośnych identyfikatorów RID. Są to nowe wartości dodawane do grafu identyfikatorów RID, które nie są powiązane z określoną wersją lub dystrybucją systemu operacyjnego i są preferowanym wyborem w przypadku korzystania z platformy .NET Core 2,0 i nowszych. Są one szczególnie przydatne w przypadku korzystania z wielu dystrybucje systemu Linux, ponieważ większość identyfikatorów RID dystrybucji jest mapowanych na przenośne identyfikatory RID.

Na poniższej liście przedstawiono mały podzestaw najbardziej typowych identyfikatorów RID użytych dla każdego systemu operacyjnego.

## <a name="windows-rids"></a>Identyfikatory RID systemu Windows

Wyświetlane są tylko typowe wartości. Aby uzyskać najnowszą i pełną wersję, zapoznaj się z tematem [runtime.jsw](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) pliku w `dotnet/runtime` repozytorium.

- Przenośne (.NET Core 2,0 lub nowsze wersje)
  - `win-x64`
  - `win-x86`
  - `win-arm`
  - `win-arm64`
- Windows 7/Windows Server 2008 R2
  - `win7-x64`
  - `win7-x86`
- Windows 8.1/Windows Server 2012 R2
  - `win81-x64`
  - `win81-x86`
  - `win81-arm`
- Windows 10/Windows Server 2016
  - `win10-x64`
  - `win10-x86`
  - `win10-arm`
  - `win10-arm64`

Aby uzyskać więcej informacji, zobacz [zależności i wymagania dotyczące platformy .NET Core](./install/windows.md#dependencies).

## <a name="linux-rids"></a>Identyfikatory RID systemu Linux

Wyświetlane są tylko typowe wartości. Aby uzyskać najnowszą i pełną wersję, zobacz [runtime.jsw](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) pliku w `dotnet/runtime` repozytorium. Urządzenia korzystające z dystrybucji niewymienionej poniżej mogą działać z jednym z przenośnych identyfikatorów RID. Na przykład urządzenia Raspberry Pi z dystrybucją systemu Linux, których nie ma na liście, mogą być wskazywane przez `linux-arm` .

- Przenośny
  - `linux-x64` (Większość dystrybucji komputerów, takich jak CentOS, Debian, Fedora, Ubuntu i pochodne)
  - `linux-musl-x64` (Lekkie dystrybucje korzystające z [MUSL](https://wiki.musl-libc.org/projects-using-musl.html) , na przykład Alpine Linux)
  - `linux-arm` (Dystrybucje systemu Linux działające na ARM, takie jak raspbian na Raspberry Pi Model 2 +)
  - `linux-arm64` (Dystrybucje systemu Linux uruchomione na 64-bitowych ARM, takich jak Ubuntu Server 64-bit in Raspberry Pi Model 3 +)
- Red Hat Enterprise Linux
  - `rhel-x64` (Zastąpione przez `linux-x64` dla RHEL powyżej wersji 6)
  - `rhel.6-x64`
- Tizen
  - `tizen`
  - `tizen.4.0.0`
  - `tizen.5.0.0`

Aby uzyskać więcej informacji, zobacz [zależności i wymagania dotyczące platformy .NET Core](./install/linux.md).

## <a name="macos-rids"></a>macOS RID

macOS RID używają starszej marki "OSX". Wyświetlane są tylko typowe wartości. Aby uzyskać najnowszą i pełną wersję, zobacz [runtime.jsw](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) pliku w `dotnet/runtime` repozytorium.

- Przenośny
  - `osx-x64` (Minimalna wersja systemu operacyjnego to macOS 10,12 Sierra)
- macOS 10,10, Yosemite
  - `osx.10.10-x64`
- macOS 10,11 El Capitan
  - `osx.10.11-x64`
- macOS 10,12 Sierra
  - `osx.10.12-x64`
- macOS 10,13, wysoka firma Sierra
  - `osx.10.13-x64`
- macOS 10,14 Mojave
  - `osx.10.14-x64`
- macOS 10,15 Catalina
  - `osx.10.15-x64`
- macOS 11,01 Big Sur
  - `osx.11.0-x64`
  - `osx.11.0-arm64`

Aby uzyskać więcej informacji, zobacz [zależności i wymagania dotyczące platformy .NET Core](./install/macos.md#dependencies).

## <a name="see-also"></a>Zobacz także

- [Identyfikatory środowiska uruchomieniowego](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/readme.md)
