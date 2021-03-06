---
title: Wdrażanie aplikacji platformy .NET dla Apache Spark w kostkach
description: Dowiedz się, jak wdrożyć aplikację platformy .NET dla Apache Spark w usłudze datakostki.
ms.date: 10/09/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: d17fd5002d47dcde804cb43fc27edb2c2c9be595
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/17/2020
ms.locfileid: "94688153"
---
# <a name="tutorial-deploy-a-net-for-apache-spark-application-to-databricks"></a>Samouczek: wdrażanie aplikacji .NET dla Apache Spark w kostkach

W tym samouczku przedstawiono sposób wdrażania aplikacji w chmurze za pośrednictwem Azure Databricks, opartej na Apache Sparkj platformie analitycznej z instalacją jednym kliknięciem, usprawnionych przepływów pracy i interaktywnego obszaru roboczego, który umożliwia współpracę.

Z tego samouczka dowiesz się, jak wykonywać następujące czynności:

> [!div class="checklist"]
>
> - Tworzenie obszaru roboczego usługi Azure Databricks.
> - Opublikuj aplikację .NET dla Apache Spark.
> - Utwórz zadanie platformy Spark i klaster Spark.
> - Uruchom aplikację w klastrze Spark.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem wykonaj następujące zadania:

* Jeśli nie masz konta platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/dotnet/).
* Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
* Ukończ [platformę .NET dla Apache Spark — Rozpocznij pracę w 10-minutowym](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) samouczku.

## <a name="create-an-azure-databricks-workspace"></a>Tworzenie obszaru roboczego usługi Azure Databricks

> [!Note]
> Tego samouczka nie można przeprowadzić za pomocą **subskrypcji bezpłatnej wersji próbnej platformy Azure**.
> Jeśli masz bezpłatne konto, przejdź do swojego profilu i Zmień subskrypcję na **płatność zgodnie z rzeczywistym** użyciem. Aby uzyskać więcej informacji, zobacz [Bezpłatne konto platformy Azure](https://azure.microsoft.com/free/dotnet/). Następnie [Usuń limit wydatków](/azure/billing/billing-spending-limit#why-you-might-want-to-remove-the-spending-limit)i [Poproś o zwiększenie limitu przydziału](/azure/azure-supportability/resource-manager-core-quotas-request) dla procesorów wirtualnych vCPU w Twoim regionie. Podczas tworzenia obszaru roboczego Azure Databricks możesz wybrać warstwę cenową **wersji próbnej (Premium-14-Days Free dBu)** , aby umożliwić dostęp do obszaru roboczego bezpłatnie Azure Databricks DBU przez 14 dni.

W tej sekcji utworzysz obszar roboczy usługi Azure Databricks przy użyciu witryny Azure Portal.

1. W Azure Portal wybierz pozycję **Utwórz**  >  **Analytics**  >  **Azure Databricks** analizy zasobów.

   ![Tworzenie zasobu Azure Databricks w Azure Portal](./media/databricks-deployment/create-databricks-resource.png)

2. W obszarze **Usługa Azure Databricks** podaj wartości umożliwiające utworzenie obszaru roboczego usługi Databricks.

    |Właściwość  |Opis  |
    |---------|---------|
    |**Nazwa obszaru roboczego**     | Podaj nazwę obszaru roboczego usługi Databricks.        |
    |**Subskrypcja**     | Z listy rozwijanej wybierz subskrypcję platformy Azure.        |
    |**Grupa zasobów**     | Określ, czy chcesz utworzyć nową grupę zasobów, czy użyć istniejącej grupy. Grupa zasobów to kontener zawierający powiązane zasoby dla rozwiązania platformy Azure. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview). |
    |**Lokalizacja**     | Wybierz preferowany region. Aby uzyskać informacje na temat dostępnych regionów, zobacz [usługi platformy Azure dostępne według regionów](https://azure.microsoft.com/regions/services/).        |
    |**Warstwa cenowa**     |  Wybierz warstwę **standardowa**, **Premium** lub **wersja próbna**. Aby uzyskać więcej informacji o tych warstwach, zobacz [stronę usługi Databricks](https://azure.microsoft.com/pricing/details/databricks/).       |
    |**Virtual Network**     |   Nie       |

3. Wybierz pozycję **Utwórz**. Tworzenie obszaru roboczego trwa kilka minut. Podczas tworzenia obszaru roboczego można wyświetlić stan wdrożenia w obszarze **powiadomienia**.

## <a name="install-azure-databricks-tools"></a>Zainstaluj narzędzia Azure Databricks

Korzystając z **interfejsu wiersza polecenia datacegłs** , można nawiązać połączenie z klastrami Azure Databricks i przekazywać do nich pliki z komputera lokalnego. Klastry datacegły uzyskują dostęp do plików za poorednictwem DBFS (system plików).

1. Interfejs wiersza polecenia datakostki wymaga języka Python 3,6 lub nowszego. Jeśli masz już zainstalowany język Python, możesz pominąć ten krok.

   **Dla systemu Windows:**

   [Pobierz Język Python dla systemu Windows](https://www.python.org/ftp/python/3.7.4/python-3.7.4.exe)

   **Dla systemu Linux:** Środowisko Python jest preinstalowane na większości dystrybucji systemu Linux. Uruchom następujące polecenie, aby sprawdzić, która wersja została zainstalowana:

   ```bash
   python3 --version
   ```

2. Użyj narzędzia PIP, aby zainstalować interfejs wiersza polecenia datakosteks. Środowisko Python 3,4 i nowsze zawierają domyślnie funkcję PIP. Użyj PIP3 dla języka Python 3. Uruchom następujące polecenie:

   ```bash
   pip3 install databricks-cli
   ```

3. Po zainstalowaniu interfejsu wiersza polecenia datakostki Otwórz nowy wiersz poleceń i uruchom polecenie `databricks` . Jeśli zostanie wyświetlony komunikat " **" nie jest rozpoznawany jako błąd wewnętrzny lub zewnętrzny**, upewnij się, że otwarto nowy wiersz polecenia.

## <a name="set-up-azure-databricks"></a>Skonfiguruj Azure Databricks

Teraz, gdy masz zainstalowany interfejs wiersza polecenia datakosteks, musisz skonfigurować szczegóły uwierzytelniania.

1. Uruchom polecenie CLI w interfejsie wiersza polecenia `databricks configure --token` .

2. Po uruchomieniu polecenia Konfiguruj zostanie wyświetlony monit o wprowadzenie hosta. Adres URL hosta używa formatu: `https://<Location>.azuredatabricks.net` . Na przykład jeśli podczas tworzenia usługi Azure Databricks wybrano opcję **eastus2** , host będzie miał wartość `https://eastus2.azuredatabricks.net` .

3. Po wprowadzeniu hosta zostanie wyświetlony monit o wprowadzenie tokenu. W Azure Portal wybierz pozycję **Uruchom obszar roboczy** , aby uruchomić Azure Databricks obszar roboczy.

   ![Uruchom Azure Databricks obszar roboczy](./media/databricks-deployment/launch-databricks-workspace.png)

4. Na stronie głównej obszaru roboczego wybierz pozycję **Ustawienia użytkownika**.

   ![Ustawienia użytkownika w obszarze roboczym Azure Databricks](./media/databricks-deployment/databricks-user-settings.png)

5. Na stronie Ustawienia użytkownika można wygenerować nowy token. Skopiuj wygenerowany token i wklej go z powrotem do wiersza polecenia.

   ![Generuj nowy token dostępu w obszarze roboczym Azure Databricks](./media/databricks-deployment/generate-token.png)

Teraz powinno być możliwe uzyskanie dostępu do dowolnych klastrów Azure Databricks tworzenia i przekazywania plików do DBFS.

## <a name="download-worker-dependencies"></a>Pobierz zależności procesów roboczych

> [!Note]
> Platformy Azure i AWS datakostki są oparte na systemie Linux. W związku z tym, Jeśli interesuje Cię wdrażanie aplikacji w kostkach, upewnij się, że aplikacja jest .NET Standard zgodna i że używasz kompilatora .NET Core do kompilowania aplikacji.

1. Aplikacja Microsoft. Spark. Worker ułatwia Apache Spark wykonywanie aplikacji, na przykład dowolnych funkcji zdefiniowanych przez użytkownika (UDF). Pobierz [pakiet Microsoft. Spark. Worker](https://github.com/dotnet/spark/releases/download/v1.0.0/Microsoft.Spark.Worker.netcoreapp3.1.linux-x64-1.0.0.tar.gz).

2. *Install-Worker.sh* to skrypt, który umożliwia skopiowanie programu .net dla Apache Spark plików zależnych do węzłów klastra.

   Utwórz nowy plik o nazwie **Install-Worker.sh** na komputerze lokalnym i wklej [zawartość Install-Worker.sh](https://raw.githubusercontent.com/dotnet/spark/master/deployment/install-worker.sh) znajdującą się w witrynie GitHub.

3. *DB-init.sh* to skrypt służący do instalowania zależności w klastrze danych platformy Spark.

   Utwórz nowy plik o nazwie **DB-init.sh** na komputerze lokalnym i wklej [zawartość DB-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) znajdującą się w witrynie GitHub.

   W właśnie utworzonym pliku Ustaw `DOTNET_SPARK_RELEASE` zmienną na `https://github.com/dotnet/spark/releases/download/v1.0.0/Microsoft.Spark.Worker.netcoreapp3.1.linux-x64-1.0.0.tar.gz` . Pozostaw resztę pliku *DB-init.sh* .

> [!Note]
> Jeśli używasz systemu Windows, upewnij się, że końce wiersza w skryptach *Install-Worker.sh* i *DB-init.sh* są w stylu systemu UNIX (LF). Końce wierszy można zmienić za pomocą edytorów tekstu, takich jak Notatnik + + i Atom.

## <a name="publish-your-app"></a>Publikowanie aplikacji

Następnie opublikujesz *mySparkApp* utworzoną w programie [.net for Apache Spark — Rozpocznij w 10-minutowym](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) samouczku, aby zapewnić, że klaster Spark ma dostęp do wszystkich plików potrzebnych do uruchomienia aplikacji.

1. Uruchom następujące polecenia, aby opublikować *mySparkApp*:

   ```dotnetcli
   cd mySparkApp
   dotnet publish -c Release -f netcoreapp3.1 -r ubuntu.16.04-x64
   ```

2. Wykonaj następujące zadania w celu przesłania plików opublikowanych aplikacji, aby można je było łatwo przekazać do klastra Spark.

   **W systemie Windows:**

   Przejdź do mySparkApp/bin/Release/netcoreapp 3.1/Ubuntu. 16.04-x64. Następnie kliknij prawym przyciskiem myszy folder **Publikowanie** i wybierz polecenie **Wyślij do > folder skompresowany (zip)**. Nadaj nazwę nowemu folderowi **publish.zip**.

   **W systemie Linux Uruchom następujące polecenie:**

   ```bash
   zip -r publish.zip .
   ```

## <a name="upload-files"></a>Przekazywanie plików

W tej sekcji przekazano kilka plików do DBFS, aby klaster miał wszystko, czego potrzebuje do uruchomienia aplikacji w chmurze. Za każdym razem, gdy przekażesz plik do DBFS, upewnij się, że znajduje się w katalogu, w którym znajduje się ten plik na komputerze.

1. Uruchom następujące polecenia, aby przekazać *DB-init.sh*, *Install-Worker.sh* i *Microsoft. Spark. Worker* do DBFS:

   ```console
   databricks fs cp db-init.sh dbfs:/spark-dotnet/db-init.sh
   databricks fs cp install-worker.sh dbfs:/spark-dotnet/install-worker.sh
   databricks fs cp Microsoft.Spark.Worker.netcoreapp3.1.linux-x64-1.0.0.tar.gz dbfs:/spark-dotnet/Microsoft.Spark.Worker.netcoreapp3.1.linux-x64-1.0.0.tar.gz
   ```

2. Uruchom następujące polecenia, aby przekazać pozostałe pliki, do których klaster będzie musiał uruchomić aplikację: spakowany folder publikowania, *input.txt* i *Microsoft-Spark-2-4_ 2.11 — 1.0.0. jar*.

   ```console
   cd mySparkApp
   databricks fs cp input.txt dbfs:/input.txt

   cd mySparkApp\bin\Release\netcoreapp3.1\ubuntu.16.04-x64 directory
   databricks fs cp publish.zip dbfs:/spark-dotnet/publish.zip
   databricks fs cp microsoft-spark-2-4_2.11-1.0.0.jar dbfs:/spark-dotnet/microsoft-spark-2-4_2.11-1.0.0.jar
   ```

## <a name="create-a-job"></a>Tworzenie zadania

Aplikacja jest uruchamiana na Azure Databricks za pomocą zadania uruchamiającego żądanie uruchomienia platformy **Spark**, które jest poleceniem używanym do uruchamiania programu .net dla Apache Spark zadań.

1. W obszarze roboczym Azure Databricks wybierz ikonę **zadania** , a następnie pozycję **+ Utwórz zadanie**.

   ![Tworzenie zadania Azure Databricks](./media/databricks-deployment/create-job.png)

2. Wybierz tytuł zadania, a następnie wybierz pozycję Skonfiguruj platformę **Spark-Submit**.

   ![Konfigurowanie usługi Spark-Submit dla zadań datakostek](./media/databricks-deployment/configure-spark-submit.png)

3. Wklej następujące parametry w konfiguracji zadania. Następnie wybierz pozycję **Potwierdź**.

   ```
   ["--class","org.apache.spark.deploy.dotnet.DotnetRunner","/dbfs/spark-dotnet/microsoft-spark-2-4_2.11-1.0.0.jar","/dbfs/spark-dotnet/publish.zip","mySparkApp"]
   ```

## <a name="create-a-cluster"></a>Tworzenie klastra

1. Przejdź do zadania i wybierz pozycję **Edytuj** , aby skonfigurować klaster zadania.

2. Ustaw klaster na platformę **Spark 2.4.1**. Następnie wybierz pozycję **Opcje zaawansowane**  >  **init skrypty**. Ustaw ścieżkę skryptu init jako `dbfs:/spark-dotnet/db-init.sh` .

   ![Skonfiguruj klaster Spark w Azure Databricks](./media/databricks-deployment/cluster-config.png)

3. Wybierz pozycję **Potwierdź** , aby potwierdzić ustawienia klastra.

## <a name="run-your-app"></a>Uruchamianie aplikacji

1. Przejdź do zadania i wybierz pozycję **Uruchom teraz** , aby uruchomić zadanie w nowo skonfigurowanym klastrze Spark.

2. Utworzenie klastra zadania może potrwać kilka minut. Po jego utworzeniu zadanie zostanie przesłane i będzie można wyświetlić dane wyjściowe.

3. Z menu po lewej stronie wybierz pozycję **klastry** , a następnie nazwę i uruchomienie zadania.

4. Wybierz pozycję **dzienniki sterowników** , aby wyświetlić dane wyjściowe zadania. Gdy aplikacja zakończy wykonywanie, zobaczysz tę samą tabelę Count wyrazów z uruchomienia lokalnego uruchamiania zapisaną w standardowej konsoli wyjściowej.

   ![Azure Databricks tabeli wyjściowej zadania](./media/databricks-deployment/table-output.png)

   Gratulacje, uruchomiono pierwszą aplikację .NET dla Apache Spark w Azure Databricks.

## <a name="clean-up-resources"></a>Czyszczenie zasobów

Jeśli obszar roboczy datakostki nie jest już potrzebny, możesz usunąć zasób Azure Databricks w Azure Portal. Dodatkowo możesz wybrać nazwę grupy zasobów, aby otworzyć stronę grupy zasobów, a następnie wybrać pozycję **Usuń grupę zasobów**.

## <a name="next-steps"></a>Następne kroki

W tym samouczku wdrożono aplikację .NET dla Apache Spark w usłudze datakostki. Aby dowiedzieć się więcej na temat datakostki, przejdź do dokumentacji Azure Databricks.

> [!div class="nextstepaction"]
> [Dokumentacja usługi Azure Databricks](/azure/azure-databricks/)
