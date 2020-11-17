---
title: Przesyłanie zadania platformy .NET dla Apache Spark do kostek
description: Dowiedz się, jak przesłać zadanie platformy .NET dla Apache Spark do datakostki przy użyciu platformy Spark — przesyłanie i Ustawianie jar.
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 4d37383ccb3c9b311e0fbd0ada195ac20113e505
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/17/2020
ms.locfileid: "94688205"
---
# <a name="submit-a-net-for-apache-spark-job-to-databricks"></a>Przesyłanie zadania platformy .NET dla Apache Spark do kostek

Możesz uruchamiać zadania programu .NET dla Apache Spark w klastrach datakostków, ale nie jest to dostępne dla Ciebie. Istnieją dwa sposoby wdrażania zadania programu .NET dla Apache Spark w kostkach: `spark-submit` i ustawić jar.

## <a name="deploy-using-spark-submit"></a>Wdrażanie przy użyciu platformy Spark — przesyłanie

Można użyć polecenia [Spark-Submit](https://spark.apache.org/docs/latest/submitting-applications.html) do przesyłania zadań programu .net dla Apache Spark do datakostki. `spark-submit` umożliwia przesyłanie tylko do klastra, który został utworzony na żądanie.

1. Przejdź do obszaru roboczego datakostki i Utwórz zadanie. Wybierz tytuł zadania, a następnie wybierz pozycję Skonfiguruj platformę **Spark-Submit**. Wklej następujące parametry w konfiguracji zadania, a następnie wybierz pozycję **Potwierdź**.

    ```
    ["--files","/dbfs/<path-to>/<app assembly/file to deploy to worker>","--class","org.apache.spark.deploy.dotnet.DotnetRunner","/dbfs/<path-to>/microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar","/dbfs/<path-to>/<app name>.zip","<app bin name>","app arg1","app arg2"]
    ```

    > [!NOTE]
    > Zaktualizuj zawartość powyższego parametru w oparciu o określone pliki i konfigurację. Na przykład należy odwołać się do wersji pliku JAR Microsoft. Spark przekazanego do DBFS i użyć odpowiedniej nazwy aplikacji i pliku zip opublikowanej aplikacji.

2. Przejdź do zadania i wybierz pozycję **Edytuj** , aby skonfigurować klaster zadania. Ustaw wersję Databricks Runtime na podstawie wersji Apache Spark, która ma być używana we wdrożeniu. Następnie wybierz **Opcje zaawansowane > init scripts** i Ustaw ścieżkę skryptu init jako `dbfs:/spark-dotnet/db-init.sh` . Wybierz pozycję **Potwierdź** , aby potwierdzić ustawienia klastra.

3. Przejdź do zadania i wybierz pozycję **Uruchom teraz** , aby uruchomić zadanie w nowo skonfigurowanym klastrze Spark. Utworzenie klastra zadania może potrwać kilka minut. Po jego utworzeniu zadanie zostanie przesłane. Możesz wyświetlić dane wyjściowe, wybierając pozycję **klastry** z menu po lewej stronie obszaru roboczego dane, a następnie wybierz polecenie **dzienniki sterowników**.

## <a name="deploy-using-set-jar"></a>Wdrażanie przy użyciu zestawu jar

Alternatywnie możesz użyć [Ustawienia jar](/azure/databricks/jobs#--create-a-job) w obszarze roboczym datakosteks, aby przesłać środowisko .net dla Apache Spark zadań do kostek. *Ustawienie jar* umożliwia przesyłanie zadań do istniejącego aktywnego klastra.

### <a name="one-time-setup"></a>Konfiguracja jednorazowa

1. Przejdź do klastra datakosteks i wybierz pozycję **Jobs (zadania** ) z menu po lewej stronie, a następnie **Ustaw jar**.

2. Przekaż odpowiednie `microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar` .

3. Zmodyfikuj następujące parametry, aby uwzględnić poprawną nazwę pliku wykonywalnego, który został opublikowany zamiast `<your-app-name>` :

    ```
    Main Class: org.apache.spark.deploy.dotnet.DotnetRunner
    Arguments /dbfs/apps/<your-app-name>.zip <your-app-name>
    ```

4. Skonfiguruj klaster tak, aby wskazywał istniejący klaster, dla którego został już ustawiony skrypt init.

### <a name="publish-and-run-your-app"></a>Publikowanie i uruchamianie aplikacji

1. Upewnij się, że aplikacja została opublikowana i że kod aplikacji nie jest używany `SparkSession.Stop()` .

2. Użyj [interfejsu wiersza polecenia datakosteks](/azure/databricks/dev-tools/databricks-cli) , aby przekazać aplikację do klastra datakostks. Na przykład użyj następującego polecenia, aby przekazać opublikowaną aplikację do klastra:

    ```console
    cd <path-to-your-app-publish-directory>
    databricks fs cp <your-app-name>.zip dbfs:/apps/<your-app-name>.zip
    ```

3. Jeśli masz jakiekolwiek funkcje zdefiniowane przez użytkownika w aplikacji, zestawy aplikacji, takie jak biblioteki DLL, które zawierają funkcje zdefiniowane przez użytkownika wraz z ich zależnościami, muszą być umieszczone w katalogu roboczym każdego *Microsoft. Spark. Worker*.

    Przekaż zestawy aplikacji do klastra datakostki:

    ```console
    cd <path-to-your-app-publish-directory>
    databricks fs cp <assembly>.dll dbfs:/apps/dependencies
    ```

    Usuń komentarz i Zmodyfikuj sekcję zależności aplikacji w [DB-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) , aby wskazywała ścieżkę zależności aplikacji. Następnie Przekaż zaktualizowane *DB-init.sh* do klastra:

    ```console
    cd <path-to-db-init-and-install-worker>
    databricks fs cp db-init.sh dbfs:/spark-dotnet/db-init.sh
    ```

4. Przejdź do **klastra datakostks > zadania > [nazwa zadania] > Uruchom teraz** , aby uruchomić zadanie.

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie do platformy .NET dla Apache Spark](../tutorials/get-started.md)
* [Wdrażanie aplikacji platformy .NET dla Apache Spark w kostkach](../tutorials/databricks-deployment.md)
* [Dokumentacja usługi Azure Databricks](/azure/azure-databricks/)
