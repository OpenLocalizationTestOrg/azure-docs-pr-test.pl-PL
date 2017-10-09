---
title: "aaaMapReduce z platformą Hadoop w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorun MapReduce zadania na platformie Hadoop w klastrach usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="c3e26-103">Korzystać z usługi MapReduce w Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3e26-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="c3e26-104">Dowiedz się, jak toorun MapReduce zadania w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3e26-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="c3e26-105">Użyj powitania po tabeli toodiscover hello różne sposoby, że MapReduce mogą być używane z usługą HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c3e26-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="c3e26-106">**Użyj tej**...</span><span class="sxs-lookup"><span data-stu-id="c3e26-106">**Use this**...</span></span> | <span data-ttu-id="c3e26-107">**.. .toodo to**</span><span class="sxs-lookup"><span data-stu-id="c3e26-107">**...toodo this**</span></span> | <span data-ttu-id="c3e26-108">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="c3e26-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="c3e26-109">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="c3e26-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="c3e26-110">SSH</span><span class="sxs-lookup"><span data-stu-id="c3e26-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="c3e26-111">Użyj polecenia Hadoop hello za pośrednictwem **SSH**</span><span class="sxs-lookup"><span data-stu-id="c3e26-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="c3e26-112">Linux</span><span class="sxs-lookup"><span data-stu-id="c3e26-112">Linux</span></span> |<span data-ttu-id="c3e26-113">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="c3e26-114">REST</span><span class="sxs-lookup"><span data-stu-id="c3e26-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="c3e26-115">Prześlij zadanie hello zdalnie przy użyciu **REST** (przykłady użycia cURL)</span><span class="sxs-lookup"><span data-stu-id="c3e26-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="c3e26-116">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-116">Linux or Windows</span></span> |<span data-ttu-id="c3e26-117">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="c3e26-118">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3e26-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="c3e26-119">Prześlij zadanie hello zdalnie przy użyciu **środowiska Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="c3e26-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="c3e26-120">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-120">Linux or Windows</span></span> |<span data-ttu-id="c3e26-121">Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-121">Windows</span></span> |
| <span data-ttu-id="c3e26-122">[Pulpit zdalny](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 i 3.3)</span><span class="sxs-lookup"><span data-stu-id="c3e26-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="c3e26-123">Użyj polecenia Hadoop hello za pośrednictwem **pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="c3e26-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="c3e26-124">Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-124">Windows</span></span> |<span data-ttu-id="c3e26-125">Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c3e26-126">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c3e26-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3e26-127">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="c3e26-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="c3e26-128"><a id="whatis"></a>Co to jest MapReduce</span><span class="sxs-lookup"><span data-stu-id="c3e26-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="c3e26-129">MapReduce z Hadoop to platforma oprogramowania do zapisywania zadania, które przetwarzają olbrzymich ilości danych.</span><span class="sxs-lookup"><span data-stu-id="c3e26-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="c3e26-130">Dane wejściowe jest podzielony na niezależne fragmenty, które następnie są przetwarzane równolegle na powitania węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c3e26-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="c3e26-131">Zadania MapReduce składa się z dwóch funkcji:</span><span class="sxs-lookup"><span data-stu-id="c3e26-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="c3e26-132">**Mapowania**: zużywa dane wejściowe, analizuje je (zazwyczaj z filtrowanie i sortowanie operations) i emituje krotek (pary klucz wartość)</span><span class="sxs-lookup"><span data-stu-id="c3e26-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="c3e26-133">**Reduktor**: wykorzystuje krotek emitowane przez hello mapowania, a następnie wykonuje operację podsumowania, która tworzy mniejsze, łączny wynik z hello danych mapowania</span><span class="sxs-lookup"><span data-stu-id="c3e26-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="c3e26-134">W przykładzie zadania MapReduce liczba podstawowe programu word przedstawiono na powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="c3e26-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="c3e26-136">dane wyjściowe Hello tego zadania jest liczbę ile razy każdego wyrazu wystąpił w hello tekstu, który został przeanalizowany.</span><span class="sxs-lookup"><span data-stu-id="c3e26-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="c3e26-137">mapowania Hello przyjmuje każdego wiersza z teksu wejściowego hello jako dane wejściowe i dzieli go na słów.</span><span class="sxs-lookup"><span data-stu-id="c3e26-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="c3e26-138">Emituje go klucz/wartość pary zawsze wyraz występuje Word hello następuje 1.</span><span class="sxs-lookup"><span data-stu-id="c3e26-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="c3e26-139">dane wyjściowe Hello są sortowane przed wysłaniem tooreducer.</span><span class="sxs-lookup"><span data-stu-id="c3e26-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="c3e26-140">Reduktor Hello sumuje tych poszczególnych liczników dla każdego wyrazu i emituje parę jednego klucza i wartości, zawierający słowo hello, następuje hello sumę jego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="c3e26-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="c3e26-141">MapReduce może być wdrożonych w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="c3e26-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="c3e26-142">Java jest implementacją najczęściej hello i jest używany w celach demonstracyjnych, w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="c3e26-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="c3e26-143">Języki programowania</span><span class="sxs-lookup"><span data-stu-id="c3e26-143">Development languages</span></span>

<span data-ttu-id="c3e26-144">Języków i platform, które są oparte na języku Java i hello maszyny wirtualnej Java można uruchomiono bezpośrednio jako zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c3e26-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="c3e26-145">przykład Witaj używane w tym dokumencie jest aplikacji Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c3e26-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="c3e26-146">Języki non-Java, takich jak C#, Python lub pliki wykonywalne autonomicznej, należy użyć przesyłania strumieniowego usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c3e26-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="c3e26-147">Przesyłanie strumieniowe Hadoop komunikuje się z mapowania hello i reduktor za pośrednictwem STDIN i STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c3e26-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="c3e26-148">mapowania Hello reduktor odczytać wiersza danych w czasie stdin i zapisać hello tooSTDOUT danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3e26-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="c3e26-149">Każdy wiersz odczytu lub emitowane przez mapowania hello i reduktor musi być w formacie hello pary klucz wartość ograniczonej przez znak tabulacji:</span><span class="sxs-lookup"><span data-stu-id="c3e26-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="c3e26-150">Aby uzyskać więcej informacji, zobacz [przesyłania strumieniowego usługi Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="c3e26-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="c3e26-151">Przykłady korzystania z platformy Hadoop przesyłania strumieniowego z usługą HDInsight Zobacz powitania po dokumentów:</span><span class="sxs-lookup"><span data-stu-id="c3e26-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="c3e26-152">Tworzenie zadań MapReduce C#</span><span class="sxs-lookup"><span data-stu-id="c3e26-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="c3e26-153">Tworzenie zadań MapReduce języka Python</span><span class="sxs-lookup"><span data-stu-id="c3e26-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="c3e26-154"><a id="data"></a>Przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="c3e26-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="c3e26-155">Usługa HDInsight zapewnia różne przykład zestawów danych, które są przechowywane w hello `/example/data` i `/HdiSamples` katalogu.</span><span class="sxs-lookup"><span data-stu-id="c3e26-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="c3e26-156">Te katalogi są hello domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="c3e26-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="c3e26-157">W tym dokumencie używamy hello `/example/data/gutenberg/davinci.txt` pliku.</span><span class="sxs-lookup"><span data-stu-id="c3e26-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="c3e26-158">Ten plik zawiera hello notesów programu Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="c3e26-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="c3e26-159"><a id="job"></a>Przykład MapReduce</span><span class="sxs-lookup"><span data-stu-id="c3e26-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="c3e26-160">Przykład MapReduce word liczba aplikacji znajduje się z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3e26-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="c3e26-161">W tym przykładzie znajduje się pod adresem `/example/jars/hadoop-mapreduce-examples.jar` na powitania domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="c3e26-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="c3e26-162">Witaj następującego kodu języka Java jest źródłem hello hello aplikacji MapReduce zawartych w hello `hadoop-mapreduce-examples.jar` pliku:</span><span class="sxs-lookup"><span data-stu-id="c3e26-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="c3e26-163">Instrukcje toowrite własnej aplikacji MapReduce, znajduje się hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="c3e26-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="c3e26-164">Tworzenie aplikacji Java MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3e26-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="c3e26-165">Tworzenie aplikacji MapReduce języka Python dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3e26-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="c3e26-166"><a id="run"></a>Uruchom hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="c3e26-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="c3e26-167">HDInsight można uruchamiać zadania HiveQL przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="c3e26-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="c3e26-168">Użyj powitania po toodecide tabeli, która metoda jest odpowiednie dla Ciebie, a następnie wykonaj hello łącze, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="c3e26-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="c3e26-169">**Użyj tej**...</span><span class="sxs-lookup"><span data-stu-id="c3e26-169">**Use this**...</span></span> | <span data-ttu-id="c3e26-170">**.. .toodo to**</span><span class="sxs-lookup"><span data-stu-id="c3e26-170">**...toodo this**</span></span> | <span data-ttu-id="c3e26-171">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="c3e26-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="c3e26-172">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="c3e26-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="c3e26-173">SSH</span><span class="sxs-lookup"><span data-stu-id="c3e26-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="c3e26-174">Użyj polecenia Hadoop hello za pośrednictwem **SSH**</span><span class="sxs-lookup"><span data-stu-id="c3e26-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="c3e26-175">Linux</span><span class="sxs-lookup"><span data-stu-id="c3e26-175">Linux</span></span> |<span data-ttu-id="c3e26-176">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="c3e26-177">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="c3e26-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="c3e26-178">Prześlij zadanie hello zdalnie przy użyciu **REST**</span><span class="sxs-lookup"><span data-stu-id="c3e26-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="c3e26-179">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-179">Linux or Windows</span></span> |<span data-ttu-id="c3e26-180">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="c3e26-181">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3e26-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="c3e26-182">Prześlij zadanie hello zdalnie przy użyciu **środowiska Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="c3e26-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="c3e26-183">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-183">Linux or Windows</span></span> |<span data-ttu-id="c3e26-184">Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-184">Windows</span></span> |
| <span data-ttu-id="c3e26-185">[Pulpit zdalny](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 i 3.3)</span><span class="sxs-lookup"><span data-stu-id="c3e26-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="c3e26-186">Użyj polecenia Hadoop hello za pośrednictwem **pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="c3e26-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="c3e26-187">Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-187">Windows</span></span> |<span data-ttu-id="c3e26-188">Windows</span><span class="sxs-lookup"><span data-stu-id="c3e26-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c3e26-189">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c3e26-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3e26-190">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="c3e26-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="c3e26-191"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3e26-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c3e26-192">toolearn więcej informacji na temat pracy z danymi w usłudze HDInsight, zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="c3e26-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="c3e26-193">Tworzenie programów Java MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3e26-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="c3e26-194">Opracowywanie Python przesyłania strumieniowego programy MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3e26-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="c3e26-195">Tworzenie zadań MapReduce sparzanie z platformy Apache Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3e26-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="c3e26-196">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c3e26-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="c3e26-197">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c3e26-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
