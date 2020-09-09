---
title: dotnet-dump-.NET Core
description: Instalowanie i używanie narzędzia wiersza polecenia dotnet-dump.
ms.date: 10/14/2019
ms.openlocfilehash: e008dcfc734a8742c495ea32a7a149c9a55c54c6
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598113"
---
# <a name="dump-collection-and-analysis-utility-dotnet-dump"></a>Narzędzie do zbierania i analizowania zrzutów (dotnet-dump)

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach

> [!NOTE]
> `dotnet-dump` nie jest obsługiwane w macOS.

## <a name="install-dotnet-dump"></a>Zainstaluj program dotnet-dump

Aby zainstalować najnowszą wersję `dotnet-dump` [pakietu NuGet](https://www.nuget.org/packages/dotnet-dump), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :

```dotnetcli
dotnet tool install -g dotnet-dump
```

## <a name="synopsis"></a>Streszczenie

```console
dotnet-dump [-h|--help] [--version] <command>
```

## <a name="description"></a>Opis

`dotnet-dump`Globalne Narzędzie to sposób zbierania i analizowania zrzutów systemów Windows i Linux bez żadnego natywnego debugera, który jest taki sam jak `lldb` w systemie Linux. To narzędzie jest ważne na platformach, takich jak Alpine Linux, gdy w pełni działa `lldb` nie jest dostępny. `dotnet-dump`Narzędzie pozwala uruchamiać polecenia sos w celu analizowania awarii i modułu wyrzucania elementów bezużytecznych (GC), ale nie jest to debuger natywny, więc nie są obsługiwane elementy, takie jak wyświetlanie natywnych ramek stosu.

## <a name="options"></a>Opcje

- **`--version`**

  Wyświetla wersję narzędzia dotnet-dump.

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

## <a name="commands"></a>Polecenia

| Polecenie                                     |
| ------------------------------------------- |
| [Platforma dotnet — Zbieranie zrzutów](#dotnet-dump-collect) |
| [Analiza zrzutów dotnet](#dotnet-dump-analyze) |

## <a name="dotnet-dump-collect"></a>Platforma dotnet — Zbieranie zrzutów

Przechwytuje Zrzut z procesu.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-dump collect [-h|--help] [-p|--process-id] [--type] [-o|--output] [--diag]
```

### <a name="options"></a>Opcje

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

- **`-p|--process-id <PID>`**

  Określa numer identyfikatora procesu, z którego ma zostać zebrany zrzut pamięci.

- **`--type <Full|Heap|Mini>`**

  Określa typ zrzutu, który określa rodzaje informacji zbieranych z procesu. Istnieją trzy typy:

  - `Full` -Największy zrzut zawierający całą pamięć, łącznie z obrazami modułu.
  - `Heap` -Duży i stosunkowo kompleksowy zrzut zawierający listy modułów, listy wątków, wszystkie stosy, informacje o wyjątkach, informacje o obsłudze i wszystkie pamięci z wyjątkiem zamapowanych obrazów.
  - `Mini` -Mały zrzut zawierający listy modułów, listy wątków, informacje o wyjątku i wszystkie stosy.

  Jeśli nie zostanie określony, `Full` jest wartością domyślną.

- **`-o|--output <output_dump_path>`**

  Pełna ścieżka i nazwa pliku, w którym ma zostać zapisany zebrany zrzut.

  Jeśli nie zostanie określony:

  - Wartość domyślna to *. \ dump_YYYYMMDD_HHMMSS. dmp* w systemie Windows.
  - Wartość domyślna to *./core_YYYYMMDD_HHMMSS* w systemie Linux.

  RRRRMMDD to rok/miesiąc/dzień, a HHMMSS to godzina/minutę/sekundę.

- **`--diag`**

  Włącza rejestrowanie diagnostyczne kolekcji zrzutów.

## <a name="dotnet-dump-analyze"></a>Analiza zrzutów dotnet

Uruchamia powłokę interaktywną w celu eksplorowania zrzutu. Powłoka akceptuje różne [polecenia sos](#analyze-sos-commands).

### <a name="synopsis"></a>Streszczenie

```console
dotnet-dump analyze <dump_path> [-h|--help] [-c|--command]
```

### <a name="arguments"></a>Argumenty

- **`<dump_path>`**

  Określa ścieżkę do pliku zrzutu do przeanalizowania.

### <a name="options"></a>Opcje

- **`-c|--command <debug_command>`**

  Określa [polecenie](#analyze-sos-commands) , które ma być uruchamiane w powłoce przy uruchamianiu.

### <a name="analyze-sos-commands"></a>Analizowanie poleceń SOS

| Polecenie                             | Funkcja                                                                                      |
| ----------------------------------- | --------------------------------------------------------------------------------------------- |
| `soshelp`                           | Wyświetla wszystkie dostępne polecenia                                                               |
| `soshelp|help <command>`            | Wyświetla określone polecenie.                                                               |
| `exit|quit`                         | Zamyka tryb interaktywny.                                                                       |
| `clrstack <arguments>`              | Dostarcza ślad stosu wyłącznie dla kodu zarządzanego.                                                  |
| `clrthreads <arguments>`            | Wyświetla listę zarządzanych wątków, na których działa program.                                                            |
| `dumpasync <arguments>`             | Wyświetla informacje o maszynach stanu asynchronicznego na stertie zebranych elementów bezużytecznych.                |
| `dumpassembly <arguments>`          | Wyświetla szczegółowe informacje o zestawie.                                                           |
| `dumpclass <arguments>`             | Wyświetla informacje o strukturze klasy EE pod podanym adresem.                     |
| `dumpdelegate <arguments>`          | Wyświetla informacje o delegacie.                                                        |
| `dumpdomain <arguments>`            | Wyświetla informacje o wszystkich domenach aplikacji i wszystkich zestawach należących do domen.                |
| `dumpheap <arguments>`              | Wyświetla informacje na temat sterty i statystyk zbierania danych bezużytecznych dotyczących obiektów.       |
| `dumpil <arguments>`                | Wyświetla język pośredni Microsoft (MSIL) skojarzony z zarządzaną metodą. |
| `dumplog <arguments>`               | Zapisuje zawartość dziennika obciążenia pamięci do określonego pliku.                         |
| `dumpmd <arguments>`                | Wyświetla informacje o strukturze MethodDesc pod podanym adresem.                   |
| `dumpmodule <arguments>`            | Wyświetla informacje o strukturze modułu EE pod podanym adresem.                    |
| `dumpmt <arguments>`                | Wyświetla informacje dotyczące tabeli metod pod podanym adresem.                           |
| `dumpobj <arguments>`               | Wyświetla informacje o obiekcie pod podanym adresem.                                       |
| `dso|dumpstackobjects <arguments>`  | Wyświetla wszystkie zarządzane obiekty znalezione w granicach bieżącego stosu.                    |
| `eeheap <arguments>`                | Wyświetla informacje o pamięci procesu używanej przez wewnętrzne struktury danych środowiska uruchomieniowego.              |
| `finalizequeue <arguments>`         | Wyświetla wszystkie obiekty zarejestrowane dla finalizacji.                                             |
| `gcroot <arguments>`                | Wyświetla informacje o odwołaniach (lub elementach głównych) do obiektu pod podanym adresem.              |
| `gcwhere <arguments>`               | Wyświetla lokalizację w stercie GC argumentu przekazano.                               |
| `ip2md <arguments>`                 | Wyświetla strukturę MethodDesc o określonym adresie w kodzie JIT.                       |
| `histclear <arguments>`             | Zwalnia wszystkie zasoby używane przez rodzinę `hist*` poleceń.                                |
| `histinit <arguments>`              | Inicjuje struktury SOS z dziennika obciążenia zapisanego w obiekcie debugowanym.                     |
| `histobj <arguments>`               | Wyświetla przemieszczenie dzienników obciążeniowych wyrzucania elementów bezużytecznych powiązanych z `<arguments>` .              |
| `histobjfind <arguments>`           | Wyświetla wszystkie wpisy dziennika, które odwołują się do obiektu pod podanym adresem.               |
| `histroot <arguments>`              | Wyświetla informacje powiązane zarówno z promocjami, jak i przeniesieniami określonego korzenia.        |
| `lm|modules`                        | Wyświetla moduły macierzyste w procesie.                                                   |
| `name2ee <arguments>`               | Wyświetla strukturę metody i strukturę EEClass dla `<argument>` .                |
| `pe|printexception <arguments>`     | Wyświetla dowolny obiekt pochodny od klasy Exception pod adresem `<argument>` .             |
| `setsymbolserver <arguments>`       | Włącza obsługę serwera symboli                                                             |
| `syncblk <arguments>`               | Wyświetla informacje o posiadaczu SyncBlock.                                                           |
| `threads|setthread <threadid>`      | Ustawia lub wyświetla bieżący identyfikator wątku dla poleceń SOS.                                  |

## <a name="using-dotnet-dump"></a>Korzystanie z akcji `dotnet-dump`

Pierwszym krokiem jest zebranie zrzutu. Ten krok można pominąć, jeśli zrzut podstawowy został już wygenerowany. System operacyjny lub wbudowana [Funkcja generowania zrzutów](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) środowiska uruchomieniowego platformy .NET Core może tworzyć zrzuty rdzeni.

```console
$ dotnet-dump collect --process-id 1902
Writing minidump to file ./core_20190226_135837
Written 98983936 bytes (24166 pages) to core file
Complete
```

Teraz Analizuj podstawowy zrzut przy użyciu `analyze` polecenia:

```console
$ dotnet-dump analyze ./core_20190226_135850
Loading core dump: ./core_20190226_135850
Ready to process analysis commands. Type 'help' to list available commands or 'help [command]' to get detailed help on a command.
Type 'quit' or 'exit' to exit the session.
>
```

Ta akcja wywołuje interaktywną sesję, która akceptuje polecenia takie jak:

```console
> clrstack
OS Thread Id: 0x573d (0)
    Child SP               IP Call Site
00007FFD28B42C58 00007fb22c1a8ed9 [HelperMethodFrame_PROTECTOBJ: 00007ffd28b42c58] System.RuntimeMethodHandle.InvokeMethod(System.Object, System.Object[], System.Signature, Boolean, Boolean)
00007FFD28B42DD0 00007FB1B1334F67 System.Reflection.RuntimeMethodInfo.Invoke(System.Object, System.Reflection.BindingFlags, System.Reflection.Binder, System.Object[], System.Globalization.CultureInfo) [/root/coreclr/src/mscorlib/src/System/Reflection/RuntimeMethodInfo.cs @ 472]
00007FFD28B42E20 00007FB1B18D33ED SymbolTestApp.Program.Foo4(System.String) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 54]
00007FFD28B42ED0 00007FB1B18D2FC4 SymbolTestApp.Program.Foo2(Int32, System.String) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 29]
00007FFD28B42F00 00007FB1B18D2F5A SymbolTestApp.Program.Foo1(Int32, System.String) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 24]
00007FFD28B42F30 00007FB1B18D168E SymbolTestApp.Program.Main(System.String[]) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 19]
00007FFD28B43210 00007fb22aa9cedf [GCFrame: 00007ffd28b43210]
00007FFD28B43610 00007fb22aa9cedf [GCFrame: 00007ffd28b43610]
```

Aby wyświetlić nieobsłużony wyjątek, który zabicia aplikacji:

```console
> pe -lines
Exception object: 00007fb18c038590
Exception type:   System.Reflection.TargetInvocationException
Message:          Exception has been thrown by the target of an invocation.
InnerException:   System.Exception, Use !PrintException 00007FB18C038368 to see more.
StackTrace (generated):
SP               IP               Function
00007FFD28B42DD0 0000000000000000 System.Private.CoreLib.dll!System.RuntimeMethodHandle.InvokeMethod(System.Object, System.Object[], System.Signature, Boolean, Boolean)
00007FFD28B42DD0 00007FB1B1334F67 System.Private.CoreLib.dll!System.Reflection.RuntimeMethodInfo.Invoke(System.Object, System.Reflection.BindingFlags, System.Reflection.Binder, System.Object[], System.Globalization.CultureInfo)+0xa7 [/root/coreclr/src/mscorlib/src/System/Reflection/RuntimeMethodInfo.cs @ 472]
00007FFD28B42E20 00007FB1B18D33ED SymbolTestApp.dll!SymbolTestApp.Program.Foo4(System.String)+0x15d [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 54]
00007FFD28B42ED0 00007FB1B18D2FC4 SymbolTestApp.dll!SymbolTestApp.Program.Foo2(Int32, System.String)+0x34 [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 29]
00007FFD28B42F00 00007FB1B18D2F5A SymbolTestApp.dll!SymbolTestApp.Program.Foo1(Int32, System.String)+0x3a [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 24]
00007FFD28B42F30 00007FB1B18D168E SymbolTestApp.dll!SymbolTestApp.Program.Main(System.String[])+0x6e [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 19]

StackTraceString: <none>
HResult: 80131604
```

## <a name="special-instructions-for-docker"></a>Specjalne instrukcje dotyczące platformy Docker

Jeśli używasz programu Docker, Zbieranie zrzutów wymaga `SYS_PTRACE` możliwości ( `--cap-add=SYS_PTRACE` lub `--privileged` ).

W przypadku obrazów platformy Docker w systemie Microsoft .NET Core SDK Linux niektóre `dotnet-dump` polecenia mogą zgłosić następujący wyjątek:

> Nieobsłużony wyjątek: System.DllNotFoundException: nie można załadować biblioteki udostępnionej "libdl.so" ani jednego z jej wyjątków zależności.

Aby obejść ten problem, zainstaluj pakiet "libc6-dev".

## <a name="see-also"></a>Zobacz też

- [Zbieranie i analizowanie blogów zrzutów pamięci](https://devblogs.microsoft.com/dotnet/collecting-and-analyzing-memory-dumps/)
- [Narzędzie do analizy sterty (dotnet-gcdump)](dotnet-gcdump.md)
