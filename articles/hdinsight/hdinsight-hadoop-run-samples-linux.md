---
title: "Uruchom przykłady MapReduce z Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy przy użyciu MapReduce próbek w pliki jar uwzględnione w usłudze HDInsight. Używanie protokołu SSH, aby połączyć się z klastrem, a następnie uruchom przykładowe zadania za pomocą polecenia Hadoop."
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
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="4544b-105">Uruchom przykłady MapReduce uwzględnione w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4544b-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="4544b-106">Dowiedz się, jak uruchomić przykłady MapReduce dołączone do platformy Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4544b-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4544b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4544b-107">Prerequisites</span></span>

* <span data-ttu-id="4544b-108">**Klaster usługi HDInsight**: zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="4544b-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4544b-109">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="4544b-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4544b-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="4544b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4544b-111">**Klient SSH**: Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4544b-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="4544b-112">Przykłady MapReduce</span><span class="sxs-lookup"><span data-stu-id="4544b-112">The MapReduce examples</span></span>

<span data-ttu-id="4544b-113">**Lokalizacja**: przykłady znajdują się w klastrze usługi HDInsight w `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="4544b-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="4544b-114">**Zawartość**: następujące przykłady znajdują się w tym archiwum:</span><span class="sxs-lookup"><span data-stu-id="4544b-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="4544b-115">`aggregatewordcount`: Agregacji na podstawie mapreduce program, który oblicza wyrażenie w plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="4544b-116">`aggregatewordhist`: Agregacji na podstawie mapreduce program, który oblicza histogram słowa plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="4544b-117">`bbp`: Mapreduce program, który używa Bailey-Borwein-Plouffe do wyliczenia dokładnej cyfr pi.</span><span class="sxs-lookup"><span data-stu-id="4544b-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="4544b-118">`dbcount`: Zadanie przykład liczby dzienników widok strony przechowywanych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="4544b-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="4544b-119">`distbbp`: Mapreduce program, który używa formuły BBP typu do obliczenia dokładne bitów pi.</span><span class="sxs-lookup"><span data-stu-id="4544b-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="4544b-120">`grep`: Mapreduce program zlicza dopasowań wyrażeń regularnych w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="4544b-121">`join`: Zadanie, które wykonuje sprzężenie za pośrednictwem sortowane, jednakowo na partycje zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="4544b-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="4544b-122">`multifilewc`: Zadanie, które zlicza wyrazy z wielu plików.</span><span class="sxs-lookup"><span data-stu-id="4544b-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="4544b-123">`pentomino`: Mapreduce kafelka zniesienia programu w celu rozwiązania problemów pentomino.</span><span class="sxs-lookup"><span data-stu-id="4544b-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="4544b-124">`pi`: Mapreduce program, który szacuje Pi przy użyciu quasi Monte Carlo metody.</span><span class="sxs-lookup"><span data-stu-id="4544b-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="4544b-125">`randomtextwriter`: Mapreduce program, który zapisuje 10 GB losowe danych tekstowych w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="4544b-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="4544b-126">`randomwriter`: Mapreduce program, który zapisuje 10 GB losowe dane w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="4544b-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="4544b-127">`secondarysort`: Przykładowy Definiowanie dodatkowej sortowania do fazy Zmniejsz.</span><span class="sxs-lookup"><span data-stu-id="4544b-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="4544b-128">`sort`: Mapreduce program napisane przez autora losowe dane są sortowane.</span><span class="sxs-lookup"><span data-stu-id="4544b-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="4544b-129">`sudoku`Solver sudoku.</span><span class="sxs-lookup"><span data-stu-id="4544b-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="4544b-130">`teragen`: Generować dane o terasort.</span><span class="sxs-lookup"><span data-stu-id="4544b-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="4544b-131">`terasort`: Uruchom terasort.</span><span class="sxs-lookup"><span data-stu-id="4544b-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="4544b-132">`teravalidate`: Sprawdzanie wyników terasort.</span><span class="sxs-lookup"><span data-stu-id="4544b-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="4544b-133">`wordcount`: Mapreduce program zlicza słowa plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="4544b-134">`wordmean`: Mapreduce program, który oblicza średnią długość słowa plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="4544b-135">`wordmedian`: Mapreduce program zlicza średniej długości słowa plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="4544b-136">`wordstandarddeviation`: Mapreduce program, który oblicza odchylenie standardowe długości wyrazów w plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="4544b-137">**Kod źródłowy**: kod źródłowy dla tych przykładów znajduje się w klastrze usługi HDInsight w `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="4544b-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="4544b-138">`2.2.4.9-1` w ścieżce jest wersja platformie Hortonworks Data Platform dla klastra usługi HDInsight i mogą być inne dla klastra.</span><span class="sxs-lookup"><span data-stu-id="4544b-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="4544b-139">Uruchomienie przykładu wordcount</span><span class="sxs-lookup"><span data-stu-id="4544b-139">Run the wordcount example</span></span>

1. <span data-ttu-id="4544b-140">Połączenie do usługi HDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4544b-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="4544b-141">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4544b-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4544b-142">Z `username@#######:~$` monit, użyj następującego polecenia, aby wyświetlić listę próbek:</span><span class="sxs-lookup"><span data-stu-id="4544b-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="4544b-143">To polecenie generuje listę przykładowych opisanych w poprzedniej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4544b-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="4544b-144">Użyj następującego polecenia, aby uzyskać pomoc dotyczącą określonego próbki.</span><span class="sxs-lookup"><span data-stu-id="4544b-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="4544b-145">W takim przypadku **wordcount** próbki:</span><span class="sxs-lookup"><span data-stu-id="4544b-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="4544b-146">Pojawi się następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="4544b-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="4544b-147">Ten komunikat oznacza, które można udostępniać wielu ścieżek dla dokumentów źródłowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="4544b-148">Ścieżka końcowego jest przechowywania danych wyjściowych (liczbę słów w dokumencie źródłowym).</span><span class="sxs-lookup"><span data-stu-id="4544b-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="4544b-149">Liczba wszystkich wyrazów w notesów programu Leonardo Da Vinci, które są dostarczane jako przykładowych danych z klastrem należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4544b-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="4544b-150">Dane wejściowe dla tego zadania zostanie odczytany z `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="4544b-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="4544b-151">Dane wyjściowe w tym przykładzie jest przechowywane w `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="4544b-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="4544b-152">Obu ścieżek znajdują się na domyślny magazyn dla klastra, a nie w lokalnym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="4544b-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4544b-153">Jak wspomniano w pomocy dla przykładu wordcount, można również określić wielu plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="4544b-154">Na przykład `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` zlicza słów w davinci.txt i ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="4544b-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="4544b-155">Po zakończeniu zadania, użyj następującego polecenia, aby wyświetlić dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="4544b-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="4544b-156">To polecenie łączy wszystkie pliki wyjściowe utworzonej przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="4544b-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="4544b-157">Wyświetla dane wyjściowe do konsoli.</span><span class="sxs-lookup"><span data-stu-id="4544b-157">It displays the output to the console.</span></span> <span data-ttu-id="4544b-158">Dane wyjściowe będą podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="4544b-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="4544b-159">Każdy wiersz zawiera słowo i jak często wystąpi w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="4544b-160">Przykład Sudoku</span><span class="sxs-lookup"><span data-stu-id="4544b-160">The Sudoku example</span></span>

<span data-ttu-id="4544b-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) jest układanki logiki, składa się z dziewięciu 3 x 3 siatki.</span><span class="sxs-lookup"><span data-stu-id="4544b-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="4544b-162">Niektóre komórki w siatce mają numery, podczas gdy inne są puste, a celem jest do rozwiązania dla puste komórki.</span><span class="sxs-lookup"><span data-stu-id="4544b-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="4544b-163">Więcej informacji na temat układanki ma poprzedniej konsolidacji, ale w tym przykładzie ma na celu rozwiązywanie dla puste komórki.</span><span class="sxs-lookup"><span data-stu-id="4544b-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="4544b-164">Dlatego nasze dane wejściowe powinny być pliku, który znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="4544b-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="4544b-165">Dziewięć wierszy dziewięć kolumn</span><span class="sxs-lookup"><span data-stu-id="4544b-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="4544b-166">Każda kolumna może zawierać wartość liczbowa lub `?` (co oznacza puste komórki)</span><span class="sxs-lookup"><span data-stu-id="4544b-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="4544b-167">Komórki są rozdzielone spacjami</span><span class="sxs-lookup"><span data-stu-id="4544b-167">Cells are separated by a space</span></span>

<span data-ttu-id="4544b-168">Brak niektórych sposób utworzenia łamigłówki Sudoku; Nie można powtórzyć liczbą kolumn lub wierszy.</span><span class="sxs-lookup"><span data-stu-id="4544b-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="4544b-169">Jest to przykład w klastrze usługi HDInsight, która została prawidłowo skonstruowana.</span><span class="sxs-lookup"><span data-stu-id="4544b-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="4544b-170">Znajduje się on w `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` i zawiera następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="4544b-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="4544b-171">Aby uruchomić ten przykład problem za pomocą przykład Sudoku, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4544b-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="4544b-172">Zostaną wyświetlone wyniki podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="4544b-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="4544b-173">Przykład pi (π)</span><span class="sxs-lookup"><span data-stu-id="4544b-173">Pi (π) example</span></span>

<span data-ttu-id="4544b-174">Przykładowe pi używa statystycznego (quasi Monte Carlo) metodę, aby oszacować wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="4544b-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="4544b-175">Punkty są umieszczane w losowo wybranym w kwadratowe jednostki.</span><span class="sxs-lookup"><span data-stu-id="4544b-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="4544b-176">Pole zawiera także okręgu.</span><span class="sxs-lookup"><span data-stu-id="4544b-176">The square also contains a circle.</span></span> <span data-ttu-id="4544b-177">Prawdopodobieństwo, że punkty objęte okręgu są równe obszaru okręgu, pi/4.</span><span class="sxs-lookup"><span data-stu-id="4544b-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="4544b-178">Wartość liczby pi można oszacować od wartości 4R.</span><span class="sxs-lookup"><span data-stu-id="4544b-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="4544b-179">R jest stosunkiem liczby punktów, które znajdują się wewnątrz okręgu całkowitą liczbę punktów, które znajdują się w kwadrat.</span><span class="sxs-lookup"><span data-stu-id="4544b-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="4544b-180">Im większa próbka punkty używane jest lepsze szacowania.</span><span class="sxs-lookup"><span data-stu-id="4544b-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="4544b-181">Użyj następującego polecenia, aby uruchomić ten przykład.</span><span class="sxs-lookup"><span data-stu-id="4544b-181">Use the following command to run this sample.</span></span> <span data-ttu-id="4544b-182">To polecenie używa 16 mapy z 10 000 000 próbek do oszacowania wartość liczby pi:</span><span class="sxs-lookup"><span data-stu-id="4544b-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="4544b-183">Wartość zwrócona przez to polecenie jest podobny do **3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="4544b-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="4544b-184">Odwołania są 3.1415926535 10 pierwszych miejsc dziesiętnych pi.</span><span class="sxs-lookup"><span data-stu-id="4544b-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="4544b-185">Przykład Greysort 10 GB</span><span class="sxs-lookup"><span data-stu-id="4544b-185">10 GB Greysort example</span></span>

<span data-ttu-id="4544b-186">GraySort jest sortowania testu wydajności.</span><span class="sxs-lookup"><span data-stu-id="4544b-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="4544b-187">Metryka jest wskaźnikiem sortowania (TB/minutę), które odbywa się podczas sortowania dużych ilości danych, zwykle 100 TB minimalnej.</span><span class="sxs-lookup"><span data-stu-id="4544b-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="4544b-188">W przykładzie użyto niewielkie 10 GB danych, aby można było uruchomić stosunkowo szybko.</span><span class="sxs-lookup"><span data-stu-id="4544b-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="4544b-189">Używa aplikacji MapReduce opracowane przez Owen O'Malley oraz organizacji i Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="4544b-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="4544b-190">Te aplikacje kupione roczne testu porównawczego sortowania terabajt ogólnego przeznaczenia ("daytona") w 2009 ze stawką 0.578 TB na minutę (100 TB 173 minut).</span><span class="sxs-lookup"><span data-stu-id="4544b-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="4544b-191">Aby uzyskać więcej informacji na ten temat oraz innych sortowania testów porównawczych, zobacz [Sortbenchmark](http://sortbenchmark.org/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="4544b-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="4544b-192">W tym przykładzie używa trzech zestawów MapReduce programów:</span><span class="sxs-lookup"><span data-stu-id="4544b-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="4544b-193">**TeraGen**: A MapReduce program, który generuje wiersze danych do sortowania</span><span class="sxs-lookup"><span data-stu-id="4544b-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="4544b-194">**TeraSort**: próbek danych wejściowych i używa MapReduce, aby posortować dane w kolejności całkowita</span><span class="sxs-lookup"><span data-stu-id="4544b-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="4544b-195">TeraSort jest standardowe sortowania MapReduce, z wyjątkiem partycjonera niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="4544b-196">Obiekt partitioner używa posortowaną listę kluczy N-1 próbkowany, definiujące klucza zakresu dla każdego Zmniejsz.</span><span class="sxs-lookup"><span data-stu-id="4544b-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="4544b-197">W szczególności, wszystkie klucze takie przykładowe [i-1] < klucz = < próbki [i] są wysyłane do i zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="4544b-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="4544b-198">Ten moduł partycjonowania gwarantuje, że dane wyjściowe zmniejszyć i wyświetlane są wszystkie mniejszej niż dane wyjściowe zmniejszyć i + 1.</span><span class="sxs-lookup"><span data-stu-id="4544b-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="4544b-199">**TeraValidate**: A MapReduce program, który sprawdza, czy dane wyjściowe są sortowane globalny</span><span class="sxs-lookup"><span data-stu-id="4544b-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="4544b-200">Tworzy jeden mapy dla każdego pliku w katalogu wyjściowego, a każda mapa zapewnia, że każdy klucz jest mniejsza niż lub równa poprzedniej.</span><span class="sxs-lookup"><span data-stu-id="4544b-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="4544b-201">Funkcja mapy generuje rekordy kluczy imię i nazwisko każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="4544b-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="4544b-202">Funkcja Zmniejsz zapewnia, że pierwszy klucz pliku i jest większy niż ostatni klucz i-1 pliku.</span><span class="sxs-lookup"><span data-stu-id="4544b-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="4544b-203">Wszelkie problemy będą raportowane jako dane wyjściowe fazy Zmniejsz z kluczami, które są poza kolejnością.</span><span class="sxs-lookup"><span data-stu-id="4544b-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="4544b-204">Użyj następujące kroki, aby wygenerować danych, sortowania, a następnie zweryfikować dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="4544b-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="4544b-205">Generowanie 10 GB danych, który jest przechowywany w magazynie domyślnego klastra usługi HDInsight przy `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="4544b-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="4544b-206">`-Dmapred.map.tasks` Informuje Hadoop ile zadań mapy do użycia dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="4544b-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="4544b-207">Końcowe dwa parametry poinstruować zadania, aby utworzyć 10 GB danych i zapisz go w `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="4544b-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="4544b-208">Aby posortować dane, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4544b-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="4544b-209">`-Dmapred.reduce.tasks` Informuje Hadoop, Zmniejsz liczbę zadań dla zadania.</span><span class="sxs-lookup"><span data-stu-id="4544b-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="4544b-210">Końcowe dwa parametry są tylko lokalizacje danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4544b-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="4544b-211">Aby sprawdzić poprawność danych wygenerowanych przez sortowanie, skorzystaj z następujących:</span><span class="sxs-lookup"><span data-stu-id="4544b-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="4544b-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4544b-212">Next steps</span></span>

<span data-ttu-id="4544b-213">W tym artykule przedstawiono sposób uruchamiania przykładów dołączone do klastrów usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="4544b-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="4544b-214">Samouczki dotyczące przy użyciu Pig, Hive i MapReduce z usługą HDInsight zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="4544b-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="4544b-215">[Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4544b-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4544b-216">[Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4544b-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4544b-217">[Używanie MapReduce z usługą Hadoop w usłudze HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4544b-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
