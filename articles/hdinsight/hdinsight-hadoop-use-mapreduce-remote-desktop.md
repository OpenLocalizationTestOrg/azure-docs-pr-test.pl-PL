---
title: "aaaMapReduce i zdalny pulpit z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse pulpitu zdalnego tooconnect tooHadoop w usłudze HDInsight i uruchamiania zadań MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Korzystać z usługi MapReduce w Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

W tym artykule będzie Dowiedz się, jak tooa tooconnect Hadoop w usłudze HDInsight klastra przy użyciu pulpitu zdalnego i za pomocą polecenia Hadoop hello i uruchom zadania MapReduce.

> [!IMPORTANT]
> Pulpit zdalny jest dostępna tylko w klastrach HDInsight opartych na systemie Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [MapReduce Użyj przy użyciu protokołu SSH](hdinsight-hadoop-use-mapreduce-ssh.md) informacji na temat łączenia toohello klastra usługi HDInsight i uruchamiania zadań MapReduce.

## <a id="prereq"></a>Wymagania wstępne
toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:

* Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)
* Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7

## <a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego
Włączenie pulpitu zdalnego dla klastra usługi HDInsight hello, a następnie połącz tooit, wykonując następujące instrukcje hello [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Użyj polecenia Hadoop hello
Po zakończeniu pulpitu toohello podłączonego do klastra usługi HDInsight hello, za pomocą hello następujące kroki toorun zadania MapReduce za pomocą polecenia Hadoop hello:

1. Na pulpicie HDInsight hello start hello **wiersza polecenia usługi Hadoop**. Zostanie otwarty nowy wiersz polecenia w hello **c:\apps\dist\hadoop-&lt;numer wersji >** katalogu.

   > [!NOTE]
   > numer wersji Hello zmieni Hadoop jest aktualizowany. Witaj **HADOOP_HOME** zmiennej środowiskowej może być używane toofind hello ścieżki. Na przykład `cd %HADOOP_HOME%` zmiany katalogów toohello katalogu Hadoop, bez konieczności wprowadzania numer wersji hello tooknow.
   >
   >
2. Witaj toouse **Hadoop** polecenia toorun przykład zadania MapReduce, użyj następującego polecenia hello:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Spowoduje to uruchomienie hello **wordcount** klasy, która jest zawarta w hello **hadoop-mapreduce-examples.jar** plik w bieżącym katalogu hello. Jako dane wejściowe, używa hello **wasb://example/data/gutenberg/davinci.txt** dokumentu, a dane wyjściowe są przechowywane w: **wasb: / / / przykład/data/WordCountOutput**.

   > [!NOTE]
   > Aby uzyskać więcej informacji o tym MapReduce zadania i hello przykładowe dane, zobacz <a href="hdinsight-use-mapreduce.md">MapReduce użycia w usłudze HDInsight Hadoop</a>.
   >
   >
3. zadanie Hello emituje szczegóły, jak są przetwarzane i zwraca informacje o podobnych toohello następujące po zakończeniu zadania hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Po zakończeniu zadania hello Użyj hello następujące polecenia toolist hello dane wyjściowe pliki przechowywane w **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    To powinien być wyświetlany dwa pliki **_SUCCESS** i **części r-00000**. Witaj **części r-00000** plik zawiera dane wyjściowe powitania dla tego zadania.

   > [!NOTE]
   > Niektóre zadania MapReduce mogą podzielone hello wyniki w wielu **części r-###** plików. Jeśli tak, użyj hello ### sufiks tooindicate kolejność hello hello plików.
   >
   >
5. dane wyjściowe hello tooview, hello Użyj następującego polecenia:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Spowoduje to wyświetlenie listy hello wyrazy, które są zawarte w hello **wasb://example/data/gutenberg/davinci.txt** pliku hello liczba wystąpił każdego wyrazu. Witaj, poniżej przedstawiono przykładowy hello danych, które zostaną uwzględnione w pliku hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Podsumowanie
Jak widać, hello polecenia Hadoop zapewnia toorun łatwy sposób na klastra usługi HDInsight, a następnie dane wyjściowe zadania hello widoku zadań MapReduce.

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:

* [Korzystać z usługi MapReduce na HDInsight Hadoop](hdinsight-use-mapreduce.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
