---
title: Co nowego w programie .NET Core 2.1
description: Dowiedz się więcej o nowych funkcjach dostępnych w programie .NET Core 2,1.
dev_langs:
- csharp
- vb
ms.date: 10/10/2018
ms.openlocfilehash: 5c15b663cf69de334771e83c1a14db8d66d30458
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437915"
---
# <a name="whats-new-in-net-core-21"></a>Co nowego w programie .NET Core 2.1

Program .NET Core 2,1 zawiera ulepszenia i nowe funkcje w następujących obszarach:

- [Narzędzia](#tooling)
- [Przewinięcie do przodu](#roll-forward)
- [Wdrożenie](#deployment)
- [Pakiet zgodności systemu Windows](#windows-compatibility-pack)
- [Ulepszenia kompilacji JIT](#jit-compiler-improvements)
- [Zmiany interfejsu API](#api-changes)

## <a name="tooling"></a>Narzędzia

Zestaw .NET Core 2,1 SDK (v 2.1.300), narzędzia dołączone do programu .NET Core 2,1, obejmują następujące zmiany i ulepszenia:

### <a name="build-performance-improvements"></a>Ulepszenia wydajności kompilacji

Głównym fokusem platformy .NET Core 2,1 jest poprawa wydajności czasu kompilacji, szczególnie w przypadku kompilacji przyrostowych. Te ulepszenia wydajności dotyczą zarówno kompilacji w wierszu polecenia `dotnet build` , jak i do kompilacji w programie Visual Studio. Niektóre indywidualne obszary poprawy obejmują:

- W przypadku rozpoznawania zasobów pakietu, rozpoznawania tylko zasobów używanych przez kompilację, a nie wszystkich zasobów.

- Buforowanie odwołań do zestawów.

- Korzystanie z długotrwałych serwerów kompilacji zestawu SDK, które są procesami, które rozciągają się między poszczególne `dotnet build` wywołania. Eliminują one potrzebę przeprowadzenia JIT operacji kompilowania dużych bloków kodu przy każdym `dotnet build` uruchomieniu. Procesy serwera kompilacji można automatycznie kończyć przy użyciu następującego polecenia:

   ```dotnetcli
   dotnet buildserver shutdown
   ```

### <a name="new-cli-commands"></a>Polecenia nowej infrastruktury CLI

Liczba narzędzi, które były dostępne tylko dla poszczególnych projektów, przy użyciu, `DotnetCliToolReference` jest teraz dostępna jako część zestaw .NET Core SDK. Do tych narzędzi należą:

- `dotnet watch` udostępnia obserwatora systemu plików, który czeka na zmianę pliku przed wykonaniem określonego zestawu poleceń. Na przykład następujące polecenie automatycznie ponownie kompiluje bieżący projekt i generuje pełne dane wyjściowe za każdym razem, gdy plik zostanie zmieniony:

   ```dotnetcli
   dotnet watch -- --verbose build
   ```

   Zwróć uwagę na `--` opcję, która poprzedza `--verbose` opcję. Ogranicza opcje przekazane bezpośrednio do `dotnet watch` polecenia z argumentów, które są przekazane do procesu podrzędnego `dotnet` . Bez tego `--verbose` opcja dotyczy `dotnet watch` polecenia, a nie `dotnet build` polecenia.
  
   Aby uzyskać więcej informacji, zobacz [opracowywanie aplikacji ASP.NET Core przy użyciu czujki dotnet](/aspnet/core/tutorials/dotnet-watch).

- `dotnet dev-certs` Program generuje i zarządza certyfikatami używanymi podczas opracowywania aplikacji ASP.NET Core.

- `dotnet user-secrets` zarządza wpisami tajnymi w magazynie kluczy tajnych użytkownika w aplikacjach ASP.NET Core.

- `dotnet sql-cache` tworzy tabelę i indeksy w bazie danych Microsoft SQL Server, które mają być używane na potrzeby rozproszonej pamięci podręcznej.

- `dotnet ef` jest narzędziem do zarządzania bazami danych, <xref:Microsoft.EntityFrameworkCore.DbContext> obiektami i migracjami w aplikacjach Entity Framework Core. Aby uzyskać więcej informacji, zobacz [EF Core narzędzia wiersza polecenia programu .NET](/ef/core/miscellaneous/cli/dotnet).

### <a name="global-tools"></a>Narzędzia globalne

Program .NET Core 2,1 obsługuje *Narzędzia globalne* — czyli narzędzia niestandardowe, które są dostępne globalnie w wierszu polecenia. Model rozszerzalności we wcześniejszych wersjach programu .NET Core udostępnia niestandardowe narzędzia dostępne dla każdego projektu, tylko przy użyciu `DotnetCliToolReference` .

Aby zainstalować narzędzie globalne, należy użyć polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) . Przykład:

```dotnetcli
dotnet tool install -g dotnetsay
```

Po zainstalowaniu narzędzie można uruchomić z wiersza polecenia, określając nazwę narzędzia. Aby uzyskać więcej informacji, zobacz [Omówienie narzędzi globalnych platformy .NET Core](../tools/global-tools.md).

### <a name="tool-management-with-the-dotnet-tool-command"></a>Zarządzanie narzędziem za pomocą `dotnet tool` polecenia

W zestawie SDK platformy .NET Core 2,1 wszystkie operacje narzędzi używają `dotnet tool` polecenia. Dostępne są następujące opcje:

- [`dotnet tool install`](../tools/dotnet-tool-install.md) Aby zainstalować narzędzie.

- [`dotnet tool update`](../tools/dotnet-tool-update.md) Aby odinstalować i ponownie zainstalować narzędzie, które efektywnie go aktualizuje.

- [`dotnet tool list`](../tools/dotnet-tool-list.md) Aby wyświetlić listę aktualnie zainstalowanych narzędzi.

- [`dotnet tool uninstall`](../tools/dotnet-tool-uninstall.md) Odinstalowywanie aktualnie zainstalowanych narzędzi.

## <a name="roll-forward"></a>Przewinięcie do przodu

Wszystkie aplikacje .NET Core, począwszy od platformy .NET Core 2,0, automatycznie przekazują do najnowszej *wersji pomocniczej* zainstalowanej w systemie.

Począwszy od platformy .NET Core 2,0, jeśli wersja platformy .NET Core, z którą została skompilowana aplikacja, nie jest obecna w czasie wykonywania, aplikacja jest uruchamiana automatycznie względem najnowszej zainstalowanej *pomocniczej wersji* platformy .NET Core. Innymi słowy, jeśli aplikacja jest skompilowana przy użyciu platformy .NET Core 2,0, a program .NET Core 2,0 nie jest obecny w systemie hosta, ale .NET Core 2,1 to, aplikacja działa z platformą .NET Core 2,1.

> [!IMPORTANT]
> To zachowanie z przekazaniem do przodu nie ma zastosowania do wersji zapoznawczej. Domyślnie nie dotyczy to również wersji głównych, ale można to zmienić przy użyciu poniższych ustawień.

To zachowanie można zmienić, zmieniając ustawienie dla opcji przechodzenie do przodu w przypadku braku kandydata udostępnionego platformy. Dostępne są następujące ustawienia:

- `0` — Wyłącz zachowanie przekazujące wersje pomocnicze. W przypadku tego ustawienia aplikacja skompilowana dla programu .NET Core 2.0.0 będzie przeniesiona do wersji .NET Core 2.0.1, ale nie do platformy .NET Core 2.2.0 lub .NET Core 3.0.0.
- `1` -Włącz zachowanie przekazujące wersje pomocnicze. Jest to wartość domyślna dla tego ustawienia. W przypadku tego ustawienia aplikacja skompilowana dla programu .NET Core 2.0.0 będzie przeniesiona do programu .NET Core 2.0.1 lub .NET Core 2.2.0, w zależności od tego, który z nich jest zainstalowany, ale nie zostanie przesunięty do programu .NET Core 3.0.0.
- `2` — Włącz proste i główne zachowanie podczas przekazywania wersji. Jeśli ta wartość jest ustawiona, są uwzględniane różne wersje główne, więc aplikacja skompilowana dla platformy .NET Core 2.0.0 przejdzie do usługi .NET Core 3.0.0.

To ustawienie można zmienić na jeden z trzech sposobów:

- Ustaw dla `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX` zmiennej środowiskowej żądaną wartość.

- Dodaj następujący wiersz z żądaną wartością do *.runtimeconfig.jsw* pliku:

   ```json
   "rollForwardOnNoCandidateFx" : 0
   ```

- W przypadku korzystania z [interfejs wiersza polecenia platformy .NET Core](../tools/index.md)należy dodać następującą opcję z odpowiednią wartością do polecenia programu .NET Core, takiego jak `run` :

   ```dotnetcli
   dotnet run --rollForwardOnNoCandidateFx=0
   ```

Wersja poprawki do przodu jest niezależna od tego ustawienia i jest wykonywana po zastosowaniu dowolnych dodatkowych lub głównych wersji do przodu.

## <a name="deployment"></a>Wdrożenie

### <a name="self-contained-application-servicing"></a>Obsługa aplikacji samodzielnych

`dotnet publish` Program publikuje teraz aplikacje samodzielne z wersją środowiska uruchomieniowego z obsługą usługi. Po opublikowaniu aplikacji samodzielnej przy użyciu zestawu .NET Core 2,1 SDK (v 2.1.300) aplikacja zawiera najnowszą wersję środowiska uruchomieniowego, znaną przez ten zestaw SDK. Po uaktualnieniu do najnowszego zestawu SDK opublikujesz go przy użyciu najnowszej wersji środowiska uruchomieniowego platformy .NET Core. Dotyczy to środowiska uruchomieniowego .NET Core 1,0 i nowszych.

Samodzielny publikowanie jest zależne od wersji środowiska uruchomieniowego w systemie NuGet.org. Na maszynie nie trzeba mieć obsługiwanego środowiska uruchomieniowego.

Przy użyciu zestawu SDK platformy .NET Core 2,0 aplikacje samodzielne są publikowane przy użyciu środowiska uruchomieniowego 2.0.0 platformy .NET Core, o ile nie zostanie określona inna wersja za pośrednictwem `RuntimeFrameworkVersion` właściwości. W przypadku tego nowego zachowania nie trzeba już ustawiać tej właściwości, aby wybrać nowszą wersję środowiska uruchomieniowego dla aplikacji samodzielnej. Najprostszym podejściem do przodu jest zawsze Publikowanie przy użyciu zestawu SDK platformy .NET Core 2,1 (v 2.1.300).

Aby uzyskać więcej informacji, zobacz [samodzielne wdrożenie środowiska uruchomieniowego wdrożenia](../deploying/runtime-patch-selection.md).

## <a name="windows-compatibility-pack"></a>Pakiet zgodności systemu Windows

Podczas przenoszenia istniejącego kodu z .NET Framework do programu .NET Core można użyć [pakietu zgodności systemu Windows](https://www.nuget.org/packages/Microsoft.Windows.Compatibility). Zapewnia dostęp do 20 000 więcej interfejsów API, niż są dostępne w programie .NET Core. Te interfejsy API obejmują typy w <xref:System.Drawing?displayProperty=nameWithType> przestrzeni nazw, <xref:System.Diagnostics.EventLog> klasy, WMI, liczniki wydajności, usługi systemu Windows oraz typy i składowe rejestru systemu Windows.

## <a name="jit-compiler-improvements"></a>Udoskonalenia kompilatora JIT

Platforma .NET Core obejmuje nową technologię kompilatora JIT o nazwie *kompilacja warstwowa* (znana również jako *Optymalizacja adaptacyjna*), która może znacząco poprawić wydajność. Kompilacja warstwowa jest ustawieniem zgody.

Jednym z ważnych zadań wykonywanych przez kompilator JIT jest optymalizacja wykonywania kodu. Jednak w przypadku niewielkich ścieżek kodu kompilator może poświęcać więcej czasu na optymalizację kodu niż środowisko uruchomieniowe spędza na uruchamianiu niezoptymalizowanego kodu. Kompilacja warstwowa wprowadza dwa etapy kompilacji JIT:

- **Pierwsza warstwa**, która generuje kod tak szybko, jak to możliwe.

- **Druga warstwa**, która generuje zoptymalizowany kod dla tych metod, które są wykonywane często. Druga warstwa kompilacji jest wykonywana równolegle w celu zwiększenia wydajności.

Możesz zdecydować się na kompilację warstwową na dwa sposoby.

- Aby użyć kompilacji warstwowej we wszystkich projektach, które używają zestawu SDK platformy .NET Core 2,1, ustaw następujące zmienne środowiskowe:

  ```console
  COMPlus_TieredCompilation="1"
  ```

- Aby użyć kompilacji warstwowej dla każdego projektu, Dodaj `<TieredCompilation>` Właściwość do `<PropertyGroup>` sekcji pliku projektu MSBuild, jak pokazano na poniższym przykładzie:

   ```xml
   <PropertyGroup>
      <!-- other property definitions -->

      <TieredCompilation>true</TieredCompilation>
   </PropertyGroup>
   ```

## <a name="api-changes"></a>Zmiany interfejsu API

### <a name="spant-and-memoryt"></a>`Span<T>` i `Memory<T>`

Platforma .NET Core 2,1 zawiera nowe typy, które ułatwiają pracę z tablicami i innymi typami pamięci. Nowe typy obejmują:

- <xref:System.Span%601?displayProperty=nameWithType> i <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> .

- <xref:System.Memory%601?displayProperty=nameWithType> i <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType> .

Bez tych typów, podczas przekazywania takich elementów jako części tablicy lub sekcji buforu pamięci należy wykonać kopię części danych przed przekazaniem jej do metody. Te typy zapewniają wirtualny widok tych danych, który eliminuje konieczność dodatkowej alokacji pamięci i operacji kopiowania.

Poniższy przykład używa <xref:System.Span%601> wystąpienia i, <xref:System.Memory%601> Aby zapewnić wirtualny widok 10 elementów tablicy.

[!code-csharp[Span\<T>](./snippets/dotnet-core-2-1/csharp/program.cs)]

[!code-vb[Memory\<T>](./snippets/dotnet-core-2-1/vb/program.vb)]

### <a name="brotli-compression"></a>Kompresja Brotli

Program .NET Core 2,1 dodaje obsługę kompresji i dekompresji Brotli. Brotli to algorytm kompresji bezstratnego ogólnego przeznaczenia, który jest zdefiniowany w [dokumencie RFC 7932](https://www.ietf.org/rfc/rfc7932.txt) i jest obsługiwany przez większość przeglądarek sieci Web i głównych serwerów sieci Web. Można użyć klasy bazującej na strumieniu <xref:System.IO.Compression.BrotliStream?displayProperty=nameWithType> lub klasy obejmującej wiele wydajności <xref:System.IO.Compression.BrotliEncoder?displayProperty=nameWithType> <xref:System.IO.Compression.BrotliDecoder?displayProperty=nameWithType> . Poniższy przykład ilustruje kompresję z <xref:System.IO.Compression.BrotliStream> klasą:

[!code-csharp[Brotli compression](./snippets/dotnet-core-2-1/csharp/brotli.cs#1)]

[!code-vb[Brotli compression](./snippets/dotnet-core-2-1/vb/brotli.vb#1)]

<xref:System.IO.Compression.BrotliStream>Zachowanie jest takie samo jak <xref:System.IO.Compression.DeflateStream> i <xref:System.IO.Compression.GZipStream> , co ułatwia konwertowanie kodu, który wywołuje te interfejsy API do programu <xref:System.IO.Compression.BrotliStream> .

### <a name="new-cryptography-apis-and-cryptography-improvements"></a>Nowe ulepszone interfejsy API kryptografii i kryptografii

Program .NET Core 2,1 zawiera liczne ulepszenia interfejsów API kryptografii:

- <xref:System.Security.Cryptography.Pkcs.SignedCms?displayProperty=nameWithType> jest dostępny w pakiecie System. Security. Cryptography. PKCS. Implementacja jest taka sama jak <xref:System.Security.Cryptography.Pkcs.SignedCms> Klasa w .NET Framework.

- Nowe przeciążenia <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHash%2A?displayProperty=nameWithType> <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString%2A?displayProperty=nameWithType> metod i akceptują identyfikator algorytmu wyznaczania wartości skrótu, aby umożliwić wywołującym pobieranie wartości odcisków palca certyfikatu przy użyciu algorytmów innych niż SHA-1.

- <xref:System.Span%601>Dostępne są nowe interfejsy API kryptografii oparte na tworzeniu skrótów, HMAC, kryptograficznej generacji liczb losowych, generowanie sygnatur asymetryczne, przetwarzanie sygnatur asymetryczne i szyfrowanie RSA.

- <xref:System.Security.Cryptography.Rfc2898DeriveBytes?displayProperty=nameWithType>Zwiększono wydajność programu o około 15% przy użyciu <xref:System.Span%601> implementacji opartej na bazie.

- Nowa <xref:System.Security.Cryptography.CryptographicOperations?displayProperty=nameWithType> Klasa obejmuje dwie nowe metody:

  - <xref:System.Security.Cryptography.CryptographicOperations.FixedTimeEquals%2A> Pobiera stałą ilość czasu, aby zwrócić do każdego z dwóch danych wejściowych o tej samej długości, co sprawia, że jest to odpowiednie do użycia w weryfikacji kryptograficznej, aby uniknąć współtworzenia informacji w kanale bocznym.

  - <xref:System.Security.Cryptography.CryptographicOperations.ZeroMemory%2A> to procedura czyszczenia pamięci, której nie można zoptymalizować.

- Metoda statyczna <xref:System.Security.Cryptography.RandomNumberGenerator.Fill%2A?displayProperty=nameWithType> wypełnia <xref:System.Span%601> losowo wartościami.

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms?displayProperty=nameWithType>Jest teraz obsługiwana w systemach Linux i macOS.

- Elliptic-Curve Diffie-Hellman (ECDH) jest teraz dostępny w <xref:System.Security.Cryptography.ECDiffieHellman?displayProperty=nameWithType> rodzinie klas. Powierzchnia obszaru jest taka sama jak w .NET Framework.

- Wystąpienie zwrócone przez <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> program umożliwia szyfrowanie lub odszyfrowywanie za pomocą OAEP przy użyciu skrótu SHA-2, a także generowanie lub weryfikowanie podpisów przy użyciu RSA-PSS.

### <a name="sockets-improvements"></a>Ulepszenia gniazd

Platforma .NET Core zawiera nowy typ, <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> i zapisany <xref:System.Net.Http.HttpMessageHandler?displayProperty=nameWithType> , który stanowi podstawę interfejsów API sieci wyższego poziomu.  <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>na przykład jest podstawą <xref:System.Net.Http.HttpClient> implementacji. W poprzednich wersjach programu .NET Core interfejsy API wyższego poziomu były oparte na natywnych implementacjach sieci.

Implementacja Sockets wprowadzona w programie .NET Core 2,1 ma wiele zalet:

- Znaczący wzrost wydajności w porównaniu z poprzednią implementacją.

- Wyeliminowanie zależności platformy, co upraszcza wdrażanie i obsługę.

- Spójne zachowanie na wszystkich platformach .NET Core.

<xref:System.Net.Http.SocketsHttpHandler> jest domyślną implementacją w programie .NET Core 2,1. Można jednak skonfigurować aplikację tak, aby używała starszej <xref:System.Net.Http.HttpClientHandler> klasy przez wywołanie <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> metody:

```csharp
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", false);
```

```vb
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", False)
```

Można również użyć zmiennej środowiskowej, aby zrezygnować z użycia implementacji Sockets w oparciu o <xref:System.Net.Http.SocketsHttpHandler> . W tym celu należy ustawić wartość `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` na `false` lub 0.

W systemie Windows można również wybrać użycie <xref:System.Net.Http.WinHttpHandler?displayProperty=nameWithType> , które korzysta z implementacji natywnej lub <xref:System.Net.Http.SocketsHttpHandler> klasy przez przekazanie wystąpienia klasy do <xref:System.Net.Http.HttpClient> konstruktora.

W systemach Linux i macOS można konfigurować tylko <xref:System.Net.Http.HttpClient> dla poszczególnych procesów. W systemie Linux należy wdrożyć [libcurl](https://curl.haxx.se/libcurl/) , jeśli chcesz użyć starej <xref:System.Net.Http.HttpClient> implementacji. (Jest instalowany z platformą .NET Core 2,0).

### <a name="breaking-changes"></a>Zmiany powodujące niezgodność

Aby uzyskać informacje o istotnych zmianach, zobacz istotne [zmiany dotyczące migracji z wersji 2,0 do 2,1](../compatibility/2.1.md).

## <a name="see-also"></a>Zobacz także

- [Co nowego w programie .NET Core 3.1](dotnet-core-3-1.md)
- [Nowe funkcje w EF Core 2,1](/ef/core/what-is-new/ef-core-2.1)
- [Co nowego w ASP.NET Core 2,1](/aspnet/core/aspnetcore-2.1)
