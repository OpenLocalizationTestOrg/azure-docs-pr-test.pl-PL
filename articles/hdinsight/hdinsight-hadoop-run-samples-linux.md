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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="3bda1-105">Uruchom hello MapReduce przykłady zawarte w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bda1-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="3bda1-106">Dowiedz się, jak toorun hello MapReduce przykłady zawarte z platformą Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bda1-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bda1-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3bda1-107">Prerequisites</span></span>

* <span data-ttu-id="3bda1-108">**Klaster usługi HDInsight**: zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3bda1-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3bda1-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3bda1-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3bda1-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="3bda1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3bda1-111">**Klient SSH**: Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3bda1-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="3bda1-112">Przykłady MapReduce Hello</span><span class="sxs-lookup"><span data-stu-id="3bda1-112">hello MapReduce examples</span></span>

<span data-ttu-id="3bda1-113">**Lokalizacja**: hello przykłady znajdują się na powitania klastra usługi HDInsight w `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="3bda1-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="3bda1-114">**Zawartość**: hello następujące przykłady znajdują się w tym archiwum:</span><span class="sxs-lookup"><span data-stu-id="3bda1-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="3bda1-115">`aggregatewordcount`: Agregacji na podstawie liczby wyrazów hello plików wejściowych hello program mapreduce.</span><span class="sxs-lookup"><span data-stu-id="3bda1-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="3bda1-116">`aggregatewordhist`: Agregacji na podstawie mapreduce program, który oblicza histogram hello hello wyrazów hello plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="3bda1-117">`bbp`: Mapreduce program, który używa Bailey-Borwein-Plouffe toocompute dokładne cyfr pi.</span><span class="sxs-lookup"><span data-stu-id="3bda1-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="3bda1-118">`dbcount`: Zadanie przykład liczby hello widok strony dzienników przechowywanych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="3bda1-119">`distbbp`: Mapreduce program, który używa typu BBP formuły toocompute dokładne bitów pi.</span><span class="sxs-lookup"><span data-stu-id="3bda1-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="3bda1-120">`grep`: Mapreduce program, który zlicza hello jest zgodny z wyrażeń regularnych w danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="3bda1-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="3bda1-121">`join`: Zadanie, które wykonuje sprzężenie za pośrednictwem sortowane, jednakowo na partycje zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="3bda1-122">`multifilewc`: Zadanie, które zlicza wyrazy z wielu plików.</span><span class="sxs-lookup"><span data-stu-id="3bda1-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="3bda1-123">`pentomino`: Mapreduce Kafelek tworzenia rozwiązań toofind program toopentomino problemów.</span><span class="sxs-lookup"><span data-stu-id="3bda1-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="3bda1-124">`pi`: Mapreduce program, który szacuje Pi przy użyciu quasi Monte Carlo metody.</span><span class="sxs-lookup"><span data-stu-id="3bda1-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="3bda1-125">`randomtextwriter`: Mapreduce program, który zapisuje 10 GB losowe danych tekstowych w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="3bda1-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="3bda1-126">`randomwriter`: Mapreduce program, który zapisuje 10 GB losowe dane w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="3bda1-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="3bda1-127">`secondarysort`: Przykładowy Definiowanie toohello sortowania zmniejszyć fazy.</span><span class="sxs-lookup"><span data-stu-id="3bda1-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="3bda1-128">`sort`: Mapreduce program sortuje dane hello napisane przez autora losowe hello.</span><span class="sxs-lookup"><span data-stu-id="3bda1-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="3bda1-129">`sudoku`Solver sudoku.</span><span class="sxs-lookup"><span data-stu-id="3bda1-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="3bda1-130">`teragen`: Generować dane o hello terasort.</span><span class="sxs-lookup"><span data-stu-id="3bda1-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="3bda1-131">`terasort`: Terasort hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3bda1-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="3bda1-132">`teravalidate`: Sprawdzanie wyników terasort.</span><span class="sxs-lookup"><span data-stu-id="3bda1-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="3bda1-133">`wordcount`: Mapreduce program zlicza hello wyrazów w hello plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="3bda1-134">`wordmean`: Mapreduce program, który oblicza średnią długość hello hello wyrazów hello plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="3bda1-135">`wordmedian`: Pliki wejściowe mapreduce program hello średniej długości wyrazów hello hello liczby.</span><span class="sxs-lookup"><span data-stu-id="3bda1-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="3bda1-136">`wordstandarddeviation`: Mapreduce program, który oblicza odchylenie standardowe hello hello długości wyrazów hello hello plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="3bda1-137">**Kod źródłowy**: kod źródłowy dla tych przykładów znajduje się na powitania klastra usługi HDInsight w `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="3bda1-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="3bda1-138">Witaj `2.2.4.9-1` w hello ścieżka hello wersji hello platformie Hortonworks Data Platform dla klastra usługi HDInsight hello i mogą być inne dla klastra.</span><span class="sxs-lookup"><span data-stu-id="3bda1-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="3bda1-139">Uruchomienie przykładu wordcount hello</span><span class="sxs-lookup"><span data-stu-id="3bda1-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="3bda1-140">Połącz tooHDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="3bda1-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="3bda1-141">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3bda1-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3bda1-142">Z hello `username@#######:~$` monit, użyj hello następujące przykłady hello toolist poleceń:</span><span class="sxs-lookup"><span data-stu-id="3bda1-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="3bda1-143">To polecenie generuje listę hello próbki z hello w poprzedniej sekcji tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="3bda1-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="3bda1-144">Użyj hello następujące polecenie tooget pomocy dla określonych próbki.</span><span class="sxs-lookup"><span data-stu-id="3bda1-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="3bda1-145">W takim przypadku hello **wordcount** próbki:</span><span class="sxs-lookup"><span data-stu-id="3bda1-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="3bda1-146">Pojawi się następujące wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="3bda1-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="3bda1-147">Ten komunikat oznacza, że może zapewniać wielu ścieżek dla dokumentów źródłowych hello.</span><span class="sxs-lookup"><span data-stu-id="3bda1-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="3bda1-148">Ścieżka końcowego Hello jest przechowywania danych wyjściowych hello (liczbę słów w dokumentach źródła hello).</span><span class="sxs-lookup"><span data-stu-id="3bda1-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="3bda1-149">Użyj powitania po toocount wszystkich wyrazów w hello notesów programu Leonardo Da Vinci, które są dostarczane jako przykładowych danych z klastrem:</span><span class="sxs-lookup"><span data-stu-id="3bda1-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="3bda1-150">Dane wejściowe dla tego zadania zostanie odczytany z `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="3bda1-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="3bda1-151">Dane wyjściowe w tym przykładzie jest przechowywane w `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="3bda1-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="3bda1-152">Obu ścieżek znajdują się na domyślnej magazynu dla klastra hello, nie hello lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="3bda1-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3bda1-153">Jak wspomniano w hello pomocy dla przykładu wordcount hello, można również określić wielu plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="3bda1-154">Na przykład `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` zlicza słów w davinci.txt i ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="3bda1-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="3bda1-155">Po zakończeniu zadania hello, użyj następujących danych wyjściowych polecenia tooview hello hello:</span><span class="sxs-lookup"><span data-stu-id="3bda1-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="3bda1-156">To polecenie łączy wszystkie pliki wyjściowe hello utworzonej przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="3bda1-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="3bda1-157">Wyświetla hello dane wyjściowe toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="3bda1-157">It displays hello output toohello console.</span></span> <span data-ttu-id="3bda1-158">Witaj danych wyjściowych jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="3bda1-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="3bda1-159">Każdy wiersz zawiera słowo i jak często wystąpi w hello dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="3bda1-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="3bda1-160">przykład Witaj Sudoku</span><span class="sxs-lookup"><span data-stu-id="3bda1-160">hello Sudoku example</span></span>

<span data-ttu-id="3bda1-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) jest układanki logiki, składa się z dziewięciu 3 x 3 siatki.</span><span class="sxs-lookup"><span data-stu-id="3bda1-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="3bda1-162">Niektóre komórki w siatce hello mają numery, podczas gdy inne są puste, a celem hello jest toosolve dla hello puste komórki.</span><span class="sxs-lookup"><span data-stu-id="3bda1-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="3bda1-163">więcej informacji na temat układanki hello ma Hello poprzedniej konsolidacji, ale hello celem tego przykładu toosolve dla hello puste komórki.</span><span class="sxs-lookup"><span data-stu-id="3bda1-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="3bda1-164">Dlatego nasze dane wejściowe powinny być plik, który jest zgodny z formatem hello:</span><span class="sxs-lookup"><span data-stu-id="3bda1-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="3bda1-165">Dziewięć wierszy dziewięć kolumn</span><span class="sxs-lookup"><span data-stu-id="3bda1-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="3bda1-166">Każda kolumna może zawierać wartość liczbowa lub `?` (co oznacza puste komórki)</span><span class="sxs-lookup"><span data-stu-id="3bda1-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="3bda1-167">Komórki są rozdzielone spacjami</span><span class="sxs-lookup"><span data-stu-id="3bda1-167">Cells are separated by a space</span></span>

<span data-ttu-id="3bda1-168">Brak niektórych tooconstruct sposób łamigłówki Sudoku; Nie można powtórzyć liczbą kolumn lub wierszy.</span><span class="sxs-lookup"><span data-stu-id="3bda1-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="3bda1-169">Jest to przykład w klastrze usługi HDInsight hello, która została prawidłowo skonstruowana.</span><span class="sxs-lookup"><span data-stu-id="3bda1-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="3bda1-170">Znajduje się on w `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` i zawiera hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="3bda1-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="3bda1-171">Użyj tego problemu przykład hello przykład Sudoku toorun hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3bda1-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="3bda1-172">Witaj wyniki zostaną wyświetlone podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="3bda1-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="3bda1-173">Przykład pi (π)</span><span class="sxs-lookup"><span data-stu-id="3bda1-173">Pi (π) example</span></span>

<span data-ttu-id="3bda1-174">Przykładowe pi Hello używa statystycznego (quasi Monte Carlo) metoda tooestimate hello wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="3bda1-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="3bda1-175">Punkty są umieszczane w losowo wybranym w kwadratowe jednostki.</span><span class="sxs-lookup"><span data-stu-id="3bda1-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="3bda1-176">kwadratowe Hello zawiera także okręgu.</span><span class="sxs-lookup"><span data-stu-id="3bda1-176">hello square also contains a circle.</span></span> <span data-ttu-id="3bda1-177">Witaj prawdopodobieństwo, że punkty hello objęte koło hello są równe toohello obszar hello koło pi/4.</span><span class="sxs-lookup"><span data-stu-id="3bda1-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="3bda1-178">od wartości hello 4R można oszacować Hello wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="3bda1-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="3bda1-179">R jest stosunek hello hello liczbę punktów, które znajdują się wewnątrz hello koło toohello łączną liczbę punktów znajdujące się w ramach hello kwadratowe.</span><span class="sxs-lookup"><span data-stu-id="3bda1-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="3bda1-180">Hello większego przykładu hello punktów używana, jest lepiej oszacować hello hello.</span><span class="sxs-lookup"><span data-stu-id="3bda1-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="3bda1-181">Należy użyć następującego polecenia toorun hello tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="3bda1-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="3bda1-182">To polecenie używa 16 mapy z 10 000 000 przykłady tooestimate hello wartość liczby pi:</span><span class="sxs-lookup"><span data-stu-id="3bda1-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="3bda1-183">Witaj wartość zwracana przez to polecenie jest podobne zbyt**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="3bda1-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="3bda1-184">W przypadku odwołania hello 10 pierwszych miejsc dziesiętnych pi są 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="3bda1-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="3bda1-185">Przykład Greysort 10 GB</span><span class="sxs-lookup"><span data-stu-id="3bda1-185">10 GB Greysort example</span></span>

<span data-ttu-id="3bda1-186">GraySort jest sortowania testu wydajności.</span><span class="sxs-lookup"><span data-stu-id="3bda1-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="3bda1-187">Metryka Hello jest szybkość sortowania hello (TB/minutę), które odbywa się podczas sortowania dużych ilości danych, zwykle 100 TB minimalnej.</span><span class="sxs-lookup"><span data-stu-id="3bda1-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="3bda1-188">W przykładzie użyto niewielkie 10 GB danych, aby można było uruchomić stosunkowo szybko.</span><span class="sxs-lookup"><span data-stu-id="3bda1-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="3bda1-189">Opracowane przez Owen O'Malley oraz organizacji i Arun Murthy aplikacji MapReduce hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="3bda1-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="3bda1-190">Te aplikacje won hello roczne ogólnego przeznaczenia ("daytona") terabajt sortowania testu porównawczego w 2009 ze stawką 0.578 TB na minutę (100 TB 173 minut).</span><span class="sxs-lookup"><span data-stu-id="3bda1-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="3bda1-191">Aby uzyskać więcej informacji na ten temat oraz innych sortowania testów porównawczych, zobacz hello [Sortbenchmark](http://sortbenchmark.org/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="3bda1-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="3bda1-192">W tym przykładzie używa trzech zestawów MapReduce programów:</span><span class="sxs-lookup"><span data-stu-id="3bda1-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="3bda1-193">**TeraGen**: A MapReduce program, który generuje wierszy toosort danych</span><span class="sxs-lookup"><span data-stu-id="3bda1-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="3bda1-194">**TeraSort**: przykłady hello danych wejściowych i używa danych hello toosort MapReduce z kolejnością całkowita</span><span class="sxs-lookup"><span data-stu-id="3bda1-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="3bda1-195">TeraSort jest standardowe sortowania MapReduce, z wyjątkiem partycjonera niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="3bda1-196">partycjoner Hello używa posortowaną listę kluczy N-1 próbkowany, definiujące hello klucza zakresu dla każdego Zmniejsz.</span><span class="sxs-lookup"><span data-stu-id="3bda1-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="3bda1-197">W szczególności, wszystkie klucze takie przykładowe [i-1] < klucz = < próbki [i] są wysyłane tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="3bda1-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="3bda1-198">Ten moduł partycjonowania gwarantuje, że elementy wyjściowe hello zmniejszyć i wyświetlane są wszystkie mniejszej niż dane wyjściowe hello zmniejszyć i + 1.</span><span class="sxs-lookup"><span data-stu-id="3bda1-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="3bda1-199">**TeraValidate**: program A MapReduce, która weryfikuje te dane wyjściowe hello globalnie jest sortowana.</span><span class="sxs-lookup"><span data-stu-id="3bda1-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="3bda1-200">Tworzy jeden mapy dla każdego pliku w katalogu wyjściowego hello, a każda mapa zapewnia, że każdy klucz jest mniejsza lub równa toohello poprzedni.</span><span class="sxs-lookup"><span data-stu-id="3bda1-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="3bda1-201">Funkcja mapy Hello najpierw generuje rekordów hello i ostatni klucze każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="3bda1-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="3bda1-202">Hello zmniejszyć funkcja zapewnia, że hello pierwszy klucz pliku jest większy niż hello ostatniego klucza i-1 pliku.</span><span class="sxs-lookup"><span data-stu-id="3bda1-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="3bda1-203">Problemów są zgłaszane jako dane wyjściowe hello zmniejszyć fazy z kluczami hello, które są poza kolejnością.</span><span class="sxs-lookup"><span data-stu-id="3bda1-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="3bda1-204">Użyj następujących hello kroki danych toogenerate sortowania, a następnie zweryfikować hello danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="3bda1-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="3bda1-205">Generowanie 10 GB danych, stanowiące magazyn domyślnego klastra usługi HDInsight toohello przechowywanych w `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="3bda1-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="3bda1-206">Witaj `-Dmapred.map.tasks` informuje Hadoop ile toouse zadania mapy dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="3bda1-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="3bda1-207">Hello końcowego dwa parametry poinstruować hello zadania toocreate 10 GB danych i toostore go w `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="3bda1-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="3bda1-208">Witaj Użyj następującego polecenia toosort hello danych:</span><span class="sxs-lookup"><span data-stu-id="3bda1-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="3bda1-209">Witaj `-Dmapred.reduce.tasks` informuje Hadoop, Zmniejsz liczbę toouse zadań dla zadania hello.</span><span class="sxs-lookup"><span data-stu-id="3bda1-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="3bda1-210">Hello końcowego dwa parametry są po prostu hello danych wejściowych i wyjściowych lokalizacje danych.</span><span class="sxs-lookup"><span data-stu-id="3bda1-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="3bda1-211">Użyj powitania po toovalidate hello dane generowane przez sortowania hello:</span><span class="sxs-lookup"><span data-stu-id="3bda1-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="3bda1-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3bda1-212">Next steps</span></span>

<span data-ttu-id="3bda1-213">Z tego artykułu wiesz, jak przykłady hello toorun dołączonego hello klastrów usługi HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="3bda1-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="3bda1-214">Samouczki dotyczące przy użyciu Pig, Hive i MapReduce z usługą HDInsight zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="3bda1-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="3bda1-215">[Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3bda1-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3bda1-216">[Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="3bda1-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="3bda1-217">[Używanie MapReduce z usługą Hadoop w usłudze HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3bda1-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
