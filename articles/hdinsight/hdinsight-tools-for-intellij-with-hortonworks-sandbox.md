---
title: "Użyj narzędzi Azure for IntelliJ z piaskownicy Hortonworks | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą narzędzi HDInsight w zestawie narzędzi Azure for IntelliJ z Hortonworks piaskownicy."
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
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy

Dowiedz się, jak narzędzia HDInsight Tools for IntelliJ umożliwia tworzenie aplikacji Apache Scala i przetestowanie aplikacji na [piaskownicy Hortonworks](http://hortonworks.com/products/sandbox/) uruchomione na stacji roboczej. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) jest środowisko deweloperskie zintegrowane Java (IDE) do tworzenia oprogramowania komputera. Po opracowany i przetestowany aplikacji w piaskownicy Hortonworks można przenieść je do [Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka potrzebna będzie:

- Hortonworks Data Platform (HDP) 2.4 dotyczącej piaskownicy Hortonworks uruchomione w środowisku lokalnym. Aby skonfigurować HDP, zobacz [wprowadzenie w ekosystemie Hadoop z piaskownicą Hadoop na maszynie wirtualnej](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Narzędzia HDInsight Tools for IntelliJ przetestowano tylko z HDP 2.4. Aby uzyskać HDP 2.4, rozwiń węzeł **Hortonworks piaskownicy archiwum** na [lokacji pobiera piaskownicy Hortonworks](http://hortonworks.com/downloads/#sandbox).

- [Java Developer Kit (JDK) w wersji 1.8 lub nowszej](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK jest wymagane przez zestaw narzędzi Azure for IntelliJ.

- [Wersja community IntelliJ IDEA](https://www.jetbrains.com/idea/download) z [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) wtyczki i [narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij.md) wtyczki. Narzędzia HDInsight Tools for IntelliJ jest dostępna jako część zestawu narzędzi platformy Azure dla IntelliJ. 

  Aby zainstalować dodatki plug-in, wykonaj następujące czynności:

  1. Otwórz środowisko IntelliJ IDEA.
  2. Na **-Zapraszamy** ekranu wybierz **Konfiguruj**, a następnie wybierz **wtyczek**.
  3. Wybierz **JetBrains zainstalować dodatek** w lewym dolnym rogu.
  4. Użyj funkcji wyszukiwania w celu wyszukania **Scala**, a następnie wybierz **zainstalować**.
  5. Wybierz **ponowne uruchomienie IntelliJ IDEA** do ukończenia instalacji.
  6. Powtórz kroki 4 i 5, aby zainstalować **narzędzi Azure dla IntelliJ**. Aby uzyskać więcej informacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Tworzenie aplikacji Spark Scala

W tej sekcji utworzysz przykładowy projekt Scala przy użyciu IntelliJ IDEA. W następnej sekcji możesz połączyć IntelliJ IDEA piaskownicy Hortonworks (emulatora), przed przesłaniem projektu.

1. Otwórz środowisko IntelliJ IDEA ze stacji roboczej. W **nowy projekt** okno dialogowe, wykonaj następujące czynności:

   a. Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.

   b. W **narzędzia kompilacji** listy, wybierz jedną z następujących czynności, w zależności od potrzeb:

    * **Maven**, obsługę języka Scala Kreator tworzenia projektu
    * **SBT**, do zarządzania zależności i budowania projektu języka Scala

   ![Okno dialogowe nowego projektu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Wybierz **dalej**.

3. W następnej **nowy projekt** okna dialogowego pole, wykonaj następujące czynności:

    ![Utwórz IntelliJ Scala właściwości projektu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. W **Nazwa projektu** wprowadź nazwę projektu.

    b. W **lokalizacja projektu** wprowadź lokalizację projektu.

    c. Obok pozycji **SDK projektu** listy rozwijanej wybierz **nowy**, wybierz pozycję **JDK**, a następnie określ folder JDK Java w wersji 1,7 lub nowszej. Wybierz **Java 1.8** dla klastra Spark 2.x lub wybierz **Java 1.7** 1.x klastra Spark. Lokalizacja domyślna to C:\Program Files\Java\jdk1.8.x_xxx.

    d. W **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje poprawnej wersji dla platformy Spark zestawy SDK i Scala. Jeśli wersja klastra Spark jest starsza niż 2.0, wybierz **Spark 1.x**. W przeciwnym razie wybierz **Spark2.x**. W tym przykładzie użyto Spark 1.6.2 (Scala 2.10.5). Upewnij się, że używasz repozytorium oznaczone Scala 2.10.x. Nie używaj repozytorium oznaczone Scala 2.11.x.

4. Wybierz pozycję **Finish** (Zakończ).

5. Jeśli **projektu** widoku nie jest jeszcze otwarty, naciśnij klawisz **Alt + 1** go otworzyć.

6. W **Eksplorator projektów**, rozwiń węzeł projektu, a następnie wybierz **src**.

7. Kliknij prawym przyciskiem myszy **src**, wskaż polecenie **nowy**, a następnie wybierz **klasy Scala**.

8. W **nazwa** wprowadź nazwę, w **rodzaj** wybierz opcję **obiektu**, a następnie wybierz **OK**.

    ![Utwórz nową klasę Scala okna](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. W pliku .scala Wklej następujący kod:

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

10. Na **kompilacji** menu, wybierz opcję **kompilacji projektu**. Upewnij się, że Kompilacja została pomyślnie ukończona.


## <a name="link-to-the-hortonworks-sandbox"></a>Łącze do piaskownicy Hortonworks

Przed połączeniem się piaskownicy Hortonworks (emulatora), musi korzystać z istniejących aplikacji IntelliJ.

Aby połączyć emulatora, wykonaj następujące czynności:

1. Otwórz projekt w IntelliJ.

2. Na **widoku** menu, wybierz opcję **narzędzi systemu Windows**, a następnie wybierz **Eksploratora Azure**.

3. Rozwiń węzeł **Azure**, kliknij prawym przyciskiem myszy **HDInsight**, a następnie wybierz **Link Emulator**.

4. W **emulatora nowe łącze A** okna, wprowadź hasło, które zostały skonfigurowane dla konta głównego piaskownicy Hortonworks, wprowadź wartości podobne do tych na poniższym zrzucie ekranu, a następnie wybierz **OK**. 

   ![Okno "Łącze Nowy Emulator"](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. Aby skonfigurować emulator, wybierz **tak**.

Po podłączeniu pomyślnie emulator, emulatora (Hortonworks piaskownicy) jest wyświetlane w węźle usługi HDInsight.

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a>Przesyłanie aplikacji Spark Scala do piaskownicy Hortonworks

Po połączeniu IntelliJ IDEA emulator, możesz przesłać projektu.

Aby przesłać projektu na emulator, wykonaj następujące czynności:

1. W **Eksplorator projektów**, kliknij prawym przyciskiem myszy projekt, a następnie wybierz **Spark przesyłania aplikacji do usługi HDInsight**.

2. Wykonaj następujące czynności:

    a. W **klastra Spark (tylko w systemie Linux)** listy rozwijanej wybierz użytkownika lokalnego Hortonworks piaskownicy.

    b. W **Nazwa klasy głównym** polu, wybierz lub wprowadź nazwę klasy głównym. W tym samouczku jest nazwa **GroupByTest**.

3. Wybierz **przesłać**. Dzienniki przesyłania zadania są wyświetlane w oknie narzędzia przesyłanie Spark.

## <a name="next-steps"></a>Następne kroki

- Aby dowiedzieć się, jak tworzenie aplikacji dla usługi HDInsight Spark przy użyciu narzędzia HDInsight Tools for IntelliJ, przejdź do [użycia narzędzi HDInsight w zestawie narzędzi Azure for IntelliJ do tworzenie aplikacji Spark dla klastra usługi HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).

- Aby obejrzeć film wideo narzędzi HDInsight for IntelliJ, przejdź do [wprowadzenie narzędzi HDInsight Tools for IntelliJ rozwoju Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- Aby dowiedzieć się, jak i debugowanie aplikacji Spark przy użyciu zestawu narzędzi zdalnie w usłudze HDInsight za pośrednictwem protokołu SSH, przejdź do [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- Aby dowiedzieć się, jak i debugowanie aplikacji Spark przy użyciu zestawu narzędzi zdalnie w usłudze HDInsight za pośrednictwem sieci VPN, przejdź do [użycia narzędzi HDInsight w zestawie narzędzi Azure for IntelliJ debugowanie aplikacji Spark zdalnie w klastrze HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- Aby dowiedzieć się, jak używać narzędzi HDInsight Tools dla programu Eclipse do tworzenia aplikacji Spark, przejdź do [użycia narzędzi HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse tworzenie aplikacji Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).

- Aby obejrzeć film narzędzi HDInsight Tools dla programu Eclipse, przejdź do [Użyj narzędzia HDInsight dla programu Eclipse tworzenie aplikacji Spark](https://mix.office.com/watch/1rau2mopb6fha).
