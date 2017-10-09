---
title: "aaaDevelop Python przesyłania strumieniowego MapReduce zadania z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Python w strumieniowym zadań MapReduce. Hadoop udostępnia interfejs API przesyłania strumieniowego dla MapReduce do pisania w językach innych niż Java."
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
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="6e706-104">Opracowywanie Python przesyłania strumieniowego programy MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e706-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="6e706-105">Dowiedz się, jak toouse Python w strumieniowym działania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6e706-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="6e706-106">Hadoop udostępnia interfejs API przesyłania strumieniowego dla MapReduce, Zmniejsz funkcje w językach innych niż Java i możliwość toowrite mapy.</span><span class="sxs-lookup"><span data-stu-id="6e706-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="6e706-107">Witaj kroki opisane w tym dokumencie hello mapy implementacji i zmniejszyć składników w języku Python.</span><span class="sxs-lookup"><span data-stu-id="6e706-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e706-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6e706-108">Prerequisites</span></span>

* <span data-ttu-id="6e706-109">Opartych na systemie Linux platformą Hadoop w klastrze usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e706-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6e706-110">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6e706-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6e706-111">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6e706-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6e706-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="6e706-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="6e706-113">Edytor tekstu</span><span class="sxs-lookup"><span data-stu-id="6e706-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6e706-114">Edytor tekstu Hello musi używać LF co hello zakończenia linii.</span><span class="sxs-lookup"><span data-stu-id="6e706-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="6e706-115">Przy użyciu wiersza koniec CRLF powoduje, że błędy podczas uruchamiania zadania MapReduce hello w klastrach HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="6e706-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="6e706-116">Witaj `ssh` i `scp` polecenia, lub [programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="6e706-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="6e706-117">Liczba programu Word</span><span class="sxs-lookup"><span data-stu-id="6e706-117">Word count</span></span>

<span data-ttu-id="6e706-118">W tym przykładzie jest podstawowe wyrazów zaimplementowana w języku python mapowania i reduktor.</span><span class="sxs-lookup"><span data-stu-id="6e706-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="6e706-119">mapowania Hello dzieli zdania na poszczególnych wyrazów, a reduktor hello agreguje hello słów i liczby tooproduce hello w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6e706-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="6e706-120">powitania po schemat blokowy przedstawia co się działo podczas mapy hello i ograniczyć faz.</span><span class="sxs-lookup"><span data-stu-id="6e706-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![Ilustracja hello mapreduce procesu](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="6e706-122">MapReduce przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="6e706-122">Streaming MapReduce</span></span>

<span data-ttu-id="6e706-123">Hadoop umożliwia toospecify pliku, który zawiera mapy hello i zmniejszyć logikę, która jest używana przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="6e706-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="6e706-124">Hello określonych wymagań dotyczących hello mapowania i zmniejszyć logiki są:</span><span class="sxs-lookup"><span data-stu-id="6e706-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="6e706-125">**Wejściowy**: hello mapy co pozwala zmniejszyć liczbę składników należy odczytać dane wejściowe z STDIN.</span><span class="sxs-lookup"><span data-stu-id="6e706-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="6e706-126">**Dane wyjściowe**: hello mapy co pozwala zmniejszyć liczbę składników musi być zapisana tooSTDOUT danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6e706-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="6e706-127">**Format danych**: hello danych używane i wyprodukowanych musi być parę klucza i wartości, rozdzielając znak tabulacji.</span><span class="sxs-lookup"><span data-stu-id="6e706-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="6e706-128">Python może z łatwością obsłużyć te wymagania przy użyciu hello `sys` tooread modułu z STDIN z zastosowaniem `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="6e706-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="6e706-129">Witaj pozostałych zadań jest po prostu formatowania danych hello za pomocą karty (`\t`) znak między hello klucz i wartość.</span><span class="sxs-lookup"><span data-stu-id="6e706-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="6e706-130">Utwórz mapowania hello i reduktor</span><span class="sxs-lookup"><span data-stu-id="6e706-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="6e706-131">Utwórz plik o nazwie `mapper.py` i hello Użyj następującego kodu jako zawartość hello:</span><span class="sxs-lookup"><span data-stu-id="6e706-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="6e706-132">Utwórz plik o nazwie **reducer.py** i hello Użyj następującego kodu jako zawartość hello:</span><span class="sxs-lookup"><span data-stu-id="6e706-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

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
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="6e706-133">Uruchamianie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e706-133">Run using PowerShell</span></span>

<span data-ttu-id="6e706-134">tooensure że pliki mają zakończenia wierszy prawo hello, hello Użyj następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6e706-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="6e706-135">Użyj hello następujące pliki hello tooupload skrypt programu PowerShell, uruchom zadanie hello i wyświetlić dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="6e706-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="6e706-136">Uruchom w sesji SSH</span><span class="sxs-lookup"><span data-stu-id="6e706-136">Run from an SSH session</span></span>

1. <span data-ttu-id="6e706-137">Ze środowiska deweloperskiego w hello sam katalogu jako `mapper.py` i `reducer.py` plików, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="6e706-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="6e706-138">Zastąp `username` z nazwą użytkownika SSH powitania dla klastra, i `clustername` o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="6e706-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="6e706-139">To polecenie kopiuje pliki hello z węzłem głównym toohello hello systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6e706-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e706-140">Jeśli używasz toosecure hasło konta SSH, zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="6e706-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="6e706-141">Jeśli używasz klucza SSH, może być toouse hello `-i` parametr i hello ścieżki toohello klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="6e706-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="6e706-142">Na przykład `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="6e706-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="6e706-143">Połącz toohello klastra przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="6e706-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="6e706-144">Aby uzyskać więcej informacji o zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6e706-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="6e706-145">tooensure hello mapper.py i reducer.py mają hello Popraw zakończenia wierszy, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="6e706-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="6e706-146">Użyj hello następujące zadania MapReduce hello toostart polecenia.</span><span class="sxs-lookup"><span data-stu-id="6e706-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="6e706-147">To polecenie ma hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6e706-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="6e706-148">**hadoop streaming.jar**: używane podczas wykonywania operacji MapReduce przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="6e706-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="6e706-149">Hadoop go interfejsów z hello MapReduce kod zewnętrzny podane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6e706-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="6e706-150">**— pliki**: dodaje określony hello zadania MapReduce toohello plików.</span><span class="sxs-lookup"><span data-stu-id="6e706-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="6e706-151">**-mapowania**: Określa, że Hadoop, która plików toouse hello mapowania.</span><span class="sxs-lookup"><span data-stu-id="6e706-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="6e706-152">**-Reduktor**: Określa, że Hadoop, która plików toouse hello reduktor.</span><span class="sxs-lookup"><span data-stu-id="6e706-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="6e706-153">**-wejściowych**: hello pliku wejściowego możemy należy policzyć wyrazów z.</span><span class="sxs-lookup"><span data-stu-id="6e706-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="6e706-154">**-dane wyjściowe**: hello katalogu, w którym hello dane wyjściowe są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="6e706-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="6e706-155">Jak działa hello zadania MapReduce, proces hello jest wyświetlana jako wartości procentowe.</span><span class="sxs-lookup"><span data-stu-id="6e706-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="6e706-156">05-15-02 19:01:04 informacji o mapreduce. Zadanie: 0% zmniejszyć mapy 0% 05-15-02 19:01:16 informacji o mapreduce. Zadanie: 0% zmniejszyć mapy 100% 05-15-02 19:01:27 informacji o mapreduce. Zadania: 100% zmniejszyć mapy 100%</span><span class="sxs-lookup"><span data-stu-id="6e706-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="6e706-157">dane wyjściowe hello tooview, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6e706-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="6e706-158">To polecenie wyświetla listę słów i ile razy program word hello wystąpił.</span><span class="sxs-lookup"><span data-stu-id="6e706-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e706-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e706-159">Next steps</span></span>

<span data-ttu-id="6e706-160">Teraz wiesz już, jak zadania przesyłania strumieniowego MapRedcue toouse z usługą HDInsight, za pomocą następującego łącza tooexplore hello toowork inne sposoby z usługą Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e706-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="6e706-161">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e706-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6e706-162">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e706-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="6e706-163">Korzystanie z zadań MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="6e706-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
