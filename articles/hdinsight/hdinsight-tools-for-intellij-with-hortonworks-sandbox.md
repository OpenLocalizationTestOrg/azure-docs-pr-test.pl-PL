---
title: "zestaw narzędzi platformy Azure dla IntelliJ z piaskownicy Hortonworks aaaUse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse HDInsight narzędzi w zestawie narzędzi Azure for IntelliJ z Hortonworks piaskownicy."
keywords: "narzędzia hadoop hive zapytania, intellij, hortonworks piaskownicy, narzędzi platformy azure dla intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy

Dowiedz się, jak hello toouse narzędzia HDInsight Tools for IntelliJ toodevelop Apache Scala aplikacji, a następnie testować aplikacje na [piaskownicy Hortonworks](http://hortonworks.com/products/sandbox/) uruchomione na stacji roboczej. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) jest środowisko deweloperskie zintegrowane Java (IDE) do tworzenia oprogramowania komputera. Po opracowany i przetestowany aplikacji w piaskownicy Hortonworks można przenieść za[Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka potrzebna będzie:

- Hortonworks Data Platform (HDP) 2.4 dotyczącej piaskownicy Hortonworks uruchomione w środowisku lokalnym. Zobacz tooconfigure HDP, [wprowadzenie w ekosystemie Hadoop hello z piaskownicą Hadoop na maszynie wirtualnej](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Narzędzia HDInsight Tools for IntelliJ przetestowano tylko z HDP 2.4. Rozwiń tooget HDP 2.4 **archiwum piaskownicy Hortonworks** na powitania [lokacji pobiera piaskownicy Hortonworks](http://hortonworks.com/downloads/#sandbox).

- [Java Developer Kit (JDK) w wersji 1.8 lub nowszej](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK jest wymagany przez hello Azure Toolkit for IntelliJ.

- [Wersja community IntelliJ IDEA](https://www.jetbrains.com/idea/download) z hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) wtyczki i hello [narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij.md) wtyczki. Narzędzia HDInsight Tools for IntelliJ jest dostępna jako część hello Azure Toolkit for IntelliJ. 

  Witaj tooinstall dodatków plug-in, hello następujące:

  1. Otwórz środowisko IntelliJ IDEA.
  2. Na powitania **-Zapraszamy** ekranu wybierz **Konfiguruj**, a następnie wybierz **wtyczek**.
  3. Wybierz **JetBrains zainstalować dodatek** w hello lewym dolnym rogu.
  4. Użyj hello wyszukiwania funkcji toosearch dla **Scala**, a następnie wybierz **zainstalować**.
  5. Wybierz **ponowne uruchomienie IntelliJ IDEA** toocomplete hello instalacji.
  6. Powtórz kroki 4 i 5 tooinstall hello **narzędzi Azure dla IntelliJ**. Aby uzyskać więcej informacji, zobacz [hello instalacji narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Tworzenie aplikacji Spark Scala

W tej sekcji utworzysz przykładowy projekt Scala przy użyciu IntelliJ IDEA. W następnej sekcji hello możesz połączyć toohello IntelliJ IDEA piaskownicy Hortonworks (emulatora) przed wysłaniem hello projektu.

1. Otwórz środowisko IntelliJ IDEA ze stacji roboczej. W hello **nowy projekt** okna dialogowego pozycję hello następujące:

   a. Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.

   b. W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:

    * **Maven**, obsługę języka Scala Kreator tworzenia projektu
    * **SBT**, do zarządzania hello zależności i budowania hello Scala projektu

   ![okno dialogowe Nowy projekt Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Wybierz **dalej**.

3. W hello dalej **nowy projekt** okna dialogowego pozycję hello następujące:

    ![Utwórz IntelliJ Scala właściwości projektu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. W hello **Nazwa projektu** wprowadź nazwę projektu.

    b. W hello **lokalizacja projektu** wprowadź lokalizację projektu.

    c. Dalej toohello **projekt zestawu SDK** listy rozwijanej wybierz **nowy**, wybierz pozycję **JDK**, a następnie określ folder hello JDK Java w wersji 1,7 lub nowszej. Wybierz **Java 1.8** dla klastra 2.x Spark hello, lub wybierz **Java 1.7** hello Spark 1.x klastra. Witaj domyślna lokalizacja to C:\Program Files\Java\jdk1.8.x_xxx.

    d. W hello **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje hello poprawnej wersji dla platformy Spark zestawy SDK i Scala. Jeśli hello klastra Spark w wersji starszej niż 2.0, wybierz **Spark 1.x**. W przeciwnym razie wybierz **Spark2.x**. W tym przykładzie użyto Spark 1.6.2 (Scala 2.10.5). Upewnij się, że używasz repozytorium hello oznaczone Scala 2.10.x. Nie używaj repozytorium hello oznaczone Scala 2.11.x.

4. Wybierz pozycję **Finish** (Zakończ).

5. Jeśli hello **projektu** widoku nie jest jeszcze otwarty, naciśnij klawisz **Alt + 1** tooopen go.

6. W **Eksplorator projektów**, rozwiń hello projektu, a następnie wybierz **src**.

7. Kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie wybierz **klasy Scala**.

8. W hello **nazwa** wprowadź nazwę, w hello **rodzaj** wybierz opcję **obiektu**, a następnie wybierz **OK**.

    ![okno Utwórz nową klasę Scala Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. W pliku .scala hello Wklej hello następującego kodu:

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. Na powitania **kompilacji** menu, wybierz opcję **kompilacji projektu**. Upewnij się, że hello Kompilacja została pomyślnie ukończona.


## <a name="link-toohello-hortonworks-sandbox"></a>Łącze toohello Hortonworks piaskownicy

Przed połączeniem tooa piaskownicy Hortonworks (emulatora), musi korzystać z istniejących aplikacji IntelliJ.

toolink tooan emulator, hello następujące:

1. Witaj Otwórz projekt w IntelliJ.

2. Na powitania **widoku** menu, wybierz opcję **narzędzi systemu Windows**, a następnie wybierz **Eksploratora Azure**.

3. Rozwiń węzeł **Azure**, kliknij prawym przyciskiem myszy **HDInsight**, a następnie wybierz **Link Emulator**.

4. W hello **emulatora nowe łącze A** okna, wprowadź hasło hello skonfigurowano dla konta głównego hello hello Hortonworks piaskownicy, wprowadź wartości podobnie toothose w hello następującego zrzutu ekranu, a następnie wybierz **OK** . 

   ![okno "Łącze Nowy Emulator" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. emulator hello tooconfigure, wybierz opcję **tak**.

Jeśli hello emulator jest połączony pomyślnie, hello emulatora (Hortonworks piaskownicy) jest wyświetlane w węźle HDInsight hello.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Przedstawia toohello aplikacji Spark Scala hello Hortonworks piaskownicy

Po połączeniu IntelliJ IDEA toohello emulatora, możesz przesłać projektu.

toosubmit emulatora tooan projektu hello następujące:

1. W **Eksplorator projektów**, kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **tooHDInsight aplikacji Spark przesłać**.

2. Witaj, po:

    a. W hello **klastra Spark (tylko w systemie Linux)** listy rozwijanej wybierz użytkownika lokalnego Hortonworks piaskownicy.

    b. W hello **Nazwa klasy głównym** polu, wybierz lub wprowadź nazwę klasy głównym hello. W tym samouczku, nazwa hello jest **GroupByTest**.

3. Wybierz **przesłać**. Dzienniki przesyłania zadania Hello są wyświetlane w okna narzędzia przesyłanie Spark hello.

## <a name="next-steps"></a>Następne kroki

- toolearn jak toocreate aplikacji Spark dla usługi HDInsight przy użyciu narzędzia HDInsight Tools for IntelliJ, przejdź zbyt[użycia narzędzi HDInsight w zestawie narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).

- toowatch wideo narzędzia HDInsight Tools for IntelliJ, przejdź zbyt[wprowadzenie narzędzi HDInsight Tools for IntelliJ rozwoju Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn jak toodebug aplikacji Spark przy użyciu hello toolkit zdalnie w usłudze HDInsight za pośrednictwem protokołu SSH, zbyt Przejdź[zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn jak toodebug aplikacji Spark przy użyciu hello toolkit zdalnie w usłudze HDInsight za pośrednictwem sieci VPN, zbyt Przejdź[użycia narzędzi HDInsight w zestawie narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- jak toouse narzędzi HDInsight Tools dla programu Eclipse toocreate aplikacji Spark, przejdź zbyt toolearn[użycia narzędzi HDInsight w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch wideo narzędzi HDInsight Tools dla programu Eclipse, przejdź zbyt[Użyj narzędzia HDInsight dla aplikacji Spark toocreate Eclipse](https://mix.office.com/watch/1rau2mopb6fha).
