---
title: Generator serializatorów XML firmy Microsoft
description: Omówienie generatora serializatorów XML firmy Microsoft. Użyj generatora serializatorów XML, aby wygenerować zestaw serializacji XML dla typów zawartych w projekcie.
author: mlacouture
ms.date: 01/19/2017
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 8005a8a3e5202b0255ec482dfb7e3c284bc2e19b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90538907"
---
# <a name="using-microsoft-xml-serializer-generator-on-net-core"></a>Używanie generatora serializatorów Microsoft XML na platformie .NET Core

W tym samouczku przedstawiono sposób użycia generatora serializatorów XML firmy Microsoft w aplikacji .NET Core w języku C#. W ramach tego samouczka nauczysz się:

> [!div class="checklist"]
>
> - Jak utworzyć aplikację .NET Core
> - Jak dodać odwołanie do pakietu Microsoft.XmlSerializer.Generator
> - Jak edytować plik MyApp.csproj, aby dodać zależności
> - Jak dodać klasę i obiekt XmlSerializer
> - Jak skompilować i uruchomić aplikację

Podobnie jak w przypadku [generatora serializatorów XML (sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md) dla .NET Framework, [ pakiet NuGetMicrosoft.Xmlserializator. Generator](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator) jest odpowiednikiem dla projektów .NET Core i .NET Standard. Tworzy zestaw serializacji XML dla typów zawartych w zestawie, aby zwiększyć wydajność podczas uruchamiania serializacji XML podczas serializacji lub deserializacji obiektów tych typów przy użyciu <xref:System.Xml.Serialization.XmlSerializer> .

## <a name="prerequisites"></a>Wymagania wstępne

W celu ukończenia tego samouczka:

- [.NET Core 2,1 SDK](https://dotnet.microsoft.com/download) lub nowszy.
- Twój ulubiony Edytor kodu.

> [!TIP]
> Musisz zainstalować Edytor kodu? Wypróbuj [program Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)!

## <a name="use-microsoft-xml-serializer-generator-in-a-net-core-console-application"></a>Używanie generatora serializatorów Microsoft XML w aplikacji konsolowej platformy .NET Core

Poniższe instrukcje pokazują, jak używać generatora serializatorów XML w aplikacji konsolowej programu .NET Core.

### <a name="create-a-net-core-console-application"></a>Tworzenie aplikacji konsolowej platformy .NET Core

Otwórz wiersz polecenia i Utwórz folder o nazwie *MojaApl*. Przejdź do utworzonego folderu i wpisz następujące polecenie:

```dotnetcli
dotnet new console
```

### <a name="add-a-reference-to-the-microsoftxmlserializergenerator-package-in-the-myapp-project"></a>Dodaj odwołanie do pakietu Microsoft.Xmlserializator. Generator w projekcie MojaApl

Użyj [`dotnet add package`](../tools/dotnet-add-package.md) polecenia, aby dodać odwołanie w projekcie.

Wpisz:

```dotnetcli
dotnet add package Microsoft.XmlSerializer.Generator -v 1.0.0
```

### <a name="verify-changes-to-myappcsproj-after-adding-the-package"></a>Sprawdź zmiany w programie MojaApl. csproj po dodaniu pakietu

Otwórz Edytor kodu i zacznijmy pracę! Nadal pracujemy nad katalogiem *MojaApl* , w którym została skompilowana aplikacja.

Otwórz w edytorze tekstów *MojaApl. csproj* .

Po uruchomieniu [`dotnet add package`](../tools/dotnet-add-package.md) polecenia do pliku projektu *MojaApl. csproj* są dodawane następujące wiersze:

 ```xml
 <ItemGroup>
    <PackageReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```

### <a name="add-another-itemgroup-section-for-net-core-cli-tool-support"></a>Dodaj kolejną sekcję elementu Item dla interfejs wiersza polecenia platformy .NET Core pomocy technicznej narzędzi

Dodaj następujące wiersze po `ItemGroup` sekcji, którą sprawdzisz:

 ```xml
 <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```

### <a name="add-a-class-in-the-application"></a>Dodawanie klasy w aplikacji

Otwórz *program.cs* w edytorze tekstu. Dodaj klasę o nazwie *MyClass* w *program.cs*.

```csharp
public class MyClass
{
   public int Value;
}
```

### <a name="create-an-xmlserializer-for-myclass"></a>Utwórz `XmlSerializer` dla elementu MyClass

Dodaj następujący wiersz w obszarze *głównym* , aby utworzyć `XmlSerializer` for MyClass:

```csharp
var serializer = new System.Xml.Serialization.XmlSerializer(typeof(MyClass));
```

### <a name="build-and-run-the-application"></a>Kompilowanie i uruchamianie aplikacji

W folderze *MojaApl* należy uruchomić aplikację za pośrednictwem programu, która [`dotnet run`](../tools/dotnet-run.md) automatycznie ładuje i używa wstępnie wygenerowanych serializatorów w czasie wykonywania.

W oknie konsoli wpisz następujące polecenie:

```dotnetcli
dotnet run
```

> [!NOTE]
> [`dotnet run`](../tools/dotnet-run.md) wywołuje [`dotnet build`](../tools/dotnet-build.md) się, by upewnić się, że cele kompilacji zostały skompilowane, a następnie wywołuje, `dotnet <assembly.dll>` Aby uruchomić aplikację docelową.

> [!IMPORTANT]
> Polecenia i kroki przedstawione w tym samouczku do uruchamiania aplikacji są używane tylko w czasie projektowania. Gdy wszystko będzie gotowe do wdrożenia aplikacji, zapoznaj się z różnymi [strategiami wdrażania](../deploying/index.md) aplikacji .NET Core i [`dotnet publish`](../tools/dotnet-publish.md) poleceniem.

Jeśli wszystko powiedzie się, zestaw o nazwie *MyApp.XmlSerializers.dll* zostanie wygenerowany w folderze wyjściowym.

Gratulacje! Masz właśnie:
> [!div class="checklist"]
>
> - Utworzono aplikację platformy .NET Core.
> - Dodano odwołanie do pakietu Microsoft.Xmlserializator. Generator.
> - Edycja programu MojaApl. csproj w celu dodania zależności.
> - Dodano klasę i element XmlSerializer.
> - Aplikacja została skompilowana i uruchomiona.

## <a name="related-resources"></a>Powiązane zasoby

- [Wprowadzenie do serializacji XML](../../standard/serialization/introducing-xml-serialization.md)
- [Jak serializować przy użyciu elementu XmlSerializer (C#)](../../standard/linq/serialize-xmlserializer.md)
- [Instrukcje: Serializowanie przy użyciu elementu XmlSerializer (Visual Basic)](../../standard/linq/serialize-xmlserializer.md)
