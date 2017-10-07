---
title: "aaaRun przykłady MapReduce z Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy przy użyciu MapReduce próbek w pliki jar uwzględnione w usłudze HDInsight. Korzystanie z SSH tooconnect toohello klastra, a następnie użyj hello Hadoop polecenia toorun przykładowe zadania."
keywords: "jar przykład hadoop, jar przykłady hadoop, przykłady mapreduce hadoop, przykłady mapreduce"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Uruchom hello MapReduce przykłady zawarte w usłudze HDInsight

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Dowiedz się, jak toorun hello MapReduce przykłady zawarte z platformą Hadoop w usłudze HDInsight.

## <a name="prerequisites"></a>Wymagania wstępne

* **Klaster usługi HDInsight**: zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* **Klient SSH**: Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>Przykłady MapReduce Hello

**Lokalizacja**: hello przykłady znajdują się na powitania klastra usługi HDInsight w `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Zawartość**: hello następujące przykłady znajdują się w tym archiwum:

* `aggregatewordcount`: Agregacji na podstawie liczby wyrazów hello plików wejściowych hello program mapreduce.
* `aggregatewordhist`: Agregacji na podstawie mapreduce program, który oblicza histogram hello hello wyrazów hello plików wejściowych.
* `bbp`: Mapreduce program, który używa Bailey-Borwein-Plouffe toocompute dokładne cyfr pi.
* `dbcount`: Zadanie przykład liczby hello widok strony dzienników przechowywanych w bazie danych.
* `distbbp`: Mapreduce program, który używa typu BBP formuły toocompute dokładne bitów pi.
* `grep`: Mapreduce program, który zlicza hello jest zgodny z wyrażeń regularnych w danych wejściowych hello.
* `join`: Zadanie, które wykonuje sprzężenie za pośrednictwem sortowane, jednakowo na partycje zestawów danych.
* `multifilewc`: Zadanie, które zlicza wyrazy z wielu plików.
* `pentomino`: Mapreduce Kafelek tworzenia rozwiązań toofind program toopentomino problemów.
* `pi`: Mapreduce program, który szacuje Pi przy użyciu quasi Monte Carlo metody.
* `randomtextwriter`: Mapreduce program, który zapisuje 10 GB losowe danych tekstowych w każdym węźle.
* `randomwriter`: Mapreduce program, który zapisuje 10 GB losowe dane w każdym węźle.
* `secondarysort`: Przykładowy Definiowanie toohello sortowania zmniejszyć fazy.
* `sort`: Mapreduce program sortuje dane hello napisane przez autora losowe hello.
* `sudoku`Solver sudoku.
* `teragen`: Generować dane o hello terasort.
* `terasort`: Terasort hello wykonywania.
* `teravalidate`: Sprawdzanie wyników terasort.
* `wordcount`: Mapreduce program zlicza hello wyrazów w hello plików wejściowych.
* `wordmean`: Mapreduce program, który oblicza średnią długość hello hello wyrazów hello plików wejściowych.
* `wordmedian`: Pliki wejściowe mapreduce program hello średniej długości wyrazów hello hello liczby.
* `wordstandarddeviation`: Mapreduce program, który oblicza odchylenie standardowe hello hello długości wyrazów hello hello plików wejściowych.

**Kod źródłowy**: kod źródłowy dla tych przykładów znajduje się na powitania klastra usługi HDInsight w `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Witaj `2.2.4.9-1` w hello ścieżka hello wersji hello platformie Hortonworks Data Platform dla klastra usługi HDInsight hello i mogą być inne dla klastra.

## <a name="run-hello-wordcount-example"></a>Uruchomienie przykładu wordcount hello

1. Połącz tooHDInsight przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Z hello `username@#######:~$` monit, użyj hello następujące przykłady hello toolist poleceń:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    To polecenie generuje listę hello próbki z hello w poprzedniej sekcji tego dokumentu.

3. Użyj hello następujące polecenie tooget pomocy dla określonych próbki. W takim przypadku hello **wordcount** próbki:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Pojawi się następujące wiadomość hello:

        Usage: wordcount <in> [<in>...] <out>

    Ten komunikat oznacza, że może zapewniać wielu ścieżek dla dokumentów źródłowych hello. Ścieżka końcowego Hello jest przechowywania danych wyjściowych hello (liczbę słów w dokumentach źródła hello).

4. Użyj powitania po toocount wszystkich wyrazów w hello notesów programu Leonardo Da Vinci, które są dostarczane jako przykładowych danych z klastrem:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    Dane wejściowe dla tego zadania zostanie odczytany z `/example/data/gutenberg/davinci.txt`. Dane wyjściowe w tym przykładzie jest przechowywane w `/example/data/davinciwordcount`. Obu ścieżek znajdują się na domyślnej magazynu dla klastra hello, nie hello lokalnego systemu plików.

   > [!NOTE]
   > Jak wspomniano w hello pomocy dla przykładu wordcount hello, można również określić wielu plików wejściowych. Na przykład `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` zlicza słów w davinci.txt i ulysses.txt.

5. Po zakończeniu zadania hello, użyj następujących danych wyjściowych polecenia tooview hello hello:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    To polecenie łączy wszystkie pliki wyjściowe hello utworzonej przez zadanie hello. Wyświetla hello dane wyjściowe toohello konsoli. Witaj danych wyjściowych jest podobne toohello następującego tekstu:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Każdy wiersz zawiera słowo i jak często wystąpi w hello dane wejściowe.

## <a name="hello-sudoku-example"></a>przykład Witaj Sudoku

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) jest układanki logiki, składa się z dziewięciu 3 x 3 siatki. Niektóre komórki w siatce hello mają numery, podczas gdy inne są puste, a celem hello jest toosolve dla hello puste komórki. więcej informacji na temat układanki hello ma Hello poprzedniej konsolidacji, ale hello celem tego przykładu toosolve dla hello puste komórki. Dlatego nasze dane wejściowe powinny być plik, który jest zgodny z formatem hello:

* Dziewięć wierszy dziewięć kolumn
* Każda kolumna może zawierać wartość liczbowa lub `?` (co oznacza puste komórki)
* Komórki są rozdzielone spacjami

Brak niektórych tooconstruct sposób łamigłówki Sudoku; Nie można powtórzyć liczbą kolumn lub wierszy. Jest to przykład w klastrze usługi HDInsight hello, która została prawidłowo skonstruowana. Znajduje się on w `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` i zawiera hello następującego tekstu:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

Użyj tego problemu przykład hello przykład Sudoku toorun hello następujące polecenie:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

Witaj wyniki zostaną wyświetlone podobne toohello następującego tekstu:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Przykład pi (π)

Przykładowe pi Hello używa statystycznego (quasi Monte Carlo) metoda tooestimate hello wartość liczby pi. Punkty są umieszczane w losowo wybranym w kwadratowe jednostki. kwadratowe Hello zawiera także okręgu. Witaj prawdopodobieństwo, że punkty hello objęte koło hello są równe toohello obszar hello koło pi/4. od wartości hello 4R można oszacować Hello wartość liczby pi. R jest stosunek hello hello liczbę punktów, które znajdują się wewnątrz hello koło toohello łączną liczbę punktów znajdujące się w ramach hello kwadratowe. Hello większego przykładu hello punktów używana, jest lepiej oszacować hello hello.

Należy użyć następującego polecenia toorun hello tego przykładu. To polecenie używa 16 mapy z 10 000 000 przykłady tooestimate hello wartość liczby pi:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Witaj wartość zwracana przez to polecenie jest podobne zbyt**3.14159155000000000000**. W przypadku odwołania hello 10 pierwszych miejsc dziesiętnych pi są 3.1415926535.

## <a name="10-gb-greysort-example"></a>Przykład Greysort 10 GB

GraySort jest sortowania testu wydajności. Metryka Hello jest szybkość sortowania hello (TB/minutę), które odbywa się podczas sortowania dużych ilości danych, zwykle 100 TB minimalnej.

W przykładzie użyto niewielkie 10 GB danych, aby można było uruchomić stosunkowo szybko. Opracowane przez Owen O'Malley oraz organizacji i Arun Murthy aplikacji MapReduce hello jest używany. Te aplikacje won hello roczne ogólnego przeznaczenia ("daytona") terabajt sortowania testu porównawczego w 2009 ze stawką 0.578 TB na minutę (100 TB 173 minut). Aby uzyskać więcej informacji na ten temat oraz innych sortowania testów porównawczych, zobacz hello [Sortbenchmark](http://sortbenchmark.org/) lokacji.

W tym przykładzie używa trzech zestawów MapReduce programów:

* **TeraGen**: A MapReduce program, który generuje wierszy toosort danych

* **TeraSort**: przykłady hello danych wejściowych i używa danych hello toosort MapReduce z kolejnością całkowita

    TeraSort jest standardowe sortowania MapReduce, z wyjątkiem partycjonera niestandardowych. partycjoner Hello używa posortowaną listę kluczy N-1 próbkowany, definiujące hello klucza zakresu dla każdego Zmniejsz. W szczególności, wszystkie klucze takie przykładowe [i-1] < klucz = < próbki [i] są wysyłane tooreduce i. Ten moduł partycjonowania gwarantuje, że elementy wyjściowe hello zmniejszyć i wyświetlane są wszystkie mniejszej niż dane wyjściowe hello zmniejszyć i + 1.

* **TeraValidate**: program A MapReduce, która weryfikuje te dane wyjściowe hello globalnie jest sortowana.

    Tworzy jeden mapy dla każdego pliku w katalogu wyjściowego hello, a każda mapa zapewnia, że każdy klucz jest mniejsza lub równa toohello poprzedni. Funkcja mapy Hello najpierw generuje rekordów hello i ostatni klucze każdego pliku. Hello zmniejszyć funkcja zapewnia, że hello pierwszy klucz pliku jest większy niż hello ostatniego klucza i-1 pliku. Problemów są zgłaszane jako dane wyjściowe hello zmniejszyć fazy z kluczami hello, które są poza kolejnością.

Użyj następujących hello kroki danych toogenerate sortowania, a następnie zweryfikować hello danych wyjściowych:

1. Generowanie 10 GB danych, stanowiące magazyn domyślnego klastra usługi HDInsight toohello przechowywanych w `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Witaj `-Dmapred.map.tasks` informuje Hadoop ile toouse zadania mapy dla tego zadania. Hello końcowego dwa parametry poinstruować hello zadania toocreate 10 GB danych i toostore go w `/example/data/10GB-sort-input`.

2. Witaj Użyj następującego polecenia toosort hello danych:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Witaj `-Dmapred.reduce.tasks` informuje Hadoop, Zmniejsz liczbę toouse zadań dla zadania hello. Hello końcowego dwa parametry są po prostu hello danych wejściowych i wyjściowych lokalizacje danych.

3. Użyj powitania po toovalidate hello dane generowane przez sortowania hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Następne kroki

Z tego artykułu wiesz, jak przykłady hello toorun dołączonego hello klastrów usługi HDInsight opartych na systemie Linux. Samouczki dotyczące przy użyciu Pig, Hive i MapReduce z usługą HDInsight zobacz następujące tematy hello:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]
* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
