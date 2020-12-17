---
title: Napisz niestandardowego hosta środowiska uruchomieniowego platformy .NET Core
description: Dowiedz się, jak hostować środowisko uruchomieniowe platformy .NET Core z kodu natywnego, aby obsługiwać zaawansowane scenariusze, które wymagają kontrolowania sposobu działania środowiska uruchomieniowego .NET Core.
author: mjrousos
ms.topic: how-to
ms.date: 12/21/2018
ms.openlocfilehash: 358cbff1ded3bd4ee9a3f78965eac1e1b1883ede
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633849"
---
# <a name="write-a-custom-net-core-host-to-control-the-net-runtime-from-your-native-code"></a>Napisz niestandardowego hosta .NET Core, aby kontrolować środowisko uruchomieniowe platformy .NET z kodu natywnego

Podobnie jak w przypadku wszystkich kodów zarządzanych, aplikacje platformy .NET Core są wykonywane przez hosta. Host jest odpowiedzialny za uruchamianie środowiska uruchomieniowego (w tym składników, takich jak moduł odzyskiwania JIT i elementów bezużytecznych) i wywoływanie zarządzanych punktów wejścia.

Hostowanie środowiska uruchomieniowego .NET Core jest zaawansowanym scenariuszem, a w większości przypadków Deweloperzy platformy .NET Core nie muszą martwić się o hosting, ponieważ procesy kompilacji platformy .NET Core udostępniają domyślny Host do uruchamiania aplikacji platformy .NET Core. W niektórych wyspecjalizowanych sytuacjach może być przydatne jawne hostowanie środowiska uruchomieniowego platformy .NET Core jako metody wywoływania kodu zarządzanego w procesie macierzystym lub w celu uzyskania większej kontroli nad sposobem działania środowiska uruchomieniowego.

Ten artykuł zawiera omówienie kroków niezbędnych do uruchomienia środowiska uruchomieniowego platformy .NET Core z kodu natywnego i wykonywania w nim kodu zarządzanego.

## <a name="prerequisites"></a>Wymagania wstępne

Ponieważ hosty są aplikacjami natywnymi, ten samouczek obejmuje konstruowanie aplikacji C++ do hostowania programu .NET Core. Konieczne będzie środowisko deweloperskie języka C++ (takie jak dostarczone przez [program Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)).

Ponadto potrzebna jest prosta aplikacja .NET Core do testowania hosta za pomocą programu, dlatego należy zainstalować [zestaw .NET Core SDK](https://dotnet.microsoft.com/download) i [utworzyć małą aplikację .NET Core test](with-visual-studio.md) (na przykład aplikację "Hello World"). Wystarczy aplikacja "Hello world" utworzona przy użyciu nowego szablonu projektu konsoli .NET Core.

## <a name="hosting-apis"></a>Hostowanie interfejsów API

Istnieją dwa różne interfejsy API, których można używać do hostowania programu .NET Core. Ten artykuł (wraz ze skojarzonymi z nim [przykłady](https://github.com/dotnet/samples/tree/master/core/hosting)) obejmuje te dwie opcje.

* Preferowaną metodą hostowania środowiska uruchomieniowego .NET Core w programie .NET Core 3,0 i nowszym jest `nethost` `hostfxr` interfejs API bibliotek i. Te punkty wejścia obsługują złożoność znajdowania i konfigurowania środowiska uruchomieniowego na potrzeby inicjowania oraz umożliwiają uruchamianie aplikacji zarządzanej i wywoływanie jej w statycznej metodzie zarządzanej.
* Preferowaną metodą hostowania środowiska uruchomieniowego .NET Core przed programem .NET Core 3,0 jest [`coreclrhost.h`](https://github.com/dotnet/runtime/blob/master/src/coreclr/hosts/inc/coreclrhost.h) interfejs API. Ten interfejs API udostępnia funkcje ułatwiające uruchamianie i zatrzymywanie środowiska uruchomieniowego oraz Wywoływanie kodu zarządzanego (przez uruchomienie zarządzanego pliku exe lub poprzez wywoływanie statycznych metod zarządzanych).

## <a name="sample-hosts"></a>Przykładowe hosty

[Przykładowe hosty](https://github.com/dotnet/samples/tree/master/core/hosting) pokazujące kroki opisane w poniższych samouczkach są dostępne w repozytorium GitHub/Samples. Komentarze w przykładach jasno kojarzą numerowane kroki z tych samouczków z miejscem, w którym są wykonywane w próbce. Aby uzyskać instrukcje dotyczące pobierania, zobacz [przykłady i samouczki](../../samples-and-tutorials/index.md#view-and-download-samples).

Należy pamiętać, że przykładowe hosty są przeznaczone do celów edukacyjnych, dzięki czemu są one jasne przy sprawdzaniu błędów i zostały zaprojektowane w celu wyróżnienia czytelności przez zwiększenie wydajności.

## <a name="create-a-host-using-nethosth-and-hostfxrh"></a>Tworzenie hosta przy użyciu programu `nethost.h` i `hostfxr.h`

Poniższe kroki szczegółowo opisują sposób użycia `nethost` `hostfxr` bibliotek i do uruchomienia środowiska uruchomieniowego platformy .NET Core w aplikacji natywnej i wywołania do zarządzanej metody statycznej. [Przykład](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithHostFxr) używa `nethost` nagłówka i biblioteki zainstalowanej z zestawem SDK .NET i kopii [`coreclr_delegates.h`](https://github.com/dotnet/runtime/blob/master/src/installer/corehost/cli/coreclr_delegates.h) [`hostfxr.h`](https://github.com/dotnet/runtime/blob/master/src/installer/corehost/cli/hostfxr.h) plików i z repozytorium [dotnet/Runtime](https://github.com/dotnet/runtime) .

### <a name="step-1---load-hostfxr-and-get-exported-hosting-functions"></a>Krok 1 — Ładowanie `hostfxr` i uzyskiwanie eksportowanych funkcji hostingu

`nethost`Biblioteka zawiera `get_hostfxr_path` funkcję do lokalizowania `hostfxr` biblioteki. `hostfxr`Biblioteka udostępnia funkcje do hostowania środowiska uruchomieniowego platformy .NET Core. Pełną listę funkcji można znaleźć w [`hostfxr.h`](https://github.com/dotnet/runtime/blob/master/src/installer/corehost/cli/hostfxr.h) dokumencie, a [natywny dokument projektu hostingu](https://github.com/dotnet/runtime/blob/master/docs/design/features/native-hosting.md). W przykładzie i w tym samouczku są używane następujące elementy:

* `hostfxr_initialize_for_runtime_config`: Inicjuje kontekst hosta i przygotowuje się do inicjalizacji środowiska uruchomieniowego platformy .NET Core przy użyciu określonej konfiguracji środowiska uruchomieniowego.
* `hostfxr_get_runtime_delegate`: Pobiera obiekt delegowany dla funkcji środowiska uruchomieniowego.
* `hostfxr_close`: Zamyka kontekst hosta.

`hostfxr`Biblioteka zostanie znaleziona przy użyciu `get_hostfxr_path` . Następnie jest ładowany, a jego eksporty są pobierane.

[!code-cpp[HostFxrHost#LoadHostFxr](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#LoadHostFxr)]

### <a name="step-2---initialize-and-start-the-net-core-runtime"></a>Krok 2 — Inicjowanie i uruchamianie środowiska uruchomieniowego platformy .NET Core

`hostfxr_initialize_for_runtime_config`Funkcje i `hostfxr_get_runtime_delegate` inicjują i uruchamiają środowisko uruchomieniowe platformy .NET Core przy użyciu konfiguracji środowiska uruchomieniowego zarządzanego składnika, który zostanie załadowany. `hostfxr_get_runtime_delegate`Funkcja służy do uzyskania delegata środowiska uruchomieniowego, który umożliwia ładowanie zestawu zarządzanego i uzyskiwanie wskaźnika funkcji do statycznej metody w tym zestawie.

[!code-cpp[HostFxrHost#Initialize](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#Initialize)]

### <a name="step-3---load-managed-assembly-and-get-function-pointer-to-a-managed-method"></a>Krok 3. Załaduj zestaw zarządzany i Pobierz wskaźnik funkcji do metody zarządzanej

Delegat środowiska uruchomieniowego jest wywoływany, aby załadować zestaw zarządzany i uzyskać wskaźnik funkcji do metody zarządzanej. Delegat wymaga ścieżki zestawu, nazwy typu i nazwy metody jako danych wejściowych i zwraca wskaźnik funkcji, którego można użyć do wywołania metody zarządzanej.

[!code-cpp[HostFxrHost#LoadAndGet](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#LoadAndGet)]

Przekazując `nullptr` jako nazwę typu delegata podczas wywoływania delegata środowiska uruchomieniowego, przykład używa sygnatury domyślnej dla metody zarządzanej:

```csharp
public delegate int ComponentEntryPoint(IntPtr args, int sizeBytes);
```

Można użyć innej sygnatury, określając nazwę typu delegata podczas wywoływania delegata środowiska uruchomieniowego.

### <a name="step-4---run-managed-code"></a>Krok 4. uruchamianie kodu zarządzanego!

Host macierzysty może teraz wywołać metodę zarządzaną i przekazać do niej odpowiednie parametry.

[!code-cpp[HostFxrHost#CallManaged](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#CallManaged)]

## <a name="create-a-host-using-coreclrhosth"></a>Tworzenie hosta za pomocą `coreclrhost.h`

Poniższe kroki szczegółowo opisują sposób użycia `coreclrhost.h` interfejsu API w celu uruchomienia środowiska uruchomieniowego .NET Core w aplikacji natywnej i wywołania do zarządzanej metody statycznej. Fragmenty kodu w tym dokumencie używają niektórych interfejsów API specyficznych dla systemu Windows, ale [pełny przykładowy Host](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithCoreClrHost) pokazuje ścieżki kodu systemu Windows i Linux.

Host współdziałający w [systemie UNIX](https://github.com/dotnet/runtime/tree/master/src/coreclr/hosts/unixcorerun) przedstawia bardziej skomplikowany, rzeczywisty przykład hostingu przy użyciu `coreclrhost.h` .

### <a name="step-1---find-and-load-coreclr"></a>Krok 1 — Znajdowanie i ładowanie CoreCLR

Interfejsy API środowiska uruchomieniowego .NET Core są w *coreclr.dll* (w systemie Windows), w *libcoreclr.so* (w systemie Linux) lub w *Libcoreclr. DYLIB* (na macOS). Pierwszym krokiem do hostowania programu .NET Core jest załadowanie biblioteki CoreCLR. Niektóre hosty sonduje różne ścieżki lub używają parametrów wejściowych do znajdowania biblioteki, podczas gdy inni wiedzą, aby załadować ją z określonej ścieżki (obok hosta, na przykład lub z lokalizacji na całym komputerze).

Po znalezieniu biblioteka jest załadowana do programu `LoadLibraryEx` (w systemie Windows) lub `dlopen` (na platformie Linux/macOS).

[!code-cpp[CoreClrHost#1](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#1)]

### <a name="step-2---get-net-core-hosting-functions"></a>Krok 2. Uzyskiwanie funkcji hostingu platformy .NET Core

CoreClrHost ma kilka ważnych metod, które są przydatne do hostowania programu .NET Core:

* `coreclr_initialize`: Uruchamia środowisko uruchomieniowe programu .NET Core i konfiguruje domyślną (i tylko) domenę aplikacji.
* `coreclr_execute_assembly`: Wykonuje zestaw zarządzany.
* `coreclr_create_delegate`: Tworzy wskaźnik funkcji do metody zarządzanej.
* `coreclr_shutdown`: Zamyka środowisko uruchomieniowe platformy .NET Core.
* `coreclr_shutdown_2`: Jak `coreclr_shutdown` , ale również Pobiera kod zakończenia kodu zarządzanego.

Po załadowaniu biblioteki CoreCLR następnym krokiem jest uzyskanie odwołań do tych funkcji przy użyciu `GetProcAddress` systemu (w systemie Windows) lub `dlsym` (w systemie Linux/macOS).

[!code-cpp[CoreClrHost#2](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#2)]

### <a name="step-3---prepare-runtime-properties"></a>Krok 3 — Przygotowanie właściwości środowiska uruchomieniowego

Przed uruchomieniem środowiska uruchomieniowego należy przygotować pewne właściwości, aby określić zachowanie (zwłaszcza dotyczące modułu ładującego zestawy).

Typowe właściwości obejmują:

* `TRUSTED_PLATFORM_ASSEMBLIES` Jest to lista ścieżek zestawu (rozdzielonych znakami ";" w systemie Windows i ":" w systemie Linux), które środowisko uruchomieniowe będzie w stanie domyślnie rozpoznać. Niektóre hosty mają zakodowane manifesty zawierające listę zestawów, które mogą zostać załadowane. Inne umieściją dowolną bibliotekę w określonych lokalizacjach (obok *coreclr.dll*, na przykład) na tej liście.
* `APP_PATHS` Jest to lista ścieżek do sondowania w przypadku zestawu, jeśli nie można go znaleźć na liście zaufanych platform (TPA). Ponieważ Host ma większą kontrolę nad tym, które zestawy są ładowane przy użyciu listy TPA, najlepszym rozwiązaniem dla hostów jest określenie, które zestawy powinny być ładowane i wyświetlać je jawnie. Jeśli jednak jest wymagana sondowanie w czasie wykonywania, ta właściwość może włączyć ten scenariusz.
* `APP_NI_PATHS` Ta lista jest podobna do APP_PATHS z tą różnicą, że jest to ścieżka, która będzie sondowana w przypadku obrazów natywnych.
* `NATIVE_DLL_SEARCH_DIRECTORIES` Ta właściwość jest listą ścieżek, które moduł ładujący powinien sondować podczas wyszukiwania bibliotek natywnych wywoływanych za pomocą p/Invoke.
* `PLATFORM_RESOURCE_ROOTS` Ta lista zawiera ścieżki do sondowania w przypadku zestawów satelickich zasobów (w podkatalogach specyficznych dla kultury).

Na tym przykładowym hoście lista TPA jest tworzona przez wyświetlenie listy wszystkich bibliotek w bieżącym katalogu:

[!code-cpp[CoreClrHost#7](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#7)]

Ponieważ przykład jest prosty, wymaga tylko `TRUSTED_PLATFORM_ASSEMBLIES` Właściwości:

[!code-cpp[CoreClrHost#3](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#3)]

### <a name="step-4---start-the-runtime"></a>Krok 4. Uruchamianie środowiska uruchomieniowego

`coreclrhost.h` Interfejsy API uruchamiają środowisko uruchomieniowe i tworzą domyślną domenę aplikacji z pojedynczym wywołaniem. `coreclr_initialize`Funkcja przyjmuje ścieżkę bazową, nazwę i właściwości opisane wcześniej i zwraca dojście do hosta za pośrednictwem `hostHandle` parametru.

[!code-cpp[CoreClrHost#4](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#4)]

### <a name="step-5---run-managed-code"></a>Krok 5 — uruchamianie kodu zarządzanego!

Po uruchomieniu środowiska uruchomieniowego host może wywołać kod zarządzany. Można to zrobić na kilka różnych sposobów. Przykładowy kod połączony z tym samouczkiem używa `coreclr_create_delegate` funkcji, aby utworzyć delegata do statycznej metody zarządzanej. Ten interfejs API przyjmuje [nazwę zestawu](../../standard/assembly/names.md), nazwę typu kwalifikowanego przestrzeni nazw i nazwę metody jako dane wejściowe i zwraca delegat, którego można użyć do wywołania metody.

[!code-cpp[CoreClrHost#5](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#5)]

W tym przykładzie host może teraz wywołać, `managedDelegate` Aby uruchomić `ManagedWorker.DoWork` metodę.

Alternatywnie, `coreclr_execute_assembly` Funkcja może służyć do uruchamiania zarządzanego pliku wykonywalnego. Ten interfejs API Pobiera ścieżkę zestawu i tablicę argumentów jako parametry wejściowe. Ładuje zestaw w tej ścieżce i wywołuje jego metodę Main.

```c++
int hr = executeAssembly(
        hostHandle,
        domainId,
        argumentCount,
        arguments,
        "HelloWorld.exe",
        (unsigned int*)&exitCode);
```

### <a name="step-6---shutdown-and-clean-up"></a>Krok 6 — Zamykanie i oczyszczanie

Na koniec, gdy host wykonuje kod zarządzany, środowisko uruchomieniowe programu .NET Core jest zamykane z systemem `coreclr_shutdown` lub `coreclr_shutdown_2` .

[!code-cpp[CoreClrHost#6](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#6)]

CoreCLR nie obsługuje ponownego inicjowania ani zwalniania. Nie wywołuj `coreclr_initialize` ponownie ani nie zwalniaj biblioteki CoreCLR.

## <a name="conclusion"></a>Podsumowanie

Po skompilowaniu hosta może on być testowany przez uruchomienie go z wiersza polecenia i przekazanie wszelkich argumentów oczekiwanych przez hosta. Podczas określania aplikacji .NET Core do uruchomienia hosta upewnij się, że korzystasz z biblioteki DLL, która jest generowana przez `dotnet build` . Pliki wykonywalne (. exe) utworzone przez `dotnet publish` dla aplikacji samodzielnych są domyślnym hostem platformy .NET Core (aby można było uruchomić aplikację bezpośrednio z wiersza polecenia w scenariuszach linii głównej); kod użytkownika jest kompilowany do biblioteki DLL o tej samej nazwie.

Jeśli elementy nie działają na początku, należy sprawdzić, czy *coreclr.dll* jest dostępny w lokalizacji oczekiwanej przez hosta, że wszystkie niezbędne biblioteki struktury znajdują się na liście TPA i CoreCLR (32-bitowy lub 64-bitowy) są zgodne z sposobem kompilowania hosta.

Hostowanie środowiska uruchomieniowego .NET Core jest zaawansowanym scenariuszem, który nie jest wymagany dla wielu deweloperów, ale dla tych, którzy muszą uruchamiać kod zarządzany z procesu macierzystego lub którzy potrzebują większej kontroli nad zachowaniem środowiska uruchomieniowego programu .NET Core, może być bardzo przydatna.
