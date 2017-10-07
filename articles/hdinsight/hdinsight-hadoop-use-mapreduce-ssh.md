---
title: "aaaMapReduce i połączenia SSH z usługą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SSH toorun MapReduce zadania przy użyciu platformy Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Używanie MapReduce z usługą Hadoop w usłudze HDInsight przy użyciu protokołu SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Dowiedz się, jak zadania toosubmit MapReduce z tooHDInsight połączeń Secure Shell (SSH).

> [!NOTE]
> Jeśli znasz już opartą na systemie Linux platformą Hadoop korzystanie z serwerów, ale nowe tooHDInsight, zobacz [porady HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Wymagania wstępne

* Klaster opartych na systemie Linux usługą HDInsight (Hadoop w usłudze HDInsight)

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Klient SSH. Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a id="ssh"></a>Połącz przy użyciu protokołu SSH

Połącz toohello klastra przy użyciu protokołu SSH. Na przykład następujące polecenie hello łączy tooa klastra o nazwie **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**Jeśli używasz klucza certyfikatu dla uwierzytelniania SSH**, może być konieczne toospecify hello lokalizację klucza prywatnego hello w systemie klienta, na przykład:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Jeśli używasz hasła dla uwierzytelniania SSH**, potrzebne tooprovide hello hasło po wyświetleniu monitu.

Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Użyj poleceń usługi Hadoop

1. Po są połączone toohello klastra usługi HDInsight, użyj następujących hello polecenia toostart zadania MapReduce:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    To polecenie uruchamia hello `wordcount` klasy, która jest zawarta w hello `hadoop-mapreduce-examples.jar` pliku. Używa hello `/example/data/gutenberg/davinci.txt` dokumentu jako dane wejściowe i wyjściowe są przechowywane w `/example/data/WordCountOutput`.

    > [!NOTE]
    > Aby uzyskać więcej informacji o tym MapReduce zadania i hello przykładowe dane, zobacz [MapReduce używany w Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md).

2. zadanie Hello emituje szczegóły przetwarzania i zwraca informacje toohello podobne następującego tekstu po zakończeniu zadania hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Po zakończeniu zadania hello, użyj hello następujące pliki wyjściowe hello toolist polecenia:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    To polecenie wyświetla dwa pliki `_SUCCESS` i `part-r-00000`. Witaj `part-r-00000` plik zawiera dane wyjściowe powitania dla tego zadania.

    > [!NOTE]
    > Niektóre zadania MapReduce mogą podzielone hello wyniki w wielu **części r-###** plików. Jeśli tak, użyj hello ### sufiks tooindicate kolejność hello hello plików.

4. dane wyjściowe hello tooview, hello Użyj następującego polecenia:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    To polecenie wyświetla listę hello wyrazy, które są zawarte w hello **wasb://example/data/gutenberg/davinci.txt** plików i hello liczba wystąpił każdego wyrazu. Witaj następujący tekst jest przykładem hello danych zawartych w pliku hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Podsumowanie

Jak widać, polecenia Hadoop zapewniają prosty sposób toorun zadań MapReduce w klastrze usługi HDInsight, a następnie dane wyjściowe zadania hello widoku.

## <a id="nextsteps"></a>Następne kroki

Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:

* [Korzystać z usługi MapReduce na HDInsight Hadoop](hdinsight-use-mapreduce.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
