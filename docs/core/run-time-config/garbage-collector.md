---
title: Ustawienia konfiguracji modułu wyrzucania elementów bezużytecznych
description: Informacje o ustawieniach czasu wykonywania w celu skonfigurowania sposobu, w jaki moduł zbierający elementy bezużyteczne zarządza pamięcią dla aplikacji platformy .NET Core.
ms.date: 07/10/2020
ms.topic: reference
ms.openlocfilehash: 91d155b638c7e69b3d2c0216266a7c0c0410db4c
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915992"
---
# <a name="run-time-configuration-options-for-garbage-collection"></a>Opcje konfiguracji czasu wykonywania dla wyrzucania elementów bezużytecznych

Ta strona zawiera informacje na temat ustawień modułu zbierającego elementy bezużyteczne (GC), które można zmienić w czasie wykonywania. Jeśli próbujesz osiągnąć szczytową wydajność uruchomionej aplikacji, rozważ użycie tych ustawień. Jednak wartości domyślne zapewniają optymalną wydajność większości aplikacji w typowych sytuacjach.

Ustawienia są ułożone w grupach na tej stronie. Ustawienia w ramach każdej grupy są często używane w połączeniu ze sobą, aby osiągnąć konkretny wynik.

> [!NOTE]
>
> - Te ustawienia mogą być również dynamicznie zmieniane przez aplikację w trakcie działania, więc wszystkie ustawione ustawienia czasu wykonywania mogą zostać zastąpione.
> - Niektóre ustawienia, takie jak [poziom opóźnienia](../../standard/garbage-collection/latency.md), są zazwyczaj ustawiane tylko za pomocą interfejsu API w czasie projektowania. Takie ustawienia zostały pominięte na tej stronie.
> - W przypadku wartości liczbowych Użyj notacji dziesiętnej dla ustawień w *runtimeconfig.jsw* notacji plik i szesnastkowy dla ustawień zmiennych środowiskowych. W przypadku wartości szesnastkowych można je określić z prefiksem "0x" lub bez niego.

## <a name="flavors-of-garbage-collection"></a>Typy wyrzucania elementów bezużytecznych

Dwa główne typy wyrzucania elementów bezużytecznych to stacja robocza i serwer GC. Aby uzyskać więcej informacji o różnicach między tymi dwoma, zobacz [stacja robocza i odzyskiwanie pamięci serwera](../../standard/garbage-collection/workstation-server-gc.md).

Podelementy wyrzucania elementów bezużytecznych są tła i niewspółbieżne.

Użyj następujących ustawień, aby wybrać typy wyrzucania elementów bezużytecznych:

- [Stacja robocza a serwer GC](#workstation-vs-server)
- [Odzyskiwanie pamięci w tle](#background-gc)

### <a name="workstation-vs-server"></a>Stacja robocza a serwer

- Określa, czy aplikacja używa wyrzucania elementów bezużytecznych stacji roboczej lub odzyskiwania pamięci serwera.
- Domyślnie: wyrzucanie elementów bezużytecznych stacji roboczej. Jest to równoznaczne z ustawieniem wartości `false` .

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.Server` | `false`-Stacja robocza<br/>`true`— serwer | .NET Core 1,0 |
| **Właściwość programu MSBuild** | `ServerGarbageCollection` | `false`-Stacja robocza<br/>`true`— serwer | .NET Core 1,0 |
| **Zmienna środowiskowa** | `COMPlus_gcServer` | `0`-Stacja robocza<br/>`1`— serwer | .NET Core 1,0 |
| **app.config .NET Framework** | [GCServer](../../framework/configure-apps/file-schema/runtime/gcserver-element.md) | `false`-Stacja robocza<br/>`true`— serwer |  |

#### <a name="examples"></a>Przykłady

*runtimeconfig.js* pliku:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.Server": true
      }
   }
}
```

Plik projektu:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <ServerGarbageCollection>true</ServerGarbageCollection>
  </PropertyGroup>

</Project>
```

### <a name="background-gc"></a>Odzyskiwanie pamięci w tle

- Określa, czy jest włączone wyrzucanie elementów bezużytecznych w tle.
- Domyślne: Użyj w tle GC. Jest to równoznaczne z ustawieniem wartości `true` .
- Aby uzyskać więcej informacji, zobacz [wyrzucanie elementów bezużytecznych w tle](../../standard/garbage-collection/background-gc.md).

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.Concurrent` | `true`-w tle GC<br/>`false`-niewspółbieżne GC | .NET Core 1,0 |
| **Właściwość programu MSBuild** | `ConcurrentGarbageCollection` | `true`-w tle GC<br/>`false`-niewspółbieżne GC | .NET Core 1,0 |
| **Zmienna środowiskowa** | `COMPlus_gcConcurrent` | `1`-w tle GC<br/>`0`-niewspółbieżne GC | .NET Core 1,0 |
| **app.config .NET Framework** | [gcConcurrent](../../framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) | `true`-w tle GC<br/>`false`-niewspółbieżne GC |  |

#### <a name="examples"></a>Przykłady

*runtimeconfig.js* pliku:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.Concurrent": false
      }
   }
}
```

Plik projektu:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
  </PropertyGroup>

</Project>
```

## <a name="manage-resource-usage"></a>Zarządzanie użyciem zasobów

Użyj następujących ustawień, aby zarządzać pamięcią i użyciem procesora przez moduł wyrzucania elementów bezużytecznych:

- [Koligacji](#affinitize)
- [Koligacji, maska](#affinitize-mask)
- [Zakresy koligacji](#affinitize-ranges)
- [Grupy CPU](#cpu-groups)
- [Liczba stert](#heap-count)
- [Limit sterty](#heap-limit)
- [Procent limitu sterty](#heap-limit-percent)
- [Duża ilość pamięci (%)](#high-memory-percent)
- [Limity sterty dla poszczególnych obiektów](#per-object-heap-limits)
- [Procent limitów sterty dla poszczególnych obiektów](#per-object-heap-limit-percents)
- [Zachowaj maszynę wirtualną](#retain-vm)

Aby uzyskać więcej informacji na temat niektórych z tych ustawień, zapoznaj się z wpisem na blogu centrum [robocze i serwer GC](https://devblogs.microsoft.com/dotnet/middle-ground-between-server-and-workstation-gc/) .

### <a name="heap-count"></a>Liczba stert

- Ogranicza liczbę stert utworzonych przez moduł wyrzucania elementów bezużytecznych.
- Dotyczy tylko wyrzucania elementów bezużytecznych serwera.
- Jeśli [koligacja procesora GC](#affinitize) jest włączona, co jest ustawieniem domyślnym, licznik sterty ustawia `n` sterty/wątki skoligacony GC na pierwszy `n` procesor. (Użyj [koligacji maska](#affinitize-mask) lub ustawienia [zakresów koligacji](#affinitize-ranges) , aby określić, które procesory mają być koligacji).
- Jeśli [koligacja procesora GC](#affinitize) jest wyłączona, to ustawienie ogranicza liczbę stert GC.
- Aby uzyskać więcej informacji, zobacz [uwagi GCHeapCount](../../framework/configure-apps/file-schema/runtime/gcheapcount-element.md#remarks).

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapCount` | *wartość dziesiętna* | .NET Core 3.0 |
| **Zmienna środowiskowa** | `COMPlus_GCHeapCount` | *wartość szesnastkowa* | .NET Core 3.0 |
| **app.config .NET Framework** | [GCHeapCount](../../framework/configure-apps/file-schema/runtime/gcheapcount-element.md) | *wartość dziesiętna* | .NET Framework 4.6.2 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapCount": 16
      }
   }
}
```

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład aby ograniczyć liczbę stert do 16, wartości dla pliku JSON i 0x10 lub 10 dla zmiennej środowiskowej.

### <a name="affinitize-mask"></a>Koligacji, maska

- Określa dokładne procesory, które powinny być używane przez wątki modułu wyrzucania elementów bezużytecznych.
- Jeśli [koligacja procesora GC](#affinitize) jest wyłączona, to ustawienie jest ignorowane.
- Dotyczy tylko wyrzucania elementów bezużytecznych serwera.
- Wartość jest maską bitową, która definiuje procesory, które są dostępne dla procesu. Na przykład wartość dziesiętna 1023 (lub wartość szesnastkowa 0x3FF lub 3FF, jeśli używana jest zmienna środowiskowa) to 0011 1111 1111 w notacji binarnej. Oznacza to, że pierwsze 10 procesorów ma być używany. Aby określić następne 10 procesorów, czyli procesorów 10-19, określ wartość dziesiętną 1047552 (lub wartość szesnastkową 0xFFC00 lub FFC00), która jest równoważna z wartością binarną 1111 1111 1100 0000 0000.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapAffinitizeMask` | *wartość dziesiętna* | .NET Core 3.0 |
| **Zmienna środowiskowa** | `COMPlus_GCHeapAffinitizeMask` | *wartość szesnastkowa* | .NET Core 3.0 |
| **app.config .NET Framework** | [GCHeapAffinitizeMask](../../framework/configure-apps/file-schema/runtime/gcheapaffinitizemask-element.md) | *wartość dziesiętna* | .NET Framework 4.6.2 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapAffinitizeMask": 1023
      }
   }
}
```

### <a name="affinitize-ranges"></a>Zakresy koligacji

- Określa listę procesorów, które mają być używane na potrzeby wątków modułu wyrzucania elementów bezużytecznych.
- To ustawienie jest podobne do [System. GC. HeapAffinitizeMask](#affinitize-mask), z tą różnicą, że umożliwia określenie więcej niż 64 procesorów.
- W przypadku systemów operacyjnych Windows należy prefiksować numer procesora lub zakres z odpowiednią [grupą procesorów CPU](/windows/win32/procthread/processor-groups), na przykład "0:1-10, 0:12, 1:50-52, 1:70".
- Jeśli [koligacja procesora GC](#affinitize) jest wyłączona, to ustawienie jest ignorowane.
- Dotyczy tylko wyrzucania elementów bezużytecznych serwera.
- Aby uzyskać więcej informacji, zobacz temat [Zapewnianie lepszej konfiguracji procesora dla GC na maszynach z > 64 procesorów CPU](https://devblogs.microsoft.com/dotnet/making-cpu-configuration-better-for-gc-on-machines-with-64-cpus/) na blogu Maoni Stephens.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.GCHeapAffinitizeRanges` | Rozdzielana przecinkami lista numerów procesorów lub zakresów numerów procesorów.<br/>Przykład UNIX: "1-10, 12, 50-52, 70"<br/>Przykład systemu Windows: "0:1-10, 0:12, 1:50-52, 1:70" | .NET Core 3.0 |
| **Zmienna środowiskowa** | `COMPlus_GCHeapAffinitizeRanges` | Rozdzielana przecinkami lista numerów procesorów lub zakresów numerów procesorów.<br/>Przykład UNIX: "1-10, 12, 50-52, 70"<br/>Przykład systemu Windows: "0:1-10, 0:12, 1:50-52, 1:70" | .NET Core 3.0 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.GCHeapAffinitizeRanges": "0:1-10,0:12,1:50-52,1:70"
      }
   }
}
```

### <a name="cpu-groups"></a>Grupy CPU

- Określa, czy moduł wyrzucania elementów bezużytecznych używa [grup CPU](/windows/win32/procthread/processor-groups) , czy nie.

  Gdy 64-bitowy komputer z systemem Windows ma wiele grup CPU, oznacza to, że istnieje więcej niż 64 procesorów, włączając ten element rozszerza wyrzucanie elementów bezużytecznych we wszystkich grupach CPU. Moduł wyrzucania elementów bezużytecznych używa wszystkich rdzeni do tworzenia i równoważenia sterty.

- Stosuje się do wyrzucania elementów bezużytecznych serwera w 64-bitowych systemach operacyjnych Windows.
- Domyślnie: GC nie rozciąga się między grupami CPU. Jest to równoznaczne z ustawieniem wartości `0` .
- Aby uzyskać więcej informacji, zobacz temat [Zapewnianie lepszej konfiguracji procesora dla GC na maszynach z > 64 procesorów CPU](https://devblogs.microsoft.com/dotnet/making-cpu-configuration-better-for-gc-on-machines-with-64-cpus/) na blogu Maoni Stephens.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.CpuGroup` | `0`-wyłączone<br/>`1`-włączone | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPlus_GCCpuGroup` | `0`-wyłączone<br/>`1`-włączone | .NET Core 1,0 |
| **app.config .NET Framework** | [GCCpuGroup](../../framework/configure-apps/file-schema/runtime/gccpugroup-element.md) | `false`-wyłączone<br/>`true`-włączone |  |

> [!NOTE]
> Aby skonfigurować środowisko uruchomieniowe języka wspólnego (CLR) do dystrybucji wątków z puli wątków we wszystkich grupach procesora, Włącz opcję [Thread_UseAllCpuGroups elementu](../../framework/configure-apps/file-schema/runtime/thread-useallcpugroups-element.md) . W przypadku aplikacji platformy .NET Core można włączyć tę opcję, ustawiając wartość `COMPlus_Thread_UseAllCpuGroups` zmiennej środowiskowej na `1` .

### <a name="affinitize"></a>Koligacji

- Określa, czy *koligacji* wątki odzyskiwania pamięci z procesorami. Aby koligacji wątek GC, oznacza to, że można go uruchomić tylko w określonym procesorze CPU. Sterta jest tworzona dla każdego wątku GC.
- Dotyczy tylko wyrzucania elementów bezużytecznych serwera.
- Domyślnie: koligacji wątki odzyskiwania pamięci z procesorami. Jest to równoznaczne z ustawieniem wartości `false` .

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.NoAffinitize` | `false`-koligacji<br/>`true`-nie koligacji | .NET Core 3.0 |
| **Zmienna środowiskowa** | `COMPlus_GCNoAffinitize` | `0`-koligacji<br/>`1`-nie koligacji | .NET Core 3.0 |
| **app.config .NET Framework** | [GCNoAffinitize](../../framework/configure-apps/file-schema/runtime/gcnoaffinitize-element.md) | `false`-koligacji<br/>`true`-nie koligacji | .NET Framework 4.6.2 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.NoAffinitize": true
      }
   }
}
```

### <a name="heap-limit"></a>Limit sterty

- Określa maksymalny rozmiar zatwierdzeń w bajtach dla sterty GC i księgowości GC.
- To ustawienie dotyczy tylko komputerów 64-bitowych.
- To ustawienie jest ignorowane, jeśli skonfigurowano [limity sterty dla poszczególnych obiektów](#per-object-heap-limits) .
- Wartość domyślna, która stosuje się tylko w niektórych przypadkach, jest większa niż 20 MB lub 75% limitu pamięci w kontenerze. Wartość domyślna ma zastosowanie, jeśli:

  - Proces jest uruchomiony wewnątrz kontenera o określonym limicie pamięci.
  - Nie ustawiono wartości [System. GC. HeapHardLimitPercent](#heap-limit-percent) .

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimit` | *wartość dziesiętna* | .NET Core 3.0 |
| **Zmienna środowiskowa** | `COMPlus_GCHeapHardLimit` | *wartość szesnastkowa* | .NET Core 3.0 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapHardLimit": 209715200
      }
   }
}
```

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład aby określić stały limit sterty wynoszący 200 mebibytes (MiB), wartości byłyby 209715200 dla pliku JSON i 0xC800000 lub C800000 dla zmiennej środowiskowej.

### <a name="heap-limit-percent"></a>Procent limitu sterty

- Określa dozwolone użycie sterty GC jako procent całkowitej ilości pamięci fizycznej.
- Jeśli zostanie również ustawiona wartość [System. GC. HeapHardLimit](#heap-limit) , to ustawienie jest ignorowane.
- To ustawienie dotyczy tylko komputerów 64-bitowych.
- Jeśli proces jest uruchomiony wewnątrz kontenera o określonym limicie pamięci, wartość procentowa jest obliczana jako wartość procentowa tego limitu pamięci.
- To ustawienie jest ignorowane, jeśli skonfigurowano [limity sterty dla poszczególnych obiektów](#per-object-heap-limits) .
- Wartość domyślna, która jest stosowana tylko w niektórych przypadkach, jest mniejsza z 20 MB lub 75% limitu pamięci dla kontenera. Wartość domyślna ma zastosowanie, jeśli:

  - Proces jest uruchomiony wewnątrz kontenera o określonym limicie pamięci.
  - Nie ustawiono wartości [System. GC. HeapHardLimit](#heap-limit) .

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitPercent` | *wartość dziesiętna* | .NET Core 3.0 |
| **Zmienna środowiskowa** | `COMPlus_GCHeapHardLimitPercent` | *wartość szesnastkowa* | .NET Core 3.0 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapHardLimitPercent": 30
      }
   }
}
```

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład aby ograniczyć użycie sterty do 30%, wartości byłyby 30 dla pliku JSON i 0x1E lub 1E dla zmiennej środowiskowej.

### <a name="per-object-heap-limits"></a>Limity sterty dla poszczególnych obiektów

Można określić możliwość użycia sterty w pamięci podręcznej na podstawie sterty dla poszczególnych obiektów. Różne sterty to sterta dużego obiektu (LOH), sterta małego obiektu (raport o niewielkich obiektach) i przypięty stos obiektów (POH).

- W przypadku określenia wartości dla dowolnego z parametrów, `COMPLUS_GCHeapHardLimitSOH` `COMPLUS_GCHeapHardLimitLOH` lub `COMPLUS_GCHeapHardLimitPOH` , należy również określić wartość dla `COMPLUS_GCHeapHardLimitSOH` i `COMPLUS_GCHeapHardLimitLOH` . Jeśli tego nie zrobisz, nie będzie można zainicjować środowiska uruchomieniowego.
- Wartość domyślna dla `COMPLUS_GCHeapHardLimitPOH` jest równa 0. `COMPLUS_GCHeapHardLimitSOH`i `COMPLUS_GCHeapHardLimitLOH` nie mają wartości domyślnych.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitSOH` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPLUS_GCHeapHardLimitSOH` | *wartość szesnastkowa* | .NET 5,0 |

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitLOH` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPLUS_GCHeapHardLimitLOH` | *wartość szesnastkowa* | .NET 5,0 |

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitPOH` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPLUS_GCHeapHardLimitPOH` | *wartość szesnastkowa* | .NET 5,0 |

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład aby określić stały limit sterty wynoszący 200 mebibytes (MiB), wartości byłyby 209715200 dla pliku JSON i 0xC800000 lub C800000 dla zmiennej środowiskowej.

### <a name="per-object-heap-limit-percents"></a>Procent limitów sterty dla poszczególnych obiektów

Można określić możliwość użycia sterty w pamięci podręcznej na podstawie sterty dla poszczególnych obiektów. Różne sterty to sterta dużego obiektu (LOH), sterta małego obiektu (raport o niewielkich obiektach) i przypięty stos obiektów (POH).

- W przypadku określenia wartości dla dowolnego z parametrów, `COMPLUS_GCHeapHardLimitSOHPercent` `COMPLUS_GCHeapHardLimitLOHPercent` lub `COMPLUS_GCHeapHardLimitPOHPercent` , należy również określić wartość dla `COMPLUS_GCHeapHardLimitSOHPercent` i `COMPLUS_GCHeapHardLimitLOHPercent` . Jeśli tego nie zrobisz, nie będzie można zainicjować środowiska uruchomieniowego.
- Te ustawienia są ignorowane `COMPLUS_GCHeapHardLimitSOH` w przypadku, gdy `COMPLUS_GCHeapHardLimitLOH` `COMPLUS_GCHeapHardLimitPOH` są określone.
- Wartość 1 oznacza, że GC używa 1% całkowitej pamięci fizycznej dla sterty obiektu.
- Każda wartość musi być większa niż zero i mniejsza niż 100. Ponadto suma trzech wartości procentowych musi być mniejsza niż 100. W przeciwnym razie nie będzie można zainicjować środowiska uruchomieniowego.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitSOHPercent` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPLUS_GCHeapHardLimitSOHPercent` | *wartość szesnastkowa* | .NET 5,0 |

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitLOHPercent` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPLUS_GCHeapHardLimitLOHPercent` | *wartość szesnastkowa* | .NET 5,0 |

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HeapHardLimitPOHPercent` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPLUS_GCHeapHardLimitPOHPercent` | *wartość szesnastkowa* | .NET 5,0 |

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład aby ograniczyć użycie sterty do 30%, wartości byłyby 30 dla pliku JSON i 0x1E lub 1E dla zmiennej środowiskowej.

### <a name="high-memory-percent"></a>Duża ilość pamięci (%)

Obciążenie pamięci jest wskazywane przez procent używanej pamięci fizycznej. Domyślnie, gdy obciążenie pamięci fizycznej osiągnie **90%**, wyrzucanie elementów bezużytecznych jest bardziej agresywne na potrzeby tworzenia pełnych, kompaktowych kolekcji elementów bezużytecznych w celu uniknięcia stronicowania. Gdy obciążenie pamięci jest poniżej 90%, system GC preferuje kolekcje w tle dla pełnych kolekcji elementów bezużytecznych, które mają krótsze przerwy, ale nie zmniejszają łącznego rozmiaru sterty o wiele. Na maszynach ze znaczną ilością pamięci (80 GB lub więcej) domyślny próg obciążenia wynosi od 90% do 97%.

Próg dużego obciążenia pamięci można dostosować za pomocą `COMPlus_GCHighMemPercent` Ustawienia zmienna środowiskowa lub `System.GC.HighMemoryPercent` Konfiguracja JSON. Należy rozważyć dostosowanie progu, jeśli chcesz kontrolować rozmiar sterty. Na przykład w przypadku procesu dominującego na komputerze z 64 GB pamięci jest uzasadnione, aby system GC uruchomił odzyskiwanie, gdy jest dostępnych 10% pamięci. Jednak w przypadku mniejszych procesów, na przykład proces, który zużywa tylko 1 GB pamięci, wykaz globalny może wygodnie działać z mniej niż 10% dostępnej pamięci. W przypadku tych mniejszych procesów należy rozważyć ustawienie progu wyższego poziomu. Z drugiej strony, jeśli chcesz, aby większa liczba procesów miała mniejsze rozmiary sterty (nawet w przypadku dużej ilości dostępnej pamięci fizycznej), obniżenie tego progu jest skutecznym sposobem, aby system GC mógł już reagować na kompaktowanie sterty.

> [!NOTE]
> W przypadku procesów uruchomionych w kontenerze GC traktuje pamięć fizyczną na podstawie limitu kontenerów.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.HighMemoryPercent` | *wartość dziesiętna* | .NET 5,0 |
| **Zmienna środowiskowa** | `COMPlus_GCHighMemPercent` | *wartość szesnastkowa* | |

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład, aby ustawić wysoki próg pamięci na 75%, wartości byłyby 75 dla pliku JSON i 0x4B lub 4B dla zmiennej środowiskowej.

### <a name="retain-vm"></a>Zachowaj maszynę wirtualną

- Określa, czy segmenty, które mają zostać usunięte, są umieszczane na liście gotowości do użycia w przyszłości lub są wyłączane z powrotem do systemu operacyjnego (OS).
- Domyślnie: segmenty wydań z powrotem do systemu operacyjnego. Jest to równoznaczne z ustawieniem wartości `false` .

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.RetainVM` | `false`— wydanie do systemu operacyjnego<br/>`true`— Umieść w stanie wstrzymania | .NET Core 1,0 |
| **Właściwość programu MSBuild** | `RetainVMGarbageCollection` | `false`— wydanie do systemu operacyjnego<br/>`true`— Umieść w stanie wstrzymania | .NET Core 1,0 |
| **Zmienna środowiskowa** | `COMPlus_GCRetainVM` | `0`— wydanie do systemu operacyjnego<br/>`1`— Umieść w stanie wstrzymania | .NET Core 1,0 |

#### <a name="examples"></a>Przykłady

*runtimeconfig.js* pliku:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.RetainVM": true
      }
   }
}
```

Plik projektu:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
  </PropertyGroup>

</Project>
```

## <a name="large-pages"></a>Duże strony

- Określa, czy mają być używane duże strony, gdy jest ustawiony limit sztywny sterty.
- Domyślnie: nie używaj dużych stron, gdy jest ustawiony limit sztywny sterty. Jest to równoznaczne z ustawieniem wartości `0` .
- Jest to ustawienie eksperymentalne.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | NIE DOTYCZY | NIE DOTYCZY | NIE DOTYCZY |
| **Zmienna środowiskowa** | `COMPlus_GCLargePages` | `0`-wyłączone<br/>`1`-włączone | .NET Core 3.0 |

## <a name="allow-large-objects"></a>Zezwalaj na duże obiekty

- Konfiguruje obsługę modułu wyrzucania elementów bezużytecznych na platformach 64-bitowych dla tablic, które są większe niż 2 gigabajty (GB) w łącznym rozmiarze.
- Domyślnie: GLOBALna obsługa tablic o pojemności większej niż 2 GB. Jest to równoznaczne z ustawieniem wartości `1` .
- Ta opcja może stać się przestarzała w przyszłej wersji platformy .NET.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | NIE DOTYCZY | NIE DOTYCZY | NIE DOTYCZY |
| **Zmienna środowiskowa** | `COMPlus_gcAllowVeryLargeObjects` | `1`-włączone<br/> `0`-wyłączone | .NET Core 1,0 |
| **app.config .NET Framework** | [gcAllowVeryLargeObjects](../../framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md) | `1`-włączone<br/> `0`-wyłączone | .NET Framework 4.5 |

## <a name="large-object-heap-threshold"></a>Próg sterty dla dużego obiektu

- Określa rozmiar progu (w bajtach), który powoduje, że obiekty są na stosie dużego obiektu (LOH).
- Domyślny próg to 85 000 bajtów.
- Określona wartość musi być większa niż wartość progu domyślnego.

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | `System.GC.LOHThreshold` | *wartość dziesiętna* | .NET Core 1,0 |
| **Zmienna środowiskowa** | `COMPlus_GCLOHThreshold` | *wartość szesnastkowa* | .NET Core 1,0 |
| **app.config .NET Framework** | [GCLOHThreshold](../../framework/configure-apps/file-schema/runtime/gclohthreshold-element.md) | *wartość dziesiętna* |  .NET Framework 4.8 |

Przykład:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.LOHThreshold": 120000
      }
   }
}
```

> [!TIP]
> Jeśli ustawiasz opcję w *runtimeconfig.jsna*, określ wartość dziesiętną. Jeśli ustawiasz opcję jako zmienną środowiskową, określ wartość szesnastkową. Na przykład, aby ustawić rozmiar progu 120 000 bajtów, wartości byłyby 120000 dla pliku JSON oraz 0x1D4C0 lub 1D4C0 dla zmiennej środowiskowej.

## <a name="standalone-gc"></a>Autonomiczna GC

- Określa ścieżkę do biblioteki zawierającej Moduł wyrzucania elementów bezużytecznych, który środowisko uruchomieniowe zamierza załadować.
- Aby uzyskać więcej informacji, zobacz [prekonstrukcja modułu ładującego GC](https://github.com/dotnet/runtime/blob/master/docs/design/features/standalone-gc-loading.md).

| | Nazwa ustawienia | Wartości | Wprowadzona wersja |
| - | - | - | - |
| **runtimeconfig.jsna** | NIE DOTYCZY | NIE DOTYCZY | NIE DOTYCZY |
| **Zmienna środowiskowa** | `COMPlus_GCName` | *string_path* | .NET Core 2.0 |
