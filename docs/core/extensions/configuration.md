---
title: Konfiguracja w programie .NET
description: Dowiedz się, jak skonfigurować aplikacje .NET przy użyciu interfejsu API konfiguracji.
author: IEvangelist
ms.author: dapine
ms.date: 09/16/2020
ms.topic: overview
ms.openlocfilehash: 5955e46c2f5acb6776ada4e3fd6a65507d3faa1f
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740125"
---
# <a name="configuration-in-net"></a>Konfiguracja w programie .NET

Konfiguracja w programie .NET jest przeprowadzana przy użyciu co najmniej jednego [dostawcy konfiguracji](#configuration-providers). Dostawcy konfiguracji odczytują dane konfiguracji z par klucz-wartość przy użyciu różnych źródeł konfiguracji:

- Pliki ustawień, takie jak *appsettings.jswłączone*
- Zmienne środowiskowe
- [Usługa Azure Key Vault](/azure/key-vault/general/overview)
- [Azure App Configuration](/azure/azure-app-configuration/overview)
- Argumenty wiersza polecenia
- Niestandardowi dostawcy, instalowani lub utworzony
- Pliki katalogu
- Obiekty w pamięci .NET

## <a name="configure-console-apps"></a>Konfigurowanie aplikacji konsolowych

Nowe aplikacje konsolowe platformy .NET utworzone przy użyciu programu [dotnet New](../tools/dotnet-new.md) lub Visual Studio domyślnie *nie* ujawniają możliwości konfiguracji. Aby dodać konfigurację w nowej aplikacji konsolowej .NET, [Dodaj odwołanie do pakietu](../tools/dotnet-add-package.md) do `Microsoft.Extensions.Hosting` . Zmodyfikuj plik *program.cs* , aby pasował do następującego kodu:

:::code language="csharp" source="snippets/configuration/console/Program.cs" highlight="18":::

<xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])?displayProperty=nameWithType>Metoda zapewnia domyślną konfigurację dla aplikacji w następującej kolejności:

1. [ChainedConfigurationProvider](xref:Microsoft.Extensions.Configuration.ChainedConfigurationSource) : Dodaje istniejący element `IConfiguration` jako źródło.
1. *appsettings.js* przy użyciu [dostawcy konfiguracji JSON](configuration-providers.md#file-configuration-provider).
1. *appSettings.* `Environment` *. JSON* przy użyciu [dostawcy konfiguracji JSON](configuration-providers.md#file-configuration-provider). Na przykład *AppSettings*. ***Produkcja * * _._json* i *AppSettings*. * * * programowanie** _._json *.
1. Wpisy tajne aplikacji, gdy aplikacja jest uruchamiana w `Development` środowisku.
1. Zmienne środowiskowe używające [dostawcy konfiguracji zmiennych środowiskowych](configuration-providers.md#environment-variable-configuration-provider).
1. Argumenty wiersza polecenia przy użyciu [dostawcy konfiguracji wiersza polecenia](configuration-providers.md#command-line-configuration-provider).

Dostawcy konfiguracji, którzy zostaną dodani później przesłaniają poprzednie ustawienia klucza. Na przykład jeśli `SomeKey` jest ustawiona zarówno w *appsettings.js* , jak i w środowisku, zostanie użyta wartość środowiska. Przy użyciu domyślnych dostawców konfiguracji [dostawca konfiguracji wiersza polecenia](configuration-providers.md#command-line-configuration-provider) zastępuje wszystkich innych dostawców.

### <a name="binding"></a>Wiązanie

Jedną z kluczowych zalet konfiguracji w programie .NET jest możliwość powiązania wartości konfiguracji z wystąpieniami obiektów .NET. Na przykład dostawca konfiguracji JSON może służyć do mapowania *appsettings.js* plików na obiekty .NET i jest używany z iniekcją zależności. Umożliwia to wzorzec opcji, wzorzec opcji używa klas w celu zapewnienia silnie określonego dostępu do grup powiązanych ustawień.

## <a name="configuration-providers"></a>Dostawcy konfiguracji

W poniższej tabeli przedstawiono dostawców konfiguracji dostępnych dla aplikacji .NET Core.

| Dostawca                                                                                                               | Zapewnia konfigurację z        |
|------------------------------------------------------------------------------------------------------------------------|------------------------------------|
| [Dostawca konfiguracji aplikacji platformy Azure](/azure/azure-app-configuration/quickstart-aspnet-core-app)                          | Azure App Configuration            |
| [Dostawca konfiguracji Azure Key Vault](/azure/key-vault/general/tutorial-net-virtual-machine)                        | W usłudze Azure Key Vault                    |
| [Dostawca konfiguracji wiersza polecenia](configuration-providers.md#command-line-configuration-provider)                  | Parametry wiersza polecenia            |
| [Niestandardowy dostawca konfiguracji](custom-configuration-provider.md)                                                      | Źródło niestandardowe                      |
| [Dostawca konfiguracji zmiennych środowiskowych](configuration-providers.md#environment-variable-configuration-provider) | Zmienne środowiskowe              |
| [Dostawca konfiguracji plików](configuration-providers.md#file-configuration-provider)                                  | Pliki JSON, XML i INI           |
| [Dostawca konfiguracji klucza dla plików](configuration-providers.md#key-per-file-configuration-provider)                  | Pliki katalogu                    |
| [Dostawca konfiguracji pamięci](configuration-providers.md#memory-configuration-provider)                              | Kolekcje w pamięci              |
| [Wpisy tajne aplikacji (Menedżer wpisów tajnych)](/aspnet/core/security/app-secrets)                                                      | Plik w katalogu profilu użytkownika |

Aby uzyskać więcej informacji na temat różnych dostawców konfiguracji, zobacz [dostawcy konfiguracji w programie .NET](configuration-providers.md).

## <a name="see-also"></a>Zobacz także

- [Dostawcy konfiguracji w programie .NET](configuration-providers.md)
- [Implementowanie niestandardowego dostawcy konfiguracji](custom-configuration-provider.md)
- Usterki konfiguracji należy utworzyć w repozytorium [GitHub.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
