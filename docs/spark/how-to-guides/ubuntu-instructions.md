---
title: Tworzenie aplikacji .NET dla platformy Spark apache na Ubuntu
description: Dowiedz się, jak zbudować aplikację .NET dla Platformy Spark na Ubuntu
ms.date: 01/29/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 6dd6f60bb89a51c47fe17182fc47de818cd00b80
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2020
ms.locfileid: "79187572"
---
# <a name="learn-how-to-build-your-net-for-apache-spark-application-on-ubuntu"></a>Dowiedz się, jak zbudować aplikację .NET dla Platformy Spark na Ubuntu

W tym artykule dowiesz się, jak utworzyć aplikacje platformy .NET dla platformy Spark w ubuntu.

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli masz już wszystkie poniższe wymagania wstępne, przejdź do kroków [kompilacji.](#build)

1. Pobierz i zainstaluj **[zestaw SDK .NET Core 2.1](https://dotnet.microsoft.com/download/dotnet-core/2.1)** lub **[.NET Core 3.1 SDK](https://dotnet.microsoft.com/download/dotnet-core/3.1)** — zainstalowanie zestawu SDK dodaje pasek `dotnet` narzędzi do ścieżki.  Obsługiwane są platformy .NET Core 2.1, 2.2 i 3.1.

2. Zainstaluj **[OpenJDK 8](https://openjdk.java.net/install/)**.

   - Można użyć następującego polecenia:

   ```bash
   sudo apt install openjdk-8-jdk
   ```

   * Sprawdź, czy można `java` uruchomić z wiersza polecenia.

      Przykładowe dane wyjściowe wersji java:

      ```bash
      openjdk version "1.8.0_191"
      OpenJDK Runtime Environment (build 1.8.0_191-8u191-b12-2ubuntu0.18.04.1-b12)
      OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)
      ```

   * Jeśli masz już zainstalowaną wiele wersji OpenJDK i chcesz wybrać OpenJDK 8, użyj następującego polecenia:

      ```bash
      sudo update-alternatives --config java
      ```

3. Zainstaluj **[Apache Maven 3.6.0+](https://maven.apache.org/download.cgi)**.

   * Uruchom następujące polecenie:

      ```bash
      mkdir -p ~/bin/maven
      cd ~/bin/maven
      wget https://www-us.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
      tar -xvzf apache-maven-3.6.0-bin.tar.gz
      ln -s apache-maven-3.6.0 current
      export M2_HOME=~/bin/maven/current
      export PATH=${M2_HOME}/bin:${PATH}
      source ~/.bashrc
      ```

       Należy pamiętać, że te zmienne środowiskowe zostaną utracone po zamknięciu terminala. Jeśli zmiany mają być trwałe, `export` dodaj wiersze do `~/.bashrc` pliku.

   * Sprawdź, czy można `mvn` uruchomić z wiersza polecenia

       Przykładowe wyjście mvn -version:

       ```
       Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-24T18:41:47Z)
       Maven home: ~/bin/apache-maven-3.6.0
       Java version: 1.8.0_191, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
       Default locale: en, platform encoding: UTF-8
       OS name: "linux", version: "4.4.0-17763-microsoft", arch: "amd64", family: "unix"
       ```

4. Zainstaluj **[Apache Spark 2.3+](https://spark.apache.org/downloads.html)**.
Pobierz [apache Spark 2.3+](https://spark.apache.org/downloads.html) i wyodrębnij go do `~/bin/spark-2.3.2-bin-hadoop2.7`lokalnego folderu (np. ). (Obsługiwane wersje iskry to 2.3.*, 2.4.0, 2.4.1, 2.4.3 i 2.4.4)

   ```bash
   tar -xvzf /path/to/spark-2.3.2-bin-hadoop2.7.tgz -C ~/bin/spark-2.3.2-bin-hadoop2.7
   ```

   * Dodać niezbędne [zmienne środowiskowe](https://www.java.com/en/download/help/path.xml) `SPARK_HOME` `~/bin/spark-2.3.2-bin-hadoop2.7/`(np.) `PATH` i (np. `$SPARK_HOME/bin:$PATH`)

      ```bash
      export SPARK_HOME=~/bin/spark-2.3.2-hadoop2.7
      export PATH="$SPARK_HOME/bin:$PATH"
      source ~/.bashrc
      ```

      Należy pamiętać, że te zmienne środowiskowe zostaną utracone po zamknięciu terminala. Jeśli zmiany mają być trwałe, `export` dodaj wiersze do `~/.bashrc` pliku.

   * Sprawdź, czy można `spark-shell` uruchomić z wiersza polecenia.

      Przykładowe wyjście konsoli:

      ```
      Welcome to
            ____              __
           / __/__  ___ _____/ /__
          _\ \/ _ \/ _ `/ __/  '_/
         /___/ .__/\_,_/_/ /_/\_\   version 2.3.2
            /_/

      Using Scala version 2.11.8 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_201)
      Type in expressions to have them evaluated.
      Type :help for more information.

      scala> sc
      res0: org.apache.spark.SparkContext = org.apache.spark.SparkContext@6eaa6b0c
      ```

Przed przejściem do `dotnet`następnej sekcji upewnij się, że można uruchomić program , `java`, `mvn` `spark-shell` z wiersza polecenia. Czujesz, że jest lepszy sposób? Proszę [otworzyć problem](https://github.com/dotnet/spark/issues) i nie krępuj się przyczynić.

## <a name="build"></a>Kompilacja

Pozostała część tego przewodnika musi być sklonowana do komputera repozytorium .NET for Apache `~/dotnet.spark/`Spark np.

```bash
git clone https://github.com/dotnet/spark.git ~/dotnet.spark
```

### <a name="build-net-for-spark-scala-extensions-layer"></a>Tworzenie warstwy rozszerzeń .NET dla platformy Spark Scala

Po przesłaniu aplikacji .NET.NET for Apache Spark ma niezbędną logikę zapisaną w Scali, która informuje Apache Spark, jak obsługiwać żądania (np. żądanie utworzenia nowej sesji Platformy Spark, żądanie przeniesienia danych ze strony .NET do strony JVM itp.). Tę logikę można znaleźć w [.NET dla Kodu Źródłowego Apache Spark Scala](https://github.com/dotnet/spark/tree/master/src/scala).

Następnym krokiem jest zbudowanie warstwy rozszerzenia .NET for Apache Spark Scala:

```bash
cd src/scala
mvn clean package
```

Powinny być widoczne jars utworzone dla obsługiwanych wersji platformy Spark:

* `microsoft-spark-2.3.x/target/microsoft-spark-2.3.x-<version>.jar`
* `microsoft-spark-2.4.x/target/microsoft-spark-2.4.x-<version>.jar`

### <a name="build-net-sample-applications-using-net-core-cli"></a>Tworzenie przykładowych aplikacji platformy .NET przy użyciu interfejsu wiersza polecenia rdzenia .NET

W tej sekcji wyjaśniono, jak utworzyć [przykładowe aplikacje](https://github.com/dotnet/spark/tree/master/examples) dla platformy .NET for Apache Spark. Te kroki pomogą w zrozumieniu ogólnego procesu tworzenia dla dowolnej aplikacji platformy .NET for Spark.

1. Zbuduj pracownika:

   ```dotnetcli
   cd ~/dotnet.spark/src/csharp/Microsoft.Spark.Worker/
   dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   ```

   Przykładowe wyjście konsoli:

   ```bash
   user@machine:/home/user/dotnet.spark/src/csharp/Microsoft.Spark.Worker$ dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   Microsoft (R) Build Engine version 16.0.462+g62fb89029d for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

      Restore completed in 36.03 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark.Worker/Microsoft.Spark.Worker.csproj.
      Restore completed in 35.94 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark/Microsoft.Spark.csproj.
      Microsoft.Spark -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark/Debug/netstandard2.0/Microsoft.Spark.dll
      Microsoft.Spark.Worker -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/Microsoft.Spark.Worker.dll
      Microsoft.Spark.Worker -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish/
   ```

2. Tworzenie próbek:

   ```dotnetcli
   cd ~/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples/
   dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   ```

   Przykładowe wyjście konsoli:

   ```bash
   user@machine:/home/user/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples$ dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   Microsoft (R) Build Engine version 16.0.462+g62fb89029d for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

      Restore completed in 37.11 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark/Microsoft.Spark.csproj.
      Restore completed in 281.63 ms for /home/user/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples/Microsoft.Spark.CSharp.Examples.csproj.
      Microsoft.Spark -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark/Debug/netstandard2.0/Microsoft.Spark.dll
      Microsoft.Spark.CSharp.Examples -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/Microsoft.Spark.CSharp.Examples.dll
      Microsoft.Spark.CSharp.Examples -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish/
   ```  

## <a name="run-the-net-for-spark-sample-applications"></a>Uruchamianie przykładowych aplikacji platformy .NET for Spark

Po utworzeniu przykładów można `spark-submit` użyć do przesłania aplikacji .NET Core. Upewnij się, że masz następujące [wymagania wstępne](#prerequisites) sekcji i zainstalowane Apache Spark.

1. Ustaw `DOTNET_WORKER_DIR` zmienną środowiskową lub `PATH` zmienną środowiskową tak, aby `~/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish`uwzględniała ścieżkę, w `Microsoft.Spark.Worker` której został wygenerowany plik binarny (np. ).

   ```bash
   export DOTNET_WORKER_DIR=~/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish
   ```

2. Otwórz terminal i przejdź do katalogu, w którym został wygenerowany `~/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish`plik binarny aplikacji (np. ).

   ```bash
   cd ~/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish
   ```

3. Uruchamianie aplikacji jest zgodne z podstawową strukturą:

   ```bash
   spark-submit \
     [--jars <any-jars-your-app-is-dependent-on>] \
     --class org.apache.spark.deploy.dotnet.DotnetRunner \
     --master local \
     <path-to-microsoft-spark-jar> \
     <path-to-your-app-binary> <argument(s)-to-your-app>
   ```

   Oto kilka przykładów, które można uruchomić:

   * **[Program Microsoft.Spark.Examples.Sql.Batch.Basic](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Batch/Basic.cs)**

      ```bash
      spark-submit \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Batch.Basic $SPARK_HOME/examples/src/main/resources/people.json
      ```

   * **[Microsoft.Spark.Examples.Sql.Streaming.StructuredNetworkWordCount](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredNetworkWordCount.cs)**

      ```bash
      spark-submit \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredNetworkWordCount localhost 9999
      ```

   * **[Microsoft.Spark.Examples.Sql.Streaming.StructuredKafkaWordCount (maven dostępne)](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredKafkaWordCount.cs)**

      ```bash
      spark-submit \
      --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.2 \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredKafkaWordCount localhost:9092 subscribe test
      ```

   * **[Microsoft.Spark.Examples.Sql.Streaming.StructuredKafkaWordCount (słoiki dostarczone)](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredKafkaWordCount.cs)**

      ```bash
      spark-submit \
      --jars path/to/net.jpountz.lz4/lz4-1.3.0.jar,path/to/org.apache.kafka/kafka-clients-0.10.0.1.jar,path/to/org.apache.spark/spark-sql-kafka-0-10_2.11-2.3.2.jar,`path/to/org.slf4j/slf4j-api-1.7.6.jar,path/to/org.spark-project.spark/unused-1.0.0.jar,path/to/org.xerial.snappy/snappy-java-1.1.2.6.jar \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredKafkaWordCount localhost:9092 subscribe test
       ```
