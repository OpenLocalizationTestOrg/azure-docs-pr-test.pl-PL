---
title: "tooSpark aaaIntroduction w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera tooSpark wprowadzenie w usłudze HDInsight i hello różnych scenariuszy, w których można używać klastra Spark w usłudze HDInsight."
keywords: "Co to jest apache spark, klastra spark, toospark wprowadzenie spark w usłudze hdinsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>Wprowadzenie tooSpark w usłudze HDInsight

Ten artykuł zawiera tooSpark wprowadzenie w usłudze HDInsight. <a href="http://spark.apache.org/" target="_blank">Platforma Apache Spark</a> platforma przetwarzania równoległego open source, który obsługuje w pamięci przetwarza tooboost hello wydajności aplikacji do analizy danych big data. Klaster Spark w usłudze HDInsight jest zgodny z usługą Azure Storage (WASB) oraz usługą Azure Data Lake Store, co pozwala na łatwe przetwarzanie istniejących danych przechowywanych na platformie Azure za pośrednictwem klastra Spark.

Tworząc klaster Spark w usłudze HDInsight, tworzysz zasoby obliczeniowe platformy Azure z zainstalowaną i skonfigurowaną platformą Spark. Trwa tylko około 10 minut klastra toocreate Spark w usłudze HDInsight. toobe danych Hello przetwarzane są przechowywane w magazynu Azure lub usługi Azure Data Lake Store. Zobacz temat [Korzystanie z usługi Azure Storage z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).

**klaster toocreate Spark w usłudze HDInsight**, zobacz [Szybki Start: Tworzenie klastra Spark w usłudze HDInsight i uruchamiania interaktywnego zapytania przy użyciu oprogramowania Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Co to jest klaster Apache Spark w usłudze Azure HDInsight?
Klastry Spark w usłudze HDInsight oferują w pełni zarządzaną usługę Spark. Poniżej przedstawiono korzyści związane z utworzeniem klastra Spark w usłudze HDInsight.

| Funkcja | Opis |
| --- | --- |
| Łatwość tworzenia klastrów Spark |Nowy klaster Spark w usłudze HDInsight można utworzyć w kilka minut przy użyciu hello portalu Azure, programu Azure PowerShell lub hello zestawu .NET SDK usługi HDInsight. Zobacz temat [Wprowadzenie do klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Łatwość obsługi |Klaster Spark w usłudze HDInsight zawiera notesy Jupyter i Zeppelin. Można ich używać do interakcyjnego przetwarzania danych i wizualizacji.|
| Interfejsy API REST |Klastry Spark w usłudze HDInsight obejmują [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), na podstawie interfejsu API REST Spark zadania serwera tooremotely przesyłania i monitorowania zadań. |
| Obsługa usługi Azure Data Lake Store | Klastra Spark w usłudze HDInsight może być skonfigurowany toouse Azure Data Lake Store jako dodatkowego magazynu, a także magazynu głównego (tylko z klastrami HDInsight 3.5). Aby uzyskać więcej informacji o usłudze Data Lake — magazyn, zobacz temat [Przegląd usługi Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md). |
| Integracja z usługami Azure |Klastra Spark w usłudze HDInsight jest dostarczany z tooAzure łącznika usługi Event Hubs. Klienci mogą tworzyć przesyłania strumieniowego aplikacji przy użyciu usługi Event Hubs hello, oprócz zbyt[Kafka](http://kafka.apache.org/), która jest już dostępna w ramach platformy Spark. |
| Obsługa platformy R Server | Można skonfigurować R Server w HDInsight Spark toorun klastra rozproszone obliczenia R z szybkością hello zapewnianą przez klaster Spark. Aby uzyskać więcej informacji, zobacz temat [Rozpoczęcie pracy z platformą R Server w usłudze HDInsight](hdinsight-hadoop-r-server-get-started.md). |
| Integracja ze zintegrowanymi środowiskami projektowymi innych firm | Usługa HDInsight zapewnia wtyczki dla IDEs, takich jak IntelliJ IDEA i Eclipse, można użyć toocreate i przesyłanie aplikacji tooan klastra Spark w usłudze HDInsight. Aby uzyskać więcej informacji, zobacz tematy [Korzystanie z zestawu narzędzi platformy Azure dla środowiska IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin.md) i [Korzystanie z zestawu narzędzi platformy Azure dla środowiska Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Zapytania jednoczesne |Klastry Spark w usłudze HDInsight obsługują zapytania jednoczesne. Dzięki temu wielu zapytań od jednego użytkownika lub wiele zapytań od różnych użytkowników i tooshare aplikacji hello same zasoby klastra. |
| Buforowanie na dyskach SSD |Można wybrać toocache dane w pamięci lub na dyskach SSD dołączony toohello węzłów klastra. Buforowanie w pamięci zapewnia najlepszą wydajność zapytań hello, ale może być kosztowne. buforowanie na dyskach SSD stanowi doskonałe rozwiązanie umożliwiające poprawę wydajności zapytań bez toocreate potrzeby hello klastra o rozmiarze, który jest wymagany toofit hello cały zestaw danych w pamięci. |
| Integracja z narzędziami do analizy biznesowej |Klastry Spark w usłudze HDInsight zawierają łączniki dla narzędzi do analizy biznesowej danych, takich jak [Power BI](http://www.powerbi.com/) i [Tableau](http://www.tableau.com/products/desktop). |
| Wstępnie załadowane biblioteki Anaconda |Klastry Spark w usłudze HDInsight są dostarczane z wstępnie zainstalowanymi bibliotekami Anaconda. [Anaconda](http://docs.continuum.io/anaconda/) udostępnia Zamknij too200 bibliotek do uczenia maszynowego, analizy danych, wizualizacji itp. |
| Skalowalność |Chociaż podczas tworzenia, można określić hello liczbę węzłów w klastrze, może mają toogrow lub zmniejszyć obciążenie toomatch klastra hello. Wszystkie klastry usługi HDInsight umożliwiają toochange hello liczby węzłów w klastrze hello. Ponadto klastry Spark można porzucić bez utraty danych, ponieważ wszystkie dane hello są przechowywane w magazynie Azure lub usługi Data Lake Store. |
| Całodobowa pomoc techniczna |Oferta klastrów Spark w usłudze HDInsight obejmuje całodobową pomoc techniczną dla przedsiębiorstw oraz umowę SLA gwarantującą 99,9% czasu działania. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Jakie są przypadki użycia hello platformy Spark w usłudze HDInsight?
Klastry Spark w usłudze HDInsight włączyć hello następujące scenariusze klucza.

### <a name="interactive-data-analysis-and-bi"></a>Interakcyjna analiza danych i analiza biznesowa
[Zobacz samouczek](hdinsight-apache-spark-use-bi-tools.md)

Klaster Apache Spark w usłudze HDInsight przechowuje dane w usłudze Azure Storage lub Azure Data Lake Store. Eksperci biznesowi i osoby podejmujące kluczowe decyzje można analizować i tworzyć raporty na tych danych i używać usługi Microsoft Power BI toobuild interakcyjnych raportów na podstawie danych hello przeanalizowane. Analitycy można Uruchom ze źródła danych bez struktury częściowej strukturze lub w magazynie klastra, zdefiniować schemat danych hello za pomocą notesów, a następnie skompilować modele danych przy użyciu usługi Microsoft Power BI. Klastry Spark w usłudze HDInsight obsługują również wiele narzędzi do analizy biznesowej innych firm, takich jak Tableau, dzięki czemu platforma Spark jest idealnym wyborem dla analityków danych, ekspertów biznesowych i osób podejmujących kluczowe decyzje.

### <a name="spark-machine-learning"></a>Spark Machine Learning
[Zobacz samouczek: przewidywanie temperatur w budynkach z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Zobacz samouczek: przewidywanie wyników inspekcji żywności](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Platforma Apache Spark jest dostarczana z biblioteką [MLlib](http://spark.apache.org/mllib/) do uczenia maszynowego opartą na platformie Spark, której można używać z klastra Spark w usłudze HDInsight. Klaster Spark w usłudze HDInsight obejmuje również platformę Anaconda — dystrybucję oprogramowania Python z szeregiem różnych pakietów do uczenia maszynowego. W połączeniu z wbudowaną obsługą notesów Jupyter i Zeppelin platforma zapewnia najwyższej jakości środowisko do tworzenia aplikacji do uczenia maszynowego.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Przesyłanie strumieniowe i analiza danych w czasie rzeczywistym na platformie Spark
[Zobacz samouczek](hdinsight-apache-spark-eventhub-streaming.md)

Klastry Spark w usłudze HDInsight zapewniają szeroką obsługę tworzenia rozwiązań do analizy w czasie rzeczywistym. Gdy Spark już łączniki tooingest danych z wielu źródeł, takich jak Kafka, Flume, Twitter, ZeroMQ lub TCP gniazda, Spark w usłudze HDInsight dodaje wysokiej klasy obsługę pobierania danych z usługi Azure Event Hubs. Centra zdarzeń to hello najczęściej używana usługa kolejkowania wiadomości na platformie Azure. Wbudowana obsługa centrum zdarzeń sprawia, że klastry Spark w usłudze HDInsight stanowią idealną platformę do tworzenia potoku analizy w czasie rzeczywistym.

## <a name="next-steps"></a>Jakie składniki wchodzą w skład klastra Spark?
Klastry Spark w usłudze HDInsight zawierają następujące składniki, które są dostępne w klastrach hello domyślnie hello.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Obejmuje takie składniki, jak Spark Core, Spark SQL, interfejsy API przesyłania strumieniowego Spark, GraphX oraz MLlib.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Notes Jupyter](https://jupyter.org)
* [Notes Zeppelin](http://zeppelin-project.org/)

Klastry Spark w usłudze HDInsight zapewniają także [sterownika ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) łączności tooSpark klastrów w usłudze HDInsight z narzędzi do analizy Biznesowej, takich jak Microsoft Power BI i Tableau.

## <a name="where-do-i-start"></a>Od czego zacząć?
Rozpocznij od utworzenia klastra Spark w usłudze HDInsight. Zobacz temat [Wprowadzenie: tworzenie klastra Apache Spark w usłudze HDInsight i uruchamianie interakcyjnych zapytań Spark SQL](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Następne kroki
### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
* [Znane problemy dotyczące platformy Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-known-issues.md).
