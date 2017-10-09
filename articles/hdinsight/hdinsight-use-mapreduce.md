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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>Korzystać z usługi MapReduce w Hadoop w usłudze HDInsight

Dowiedz się, jak toorun MapReduce zadania w klastrach usługi HDInsight. Użyj powitania po tabeli toodiscover hello różne sposoby, że MapReduce mogą być używane z usługą HDInsight:

| **Użyj tej**... | **.. .toodo to** | .. zwykle to **systemu operacyjnego klastra** | .. .from to **system operacyjny klienta** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Użyj polecenia Hadoop hello za pośrednictwem **SSH** |Linux |Linux, Unix, Mac OS X lub systemu Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Prześlij zadanie hello zdalnie przy użyciu **REST** (przykłady użycia cURL) |Linux lub Windows |Linux, Unix, Mac OS X lub systemu Windows |
| [Środowisko Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Prześlij zadanie hello zdalnie przy użyciu **środowiska Windows PowerShell** |Linux lub Windows |Windows |
| [Pulpit zdalny](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 i 3.3) |Użyj polecenia Hadoop hello za pośrednictwem **pulpitu zdalnego** |Windows |Windows |

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a id="whatis"></a>Co to jest MapReduce

MapReduce z Hadoop to platforma oprogramowania do zapisywania zadania, które przetwarzają olbrzymich ilości danych. Dane wejściowe jest podzielony na niezależne fragmenty, które następnie są przetwarzane równolegle na powitania węzłach w klastrze. Zadania MapReduce składa się z dwóch funkcji:

* **Mapowania**: zużywa dane wejściowe, analizuje je (zazwyczaj z filtrowanie i sortowanie operations) i emituje krotek (pary klucz wartość)

* **Reduktor**: wykorzystuje krotek emitowane przez hello mapowania, a następnie wykonuje operację podsumowania, która tworzy mniejsze, łączny wynik z hello danych mapowania

W przykładzie zadania MapReduce liczba podstawowe programu word przedstawiono na powitania po diagramu:

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

dane wyjściowe Hello tego zadania jest liczbę ile razy każdego wyrazu wystąpił w hello tekstu, który został przeanalizowany.

* mapowania Hello przyjmuje każdego wiersza z teksu wejściowego hello jako dane wejściowe i dzieli go na słów. Emituje go klucz/wartość pary zawsze wyraz występuje Word hello następuje 1. dane wyjściowe Hello są sortowane przed wysłaniem tooreducer.
* Reduktor Hello sumuje tych poszczególnych liczników dla każdego wyrazu i emituje parę jednego klucza i wartości, zawierający słowo hello, następuje hello sumę jego wystąpienia.

MapReduce może być wdrożonych w różnych językach. Java jest implementacją najczęściej hello i jest używany w celach demonstracyjnych, w tym dokumencie.

## <a name="development-languages"></a>Języki programowania

Języków i platform, które są oparte na języku Java i hello maszyny wirtualnej Java można uruchomiono bezpośrednio jako zadania MapReduce. przykład Witaj używane w tym dokumencie jest aplikacji Java MapReduce. Języki non-Java, takich jak C#, Python lub pliki wykonywalne autonomicznej, należy użyć przesyłania strumieniowego usługi Hadoop.

Przesyłanie strumieniowe Hadoop komunikuje się z mapowania hello i reduktor za pośrednictwem STDIN i STDOUT. mapowania Hello reduktor odczytać wiersza danych w czasie stdin i zapisać hello tooSTDOUT danych wyjściowych. Każdy wiersz odczytu lub emitowane przez mapowania hello i reduktor musi być w formacie hello pary klucz wartość ograniczonej przez znak tabulacji:

    [key]/t[value]

Aby uzyskać więcej informacji, zobacz [przesyłania strumieniowego usługi Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Przykłady korzystania z platformy Hadoop przesyłania strumieniowego z usługą HDInsight Zobacz powitania po dokumentów:

* [Tworzenie zadań MapReduce C#](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Tworzenie zadań MapReduce języka Python](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Przykładowe dane

Usługa HDInsight zapewnia różne przykład zestawów danych, które są przechowywane w hello `/example/data` i `/HdiSamples` katalogu. Te katalogi są hello domyślny magazyn dla klastra. W tym dokumencie używamy hello `/example/data/gutenberg/davinci.txt` pliku. Ten plik zawiera hello notesów programu Leonardo Da Vinci.

## <a id="job"></a>Przykład MapReduce

Przykład MapReduce word liczba aplikacji znajduje się z klastrem usługi HDInsight. W tym przykładzie znajduje się pod adresem `/example/jars/hadoop-mapreduce-examples.jar` na powitania domyślny magazyn dla klastra.

Witaj następującego kodu języka Java jest źródłem hello hello aplikacji MapReduce zawartych w hello `hadoop-mapreduce-examples.jar` pliku:

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

Instrukcje toowrite własnej aplikacji MapReduce, znajduje się hello w następujących dokumentach:

* [Tworzenie aplikacji Java MapReduce dla usługi HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Tworzenie aplikacji MapReduce języka Python dla usługi HDInsight](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Uruchom hello MapReduce

HDInsight można uruchamiać zadania HiveQL przy użyciu różnych metod. Użyj powitania po toodecide tabeli, która metoda jest odpowiednie dla Ciebie, a następnie wykonaj hello łącze, aby uzyskać wskazówki.

| **Użyj tej**... | **.. .toodo to** | .. zwykle to **systemu operacyjnego klastra** | .. .from to **system operacyjny klienta** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Użyj polecenia Hadoop hello za pośrednictwem **SSH** |Linux |Linux, Unix, Mac OS X lub systemu Windows |
| [Narzędzie curl](hdinsight-hadoop-use-mapreduce-curl.md) |Prześlij zadanie hello zdalnie przy użyciu **REST** |Linux lub Windows |Linux, Unix, Mac OS X lub systemu Windows |
| [Środowisko Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Prześlij zadanie hello zdalnie przy użyciu **środowiska Windows PowerShell** |Linux lub Windows |Windows |
| [Pulpit zdalny](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 i 3.3) |Użyj polecenia Hadoop hello za pośrednictwem **pulpitu zdalnego** |Windows |Windows |

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a id="nextsteps"></a>Następne kroki

toolearn więcej informacji na temat pracy z danymi w usłudze HDInsight, zobacz hello w następujących dokumentach:

* [Tworzenie programów Java MapReduce dla usługi HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Opracowywanie Python przesyłania strumieniowego programy MapReduce dla usługi HDInsight](hdinsight-hadoop-streaming-python.md)

* [Tworzenie zadań MapReduce sparzanie z platformy Apache Hadoop w usłudze HDInsight](hdinsight-hadoop-mapreduce-scalding.md)

* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]

* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
