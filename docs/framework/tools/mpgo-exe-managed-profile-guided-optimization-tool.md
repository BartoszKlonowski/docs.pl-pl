---
title: Mpgo.exe (narzędzie optymalizacji sterowania zarządzanym profilem)
description: Użyj Mpgo.exe, narzędzia do optymalizacji z przewodnikiem zarządzanym profilem. Za pomocą tego narzędzia Optymalizuj zestawy obrazów natywnych utworzone przez generator obrazu natywnego (Ngen.exe).
ms.date: 03/30/2017
helpviewer_keywords:
- Mpgo.exe
- training scenarios, generating profiles with
- Managed Profile Guided Optimization Tool
- Ngen.exe
- Ngen.exe, profilers and native images
ms.assetid: f6976502-a000-4fbe-aaf5-a7aab9ce4ec2
ms.openlocfilehash: f8830b13cb64c737525f5399beb244aeb6d9817f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721897"
---
# <a name="mpgoexe-managed-profile-guided-optimization-tool"></a>Mpgo.exe (narzędzie optymalizacji sterowania zarządzanym profilem)

Zarządzane profilowanie narzędzia do optymalizacji z przewodnikiem (Mpgo.exe) to narzędzie wiersza polecenia, które używa typowych scenariuszy użytkowników końcowych do optymalizowania zestawów obrazów natywnych, które są tworzone przez [Generator obrazu natywnego (Ngen.exe)](ngen-exe-native-image-generator.md). To narzędzie umożliwia uruchamianie scenariuszy szkoleniowych, które generują dane profilu. [Generator obrazu natywnego (Ngen.exe)](ngen-exe-native-image-generator.md) używa tych danych do optymalizowania wygenerowanych zestawów aplikacji obrazu natywnego. Scenariusz szkoleniowy jest próbnym uruchomieniem oczekiwanego użycia aplikacji. Mpgo.exe jest dostępny w programie Visual Studio Ultimate 2012 i jego nowszych wersjach. Począwszy od Visual Studio 2013, można także użyć Mpgo.exe do optymalizowania aplikacji ze sklepu Windows 8. x.

Profilowana optymalizacja poprawia czas uruchamiania aplikacji, wykorzystanie pamięci (rozmiar zestawu roboczego) i przepustowość przez zbieranie danych ze scenariuszy szkoleniowych i używanie ich do optymalizowania układu obrazów natywnych.

Jeśli wystąpią problemy z wydajnością czasu uruchamiania i rozmiarem zestawu roboczego dla zestawów języka pośredniego (IL), zaleca się użyć w pierwszej kolejności Ngen.exe, aby wyeliminować koszty kompilacji JIT oraz umożliwić udostępnianie kodu. Jeśli potrzebujesz dodatkowych usprawnień, możesz użyć Mpgo.exe do dalszej optymalizacji aplikacji. Dane dotyczące wydajności z zestawów niezoptymalizowanego obrazu natywnego można zastosować jako podstawę do oszacowania wzrostu wydajności. Użycie Mpgo.exe może spowodować przyspieszenie zimnego uruchamiania i zmniejszenie rozmiaru zestawu roboczego. Mpgo.exe dodaje informacje do zestawów IL, których Ngen.exe używa do tworzenia zoptymalizowanych zestawów obrazu natywnego. Aby uzyskać więcej informacji, zobacz wpis [Poprawianie wydajności uruchamiania aplikacji klasycznych](https://devblogs.microsoft.com/dotnet/improving-launch-performance-for-your-desktop-applications/) w blogu platformy .NET.

To narzędzie jest instalowane automatycznie z programem Visual Studio. Aby uruchomić narzędzie, użyj wiersz polecenia dla deweloperów dla programu Visual Studio (lub wiersza polecenia programu Visual Studio w systemie Windows 7) z poświadczeniami administratora, a następnie wpisz następujące polecenie w wierszu polecenia. Aby uzyskać więcej informacji, zobacz [wiersza polecenia](developer-command-prompt-for-vs.md).

W przypadku aplikacji klasycznych:

```console
mpgo –Scenario <command> [-Import <directory>] –AssemblyList <assembly1>  <assembly2> ... -OutDir <directory> [options]
```

W przypadku aplikacji ze sklepu Windows 8. x:

## <a name="syntax"></a>Składnia

```console
mpgo –Scenario <packageName> -AppID <appId> -Timeout <seconds>
```

## <a name="parameters"></a>Parametry
 We wszystkich argumentach programu Mpgo.exe nie jest rozróżniana wielkość liter. Polecenia są poprzedzone kreską.

> [!NOTE]
> Możesz użyć albo `–Scenario` `–Import` jako wymaganego polecenia, ale nie obu jednocześnie. Jeśli określisz opcję, żaden z wymaganych parametrów nie jest używany `–Reset` .

|Wymagany parametr|Opis|
|------------------------|-----------------|
|`-Scenario` \<*command*><br /><br /> —lub—<br /><br /> `-Scenario` \<*packageName*><br /><br /> -lub-<br /><br /> `-Import` \<*directory*>|W przypadku aplikacji klasycznych Użyj `–Scenario` polecenia, aby określić polecenie uruchomienia aplikacji, którą chcesz zoptymalizować, w tym wszystkie argumenty wiersza polecenia. Użyj trzech zestawów podwójnych cudzysłowów wokół *polecenia* , jeśli określa ścieżkę obejmującą spacje; na przykład: `mpgo.exe -scenario """C:\My App\myapp.exe""" -assemblylist """C:\My App\myapp.exe""" -outdir "C:\optimized files"` . Nie należy używać podwójnych cudzysłowów; nie będą one działały prawidłowo, jeśli *polecenie* zawiera spacje.<br /><br /> -lub-<br /><br /> W przypadku aplikacji ze sklepu Windows 8. x Użyj, `–Scenario` Aby określić pakiet, dla którego chcesz wygenerować informacje o profilu. Jeśli określisz nazwę wyświetlaną pakietu lub nazwę rodziny pakietów zamiast pełnej nazwy pakietu, Mpgo.exe wybierze pakiet, który pasuje do podanej nazwy, pod warunkiem, że istnieje tylko jedno dopasowanie. Jeśli kilka pakietów odpowiada określonej nazwie, Mpgo.exe wyświetli monit o wybrania pakietu.<br /><br /> —lub—<br /><br /> Użyj `-Import` , aby określić, że dane optymalizacji z wcześniej zoptymalizowanych zestawów powinny być używane do optymalizowania zestawów w programie `-AssemblyList` . *katalog* określa katalog, który zawiera poprzednio zoptymalizowane pliki. Zestawy określone w `–AssemblyList` lub `–AssemblyListFile` są nowymi wersjami zestawów, które mają zostać zoptymalizowane przy użyciu danych z zaimportowanych plików. Używanie danych optymalizacji ze starszych wersji zestawów pozwala zoptymalizować nowsze wersje zestawów bez ponownego uruchamiania scenariusza.  Jednakże, jeśli zaimportowany i docelowy zestaw zawierają znacznie różniący się kod, dane optymalizacji będą nieskuteczne. Nazwy zestawów określone w `–AssemblyList` lub `–AssemblyListFile` muszą znajdować się w katalogu określonym przez `–Import` *katalog*. Użyj trzech zestawów podwójnych cudzysłowów wokół *katalogu* , jeśli określa ścieżkę obejmującą spacje.<br /><br /> Należy określić albo `–Scenario` `–Import` , ale nie oba parametry.|
|`-OutDir` \<*directory*>|Katalog, w którym będą umieszczone zoptymalizowane zestawy. Jeśli zestaw już istnieje w folderze katalogu wyjściowego, tworzona jest nowa kopia, a do jego nazwy jest dołączany numer indeksu. na przykład: *assemblyname*-1.exe. Użyj podwójnych cudzysłowów wokół *katalogu* , jeśli określa ścieżkę zawierającą spacje.|
|`-AssemblyList` \<*assembly1 assembly2 ...*><br /><br /> —lub—<br /><br /> `-AssemblyListFile` \<*file*>|Lista zestawów (w tym pliki exe i dll) rozdzielonych spacjami, dla których chcesz zbierać informacje profilowe. Możesz określić `C:\Dir\*.dll` lub `*.dll` wybrać wszystkie zestawy w wydzielonym lub bieżącym katalogu roboczym. Zobacz sekcję Spostrzeżenia, aby uzyskać więcej informacji.<br /><br /> —lub—<br /><br /> Plik tekstowy, który zawiera listę zestawów, dla których chcesz zebrać informacje o profilu. W każdym wierszu wymieniony jest jeden zestaw. Jeśli nazwa zestawu rozpoczyna się łącznikiem (-), użyj listy plików zestawów lub zmień nazwę zestawu.|
|`-AppID` \<*appId*>|Identyfikator aplikacji w określonym pakiecie. Jeśli używasz symbolu wieloznacznego ( \* ), Mpgo.exe spróbuje wyliczyć identyfikatory aplikacji w pakiecie i nastąpi powrót do \<*package_family_name*> ! Aplikacja w przypadku niepowodzenia. Jeżeli określono ciąg, który jest poprzedzony znakiem wykrzyknika (!), Mpgo.exe będzie łączyć nazwę rodziny pakietu z dostarczonym argumentem.|
|`-Timeout` \<*seconds*>|Ilość czasu zezwalająca na uruchomienie aplikacji ze sklepu Windows 8. x przed zakończeniem działania aplikacji.|

|Parametr opcjonalny|Opis|
|------------------------|-----------------|
|`-64bit`|Instrumentuje zestawy do systemów 64-bitowych.  Nawet jeśli zestaw jest zadeklarowany jako 64-bitowy, należy określić ten parametr dla zestawów 64-bitowych.|
|`-ExeConfig` \<*filename*>|Określa plik konfiguracji używany przez scenariusz do określenia informacje o wersji i module ładującym.|
|`-f`|Wymusza umieszczenie danych profilu w zestawie binarnym, nawet jeśli jest podpisany.  Jeśli zestaw jest podpisany, musi zostać ponownie podpisany; w przeciwnym razie zestawu nie będzie można załadować i uruchomić.|
|`-Reset`|Resetuje środowisko, aby była pewność, że przerwane sesje profilowania nie mają wpływu na swoje zestawy, a następnie kończy działanie. Środowisko jest resetowane domyślnie przed i po sesji profilowania.|
|`-Timeout` \<*time in seconds*>|Określa czas profilowania w sekundach. Użyj wartości, która jest nieco większa niż obserwowane czasy uruchamiania aplikacji GUI. Na koniec limitu czasu dane profilu są rejestrowana, mimo że aplikacja kontynuuje działanie. Jeśli ta opcja nie zostanie ustawiona, profilowanie będzie kontynuowane do czasu zamknięcia aplikacji, w czasie którym dane będą rejestrowane.|
|`-LeaveNativeImages`|Określa, że zinstrumentowane obrazy natywne nie powinny zostać usunięte po uruchomieniu tego scenariusza. Ta opcja jest używana przede wszystkim, gdy uzyskujesz aplikację, którą określono dla działającego scenariusza. Uniemożliwi to odtworzenie obrazów natywnych dla kolejnych uruchomień Mpgo.exe. W przypadku użycia tej opcji opcję w pamięci podręcznej po zakończeniu działania aplikacji mogą znajdować się oddzielone obrazy natywne. W takim przypadku należy uruchomić Mpgo.exe z tym samym scenariuszem i listą zestawów i użyć `–RemoveNativeImages` parametru, aby usunąć te obrazy natywne.|
|`-RemoveNativeImages`|Czyści z przebiegu, gdzie `–LeaveNativeImages` został określony. Jeśli określisz `-RemoveNativeImages` , Mpgo.exe ignoruje wszelkie argumenty z wyjątkiem `-64bit` i i `–AssemblyList` opuszcza po usunięciu wszystkich obrazów natywnych Instrumentacji.|

## <a name="remarks"></a>Uwagi
 `–AssemblyList` `- AssemblyListFile` W wierszu polecenia można wielokrotnie używać obu tych wartości.

 Jeśli nie określisz pełnych ścieżek podczas określania zestawów, Mpgo.exe będzie ich szukać w bieżącym katalogu. Jeśli określona ścieżka jest niepoprawna, Mpgo.exe wyświetla komunikat o błędzie, ale kontynuuje generowanie danych dla innych zestawów. Jeśli określisz zestaw, który nie jest ładowany podczas scenariusza szkoleniowego, żadne dane szkoleniowe nie są generowane dla tego zestawu.

 Jeśli zestaw na liście jest w globalnej pamięci podręcznej zestawów, nie będzie można zaktualizować go, aby zawierał informacje o profilu.  Usuń go z globalnej pamięci podręcznej zestawów, aby zebrać informacje o profilu.

 Użycie Ngen.exe i Mpgo.exe jest zalecane tylko dla dużych zarządzanych aplikacji, ponieważ korzyści wynikające ze wstępnie skompilowanym obrazów natywnych zazwyczaj są widoczne tylko wtedy, gdy eliminuje dużą część kompilacji JIT w czasie wykonywania. Uruchamianie Mpgo.exe w aplikacjach w stylu "Hello world", które nie działają w znacznym stopniu, nie zapewnia żadnych korzyści i Mpgo.exe może nawet nie być możliwe zebranie danych profilu.

> [!NOTE]
> Nie zaleca się stosowania Ngen.exe i Mpgo.exe w odniesieniu do aplikacji ASP.NET i usług Windows Communication Foundation (WCF).

## <a name="to-use-mpgoexe"></a>Aby użyć Mpgo.exe

1. Użyj komputera, na którym zainstalowano Visual Studio Ultimate 2012 i aplikację.

2. Uruchom Mpgo.exe jako administrator z wymaganymi parametrami.  W następnej sekcji znajdują się przykładowe polecenia.

     Zoptymalizowane zestawy języka pośredniego (IL) są tworzone w folderze określonym przez `–OutDir` parametr (w przykładach jest to `C:\Optimized` folder).

3. Zastąp zestawy IL używane na potrzeby Ngen.exe z nowymi zestawami IL zawierającymi informacje o profilu z katalogu określonego przez `–OutDir` .

4. Instalator aplikacji (przy użyciu obrazów dostarczonych przez Mpgo.exe) zainstaluje zoptymalizowane obrazy natywne.

## <a name="suggested-workflow"></a>Sugerowany przebieg pracy

1. Utwórz zestaw zoptymalizowanych zestawów IL przy użyciu Mpgo.exe z `–Scenario` parametrem.

2. Sprawdź zoptymalizowane zestawy IL w kontroli źródła.

3. W procesie kompilacji Wywołaj Mpgo.exe z `–Import` parametrem jako krok po kompilacji, aby generować zoptymalizowane obrazy Il do przekazania do Ngen.exe.

 Ten proces daje pewność, że wszystkie zestawy posiadają dane optymalizacji. Jeśli ewidencjonujesz zaktualizowane zoptymalizowane zestawy (kroki 1 i 2) częściej, wydajności będą spójniejsze w całym procesie tworzenia produktu.

## <a name="using-mpgoexe-from-visual-studio"></a>Przy użyciu Mpgo.exe z Visual Studio
 Mpgo.exe można uruchomić z programu Visual Studio (Zobacz artykuł [How to: Określanie zdarzeń kompilacji (C#)](/visualstudio/ide/how-to-specify-build-events-csharp)) z następującymi ograniczeniami:

- Nie można używać ścieżek w cudzysłowie ze znakami ukośnika na końcu, ponieważ makra Visual Studio również domyślnie używają końcowych ukośników. (Na przykład `–OutDir "C:\Output Folder\"` jest nieprawidłowy). Aby obejść to ograniczenie, można wyjść z końcowym ukośnikiem. (Na przykład użyj `-OutDir "$(OutDir)\"` zamiast tego).

- Domyślnie program Mpgo.exe nie znajduje się w ścieżce kompilacji programu Visual Studio. Możesz dodać ścieżkę do programu Visual Studio lub podać pełną ścieżkę w wierszu polecenia Mpgo. Możesz użyć albo `–Scenario` `–Import` parametru w zdarzeniu po kompilacji w programie Visual Studio. Typowym procesem jest jednak użycie `–Scenario` jednego czasu z wiersz polecenia dla deweloperów dla programu Visual Studio, a następnie użycie `–Import` go do zaktualizowania zoptymalizowanych zestawów po każdej kompilacji; na przykład:  `"C:\Program Files\Microsoft Visual Studio 11.0\Team Tools\Performance Tools\mpgo.exe" -import "$(OutDir)tmp" -assemblylist "$(TargetPath)" -outdir "$(OutDir)\"` .

<a name="samples"></a>
## <a name="examples"></a>Przykłady
 Następujące polecenie Mpgo.exe z wiersz polecenia dla deweloperów dla programu Visual Studio optymalizuje aplikację podatkową:

```console
mpgo –scenario "C:\MyApp\MyTax.exe /params par" –AssemblyList Mytax.dll MyTaxUtil2011.dll –OutDir C:\Optimized –TimeOut 15
```

 Następujące polecenie Mpgo.exe optymalizuje zdrową aplikację:

```console
mpgo –scenario "C:\MyApp\wav2wma.exe –input song1.wav –output song1.wma" –AssemblyList transcode.dll –OutDir C:\Optimized –TimeOut 15
```

 Następujące polecenie Mpgo.exe korzysta z danych z zestawów wcześniej zoptymalizowanych do optymalizacji nowszych wersji zestawów:

```console
mpgo.exe -import "C:\Optimized" -assemblylist "C:\MyApp\MyTax.dll" "C:\MyApp\MyTaxUtil2011.dll" -outdir C:\ReOptimized
```

## <a name="see-also"></a>Zobacz także

- [Ngen.exe (Generator obrazu natywnego)](ngen-exe-native-image-generator.md)
- [Wiersze poleceń](developer-command-prompt-for-vs.md)
- [Poprawianie wydajności uruchamiania aplikacji klasycznych](https://devblogs.microsoft.com/dotnet/improving-launch-performance-for-your-desktop-applications/)
- [Omówienie ulepszeń wydajności w .NET Framework 4,5](/archive/msdn-magazine/2012/april/clr-an-overview-of-performance-improvements-in-net-4-5)
