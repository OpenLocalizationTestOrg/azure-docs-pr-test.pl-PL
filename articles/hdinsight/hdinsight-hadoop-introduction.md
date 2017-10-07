---
title: "aaaWhat są HDInsight, stos technologiczny Hadoop hello & klastrów? — platforma Azure | Microsoft Docs"
description: "Wprowadzenie tooHDInsight i hello stosem platformy Hadoop technologii i składników, w tym Spark, Kafka, Hive, HBase, analizy danych big data."
keywords: "Azure hadoop, hadoop azure, wprowadzenie do platformy hadoop, wprowadzenie hadoop, stos technologiczny hadoop, wprowadzenie toohadoop, toohadoop wprowadzenie, co to jest klastra usługi hadoop, co jest klaster usługi hadoop, hadoop do czego służy"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Wprowadzenie tooAzure HDInsight, stos technologiczny hello Hadoop i klastrów platformy Hadoop
 Ten artykuł zawiera wprowadzenie tooAzure HDInsight, stosu technologii Hadoop hello dystrybucji chmury. Wyjaśnia on również, czym jest klaster Hadoop i kiedy należy go używać. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>Co to jest HDInsight i hello stosu technologii Hadoop? 
Usługa Azure HDInsight jest dystrybucji chmury składników Hadoop hello z hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) został hello oryginalnego framework open source przetwarzania rozproszonego i analizy dużych zestawów danych w klastrach komputerów. 


stos technologiczny Hadoop Hello obejmuje oprogramowania związane z a utilities, w tym Apache Hive, HBase, Spark, Kafka i wielu innych. toosee dostępne składniki platformy Hadoop technologii stosu w usłudze HDInsight, zobacz [składniki i wersje dostępne w usłudze HDInsight][component-versioning]. tooread więcej informacji na temat platformy Hadoop w usłudze HDInsight, zobacz hello [stronę opisującą funkcje platformy Azure dla usługi HDInsight](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Co to jest klaster Hadoop i kiedy należy go używać?
*Hadoop* jest również typem klastra, który zapewnia:

* YARN do planowania zadań i zarządzania zasobami
* MapReduce do przetwarzania równoległego
* Witaj Hadoop rozproszonego systemu plików (HDFS)
  
Klastry Hadoop są najczęściej używane do przetwarzania wsadowego przechowywanych danych. Inne rodzaje klastrów w usłudze HDInsight oferują dodatkowe możliwości: platforma Spark jest coraz bardziej popularna dzięki możliwościom szybszego przetwarzania w pamięci. Aby uzyskać szczegółowe informacje, zobacz sekcję [Typy klastrów w usłudze HDInsight](#overview).

## <a name="what-is-big-data"></a>Co to są dane big data?
Dane big data opisują dowolną dużą porcję danych cyfrowych, takich jak:

* Dane z czujnika sprzętu przemysłowego
* Działania klienta zebrane z witryny sieci Web
* Kanał aktualności w serwisie Twitter

Dane big data są gromadzone szybciej, w większych ilościach i bardziej różnorodnych formatach. Może być historyczne (znaczenie przechowywane) lub czasu rzeczywistego (znaczenie przesyłania strumieniowego ze źródła hello). 

## <a name="overview"></a>Typy klastrów w usłudze HDInsight
Usługa HDInsight zawiera określone typy klastrów i oferuje możliwości dostosowywania klastra, takie jak dodawanie składników, narzędzi i języków.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Klastry typu Spark, Kafka, Interactive Hive, HBase, niestandardowe i inne
HDInsight oferuje hello następujące typy klastra:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: używa [HDFS](#hdfs), [YARN](#yarn) zarządzania zasobami i prosty [MapReduce](#mapreduce) tooprocess modelu programowania i Analizuj dane wsadowe równolegle.
* **[Platforma Apache Spark](http://spark.apache.org/)**: platforma przetwarzania równoległego, która obsługuje przetwarzanie w pamięci tooboost hello wydajności aplikacji do analizy danych big data, platforma Spark jest odpowiednia dla bazy danych SQL, strumieniowego przesyłania danych oraz uczenia maszynowego. Zobacz temat [Przegląd: platforma Apache Spark w usłudze HDInsight](hdinsight-apache-spark-overview.md).
* **[Apache HBase](http://hbase.apache.org/)**: baza danych NoSQL oparta na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą lub bez struktury — potencjalnie miliardów wierszy pomnożonych przez miliony kolumn. Zobacz temat [Co to jest usługa HBase w usłudze HDInsight?](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: serwer przeznaczony do hostowania równoległych, rozproszonych procesów języka R oraz zarządzania nimi. Z tooscalable dostęp na żądanie, rozproszonej metody analizy w usłudze HDInsight oferuje analityków danych, chi i programistom R. Zobacz temat [Overview of R Server on HDInsight](hdinsight-hadoop-r-server-overview.md) (Omówienie serwera R Server w usłudze HDInsight).
* **[Apache Storm](https://storm.incubator.apache.org/)**: rozproszony system obliczeniowy działający w czasie rzeczywistym do szybkiego przetwarzania dużych strumieni danych. Storm jest oferowany jako zarządzany klaster w usłudze HDInsight. Zobacz temat [Analyze real-time sensor data using Storm and Hadoop](hdinsight-storm-sensor-data-analysis.md) (Analizowanie danych czujnika w czasie rzeczywistym przy użyciu platform Storm i Hadoop).
* **[Apache Interactive Hive (Live Long and Process) w wersji zapoznawczej](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: buforowanie w pamięci umożliwiające interaktywne i szybsze zapytania programu Hive. Zobacz temat [Use Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) (Używanie oprogramowania Interactive Hive w usłudze HDInsight).
* **[Apache Kafka](https://kafka.apache.org/)**: platforma typu „open source” służąca do tworzenia potoków danych przesyłanych strumieniowo i aplikacji do obsługi tych danych. Kafka udostępnia funkcje kolejki komunikatów, które pozwala toopublish i subskrybowania toodata strumieni. Zobacz [tooApache wprowadzenie Kafka w usłudze HDInsight](hdinsight-apache-kafka-introduction.md).

Można również skonfigurować przy użyciu hello następujące metody:
* **[Podgląd przyłączonych do domeny klastrów](hdinsight-domain-joined-introduction.md)**: klastra przyłączone do domeny usługi Active Directory tooan, dzięki czemu można kontrolować dostęp i sprawujący Zarząd danych.
* **[Klastry niestandardowe z akcjami skryptu](hdinsight-hadoop-customize-cluster-linux.md)**: klastry ze skryptami, które są uruchamiane podczas aprowizacji i instalują dodatkowe składniki.

### <a name="example-cluster-customization-scripts"></a>Przykładowe skrypty dostosowania klastra
Akcje skryptu to skrypty Bash w systemie Linux podczas inicjowania obsługi klastra z systemem i które może być używane tooinstall dodatkowych składników w klastrze hello. 

Witaj następujące przykładowe skrypty są dostarczane przez zespół usługi HDInsight hello:

* **[HUE](hdinsight-hadoop-hue-linux.md)**: zestaw toointeract aplikacje używane w sieci web z klastrem. Tylko klastry z systemem Linux.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: wykres przetwarzania toomodel relacji między rzeczami lub osobami.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: platforma wyszukiwania w skali przedsiębiorstwa, która umożliwia pełnotekstowe wyszukiwanie danych.

Informacje na temat tworzenia własnych akcji skryptu można znaleźć w temacie [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md) (Tworzenie akcji skryptu za pomocą usługi HDInsight).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Składniki i narzędzia w klastrach HDInsight
Witaj następujące składniki i narzędzia znajdują się w klastrach HDInsight:

* **[Ambari](#ambari)**: inicjowanie obsługi klastrów, zarządzanie nimi, ich monitorowanie oraz narzędzia.
* **[Avro](#avro)**  (Biblioteka Microsoft .NET dla Avro): serializacja danych w środowisku Microsoft .NET hello. 
* **[Hive i HCatalog](#hive)**: przeszukiwanie w sposób przypominający kwerendę SQL oraz warstwa zarządzania tabelą i magazynem.
* **[Mahout](#mahout)**: na potrzeby skalowalnych aplikacji uczenia maszynowego.
* **[MapReduce](#mapreduce)**: Starsza struktura do przetwarzania rozproszonego oraz zarządzania zasobami w ramach platformy Hadoop. Zobacz sekcję [YARN](#yarn).
* **[Oozie](#oozie)**: zarządzanie przepływem pracy.
* **[Phoenix](#phoenix)**: warstwa relacyjnej bazy danych za pośrednictwem HBase.
* **[Pig](#pig)**: łatwiejsze wykonywanie skryptów do transformacji MapReduce.
* **[Sqoop](#sqoop)**: importowanie i eksportowanie danych.
* **[Tez](#tez)**: wydajnie umożliwia toorun procesów przetwarzających duże ilości danych na dużą skalę.
* **[YARN](#yarn)**: Zarządzanie zasobami, który jest częścią podstawowej biblioteki platformy Hadoop hello.
* **[ZooKeeper](#zookeeper)**: koordynacja procesów w systemach rozproszonych.

> [!NOTE]
> Aby uzyskać informacje na temat określonych składników hello oraz informacje o wersji, zobacz [Hadoop składnikami i wersji w usłudze HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari służy do aprowizacji i monitorowania klastrów Apache Hadoop oraz zarządzania nimi. Obejmuje intuicyjny zestaw narzędzi operatora oraz niezawodny zestaw interfejsów API, które neutralizują złożoność hello Hadoop, upraszczając działanie hello klastrów. Klastry usługi HDInsight w systemie Linux zapewniają zarówno hello interfejsu użytkownika sieci web Ambari i interfejs API REST Ambari hello. Widoki Ambari w klastrach HDInsight zapewniają funkcje interfejsu użytkownika wtyczek.
Zobacz tematy [Zarządzanie klastrami HDInsight przy użyciu Ambari](hdinsight-hadoop-manage-ambari.md) i <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Apache Ambari API reference</a> (Dokumentacja interfejsu API Apache Ambari).

### <a name="avro"></a>Avro (biblioteka programu Microsoft .NET dla Avro)
Hello Biblioteka Microsoft .NET dla Avro wdraża format wymiany danych binarnych hello Apache Avro do serializacji dla środowiska Microsoft .NET hello. Definiuje schemat niezależny od języka, aby dane serializowane w jednym języku mogły być odczytywane w innym. Szczegółowe informacje o formacie hello znajdują się w hello < element docelowy = _ "blank" href = "http://avro.apache.org/docs/current/spec.html" > Apache Avro Specification</a>. format Avro plików obsługuje hello Hello rozproszonych model programowania MapReduce: pliki są "podzielne", co oznacza można wyszukiwać dowolne miejsce w pliku i rozpocząć odczytywanie od określonego bloku. toofind informacje, zobacz [serializować danych za pomocą hello Biblioteka Microsoft .NET dla Avro](hdinsight-dotnet-avro-serialization.md). Toocome obsługi opartej na systemie Linux klaster.

### <a name="hdfs"></a>HDFS
System plików rozproszonych Hadoop (HDFS) jest system plików, który YARN i MapReduce, jest core hello technologii Hadoop. Tego hello standardowym systemem plików klastrów platformy Hadoop w usłudze HDInsight. Zobacz temat [Korzystanie z magazynu zgodnego z systemem plików HDFS w połączeniu z platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Hive i HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> danych magazynu oprogramowania na platformie Hadoop, która pozwala tooquery i zarządzać dużych zestawów danych w magazynie rozproszonym przy użyciu języka przypominającego SQL o nazwie HiveQL. Program Hive, tak samo jak Pig, jest warstwą abstrakcji nałożoną na model MapReduce, który przekłada zapytania na serię zadań MapReduce. Gałąź to system zarządzania relacyjnymi bazami danych tooa bliżej niż program Pig i jest używany z bardziej ustrukturyzowanymi danymi. W przypadku danych bez struktury Pig jest hello lepszym rozwiązaniem. Zobacz temat [Use Hive with Hadoop in HDInsight](hdinsight-use-hive.md) (Używanie Hive w ramach platformy Hadoop w usłudze HDInsight).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> to warstwa zarządzania tabelami i magazynem dla platformy Hadoop, która zapewnia relacyjny widok danych. W usłudze HCatalog można odczytywać i zapisywać pliki w dowolnym formacie obsługiwanym przez bibliotekę Hive SerDe (serializator-deserializator).

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> to biblioteka algorytmów uczenia maszynowego, która działa na platformie Hadoop. Zgodnie z zasadami statystyki, aplikacje do uczenia maszynowego nauczyć toolearn systemów z danych i toouse poza zachowanie w przyszłości toodetermine wyników. Zobacz temat [Generate movie recommendations using Mahout on Hadoop](hdinsight-mahout.md) (Generowanie zaleceń filmu przy użyciu Mahout na platformie Hadoop).

### <a name="mapreduce"></a>MapReduce
MapReduce jest hello starsza Platforma oprogramowania dla platformy Hadoop do zapisywania aplikacji dużych zestawów danych toobatch procesu równolegle. Zadanie MapReduce dzieli duże zestawy danych i organizuje dane hello w pary klucz wartość do przetworzenia. Zadania MapReduce są uruchamiane w strukturze [YARN](#yarn). Zobacz <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> w hello Hadoop Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> to system koordynacji przepływu pracy, który zarządza zadaniami na platformie Hadoop. Jego jest zintegrowany z hello stosem platformy Hadoop i obsługuje zadania platformy Hadoop dla MapReduce, Pig, Hive i Sqoop. Można także używane tooschedule systemu tooa określonych zadań, np. programów Java lub skryptów powłoki. Zobacz [Use Oozie with Hadoop](hdinsight-use-oozie-linux-mac.md) (Stosowanie systemu Oozie z platformą Hadoop).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> to warstwa relacyjnej bazy danych za pośrednictwem HBase. Phoenix obejmuje sterownik JDBC, który pozwala tooquery i bezpośrednie zarządzanie tabelami SQL. Phoenix tłumaczy zapytania i inne instrukcje do macierzystych wywołań interfejsu API NoSQL — zamiast używać MapReduce — umożliwiając szybsze zastosowania w ramach magazynów NoSQL. Zobacz temat [Use Apache Phoenix and SQuirreL with HBase clusters](hdinsight-hbase-phoenix-squirrel.md) (Używanie Apache Phoenix i SQuirreL z klastrami HBase).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> to platforma wysokiego poziomu, która pozwala tooperform złożonych przekształceń MapReduce na dużych zestawach danych przy użyciu prostego języka skryptowego o nazwie Pig Latin. Pig tłumaczy skrypty Pig Latin hello, by działały w ramach platformy Hadoop. Można utworzyć funkcje zdefiniowane przez użytkownika (UDF) tooextend Pig Latin. Zobacz [Use Pig with Hadoop](hdinsight-use-pig.md) (Stosowanie języka Pig z platformą Hadoop).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> to narzędzie, które przenosi dane zbiorcze pomiędzy platformą Hadoop a relacyjnymi bazami danych, takimi jak SQL lub inne strukturalne magazyny danych, w sposób możliwie najbardziej wydajny. Zobacz temat [Use Sqoop with Hadoop](hdinsight-use-sqoop.md) (Korzystanie ze Sqoop przy użyciu platformy Hadoop).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> to struktura aplikacji działająca w oparciu o Hadoop YARN, wykonująca złożone, acykliczne wykresy będące wynikiem ogólnego przetwarzania danych. Jest bardziej elastycznym i wydajnym następnika toohello MapReduce platforma, która pozwala procesów przetwarzających duże ilości danych, takich jak Hive, toorun wydajniej na dużą skalę. Zobacz część [„Use Apache Tez for improved performance” („Używanie Apache Tez w celu zwiększenia wydajności”) w temacie Use Hive and HiveQL (Korzystanie z Hive i HiveQL) ](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Struktura Apache YARN hello generacji MapReduce (MapReduce 2.0 lub MRv2) i obsługuje scenariusze przetwarzania danych poza przetwarzaniem wsadowym MapReduce z większą skalowalnością i przetwarzanie w czasie rzeczywistym. YARN umożliwia zarządzanie zasobami oraz rozproszoną strukturę aplikacji. Zadania MapReduce działają w ramach platformy YARN. Zobacz temat <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> koordynuje procesy w dużych systemach rozproszonych za pomocą udostępnionego hierarchicznego obszaru nazw rejestrów danych (znode). Rejestry Znode zawierają niewielkie ilości metadanych potrzebnych toocoordinate procesów: stan, lokalizację, konfigurację i tak dalej. Zobacz przykład [ZooKeeper z klastrem HBase i Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Języki programowania w usłudze HDInsight
Klastry HDInsight — Spark, HBase, Kafka, Hadoop i inne — obsługują wiele języków programowania, ale niektóre z nich nie są instalowane domyślnie. Dla bibliotek, modułów lub pakietów niezainstalowanych domyślnie [składnik hello tooinstall akcji skryptu używany](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Domyślna obsługa języka programowania
Domyślnie klastry usługi HDInsight obsługują języki:

* Java
* Python

Dodatkowe języki można zainstalować przy użyciu [akcji skryptu](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Języki maszyny wirtualnej Java (JVM)
Wiele języków innych niż Java można uruchomić na maszynie wirtualnej Java (JVM); Jednak niektóre z tych języków systemem może wymagać dodatkowe składniki zainstalowane w klastrze hello.

Te języki działające w oparciu o JVM są obsługiwane w klastrach usługi HDInsight:

* Clojure
* Jython (Python dla platformy Java)
* Scala

### <a name="hadoop-specific-languages"></a>Języki specyficzne dla platformy Hadoop
Klastry usługi HDInsight obsługuje następujące języki, które mają stosu technologii Hadoop toohello określonych hello:

* Pig Latin do zadań Pig
* HiveQL do zadań Hive oraz SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard i HDInsight Premium
Usługa HDInsight zapewnia oferty danych big data w chmurze w dwóch różnych kategoriach, Standard i Premium. HDInsight Standard zapewnia klaster w skali przedsiębiorstwa czy organizacje mogą używać toorun ich obciążeń danych big data. HDInsight Premium zapewnia możliwości kategorii Standard poszerzone o zaawansowane funkcje analityczne i zabezpieczenia dla klastra usługi HDInsight. Więcej informacji można znaleźć w temacie [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Analiza biznesowa Microsoft i usługa HDInsight
Znanych business intelligence (BI) narzędzia pobierania, analizować i raportują dane zintegrowane z usługą HDInsight przy użyciu albo hello dodatku Power Query lub hello sterownik Microsoft Hive ODBC:

* [Łączenie programu Excel tooHadoop z dodatku Power Query](hdinsight-connect-excel-power-query.md): Dowiedz się, jak hello tooconnect Excel toohello konta magazynu Azure, która przechowuje dane z klastrem usługi HDInsight przy użyciu programu Microsoft Power Query dla programu Excel. Wymagana stacja robocza z systemem Windows. 
* [Łączenie programu Excel tooHadoop z hello sterownik Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md): Dowiedz się, jak tooimport dane z usługi HDInsight za pomocą hello sterownik Microsoft Hive ODBC. Wymagana stacja robocza z systemem Windows. 
* [Microsoft Cloud Platform](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Dowiedz się więcej o usłudze Power BI dla Office 365, Pobierz wersję próbną programu SQL Server hello i konfigurowanie programu SharePoint Server 2013 i analizy Biznesowej programu SQL Server.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie do platformy Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): samouczek Szybki start dotyczący aprowizowania klastrów platformy Hadoop w usłudze HDInsight i uruchamiania przykładowych zapytań Hive.
* [Wprowadzenie do platformy Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): samouczek Szybki start dotyczący tworzenia klastra Spark i uruchamiania interaktywnych zapytań SQL Spark.
* [Use R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md) (Stosowanie platformy R Server w usłudze HDInsight): rozpoczynanie korzystania z platformy R Server w usłudze HDInsight Premium.
* [Obsługa administracyjna klastrów HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Dowiedz się, jak tooprovision klastra usługi HDInsight Hadoop za pomocą hello portalu Azure, Azure CLI lub Azure PowerShell.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/