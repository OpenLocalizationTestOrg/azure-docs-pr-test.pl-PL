---
title: "MapReduce z Hadoop w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie uruchamiania zadań MapReduce na platformie Hadoop w klastrach usługi HDInsight."
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="089f3-103">Korzystać z usługi MapReduce w Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="089f3-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="089f3-104">Informacje o sposobie uruchamiania zadań MapReduce na klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="089f3-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="089f3-105">Skorzystaj z poniższej tabeli, aby odnaleźć różne sposoby, że MapReduce mogą być używane z usługą HDInsight:</span><span class="sxs-lookup"><span data-stu-id="089f3-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="089f3-106">**Użyj tej**...</span><span class="sxs-lookup"><span data-stu-id="089f3-106">**Use this**...</span></span> | <span data-ttu-id="089f3-107">**. Aby to zrobić**</span><span class="sxs-lookup"><span data-stu-id="089f3-107">**...to do this**</span></span> | <span data-ttu-id="089f3-108">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="089f3-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="089f3-109">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="089f3-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="089f3-110">SSH</span><span class="sxs-lookup"><span data-stu-id="089f3-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="089f3-111">Użyj polecenia Hadoop za pomocą **SSH**</span><span class="sxs-lookup"><span data-stu-id="089f3-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="089f3-112">Linux</span><span class="sxs-lookup"><span data-stu-id="089f3-112">Linux</span></span> |<span data-ttu-id="089f3-113">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="089f3-114">REST</span><span class="sxs-lookup"><span data-stu-id="089f3-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="089f3-115">Przesłać zadanie zdalnie przy użyciu **REST** (przykłady użycia cURL)</span><span class="sxs-lookup"><span data-stu-id="089f3-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="089f3-116">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-116">Linux or Windows</span></span> |<span data-ttu-id="089f3-117">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="089f3-118">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="089f3-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="089f3-119">Przesłać zadanie zdalnie przy użyciu **środowiska Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="089f3-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="089f3-120">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-120">Linux or Windows</span></span> |<span data-ttu-id="089f3-121">Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-121">Windows</span></span> |
| <span data-ttu-id="089f3-122">[Pulpit zdalny](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 i 3.3)</span><span class="sxs-lookup"><span data-stu-id="089f3-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="089f3-123">Użyj polecenia Hadoop za pomocą **pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="089f3-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="089f3-124">Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-124">Windows</span></span> |<span data-ttu-id="089f3-125">Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="089f3-126">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="089f3-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="089f3-127">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="089f3-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="089f3-128"><a id="whatis"></a>Co to jest MapReduce</span><span class="sxs-lookup"><span data-stu-id="089f3-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="089f3-129">MapReduce z Hadoop to platforma oprogramowania do zapisywania zadania, które przetwarzają olbrzymich ilości danych.</span><span class="sxs-lookup"><span data-stu-id="089f3-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="089f3-130">Dane wejściowe jest podzielony na niezależne fragmenty, które następnie są przetwarzane równolegle w węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="089f3-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="089f3-131">Zadania MapReduce składa się z dwóch funkcji:</span><span class="sxs-lookup"><span data-stu-id="089f3-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="089f3-132">**Mapowania**: zużywa dane wejściowe, analizuje je (zazwyczaj z filtrowanie i sortowanie operations) i emituje krotek (pary klucz wartość)</span><span class="sxs-lookup"><span data-stu-id="089f3-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="089f3-133">**Reduktor**: wykorzystuje krotek emitowane przez funkcję mapowania, a następnie wykonuje operację podsumowania, która tworzy mniejsze, łączny wynik z danych mapowania</span><span class="sxs-lookup"><span data-stu-id="089f3-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="089f3-134">Na poniższym diagramie przedstawiono w przykładzie zadania MapReduce liczba podstawowe programu word:</span><span class="sxs-lookup"><span data-stu-id="089f3-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="089f3-136">Dane wyjściowe tego zadania jest liczba ile razy każdego wyrazu wystąpił tekst, który został przeanalizowany.</span><span class="sxs-lookup"><span data-stu-id="089f3-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="089f3-137">Podziały go na słowa mapowania i przyjmuje każdego wiersza w tekście wejściowych jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="089f3-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="089f3-138">Emituje go klucz/wartość pary zawsze wyraz występuje Word następuje 1.</span><span class="sxs-lookup"><span data-stu-id="089f3-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="089f3-139">Dane wyjściowe są sortowane przed wysłaniem ich do reduktor.</span><span class="sxs-lookup"><span data-stu-id="089f3-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="089f3-140">Reduktor sumuje tych poszczególnych liczników dla każdego wyrazu i emituje parę jednego klucza i wartości, zawierający słowo następuje sumę jego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="089f3-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="089f3-141">MapReduce może być wdrożonych w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="089f3-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="089f3-142">Java najczęściej implementacji i jest używany w celach demonstracyjnych, w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="089f3-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="089f3-143">Języki programowania</span><span class="sxs-lookup"><span data-stu-id="089f3-143">Development languages</span></span>

<span data-ttu-id="089f3-144">Języków i platform, które są oparte na języku Java i maszyny wirtualnej Java można uruchomiono bezpośrednio jako zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="089f3-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="089f3-145">Przykład używane w tym dokumencie jest aplikacji Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="089f3-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="089f3-146">Języki non-Java, takich jak C#, Python lub pliki wykonywalne autonomicznej, należy użyć przesyłania strumieniowego usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="089f3-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="089f3-147">Przesyłanie strumieniowe Hadoop komunikuje się z mapowania i reduktor za pośrednictwem STDIN i STDOUT.</span><span class="sxs-lookup"><span data-stu-id="089f3-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="089f3-148">Mapowania i reduktor danych wiersza w czasie stdin, do odczytu i zapisu danych wyjściowych STDOUT.</span><span class="sxs-lookup"><span data-stu-id="089f3-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="089f3-149">Każdy wiersz odczytu lub emitowane przez program mapowania i reduktor musi być w formacie parę klucz wartość ograniczonej przez znak tabulacji:</span><span class="sxs-lookup"><span data-stu-id="089f3-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="089f3-150">Aby uzyskać więcej informacji, zobacz [przesyłania strumieniowego usługi Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="089f3-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="089f3-151">Przykłady korzystania z platformy Hadoop przesyłania strumieniowego z usługą HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="089f3-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="089f3-152">Tworzenie zadań MapReduce C#</span><span class="sxs-lookup"><span data-stu-id="089f3-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="089f3-153">Tworzenie zadań MapReduce języka Python</span><span class="sxs-lookup"><span data-stu-id="089f3-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="089f3-154"><a id="data"></a>Przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="089f3-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="089f3-155">Usługa HDInsight zapewnia różne przykład zestawów danych, które są przechowywane w `/example/data` i `/HdiSamples` katalogu.</span><span class="sxs-lookup"><span data-stu-id="089f3-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="089f3-156">Te katalogi są domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="089f3-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="089f3-157">W tym dokumencie używamy `/example/data/gutenberg/davinci.txt` pliku.</span><span class="sxs-lookup"><span data-stu-id="089f3-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="089f3-158">Ten plik zawiera notebooki Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="089f3-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="089f3-159"><a id="job"></a>Przykład MapReduce</span><span class="sxs-lookup"><span data-stu-id="089f3-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="089f3-160">Przykład MapReduce word liczba aplikacji znajduje się z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="089f3-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="089f3-161">W tym przykładzie znajduje się pod adresem `/example/jars/hadoop-mapreduce-examples.jar` na domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="089f3-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="089f3-162">Poniższy kod języka Java jest źródłem zawartych w aplikacji MapReduce `hadoop-mapreduce-examples.jar` pliku:</span><span class="sxs-lookup"><span data-stu-id="089f3-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="089f3-163">Aby uzyskać instrukcje dotyczące pisać własne aplikacje MapReduce można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="089f3-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="089f3-164">Tworzenie aplikacji Java MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="089f3-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="089f3-165">Tworzenie aplikacji MapReduce języka Python dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="089f3-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="089f3-166"><a id="run"></a>Uruchom MapReduce</span><span class="sxs-lookup"><span data-stu-id="089f3-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="089f3-167">HDInsight można uruchamiać zadania HiveQL przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="089f3-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="089f3-168">Skorzystaj z poniższej tabeli do określania, która metoda jest odpowiednie dla Ciebie, a następnie kliknij link, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="089f3-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="089f3-169">**Użyj tej**...</span><span class="sxs-lookup"><span data-stu-id="089f3-169">**Use this**...</span></span> | <span data-ttu-id="089f3-170">**. Aby to zrobić**</span><span class="sxs-lookup"><span data-stu-id="089f3-170">**...to do this**</span></span> | <span data-ttu-id="089f3-171">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="089f3-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="089f3-172">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="089f3-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="089f3-173">SSH</span><span class="sxs-lookup"><span data-stu-id="089f3-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="089f3-174">Użyj polecenia Hadoop za pomocą **SSH**</span><span class="sxs-lookup"><span data-stu-id="089f3-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="089f3-175">Linux</span><span class="sxs-lookup"><span data-stu-id="089f3-175">Linux</span></span> |<span data-ttu-id="089f3-176">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="089f3-177">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="089f3-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="089f3-178">Przesłać zadanie zdalnie przy użyciu **REST**</span><span class="sxs-lookup"><span data-stu-id="089f3-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="089f3-179">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-179">Linux or Windows</span></span> |<span data-ttu-id="089f3-180">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="089f3-181">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="089f3-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="089f3-182">Przesłać zadanie zdalnie przy użyciu **środowiska Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="089f3-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="089f3-183">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-183">Linux or Windows</span></span> |<span data-ttu-id="089f3-184">Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-184">Windows</span></span> |
| <span data-ttu-id="089f3-185">[Pulpit zdalny](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 i 3.3)</span><span class="sxs-lookup"><span data-stu-id="089f3-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="089f3-186">Użyj polecenia Hadoop za pomocą **pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="089f3-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="089f3-187">Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-187">Windows</span></span> |<span data-ttu-id="089f3-188">Windows</span><span class="sxs-lookup"><span data-stu-id="089f3-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="089f3-189">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="089f3-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="089f3-190">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="089f3-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="089f3-191"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="089f3-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="089f3-192">Aby dowiedzieć się więcej na temat pracy z danymi w usłudze HDInsight, można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="089f3-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="089f3-193">Tworzenie programów Java MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="089f3-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="089f3-194">Opracowywanie Python przesyłania strumieniowego programy MapReduce dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="089f3-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="089f3-195">Tworzenie zadań MapReduce sparzanie z platformy Apache Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="089f3-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="089f3-196">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="089f3-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="089f3-197">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="089f3-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
