---
title: Zainstaluj platformę .NET dla Apache Spark w notesach Jupyter w klastrach Azure HDInsight Spark
description: Dowiedz się, jak zainstalować platformę .NET dla Apache Spark w notesach Jupyter usługi Azure HDInsight.
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: ff6b3a64c01fb9148d3abe3d04579233d11a4f73
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599658"
---
# <a name="install-net-for-apache-spark-on-jupyter-notebooks-on-azure-hdinsight-spark-clusters"></a>Zainstaluj platformę .NET dla Apache Spark w notesach Jupyter w klastrach Azure HDInsight Spark

W tym artykule przedstawiono sposób instalowania programu .NET for Apache Spark w notesach Jupyter w klastrach Azure HDInsight Spark. Platformę .NET dla Apache Spark w klastrach usługi Azure HDInsight można wdrożyć za pomocą kombinacji wiersza polecenia i Azure Portal (Aby uzyskać więcej informacji, zobacz artykuł [jak wdrożyć aplikację .net for Apache Spark w usłudze Azure HDInsight](../tutorials/hdinsight-deployment.md)), ale notesy zapewniają bardziej interaktywną i iteracyjną pracę.

Klastry usługi Azure HDInsight są już dołączone do notesów Jupyter, więc wystarczy skonfigurować notesy Jupyter do uruchamiania programu .NET dla Apache Spark. Aby można było używać platformy .NET do Apache Spark w notesach Jupyter, w języku c# REPL jest potrzebny do wykonania kodu w języku C# i zachowania stanu wykonywania w razie potrzeby. [Wypróbuj platformę .NET](https://github.com/dotnet/try) jako oficjalną REPL .NET.

Aby włączyć platformę .NET dla Apache Spark za pomocą środowiska Jupyter notesy, należy wykonać kilka ręcznych czynności za pomocą [Ambari](/azure/hdinsight/hdinsight-hadoop-manage-ambari) i przesłać [Akcje skryptu](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) w klastrze usługi HDInsight Spark.

> [!NOTE]
> Ta funkcja jest *eksperymentalna* i nie jest obsługiwana przez zespół usługi HDInsight Spark.

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli jeszcze tego nie masz, Utwórz klaster [Azure HDInsight Spark](/azure/hdinsight/spark/apache-spark-jupyter-spark-sql-use-portal#create-an-apache-spark-cluster-in-hdinsight) .

1. Odwiedź [Azure Portal](https://portal.azure.com) i wybierz pozycję **+ Utwórz zasób**.

1. Utwórz nowy zasób klastra usługi Azure HDInsight. Wybierz pozycję **Spark 2,4** i **HDI 4,0** podczas tworzenia klastra.

## <a name="install-net-for-apache-spark"></a>Zainstaluj platformę .NET dla Apache Spark

W Azure Portal wybierz **klaster HDInsight Spark** utworzony w poprzednim kroku.

### <a name="stop-the-livy-server"></a>Zatrzymaj serwer usługi Livy

1. W portalu wybierz pozycję **Przegląd**, a następnie wybierz pozycję **Strona główna Ambari**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla klastra.

   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/select-ambari.png)

2. Wybierz pozycję **Spark2** w menu nawigacji po lewej stronie, a następnie wybierz pozycję **usługi LIVY dla Spark2 Server**.

   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/select-livyserver.png)

3. Wybierz **hn0... Host**.

   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/select-host.png)

4. Wybierz wielokropek obok pozycji **usługi Livy dla serwera Spark2** i wybierz pozycję **Zatrzymaj**. Po wyświetleniu monitu wybierz pozycję **OK** , aby wykonać operację.

   Zatrzymaj usługi Livy dla serwera Spark2.
   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/stop-server.png)

5. Powtórz poprzednie kroki dla **hn1... Host**.

### <a name="submit-an-hdinsight-script-action"></a>Prześlij akcję skryptu usługi HDInsight

1. `install-interactive-notebook.sh`To skrypt instalujący platformę .NET dla Apache Spark i wprowadza zmiany w oprogramowaniu Apache usługi Livy i sparkmagic. Przed przesłaniem akcji skryptu do usługi HDInsight należy utworzyć i przekazać `install-interactive-notebook.sh` .

   Utwórz nowy plik o nazwie **Install-Interactive-Notebook.sh** na komputerze lokalnym i wklej zawartość [Install-Interactive-Notebook.sh zawartości](https://raw.githubusercontent.com/dotnet/spark/master/deployment/HDI-Spark/Notebooks/install-interactive-notebook.sh).

   Przekaż skrypt do [identyfikatora URI](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#understand-script-actions) , który jest dostępny z klastra usługi HDInsight. Na przykład `https://<my storage account>.blob.core.windows.net/<my container>/<some dir>/install-interactive-notebook.sh`.

2. Uruchom `install-interactive-notebook.sh` w klastrze przy użyciu [akcji skryptu HDInsight](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   Wróć do klastra HDI w Azure Portal i wybierz pozycję **Akcje skryptu** z opcji po lewej stronie. Przesyłasz jedną akcję skryptu do wdrożenia platformy .NET dla Apache Spark REPL w klastrze usługi HDInsight Spark. Użyj następujących ustawień:

   |Właściwość  |Opis  |
   |---------|---------|
   | Typ skryptu | Niestandardowy |
   | Nazwa | *Zainstaluj program .NET dla Apache Spark interaktywnego środowiska notesu* |
   | Identyfikator URI skryptu bash | Identyfikator URI, do którego został przekazany `install-interactive-notebook.sh` . |
   | Typy węzłów| Kierownik i proces roboczy |
   | Parametry | Wersja platformy .NET dla Apache Spark. Możesz sprawdzić, czy program [.net ma Apache Spark wydania](https://github.com/dotnet/spark/releases). Na przykład jeśli chcesz zainstalować program Sparkdotnet w wersji 1.0.0, może to być `1.0.0` .

   Przejdź do następnego kroku, gdy zielony znacznik wyboru pojawia się obok stanu akcji skryptu.

### <a name="start-the-livy-server"></a>Uruchom serwer usługi Livy

Postępuj zgodnie z instrukcjami w sekcji [Zatrzymaj usługi Livy Server](#stop-the-livy-server) , aby **uruchomić** (zamiast **zatrzymać**) usługi Livy for Spark2 Server for hosts **hn0** and **hn1**.

### <a name="set-up-spark-default-configurations"></a>Konfigurowanie domyślnych konfiguracji platformy Spark

1. W portalu wybierz pozycję **Przegląd**, a następnie wybierz pozycję **Strona główna Ambari**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla klastra.

2. Wybierz pozycję **Spark2** i **configs**. Następnie wybierz pozycję **niestandardowe spark2 — ustawienia domyślne**.

   ![Ustawienia konfiguracji](./media/hdinsight-notebook-installation/spark-configs.png)

3. Wybierz pozycję **Dodaj właściwość...** , aby dodać domyślne ustawienia platformy Spark.

   ![Dodaj właściwość](./media/hdinsight-notebook-installation/add-property.png)

   Istnieją trzy poszczególne właściwości. Dodaj je pojedynczo przy użyciu typu właściwości **Text** w trybie dodawania pojedynczej właściwości. Sprawdź, czy nie masz żadnych dodatkowych spacji przed ani po żadnym z kluczy/wartości.

   * **Właściwość 1**
       * Głównych&ensp;&ensp;`spark.dotnet.shell.command`
       * Wartość: `/usr/share/dotnet-tools/dotnet-try,kernel-server,--default-kernel,csharp`

   * **Właściwość 2** Użyj wersji platformy .NET dla Apache Spark, która została uwzględniona w poprzedniej akcji skryptu.
       * Głównych&ensp;&ensp;`spark.dotnet.packages`
       * Wartość: `["nuget: Microsoft.Spark, 1.0.0", "nuget: Microsoft.Spark.Extensions.Delta, 1.0.0"]`

   * **Właściwość 3**
       * Głównych&ensp;&ensp;`spark.dotnet.interpreter`
       * Wartość: `try`

   Na przykład poniższy obraz przechwytuje ustawienie do dodawania właściwości 1:

   ![Ustawienia konfiguracji](./media/hdinsight-notebook-installation/add-sparkconfig.png)

   Po dodaniu trzech właściwości wybierz pozycję **Zapisz**. Jeśli widzisz ekran ostrzegawczy zaleceń dotyczących konfiguracji, wybierz pozycję **nadal mimo wszystko**.

4. Uruchom ponownie składniki, których to dotyczy.

   Po dodaniu nowych właściwości należy ponownie uruchomić składniki, na które miały wpływ zmiany. W górnej części wybierz pozycję **Uruchom ponownie**, a następnie **ponownie uruchom wszystkie** z listy rozwijanej.

   ![Ustawienia konfiguracji](./media/hdinsight-notebook-installation/restart-affected.png)

   Po wyświetleniu monitu wybierz pozycję **Potwierdź ponowne uruchomienie wszystkiego** , aby kontynuować, a następnie kliknij przycisk **OK** , aby zakończyć.

## <a name="submit-jobs-through-a-jupyter-notebook"></a>Przesyłanie zadań za pomocą Jupyter Notebook

Po zakończeniu poprzednich kroków można teraz przesyłać zadania platformy .NET dla Apache Spark za pomocą notesów Jupyter.

1. Utwórz nowy Notes platformy .NET dla Apache Spark. W Azure Portal Uruchom Jupyter Notebook z klastra HDI.

   ![Jupyter Notebook uruchamiania](./media/hdinsight-notebook-installation/launch-notebook.png)

   Następnie wybierz pozycję **Nowy**  >  **.NET Spark (C#)** , aby utworzyć Notes.

   ![Notes Jupyter](./media/hdinsight-notebook-installation/create-sparkdotnet-notebook.png)

2. Przesyłanie zadań przy użyciu platformy .NET dla Apache Spark.

   Użyj poniższego fragmentu kodu, aby utworzyć ramkę danych:

   ```csharp
   var df = spark.Range(0,5);
   df.Show();
   ```

   ![Prześlij zadanie platformy Spark](./media/hdinsight-notebook-installation/create-df.png)

   Poniższy fragment kodu służy do rejestrowania funkcji zdefiniowanej przez użytkownika (UDF) i używania UDF z ramkami danych:

   ```csharp
   var myawesomeudf = Udf<int, string>((id) => $"hello {id}");
   df.Select(myawesomeudf(df["id"])).Show();
   ```

   ![Prześlij zadanie platformy Spark](./media/hdinsight-notebook-installation/run-udf.png)

## <a name="next-steps"></a>Następne kroki

* [Wdrażanie aplikacji platformy .NET dla Apache Spark w usłudze Azure HDInsight](../tutorials/hdinsight-deployment.md)
* [Dokumentacja usługi HDInsight](/azure/hdinsight/)
