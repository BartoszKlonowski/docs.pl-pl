---
description: -platform (opcje kompilatora C#)
title: -platform (opcje kompilatora C#)
ms.date: 07/20/2015
f1_keywords:
- /platform
helpviewer_keywords:
- platform compiler option [C#]
- -platform compiler option [C#]
- /platform compiler option [C#]
ms.assetid: c290ff5e-47f4-4a85-9bb3-9c2525b0be04
ms.openlocfilehash: 3fdb030dfc141b011f5faa827a4e4bb45ae38d19
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2020
ms.locfileid: "89466017"
---
# <a name="-platform-c-compiler-options"></a>-platform (opcje kompilatora C#)

Określa, która wersja środowiska uruchomieniowego języka wspólnego (CLR) może uruchomić zestaw.

## <a name="syntax"></a>Składnia

```console
-platform:string
```

## <a name="parameters"></a>Parametry

`string` \
AnyCPU (domyślnie), anycpu32bitpreferred, ARM, x64, x86 lub Itanium.

## <a name="remarks"></a>Uwagi

- **AnyCPU** (domyślnie) kompiluje zestaw do uruchomienia na dowolnej platformie. Aplikacja działa jako proces 64-bitowy, gdy jest to możliwe, i wraca do 32-bitowej, gdy dostępny jest tylko ten tryb.

- **anycpu32bitpreferred** kompiluje zestaw do uruchamiania na dowolnej platformie. Aplikacja działa w trybie 32-bitowym w systemach, które obsługują zarówno aplikacje 64-bitowe, jak i 32-bitowe. Tę opcję można określić tylko dla projektów przeznaczonych dla .NET Framework 4,5 lub nowszych.

- **ARM** kompiluje zestaw do uruchomienia na komputerze z procesorem Advanced RISC Machine (ARM).

- **Arm64** kompiluje zestaw do uruchomienia przez 64-bitowe środowisko CLR na komputerze z procesorem Advanced RISC Machine (ARM), który obsługuje zestaw instrukcji A64.

- **x64** kompiluje zestaw do uruchomienia przez 64-bitowe środowisko CLR na komputerze, który obsługuje zestaw instrukcji AMD64 lub EM64T.

- **x86** kompiluje zestaw do uruchomienia przez 32-bitowe środowisko CLR zgodne z architekturą x86.

- **Procesor Itanium** kompiluje zestaw do uruchomienia przez 64-bitowe środowisko CLR na komputerze z procesorem Itanium.

W 64-bitowym systemie operacyjnym Windows:

- Zestawy skompilowane przy użyciu **-platform: x86** wykonaj na 32-bitowym CLR uruchomionym w emulatorze WOW64.

- Biblioteka DLL skompilowana z użyciem **platformy: anycpu** jest wykonywana w tym samym środowisku CLR co proces, w którym jest załadowana.

- Pliki wykonywalne, które są kompilowane z **-platformą: anycpu** execute na 64-bitowym CLR.

- Pliki wykonywalne skompilowane z **-platformą: anycpu32bitpreferred** execute na 32-bitowym CLR.

Ustawienie **anycpu32bitpreferred** jest prawidłowe tylko dla pliku wykonywalnego (. EXE) i wymaga .NET Framework 4,5 lub nowszego.

Aby uzyskać więcej informacji na temat tworzenia aplikacji do uruchamiania w systemie operacyjnym Windows 64-bitowym, zobacz [64-bitowe aplikacje](../../../framework/64-bit-apps.md).

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Aby ustawić tę opcję kompilatora w środowisku programowania Visual Studio

1. Otwórz stronę **Właściwości** dla projektu.

2. Kliknij stronę właściwości **kompilacja** .

3. Zmodyfikuj właściwość **Target platformy** i dla projektów, które są przeznaczone dla .NET Framework 4,5 lub nowszych, zaznacz lub wyczyść pole wyboru **Preferuj 32-bitowe** .

> [!NOTE]
> `-platform` nie jest dostępny w środowisku programistycznym w programie Visual C# Express.

Aby uzyskać informacje na temat sposobu, w jaki można programowo ustawić tę opcję kompilatora, zobacz <xref:VSLangProj80.CSharpProjectConfigurationProperties3.PlatformTarget%2A> .

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak używać opcji **-platform** , aby określić, że aplikacja powinna być uruchamiana przez 64-bitowe środowisko CLR w 64-bitowym systemie operacyjnym Windows.

```console
csc -platform:anycpu filename.cs
```

## <a name="see-also"></a>Zobacz także

- [Opcje kompilatora C#](index.md)
- [Zarządzanie właściwościami projektów i rozwiązań](/visualstudio/ide/managing-project-and-solution-properties)
