---
title: aaaCreate Scala aplikacji toorun na klastry Spark - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji Spark napisanych w języku Scala z Apache Maven, jak hello kompilacji systemu i istniejące archetype Maven dla Scala podał IntelliJ IDEA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Utwórz toorun aplikacji Scala Maven w klastrze Apache Spark w usłudze HDInsight

Dowiedz się, jak toocreate aplikacji Spark, napisanych w języku Scala za pomocą programu Maven z ROZWIĄZANIEM IntelliJ. Artykuł Hello używa Apache Maven hello systemu do kompilacji i rozpoczyna się od istniejącej archetype Maven dla Scala podał IntelliJ IDEA.  Tworzenie aplikacji Scala w IntelliJ IDEA obejmuje hello następujące kroki:

* Używanie programu Maven jako hello system kompilacji.
* Aktualizowanie projektu Object Model (POM) pliku tooresolve Spark modułu zależności.
* Pisanie aplikacji w języku Scala.
* Wygeneruj plik jar, które mogą być przesłane tooHDInsight klastry Spark.
* Uruchom aplikację hello w klastrze Spark przy użyciu programu Livy.

> [!NOTE]
> Usługa HDInsight zapewnia również IntelliJ IDEA wtyczki narzędzia tooease hello proces tworzenia i przesyłanie aplikacji tooan klastra Spark w usłudze HDInsight w systemie Linux. Aby uzyskać więcej informacji, zobacz [Użyj HDInsight Tools Plugin for IntelliJ IDEA toocreate i przesyłanie aplikacji Spark](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development kit. Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Java IDE. W tym artykule wykorzystano IntelliJ IDEA 15.0.1. Możesz zainstalować ją z [tutaj](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Instalowanie wtyczki Scala for IntelliJ IDEA
IntelliJ IDEA instalacji nie nie Monituj o włączenie wtyczki Scala, uruchom IntelliJ IDEA i przejść za pomocą hello następujące kroki tooinstall hello wtyczki:

1. Uruchom IntelliJ IDEA i na ekranie powitalnym kliknij **Konfiguruj** , a następnie kliknij przycisk **wtyczek**.
   
    ![Włączanie wtyczki scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Na następnym ekranie powitania kliknij **JetBrains zainstalować dodatek** z hello lewym dolnym rogu. W hello **Przeglądaj wtyczek JetBrains** okno dialogowe zostanie otwarte, wyszukaj Scala, a następnie kliknij przycisk **zainstalować**.
   
    ![Instalowanie wtyczki scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Po zainstalowaniu dodatku hello pomyślnie, kliknij przycisk hello **przycisk Uruchom ponownie IntelliJ IDEA** toorestart hello IDE.

## <a name="create-a-standalone-scala-project"></a>Tworzenie projektu Scala autonomiczny
1. Uruchom IntelliJ IDEA i Utwórz nowy projekt. W powitalne okno dialogowe Nowy projekt, wprowadź hello następujące opcje, a następnie kliknij przycisk **dalej**.
   
    ![Utwórz projekt Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Wybierz **Maven** jako hello typu projektu.
   * Określ **projekt zestawu SDK**. Kliknij przycisk Nowy i zwykle Przejdź katalogu instalacyjnego Java toohello `C:\Program Files\Java\jdk1.8.0_66`.
   * Wybierz hello **Utwórz z archetype** opcji.
   * Wybierz z listy hello archetypes, **org.scala tools.archetypes:scala-archetype — prosty**. Spowoduje to utworzenie struktury katalogów prawo hello i pobrać wymagane hello domyślnego zależności toowrite Scala programu.
2. Podaj odpowiednie wartości dla **GroupId**, **ArtifactId**, i **wersji**. Kliknij przycisk **Dalej**.
3. W hello następne okno dialogowe, której określić katalog macierzysty Maven i inne ustawienia użytkownika, zaakceptuj ustawienia domyślne hello, a następnie kliknij przycisk **dalej**.
4. W ostatniej okno dialogowe hello, określ nazwę projektu i lokalizację, a następnie kliknij przycisk **Zakończ**.
5. Usuń hello **MySpec.Scala** o plików **src\test\scala\com\microsoft\spark\example**. Nie trzeba to dla aplikacji hello.
6. W razie potrzeby zmień nazwy plików źródła i test domyślne hello. W lewym okienku hello w hello IntelliJ IDEA, przejdź zbyt**src\main\scala\com.microsoft.spark.example**. Kliknij prawym przyciskiem myszy **App.scala**, kliknij przycisk **Refaktoryzuj**, kliknij przycisk Zmień nazwę pliku i okno dialogowe hello, podaj nazwę nowego hello aplikacji hello, a następnie kliknij przycisk **Refaktoryzuj**.
   
    ![Zmień nazwy plików](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. W kolejnych krokach hello spowoduje zaktualizowanie hello pom.xml toodefine hello zależności dla aplikacji Spark Scala hello. Te zależności toobe pobrana i rozwiązany automatycznie, należy odpowiednio skonfigurować Maven.
   
    ![Skonfigurować automatyczne pobieranie Maven](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. Z hello **pliku** menu, kliknij przycisk **ustawienia**.
   2. W hello **ustawienia** oknie dialogowym Wybierz zbyt**, wykonanie, wdrożenie kompilacji** > **Build Tools** > **Maven**  >  **Importowania**.
   3. Wybierz opcję hello zbyt**Import Maven projektów automatycznie**.
   4. Kliknij przycisk **Zastosuj**, a następnie kliknij przycisk **OK**.
8. Zaktualizuj tooinclude plik źródłowy języka Scala hello kod aplikacji. Otwórz i Zastąp hello istniejących przykładowego kodu z hello następującego kodu i Zapisz zmiany hello. Ten kod odczytuje dane hello z hello HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera hello wiersze z tylko jedną cyfrę w kolumnie szóstego hello i zapisuje dane wyjściowe hello zbyt**/HVACOut** obszarze hello domyślny magazyn kontener hello klastra.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Zaktualizuj hello pom.xml.
   
   1. W ramach `<project>\<properties>` Dodaj hello:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. W ramach `<project>\<dependencies>` Dodaj hello:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Zapisz zmiany toopom.xml.
10. Utwórz plik JAR hello. IntelliJ IDEA umożliwia tworzenie JAR jako artefaktu projektu. Wykonaj następujące kroki hello.
    
    1. Z hello **pliku** menu, kliknij przycisk **struktury projektu**.
    2. W hello **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** a następnie kliknij przycisk hello oraz symboli. Na powitania wyskakującym oknie dialogowym kliknij pozycję **JAR**, a następnie kliknij przycisk **z modułów z zależnościami**.
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. W hello **utworzyć JAR z modułów** okna dialogowego, kliknij przycisk wielokropka hello (![wielokropka](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) przed hello **klasy głównym**.
    4. W hello **Wybierz klasy głównym** okno dialogowe, wybierz hello klasy, która jest wyświetlany domyślnie, a następnie kliknij przycisk **OK**.
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. W hello **utworzyć JAR z modułów** okna dialogowego polu należy upewnić się, ta opcja hello zbyt**wyodrębnić docelowy toohello JAR** jest zaznaczone, a następnie kliknij przycisk **OK**. Spowoduje to utworzenie jednego JAR z wszystkie zależności.
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. Hello dane wyjściowe układu karcie wyświetlane są wszystkie słoików hello, które są dołączane jako część hello projekt Maven. Można wybrać i hello Usuń te, na którym hello Scala aplikacji nie ma żadnych zależności bezpośrednich. Dla aplikacji hello jest tworzone w tym miejscu, należy usunąć wszystkie elementy oprócz hello ostatnią (**danych wyjściowych kompilacji SparkSimpleApp**). Wybierz toodelete słoików hello, a następnie kliknij przycisk hello **usunąć** ikony.
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Upewnij się, że **kompilacji w upewnij** pole jest zaznaczone, co zapewnia, że jar hello jest tworzony za każdym razem, gdy projekt hello jest utworzony lub zaktualizowany. Kliknij przycisk **zastosować** , a następnie **OK**.
    7. Na pasku menu hello, kliknij przycisk **kompilacji**, a następnie kliknij przycisk **projektu należy**. Możesz również kliknąć **artefaktów kompilacji** toocreate hello jar. Hello jar dane wyjściowe utworzony na podstawie **\out\artifacts**.
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Uruchamianie aplikacji hello w klastrze Spark hello
Aplikacja hello toorun na powitania klastra, należy wykonać następujące hello:

* **Kopiuj hello aplikacji jar toohello magazynu Azure blob** skojarzony z klastrem hello. Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), więc toodo, narzędzie wiersza polecenia. Istnieje wiele innych klientów również użyć tooupload danych. Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).
* **Użyj toosubmit Livy zadanie aplikacji zdalnie** toohello klastra Spark. Klastry Spark w usłudze HDInsight obejmuje Livy ujawniającym punkty końcowe REST, tooremotely przesyłania zadań Spark. Aby uzyskać więcej informacji, zobacz [zadania przesyłania Spark klastrów zdalnie przy użyciu programu Livy z platformy Spark w usłudze HDInsight](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Następny krok

W niniejszym artykule możesz przedstawiono sposób toocreate Spark scala aplikacji. ADVANCE toohello dalej artykułu toolearn jak toorun tej aplikacji na HDInsight Spark klastra przy użyciu programu Livy.

> [!div class="nextstepaction"]
>[Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

