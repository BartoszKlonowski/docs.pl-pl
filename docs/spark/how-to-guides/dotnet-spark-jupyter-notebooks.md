---
title: Korzystanie z notesów Jupyter
titleSuffix: .NET for Apache Spark
description: Korzystanie z platformy .NET dla Apache Spark w środowiskach interaktywnych, takich jak Jupyter Notebook, Jupyter Lab lub Visual Studio Code (VS Code)
ms.author: luquinta
author: luisquintanilla
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc, how-to
ms.openlocfilehash: cf19b4e4b7a7b9033fb97b2b2736ab0383c11f93
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96598936"
---
# <a name="use-net-for-apache-spark-in-jupyter-notebooks"></a>Korzystanie z platformy .NET dla Apache Spark w notesach Jupyter

W tym artykule dowiesz się, jak uruchomić program .NET dla zadań Apache Spark interaktywnie w Jupyter Notebook i Visual Studio Code (VS Code) przy użyciu programu .NET Interactive.

## <a name="about-jupyter"></a>Informacje o Jupyter

[Jupyter](https://jupyter.org/) to środowisko obliczeniowe typu "open source", które zapewnia użytkownikom interaktywny prototyp i programowanie aplikacji. Można korzystać z Jupyter za pomocą wielu różnych interfejsów, takich jak Jupyter Notebook, Jupyter Lab i VS Code.

W kontekście platformy .NET, [.NET Interactive](https://github.com/dotnet/interactive), narzędzia globalne platformy .NET Core, zapewnia jądro do pisania kodu platformy .NET (C#/f #) w środowiskach interaktywnego przetwarzania, takich jak Jupyter Notebook.

## <a name="prerequisites"></a>Wymagania wstępne

- [Zestaw SDK platformy .NET Core 3,1](../../core/install/index.yml)
- [Apache Spark](https://spark.apache.org/downloads.html)
- [Apache Spark proces roboczy platformy .NET](https://github.com/dotnet/spark/releases)

Zobacz [samouczek wprowadzenie](../tutorials/get-started.md) , aby uzyskać więcej informacji na temat konfigurowania środowiska .net for Apache Spark.

## <a name="prepare-environment"></a>Przygotowywanie środowiska

Aby pracować z notesami Jupyter, musisz mieć dwie rzeczy.

1. Zainstaluj [interaktywne narzędzie .NET Interactive](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)
1. Pobierz `Microsoft.Spark` pakiet NuGet.
    1. Przejdź do strony pakietu NuGet [Microsoft. Spark](https://www.nuget.org/packages/Microsoft.Spark/) .

        > [!IMPORTANT]
        > Domyślnie pobierana jest Najnowsza wersja pakietu. **Upewnij się, że pobierana wersja jest taka sama jak Apache Spark roboczym programu .NET.**

    1. W okienku **informacje** wybierz pozycję **Pobierz pakiet** , aby pobrać najnowszą wersję pakietu. Nazwa pakietu jest podobna do  *Microsoft. Spark. [ Pakiet — wersja]. nupkg*.
    1. Rozpakuj pobrany pakiet. Niespakowany katalog powinien zawierać podkatalog o nazwie *Jars*. Zanotuj ścieżkę, ponieważ jest ona używana w późniejszym czasie.

## <a name="start-net-for-apache-spark"></a>Uruchom platformę .NET dla Apache Spark

Uruchom następujące polecenie, aby uruchomić platformę .NET dla Apache Spark w trybie debugowania. To `spark-submit` polecenie uruchamia proces i czeka na połączenia z [SparkSession](xref:Microsoft.Spark.Sql.SparkSession). Upewnij się, że ścieżka do `microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar` odpowiedniej wersji platformy .NET dla Apache Spark jest używana.

**Ubuntu**

```bash
spark-submit \
    --class org.apache.spark.deploy.dotnet.DotnetRunner \
    --master local \
    <path-to-microsoft-spark-jar> \
    debug
```

**Windows**

```cmd
spark-submit ^
    --class org.apache.spark.deploy.dotnet.DotnetRunner ^
    --master local ^
    <path-to-microsoft-spark-jar> ^
    debug
```

## <a name="create-a-notebook"></a>Tworzenie notesu

Można użyć różnych interfejsów do współpracy z Jupyter. W przypadku interfejsu opartego na przeglądarce należy używać notesów Jupyter lub laboratorium Jupyter. W przypadku środowiska lokalnego edytora Użyj VS Code.

### <a name="jupyter-notebooks--jupyter-lab"></a>Jupyter notesy & Jupyter Lab

1. W innym wierszu polecenia Uruchom Jupyter Notebook lub Jupyter Lab przy użyciu jednego z poniższych poleceń:

    **Jupyter Notebook**

    ```bash
    jupyter notebook
    ```

    **Jupyter Lab**

    ```bash
    jupyter lab
    ```

    Te polecenia powodują uruchomienie okna przeglądarki z interfejsem laboratorium Jupyter Notebook lub Jupyter.

1. W przeglądarce Utwórz nowy Notes.

    **Jupyter Notebook**

    Wybierz pozycję **nowy > .NET (C#)** lub **Nowy > .NET (F #)**

    **Jupyter Lab**

    W oknie uruchamiania wybierz pozycję **.NET (C#)** lub **.NET (F #)**

### <a name="visual-studio-code-preview"></a>Visual Studio Code (wersja zapoznawcza)

> [!IMPORTANT]
> Aby korzystać z notesów Jupyter w VS Code, należy zainstalować następujące polecenie:
>
>- [VS Code niejawnych testerów](https://code.visualstudio.com/insiders/)
>- [Rozszerzenie programu .NET Interactive Notes](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)

1. Otwórz program VS Code.
1. Otwórz widok palety poleceń **> palecie poleceń**.

    Gdy zostanie wyświetlona paleta poleceń, wprowadź następujące polecenie, aby utworzyć nowy interaktywny Notes .NET:

    ```text
    >.NET Interactive: Create new blank notebook
    ```

    Alternatywnie, jeśli chcesz otworzyć istniejący Notes programu .NET Interactive z rozszerzeniem *ipynb* , użyj następującego polecenia:

    ```text
    >.NET Interactive: Open notebook
    ```

## <a name="initialize-a-spark-session"></a>Inicjowanie sesji platformy Spark

1. Po otwarciu notesu zainstaluj `Microsoft.Spark` pakiet NuGet. Upewnij się, że instalowana wersja jest taka sama jak proces roboczy platformy .NET.

    ```text
    #r "nuget:Microsoft.Spark, 0.12.1"
    ```

1. Dodaj następującą instrukcję using do notesu.

    ```csharp
    using Microsoft.Spark.Sql;
    ```

1. Zainicjuj [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).

    ```csharp
    var sparkSession =
    SparkSession
        .Builder()
        .AppName("dotnet-interactive-spark")
        .GetOrCreate();
    ```

Notes powinien wyglądać podobnie do poniższego na poniższej ilustracji. Ten przykład używa VS Code, ale Jupyter Notebook i Jupyter Lab powinien wyglądać tak samo.

> [!div class="mx-imgBorder"]
![Środowisko .NET dla Apache Spark Jupyter Notebook VS Code](media/dotnet-spark-jupyter-notebooks/jupyter-notebooks-dotnet-spark-vscode.png)

## <a name="next-steps"></a>Następne kroki

- [Wprowadzenie do platformy .NET dla Apache Spark](../tutorials/get-started.md)
- [Przewidywania tonacji przy użyciu platformy .NET dla Apache Spark i ML.NET](../tutorials/ml-sentiment-analysis.md)
- Aby uzyskać więcej informacji na temat programu .NET Interactive, zapoznaj się z [dokumentacją programu .NET Interactive](https://github.com/dotnet/interactive/blob/main/docs/README.md).
