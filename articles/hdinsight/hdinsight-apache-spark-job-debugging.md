---
title: "Debugowanie Apache Spark zadań uruchamianych w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj interfejsu użytkownika YARN, Spark interfejsu użytkownika i serwera Spark historii śledzenie i debugowanie zadań uruchamianych w klastrze Spark w usłudze Azure HDInsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Debugowanie Apache Spark zadań uruchamianych w usłudze Azure HDInsight

W tym artykule dowiesz się, jak śledzenie i debugowanie zadań Spark uruchomionych w klastrach HDInsight przy użyciu interfejsu użytkownika YARN, Spark interfejsu użytkownika i serwera historii Spark. W tym artykule, firma Microsoft uruchomi zadanie Spark przy użyciu Notes dostępnych z klastrem Spark **uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib**. Poniższe kroki można użyć do śledzenia aplikacji, która zostanie przesłane za pomocą jakiejkolwiek innej metody, jak również na przykład **przesłać spark**.

## <a name="prerequisites"></a>Wymagania wstępne
Należy dysponować następującymi elementami:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Powinien mieć uruchomienia notesie  **[uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Aby uzyskać instrukcje na temat uruchamiania tego notesu kliknij link.  

## <a name="track-an-application-in-the-yarn-ui"></a>Śledzenie aplikacji w Interfejsie użytkownika YARN
1. Uruchom interfejs użytkownika YARN. W bloku klastra, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **YARN**.
   
    ![Uruchom interfejs użytkownika YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Alternatywnie można również uruchomić interfejsie użytkownika YARN z poziomu interfejsu użytkownika narzędzia Ambari. Aby uruchomić interfejs użytkownika narzędzia Ambari w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**. W interfejsie użytkownika narzędzia Ambari, kliknij przycisk **YARN**, kliknij przycisk **szybkie linki**, kliknij pozycję Menedżer zasobów aktywne, a następnie kliknij przycisk **interfejsu użytkownika Menedżera ResourceManager**.    
   > 
   > 
2. Ponieważ uruchomiono zadanie Spark za pomocą notesów Jupyter aplikacji ma nazwę **remotesparkmagics** (jest to nazwa dla wszystkich aplikacji, które są uruchamiane z notesów). Kliknij przycisk Identyfikator aplikacji i nazwa aplikacji, aby uzyskać więcej informacji o zadaniu. Spowoduje to uruchomienie widoku aplikacji.
   
    ![Znajdź identyfikator aplikacji Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Dla tych aplikacji, które są uruchamiane z notesów Jupyter, stan jest zawsze **systemem** aż do zakończenia notesu.
3. Z widoku aplikacji użytkownik może przejść do szczegółów po dowiedzieć kontenery skojarzonych z aplikacji i dzienniki (stdout/stderr). Można również Uruchom interfejs użytkownika Spark, klikając połączeń odpowiadający **URL śledzenia**, jak pokazano poniżej. 
   
    ![Pobierz dzienniki kontenera](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a>Śledzenie aplikacji w Interfejsie użytkownika Spark
W Interfejsie użytkownika Spark można przejść się do zadań Spark, które są zduplikowany przez aplikację, który został wcześniej uruchomiony.

1. Aby uruchomić interfejs użytkownika Spark z widoku aplikacji, kliknij łącze przed **URL śledzenia**, jak pokazano na zrzucie ekranu powyżej. Można wyświetlić wszystkich zadań Spark, które będą uruchamiane przez aplikację w notesu Jupyter.
   
    ![Wyświetlanie zadań Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Kliknij przycisk **modułów** kartę do przetwarzania i przechowywania informacji dotyczących każdego Moduł wykonujący. Można również pobierać stos wywołań, klikając **wątku zrzutu** łącza.
   
    ![Widok modułów Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Kliknij przycisk **etapy** kartę, aby wyświetlić etapy skojarzone z aplikacją.
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Na każdym z etapów może mieć wielu zadań, dla których można wyświetlić statystyki wykonania tak samo, jak pokazano poniżej.
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Na stronie szczegółów etapu można uruchomić wizualizacji grupy DAG. Rozwiń węzeł **wizualizacji DAG** link w górnej części strony, jak pokazano poniżej.
   
    ![Wyświetl Spark etapy DAG wizualizacji](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG lub bezpośredniego wykres Aclyic reprezentuje różne etapy w aplikacji. Każde pole blue na wykresie reprezentuje operację Spark wywoływane z aplikacji.
5. Na stronie szczegółów etapu można również uruchomić widoku osi czasu aplikacji. Rozwiń węzeł **osi czasu zdarzeń** link w górnej części strony, jak pokazano poniżej.
   
    ![Wyświetl Spark etapy zdarzeń w osi czasu](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Zostaną wyświetlone zdarzenia Spark w formie osi czasu. Widok osi czasu jest dostępny na trzech poziomach między zadania, zadania i w ramach etapu. Powyższy obraz przechwytuje widoku osi czasu dla danego etapu.
   
   > [!TIP]
   > W przypadku wybrania **włączyć powiększanie** pole wyboru można przechodzić z lewej i prawej w widoku osi czasu.
   > 
   > 
6. Inne karty w Interfejsie użytkownika Spark dostarczające przydatnych informacji na temat z wystąpieniem platformy Spark.
   
   * Karta magazynu — Jeśli aplikacja tworzy RDDs można znaleźć informacje o tych na karcie pamięci masowej.
   * Karta środowiska — ta karta zawiera wiele przydatnych informacji o wystąpieniu Spark takich jak 
     * Wersja języka scala
     * Katalog dziennika zdarzeń skojarzony z klastra
     * Liczba rdzeni Moduł wykonujący dla aplikacji
     * Itp.

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a>Informacje o zakończonych zadań przy użyciu serwera Spark historii
Po ukończeniu zadania w serwerze historii Spark jest trwały informacji o zadaniu.

1. Można uruchomić serwera historii Spark, w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **Spark historii serwera**.
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Można również będzie można uruchomić interfejs użytkownika serwera historii Spark w interfejsie użytkownika narzędzia Ambari. Aby uruchomić interfejs użytkownika narzędzia Ambari w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**. W interfejsie użytkownika narzędzia Ambari, kliknij przycisk **Spark**, kliknij przycisk **szybkie linki**, a następnie kliknij przycisk **interfejsu użytkownika serwera historii Spark**.
   > 
   > 
2. Wyświetlona zostanie ukończone aplikacje wymienione. Kliknij przycisk Identyfikator aplikacji, aby przejść do aplikacji, aby uzyskać więcej informacji.
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Zobacz też
*  [Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Dla analityków danych

* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Dla deweloperów platformy Spark

* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


