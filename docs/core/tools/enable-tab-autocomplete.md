---
title: Włączanie uzupełniania po naciśnięciu tabulatora
description: W tym artykule opisano, jak włączyć uzupełnianie kart dla interfejs wiersza polecenia platformy .NET Core dla programu PowerShell, bash i ZSH.
author: adegeo
ms.author: adegeo
ms.topic: how-to
ms.date: 11/03/2019
ms.openlocfilehash: cd46305b8cd82825671a3a1568e8b93de1bbab26
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062811"
---
# <a name="how-to-enable-tab-completion-for-the-net-core-cli"></a>Jak włączyć uzupełnianie kart dla interfejs wiersza polecenia platformy .NET Core

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach

W tym artykule opisano sposób konfigurowania uzupełniania tabulatorów dla trzech powłok, programu PowerShell, bash i ZSH. W przypadku innych powłok należy zapoznać się z dokumentacją dotyczącą konfigurowania uzupełniania kart.

Po skonfigurowaniu, uzupełnianie kart dla interfejs wiersza polecenia platformy .NET Core jest wyzwalane przez wpisanie `dotnet` polecenia w powłoce, a następnie naciśnięcie klawisza Tab. Bieżący wiersz polecenia jest wysyłany do `dotnet complete` polecenia, a wyniki są przetwarzane przez powłokę. Wyniki można testować bez włączania kończenia karty, wysyłając coś bezpośrednio do `dotnet complete` polecenia. Na przykład:

```console
> dotnet complete "dotnet a"
add
clean
--diagnostics
migrate
pack
```

Jeśli to polecenie nie działa, upewnij się, że jest zainstalowany zestaw .NET Core 2,0 SDK lub nowszy. Jeśli jest zainstalowana, ale to polecenie nadal nie działa, upewnij się, że `dotnet` polecenie jest rozpoznawane jako wersja zestawu SDK platformy .NET Core 2,0 i nowsze. Użyj `dotnet --version` polecenia, aby sprawdzić `dotnet` , która wersja bieżącej ścieżki jest rozpoznawana. Aby uzyskać więcej informacji, zobacz [Wybieranie wersji platformy .NET Core do użycia](../versions/selection.md).

### <a name="examples"></a>Przykłady

Poniżej przedstawiono kilka przykładów zapewniania przez uzupełnianie kart:

Dane wejściowe                                | stanowi                                                                     | , ponieważ klienci usługi
:------------------------------------|:----------------------------------------------------------------------------|:--------------------------------
`dotnet a⇥`                          | `dotnet add`                                                                 | `add`to pierwsze polecenie, alfabetycznie.
`dotnet add p⇥`                      | `dotnet add --help`                                                          | Uzupełnianie tabulacji dopasowuje podciągi i pojawia się w `--help` pierwszej kolejności alfabetycznie.
`dotnet add p⇥⇥`                    | `dotnet add package`                                                          | Naciśnięcie klawisza Tab drugi raz spowoduje wyświetlenie następnej sugestii.
`dotnet add package Microsoft⇥`      | `dotnet add package Microsoft.ApplicationInsights.Web`                      | Wyniki są zwracane w porządku alfabetycznym.
`dotnet remove reference ⇥`          | `dotnet remove reference ..\..\src\OmniSharp.DotNet\OmniSharp.DotNet.csproj` | Uzupełnianie karty jest świadome pliku projektu.

## <a name="powershell"></a>PowerShell

Aby dodać uzupełnianie tabulatorów do **programu PowerShell** dla interfejs wiersza polecenia platformy .NET Core, Utwórz lub Edytuj profil przechowywany w zmiennej `$PROFILE` . Aby uzyskać więcej informacji, zobacz [jak utworzyć profil](/powershell/module/microsoft.powershell.core/about/about_profiles#how-to-create-a-profile) i [zasady wykonywania](/powershell/module/microsoft.powershell.core/about/about_profiles#profiles-and-execution-policy).

Dodaj następujący kod do swojego profilu:

```powershell
# PowerShell parameter completion shim for the dotnet CLI
Register-ArgumentCompleter -Native -CommandName dotnet -ScriptBlock {
     param($commandName, $wordToComplete, $cursorPosition)
         dotnet complete --position $cursorPosition "$wordToComplete" | ForEach-Object {
            [System.Management.Automation.CompletionResult]::new($_, $_, 'ParameterValue', $_)
         }
 }
```

## <a name="bash"></a>bash

Aby dodać uzupełnianie karty do powłoki **bash** dla interfejs wiersza polecenia platformy .NET Core, Dodaj następujący kod do `.bashrc` pliku:

```bash
# bash parameter completion for the dotnet CLI

_dotnet_bash_complete()
{
  local word=${COMP_WORDS[COMP_CWORD]}

  local completions
  completions="$(dotnet complete --position "${COMP_POINT}" "${COMP_LINE}" 2>/dev/null)"
  if [ $? -ne 0 ]; then
    completions=""
  fi

  COMPREPLY=( $(compgen -W "$completions" -- "$word") )
}

complete -f -F _dotnet_bash_complete dotnet
```

## <a name="zsh"></a>zsh

Aby dodać uzupełnianie karty do powłoki **ZSH** dla interfejs wiersza polecenia platformy .NET Core, Dodaj następujący kod do `.zshrc` pliku:

```zsh
# zsh parameter completion for the dotnet CLI

_dotnet_zsh_complete()
{
  local completions=("$(dotnet complete "$words")")

  reply=( "${(ps:\n:)completions}" )
}

compctl -K _dotnet_zsh_complete dotnet
```
