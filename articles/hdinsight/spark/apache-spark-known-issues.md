---
title: "Rozwiązywanie problemów z klastra Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat związane z klastrami Apache Spark w usłudze Azure HDInsight i sposobu obejścia tych problemów."
services: hdinsight
documentationcenter: 
author: nitinme
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
ms.date: 11/28/2017
ms.author: nitinme
ms.openlocfilehash: bb5557eb0672b9ad137bc5817e47bf4f89e1c34d
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Znane problemy dotyczące klastra Apache Spark w usłudze HDInsight

Ten dokument przechowuje informacje o znanych problemów w publicznej wersji zapoznawczej HDInsight Spark.  

## <a name="livy-leaks-interactive-session"></a>Livy przecieków sesja interaktywna
Podczas Livy ponownego uruchomienia (od Ambari lub z powodu ponownego uruchomienia maszyny wirtualnej headnode 0) z sesji interaktywnej wciąż jest aktywny, sesji interakcyjne zadania zostaną ujawnione. W związku z tym nowe zadania można zablokowane w stanie zaakceptowane i nie można uruchomić.

**Środki zaradcze:**

Użyj poniższej procedury w celu obejścia tego problemu:

1. SSH do headnode. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).

2. Uruchom następujące polecenie, aby znaleźć identyfikatory aplikacji interaktywnych zadania uruchamiane za pośrednictwem programu Livy. 
   
        yarn application –list
   
    Nazwy zostaną określone Livy Jeśli zadań została uruchomiona przy użyciu programu Livy sesji interakcyjne nie jawne nazwy sesji dla Livy uruchomione przez notesu Jupyter zadania domyślna nazwa zadania rozpoczyna się od remotesparkmagics_ *. 
3. Uruchom następujące polecenie, aby kill te zadania. 
   
        yarn application –kill <Application ID>

Nowe zadania zostaną uruchomione. 

## <a name="spark-history-server-not-started"></a>Platforma Spark historii serwer nie został uruchomiony
Platforma Spark historii serwera nie jest uruchamiana automatycznie po utworzeniu klastra.  

**Środki zaradcze:** 

Ręcznie uruchom serwer historii z narzędzia Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problem uprawnień w katalogu dzienników Spark
Gdy hdiuser przesyła zadanie o spark-submit, jest java.io.FileNotFoundException błąd: /var/log/spark/sparkdriver_hdiuser.log (odmowa uprawnień) i dziennika sterownik nie jest zapisywany. 

**Środki zaradcze:**

1. Dodaj hdiuser do grupy usługi Hadoop. 
2. Podaj 777 uprawnienia na /var/log/spark po utworzeniu klastra. 
3. Zaktualizuj lokalizację dziennika spark przy użyciu narzędzia Ambari katalogiem 777 uprawnienia.  
4. Uruchom spark — przedstawia jako sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Spark Phoenix łącznik nie jest obsługiwany.

Obecnie łącznik Spark Phoenix nie jest obsługiwany z klastra usługi HDInsight Spark.

**Środki zaradcze:**

Zamiast tego należy użyć łącznika Spark HBase. Instrukcje można znaleźć [sposobu korzystania z łącznika Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-to-jupyter-notebooks"></a>Problemy związane z notesów Jupyter
Poniżej przedstawiono niektóre znane problemy związane z notesów Jupyter.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notesów znaków innych niż ASCII w nazwach plików
Notesów Jupyter, których można użyć w klastrach Spark HDInsight nie powinna mieć znaki spoza zestawu ASCII w nazwach plików. Próba przekazania pliku za pośrednictwem interfejsu użytkownika Jupyter mającej filename spoza zestawu ASCII nie będzie dyskretnie (to znaczy Jupyter nie możesz przekazać plik, ale go nie albo zgłosić błąd widoczne). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Wystąpił błąd podczas ładowania notesów o większych rozmiarach
Można napotkać błąd  **`Error loading notebook`**  podczas ładowania notebooki, które są większe.  

**Środki zaradcze:**

Jeśli ten błąd nie oznacza to, że dane są uszkodzone lub zostały utracone.  Notesy nadal znajdują się na dysku w `/var/lib/jupyter`, i może SSH w klastrze, aby uzyskiwać do nich dostęp. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).

Po połączeniu się z klastrem przy użyciu protokołu SSH, możesz skopiować notesy z klastra na komputerze lokalnym (przy użyciu protokołu SCP lub WinSCP) jako kopię zapasową, aby uniknąć utraty ważnych danych w notesie. Można następnie tunelu SSH w Twojej headnode 8001 dostęp bez pośrednictwa bramy Jupyter do portu.  Z tego miejsca możesz wyczyścić dane wyjściowe notesu i Zapisz ponownie, aby zminimalizować rozmiar notesu.

Aby uniknąć tego błędu w przyszłości w przyszłości, należy wykonać najlepsze rozwiązania:

* Należy zachować mały rozmiar notesu. Żadnych danych wyjściowych z zadaniami Spark, które są wysyłane do aplikacji Jupyter jest trwały notesu.  Ogólnie jest najlepszym rozwiązaniem z Jupyter w celu uniknięcia uruchomiona `.collect()` w dużych RDD firmy lub dataframes; zamiast tego, jeśli chcesz uzyskać wgląd w zawartość RDD, należy wziąć pod uwagę uruchomiona `.take()` lub `.sample()` , tak aby dane wyjściowe nie uzyskać zbyt duży.
* Ponadto podczas zapisywania Notes wyczyść wszystkie dane wyjściowe komórek, aby zmniejszyć rozmiar.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Notesu uruchamiania początkowego trwa dłużej, niż oczekiwano
Pierwsza instrukcja kodu w notesu Jupyter przy użyciu Spark magic może zająć więcej niż kilka minut.  

**Wyjaśnienie:**

Dzieje się tak, ponieważ po uruchomieniu pierwszej komórki kodu. W tle to inicjuje konfigurację sesji, Spark SQL, i są ustawione kontekstów Hive. Po kontekstów te są ustawione, pierwsza instrukcja jest uruchamiane, co powoduje wrażenie który instrukcji przez długi czas do ukończenia.

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a>Limit czasu notesu Jupyter w tworzenia sesji
Gdy klaster Spark jest za mało zasobów, Spark i Pyspark jądra notesu Jupyter będzie limit czasu próby utworzenia sesji. 

**Środki zaradcze:** 

1. Zwolnij na nim w klastrze Spark przez niektóre zasoby:
   
   * Zatrzymywanie innych notesów Spark, przechodząc do menu Close and Halt lub kliknąć przycisk zamykania w Eksploratorze notesu.
   * Zatrzymywanie innych aplikacji Spark z YARN.
2. Uruchom ponownie notesu, który chcesz uruchomić. Za mało zasobów powinny być dostępne dla Ciebie do utworzenia sesji teraz.

## <a name="see-also"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności](apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA](apache-spark-intellij-tool-plugin.md)
* [Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight](apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](apache-spark-job-debugging.md)

