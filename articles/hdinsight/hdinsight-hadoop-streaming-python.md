---
title: "Tworzenie zadań MapReduce z usługą HDInsight - Azure przesyłania strumieniowego Python | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie korzystania z języka Python w strumieniowym zadań MapReduce. Hadoop udostępnia interfejs API przesyłania strumieniowego dla MapReduce do pisania w językach innych niż Java."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="64367-104">Opracowywanie Python przesyłania strumieniowego programy MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="64367-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="64367-105">Informacje o sposobie korzystania z języka Python w strumieniowym działania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="64367-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="64367-106">Hadoop udostępnia interfejs API przesyłania strumieniowego dla MapReduce, umożliwiającą zapis mapy i ograniczyć funkcje w językach innych niż Java.</span><span class="sxs-lookup"><span data-stu-id="64367-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="64367-107">Kroki opisane w tym dokumencie mapy implementacji i zmniejszyć składników w języku Python.</span><span class="sxs-lookup"><span data-stu-id="64367-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64367-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64367-108">Prerequisites</span></span>

* <span data-ttu-id="64367-109">Opartych na systemie Linux platformą Hadoop w klastrze usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="64367-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="64367-110">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="64367-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="64367-111">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="64367-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="64367-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="64367-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="64367-113">Edytor tekstu</span><span class="sxs-lookup"><span data-stu-id="64367-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="64367-114">Edytor tekstu, należy użyć LF jako zakończenia linii.</span><span class="sxs-lookup"><span data-stu-id="64367-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="64367-115">Przy użyciu wiersza koniec CRLF powoduje, że błędy podczas uruchamiania zadania MapReduce w klastrach HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="64367-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="64367-116">`ssh` i `scp` polecenia, lub [programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="64367-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="64367-117">Liczba programu Word</span><span class="sxs-lookup"><span data-stu-id="64367-117">Word count</span></span>

<span data-ttu-id="64367-118">W tym przykładzie jest podstawowe wyrazów zaimplementowana w języku python mapowania i reduktor.</span><span class="sxs-lookup"><span data-stu-id="64367-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="64367-119">Mapowania dzieli zdania na poszczególnych wyrazów, a reduktor agreguje słowa i liczby do generowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="64367-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="64367-120">Poniższy schemat przedstawia co się dzieje podczas mapy i ograniczyć faz.</span><span class="sxs-lookup"><span data-stu-id="64367-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![Ilustracja procesu mapreduce](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="64367-122">MapReduce przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="64367-122">Streaming MapReduce</span></span>

<span data-ttu-id="64367-123">Hadoop umożliwia Określ plik, który zawiera mapy i zmniejszyć logikę, która jest używana przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="64367-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="64367-124">Określone wymagania dotyczące mapy i zmniejszyć logiki są:</span><span class="sxs-lookup"><span data-stu-id="64367-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="64367-125">**Wejściowy**: mapy i zmniejszyć składniki muszą odczytać dane wejściowe z STDIN.</span><span class="sxs-lookup"><span data-stu-id="64367-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="64367-126">**Dane wyjściowe**: mapy i zmniejszyć składniki musi zapisać danych wyjściowych stdout.</span><span class="sxs-lookup"><span data-stu-id="64367-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="64367-127">**Format danych**: dane używane i wyprodukowanych muszą być parę klucza i wartości, rozdzielając znak tabulacji.</span><span class="sxs-lookup"><span data-stu-id="64367-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="64367-128">Python może z łatwością obsłużyć te wymagania przy użyciu `sys` modułu do odczytu z STDIN z zastosowaniem `print` do drukowania do STDOUT.</span><span class="sxs-lookup"><span data-stu-id="64367-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="64367-129">Pozostałe zadania jest po prostu formatowania danych przy użyciu karty (`\t`) znak między kluczem i wartością.</span><span class="sxs-lookup"><span data-stu-id="64367-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="64367-130">Utwórz mapowania i reduktor</span><span class="sxs-lookup"><span data-stu-id="64367-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="64367-131">Utwórz plik o nazwie `mapper.py` i użyć poniższego kodu jako zawartości:</span><span class="sxs-lookup"><span data-stu-id="64367-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="64367-132">Utwórz plik o nazwie **reducer.py** i użyć poniższego kodu jako zawartości:</span><span class="sxs-lookup"><span data-stu-id="64367-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="64367-133">Uruchamianie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="64367-133">Run using PowerShell</span></span>

<span data-ttu-id="64367-134">Aby upewnić się, że pliki mają prawo zakończenia wierszy, użyj następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="64367-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="64367-135">[!code-powershell[główne](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="64367-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="64367-136">Poniższy skrypt programu PowerShell umożliwia przekazanie plików, uruchom zadanie i wyświetlić dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="64367-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="64367-137">[!code-powershell[główne](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="64367-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="64367-138">Uruchom w sesji SSH</span><span class="sxs-lookup"><span data-stu-id="64367-138">Run from an SSH session</span></span>

1. <span data-ttu-id="64367-139">Ze środowiska programowania, w tym samym katalogu co `mapper.py` i `reducer.py` pliki, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="64367-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="64367-140">Zastąp `username` z nazwą użytkownika SSH dla klastra, i `clustername` z nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="64367-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="64367-141">To polecenie kopiuje pliki z systemu lokalnego do węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="64367-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="64367-142">Jeśli użyto hasła, aby zabezpieczyć konto SSH, zostanie wyświetlony monit o hasło.</span><span class="sxs-lookup"><span data-stu-id="64367-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="64367-143">Jeśli używasz klucza SSH, może być konieczne użycie `-i` parametru i ścieżkę do klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="64367-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="64367-144">Na przykład `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="64367-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="64367-145">Połącz się z klastrem przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="64367-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="64367-146">Aby uzyskać więcej informacji o zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64367-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="64367-147">Aby zapewnić, że mapper.py i reducer.py mają zakończenia prawidłowe wierszy, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="64367-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="64367-148">Użyj następującego polecenia, aby uruchomić zadanie MapReduce.</span><span class="sxs-lookup"><span data-stu-id="64367-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="64367-149">To polecenie zawiera następujące części:</span><span class="sxs-lookup"><span data-stu-id="64367-149">This command has the following parts:</span></span>

   * <span data-ttu-id="64367-150">**hadoop streaming.jar**: używane podczas wykonywania operacji MapReduce przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="64367-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="64367-151">Hadoop go interfejsów z kodu zewnętrznego MapReduce, podane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="64367-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="64367-152">**— pliki**: Dodaje określone pliki do zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="64367-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="64367-153">**-mapowania**: Określa plik, który ma być używana jako mapowania Hadoop.</span><span class="sxs-lookup"><span data-stu-id="64367-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="64367-154">**-Reduktor**: Określa plik, który ma być używana jako reduktor Hadoop.</span><span class="sxs-lookup"><span data-stu-id="64367-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="64367-155">**-wejściowych**: wejściowego, możemy należy policzyć wyrazów z.</span><span class="sxs-lookup"><span data-stu-id="64367-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="64367-156">**-dane wyjściowe**: katalog, w którym są zapisywane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="64367-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="64367-157">Jak działa zadania MapReduce, proces jest wyświetlana jako wartości procentowe.</span><span class="sxs-lookup"><span data-stu-id="64367-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="64367-158">05-15-02 19:01:04 informacji o mapreduce. Zadanie: 0% zmniejszyć mapy 0% 05-15-02 19:01:16 informacji o mapreduce. Zadanie: 0% zmniejszyć mapy 100% 05-15-02 19:01:27 informacji o mapreduce. Zadania: 100% zmniejszyć mapy 100%</span><span class="sxs-lookup"><span data-stu-id="64367-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="64367-159">Aby wyświetlić dane wyjściowe, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="64367-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="64367-160">To polecenie wyświetla listę słów i ile razy wyraz wystąpił.</span><span class="sxs-lookup"><span data-stu-id="64367-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64367-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64367-161">Next steps</span></span>

<span data-ttu-id="64367-162">Teraz, kiedy znasz sposobu używania zadań przesyłania strumieniowego MapRedcue z usługą HDInsight, użyj następujących linków, aby poznać inne sposoby pracy z usługą Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64367-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="64367-163">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="64367-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="64367-164">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="64367-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="64367-165">Korzystanie z zadań MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="64367-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
