---
title: "klaster aaaTroubleshoot problemy z platformy Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat problemów powiązanych tooApache klastry Spark w usłudze Azure HDInsight i jak toowork wokół tych."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Znane problemy dotyczące klastra Apache Spark w usłudze HDInsight

Ten dokument przechowuje informacje o wszystkich hello znane problemy dotyczące hello Spark w usłudze HDInsight w publicznej wersji zapoznawczej.  

## <a name="livy-leaks-interactive-session"></a>Livy przecieków sesja interaktywna
Podczas Livy ponownego uruchomienia (od Ambari lub powodu ponownego uruchomienia maszyny wirtualnej tooheadnode 0) z sesji interaktywnej wciąż jest aktywny, sesji interakcyjne zadania zostaną ujawnione. W związku z tym nowego zadania może zablokowana na powitania stanu zaakceptowane i nie można uruchomić.

**Środki zaradcze:**

Użyj hello następujące procedury tooworkaround hello problemu:

1. SSH do headnode. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Hello uruchom następujące polecenie toofind hello aplikacji identyfikatorów zadań interakcyjne hello uruchomiony przy użyciu programu Livy. 
   
        yarn application –list
   
    Witaj domyślne nazwy zadania zostaną Livy Jeśli hello zadań została uruchomiona przy użyciu programu Livy sesji interakcyjne nie jawne nazwy parametrów hello sesji Livy uruchomione przez notesu Jupyter hello Nazwa zadania rozpocznie się o remotesparkmagics_ *. 
3. Uruchom następujące polecenie tookill hello te zadania. 
   
        yarn application –kill <Application ID>

Nowe zadania zostaną uruchomione. 

## <a name="spark-history-server-not-started"></a>Platforma Spark historii serwer nie został uruchomiony
Platforma Spark historii serwera nie jest uruchamiana automatycznie po utworzeniu klastra.  

**Środki zaradcze:** 

Ręcznie uruchom hello historii serwera z narzędzia Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problem uprawnień w katalogu dzienników Spark
Gdy hdiuser przesyła zadanie o spark-submit, jest java.io.FileNotFoundException błąd: /var/log/spark/sparkdriver_hdiuser.log (odmowa uprawnień) i hello dziennik sterownik nie jest zapisywany. 

**Środki zaradcze:**

1. Dodaj grupę Hadoop toohello hdiuser. 
2. Podaj 777 uprawnienia na /var/log/spark po utworzeniu klastra. 
3. Zaktualizuj lokalizacja dziennika spark hello przy użyciu Ambari toobe katalogu z uprawnieniami 777.  
4. Uruchom spark — przedstawia jako sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Spark Phoenix łącznik nie jest obsługiwany.

Obecnie hello Spark Phoenix łącznik nie jest obsługiwany z klastra usługi HDInsight Spark.

**Środki zaradcze:**

Zamiast tego należy użyć hello Spark HBase łącznika. Instrukcje można znaleźć [jak łącznik toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Problemy związane z notesów tooJupyter
Poniżej przedstawiono niektóre notesów pokrewne tooJupyter znane problemy.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notesów znaków innych niż ASCII w nazwach plików
Notesów Jupyter, których można użyć w klastrach Spark HDInsight nie powinna mieć znaki spoza zestawu ASCII w nazwach plików. Jeśli spróbujesz tooupload pliku za pośrednictwem hello Jupyter interfejsu użytkownika, którego filename spoza zestawu ASCII nie będzie dyskretnie (oznacza to, że Jupyter nie możesz przekazać plik hello, ale go nie albo zgłosić błąd widoczne). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Wystąpił błąd podczas ładowania notesów o większych rozmiarach
Można napotkać błąd  **`Error loading notebook`**  podczas ładowania notebooki, które są większe.  

**Środki zaradcze:**

Jeśli ten błąd nie oznacza to, że dane są uszkodzone lub zostały utracone.  Notesy nadal znajdują się na dysku w `/var/lib/jupyter`, i może SSH do tooaccess klastra hello je. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Po połączeniu toohello klastra przy użyciu protokołu SSH, możesz skopiować notesy z komputera lokalnego klastra tooyour (przy użyciu protokołu SCP lub WinSCP) utratę hello tooprevent kopii zapasowej wszystkich ważnych danych w notesie hello. Można następnie tunelu SSH w Twojej headnode na port 8001 tooaccess Jupyter bez pośrednictwa hello bramy.  Z tego miejsca, można wyczyścić dane wyjściowe hello notesu i zapisz go ponownie rozmiar toominimize hello notesu.

tooprevent ten błąd zapobiec w hello w przyszłości, należy wykonać, najlepsze rozwiązania:

* To mały rozmiar notesu hello tookeep ważne. Wszystkie dane wyjściowe zadań Spark wysyłany ponownie się, że w notesie hello jest trwały tooJupyter.  Jest najlepszym rozwiązaniem z Jupyter w ogólne tooavoid systemem `.collect()` w dużych RDD firmy lub dataframes; zamiast tego należy toopeek na RDD zawartość należy wziąć pod uwagę uruchomiona `.take()` lub `.sample()` , tak aby dane wyjściowe nie uzyskać zbyt duży.
* Ponadto podczas zapisywania notesu wyczyść wszystkie dane wyjściowe komórek tooreduce hello rozmiar.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Notesu uruchamiania początkowego trwa dłużej, niż oczekiwano
Pierwsza instrukcja kodu w notesu Jupyter przy użyciu Spark magic może zająć więcej niż kilka minut.  

**Wyjaśnienie:**

Dzieje się tak, ponieważ po uruchomieniu pierwszej komórki kodu hello. W tle hello to inicjuje konfigurację sesji, Spark SQL, i są ustawione kontekstów Hive. Skonfigurowanie tych kontekstów hello pierwszą instrukcją zostanie uruchomione, a dzięki temu hello wrażenie, że instrukcja hello miały toocomplete dużo czasu.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Limit czasu notesu Jupyter w tworzeniu hello sesji
Gdy klaster Spark jest za mało zasobów, hello Spark i jądra Pyspark notesu Jupyter hello będzie upłynął limit czasu próby toocreate hello sesji. 

**Środki zaradcze:** 

1. Zwolnij na nim w klastrze Spark przez niektóre zasoby:
   
   * Zatrzymywanie innych notesów Spark przechodzi toohello Zamknij i menu zatrzymania lub klikając zamknięcia w Eksploratorze notesu hello.
   * Zatrzymywanie innych aplikacji Spark z YARN.
2. Uruchom ponownie notesu hello, którą chcesz toostart się. Za mało zasobów powinny być dostępne dla toocreate możesz teraz sesji.

## <a name="see-also"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

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

