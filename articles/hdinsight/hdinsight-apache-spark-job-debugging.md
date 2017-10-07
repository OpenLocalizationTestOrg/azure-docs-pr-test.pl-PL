---
title: "aaaDebug Apache Spark, że zadania uruchomione w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj interfejsu użytkownika YARN, Spark interfejsu użytkownika i historię Spark serwera tootrack i debugowanie zadań uruchamianych w klastrze Spark w usłudze Azure HDInsight"
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
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Debugowanie Apache Spark zadań uruchamianych w usłudze Azure HDInsight

W tym artykule dowiesz się, jak tootrack i debugowania Spark zadania uruchomione w klastrach HDInsight przy użyciu hello interfejsie użytkownika YARN, Spark interfejsu użytkownika i hello Spark historii serwera. W tym artykule, firma Microsoft uruchomi zadanie Spark przy użyciu Notes dostępnych z klastrem Spark hello, **uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib**. Można użyć hello kroków poniżej tootrack aplikacji, która zostanie przesłane za pomocą jakiejkolwiek innej metody, jak również na przykład **przesłać spark**.

## <a name="prerequisites"></a>Wymagania wstępne
Musi mieć następujące hello:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Powinien mieć uruchomienia notesu hello  **[uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Aby uzyskać instrukcje dotyczące toorun tego notesu wykonaj hello łącza.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Śledzenie aplikacji w interfejsie użytkownika YARN hello
1. Uruchom program hello interfejsie użytkownika YARN. W bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **YARN**.
   
    ![Uruchom interfejs użytkownika YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Można również będzie można uruchomić hello interfejsie użytkownika YARN z hello interfejsu użytkownika narzędzia Ambari. toolaunch hello interfejsu użytkownika narzędzia Ambari, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**. Hello interfejsu użytkownika narzędzia Ambari, kliknij **YARN**, kliknij przycisk **szybkie linki**, kliknij pozycję Menedżer zasobów active hello, a następnie kliknij przycisk **interfejsu użytkownika Menedżera ResourceManager**.    
   > 
   > 
2. Ponieważ uruchomiono zadanie Spark hello za pomocą notesów Jupyter aplikacji hello ma nazwę hello **remotesparkmagics** (jest to nazwa powitania dla wszystkich aplikacji, które są uruchamiane z notesów hello). Kliknij identyfikator aplikacji hello przed tooget nazwy aplikacji hello więcej informacji na temat hello zadania. Spowoduje to uruchomienie widoku aplikacji hello.
   
    ![Znajdź identyfikator aplikacji Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Dla tych aplikacji, które są uruchamiane z notesów Jupyter hello, stan hello jest zawsze **systemem** aż do zakończenia hello notesu.
3. Z widoku aplikacji hello można przejść dalsze toofind limit kontenery hello skojarzone z aplikacji hello i dzienniki hello (stdout/stderr). Hello Spark interfejsu użytkownika również można uruchomić, klikając hello łączenie odpowiedniego toohello **URL śledzenia**, jak pokazano poniżej. 
   
    ![Pobierz dzienniki kontenera](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Śledzenie aplikacji w hello Spark interfejsu użytkownika
W hello Spark interfejsu użytkownika można przejść się do hello Spark zadania, które są zduplikowany przez aplikacji hello, który został wcześniej uruchomiony.

1. toolaunch hello Spark interfejsu użytkownika, z widoku aplikacji hello, kliknij łącze hello przed hello **URL śledzenia**, jak pokazano w hello Przechwytywanie ekranu powyżej. Wszystkie zadania Spark hello, które będą uruchamiane przez aplikacja hello notesu Jupyter hello jest widoczny.
   
    ![Wyświetlanie zadań Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Kliknij przycisk hello **modułów** karcie toosee przetwarzania i przechowywania informacji dla każdego Moduł wykonujący. Można również pobierać hello stos wywołań, klikając hello **wątku zrzutu** łącza.
   
    ![Widok modułów Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Kliknij przycisk hello **etapy** karcie etapy hello toosee skojarzoną z aplikacją hello.
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Na każdym z etapów może mieć wielu zadań, dla których można wyświetlić statystyki wykonania tak samo, jak pokazano poniżej.
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Na stronie szczegółów etap hello można uruchomić wizualizacji DAG. Rozwiń węzeł hello **wizualizacji DAG** łącze u góry hello hello strony, jak pokazano poniżej.
   
    ![Wyświetl Spark etapy DAG wizualizacji](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG lub bezpośredniego wykres Aclyic reprezentuje hello różnych etapach aplikacji hello. Każde pole blue wykresie hello reprezentuje operację Spark wywoływane z aplikacji hello.
5. Na stronie szczegółów etap hello możesz uruchomić widoku osi czasu aplikacji hello. Rozwiń węzeł hello **osi czasu zdarzeń** łącze u góry hello hello strony, jak pokazano poniżej.
   
    ![Wyświetl Spark etapy zdarzeń w osi czasu](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Zostaną wyświetlone zdarzenia Spark hello w postaci hello osi czasu. Widok osi czasu Hello jest dostępny na trzech poziomach między zadania, zadania i w ramach etapu. Powyższy obraz powitania przechwytuje hello widoku osi czasu dla danego etapu.
   
   > [!TIP]
   > W przypadku wybrania hello **włączyć powiększanie** pole wyboru można przechodzić z lewej i prawej między hello widoku osi czasu.
   > 
   > 
6. Inne karty w hello interfejsu użytkownika Spark dostarczające przydatnych informacji na temat hello Spark również wystąpienia.
   
   * Karta magazynu — Jeśli aplikacja tworzy RDDs można znaleźć informacje o tych hello karcie magazynu.
   * Karta środowiska — ta karta zawiera wiele przydatnych informacji o Spark wystąpienia takich jak hello 
     * Wersja języka scala
     * Katalog dziennika zdarzeń skojarzony z klastrem hello
     * Liczba rdzeni Moduł wykonujący dla aplikacji hello
     * Itp.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Informacje o zakończonych zadań przy użyciu hello Spark historii serwera
Po ukończeniu zadania w hello Spark historii serwera jest trwały hello informacji o zadaniu hello.

1. toolaunch hello Spark historii serwera, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **Spark historii serwera**.
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Można również będzie można uruchomić hello interfejsu użytkownika serwera historii Spark z hello interfejsu użytkownika narzędzia Ambari. toolaunch hello interfejsu użytkownika narzędzia Ambari, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**. Hello interfejsu użytkownika narzędzia Ambari, kliknij **Spark**, kliknij przycisk **szybkie linki**, a następnie kliknij przycisk **interfejsu użytkownika serwera historii Spark**.
   > 
   > 
2. Zostanie wyświetlone wszystkie aplikacje ukończyć powitalnych wymienione. Kliknij przycisk toodrill identyfikator aplikacji w dół do aplikacji, aby uzyskać więcej informacji.
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Zobacz też
*  [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Dla analityków danych

* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Dla deweloperów platformy Spark

* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


