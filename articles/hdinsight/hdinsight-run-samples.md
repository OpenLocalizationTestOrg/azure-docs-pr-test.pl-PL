---
title: "Przykłady aaaRun hello Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy przy użyciu usługi Azure HDInsight hello z hello przykłady. Za pomocą skryptów środowiska PowerShell, które uruchamiać programy MapReduce w klastrach danych."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Uruchom przykłady MapReduce z Hadoop w HDInsight opartych na systemie Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Zestaw przykładów podano toohelp rozpocząć pracę, uruchomionych zadań MapReduce na klastrów platformy Hadoop za pomocą usługi Azure HDInsight. Te przykłady są udostępniane na każdym hello HDInsight klastrami zarządzanymi, które można utworzyć. Uruchamianie przykładów zapoznanie się z za pomocą zadania toorun poleceń cmdlet programu Azure PowerShell dotyczących klastrów platformy Hadoop.

* [**Word liczba**][hdinsight-sample-wordcount]: liczby wystąpień programu word w pliku tekstowym.
* [**C# przesyłania strumieniowego wyrazów**][hdinsight-sample-csharp-streaming]: liczby wystąpień programu word w pliku tekstowym przy użyciu hello Hadoop interfejsu strumienia.
* [**Narzędzia do szacowania pi**][hdinsight-sample-pi-estimator]: używa statystycznego (quasi Monte Carlo) metoda tooestimate hello wartość liczby pi.
* [**10 GB Graysort**][hdinsight-sample-10gb-graysort]: Uruchom ogólnego przeznaczenia GraySort pliku 10 GB, za pomocą usługi HDInsight. Istnieją trzy toorun zadania: Teragen toogenerate hello danych, danych hello toosort Terasort i tooconfirm Teravalidate poprawnie sortowane hello danych.

> [!NOTE]
> Kod źródłowy Hello znajdują się w hello dodatku.

Znacznie dodatkową dokumentację istnieje w sieci web powitania dla technologii związanych z platformy Hadoop, takich jak programowania MapReduce opartych na języku Java i przesyłanie strumieniowe i dokumentację dotyczącą hello poleceń cmdlet, które są używane w programie Windows PowerShell skryptów. Aby uzyskać więcej informacji na temat tych zasobów Zobacz:

* [Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [Przesyłanie zadań Hadoop w usłudze HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Wprowadzenie tooAzure HDInsight][hdinsight-introduction]

Dzisiaj wiele osób wybiera Hive i Pig na MapReduce.  Aby uzyskać więcej informacji, zobacz:

* [Korzystanie z programu Hive w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig w usłudze HDInsight](hdinsight-use-pig.md)

**Wymagania wstępne**:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **klaster usługi HDInsight**. Aby uzyskać instrukcje na różne sposoby, w których można tworzyć takie klastry hello, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Stacja robocza z programem Azure PowerShell**.

    > [!IMPORTANT]
    > Obsługa środowiska Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i zostanie usunięta z dniem 1 stycznia 2017 r. Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Wykonaj kroki hello w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell. Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Liczba - Java w programie Word
toosubmit projektu MapReduce, należy najpierw utworzyć definicji zadania MapReduce. W definicji zadania hello, należy określić plik jar programu MapReduce hello i hello lokalizację pliku jar hello, który jest **wasb:///example/jars/hadoop-mapreduce-examples.jar**hello nazwę klasy i hello argumentów.  Hello wordcount MapReduce program przyjmuje dwa argumenty: hello plik źródłowy, który jest używane toocount słów i hello lokalizacji dla danych wyjściowych.

Kod źródłowy Hello znajdują się w hello [dodatek a.](#apendix-a---the-word-count-MapReduce-program-in-java).

Procedury hello powstania Java MapReduce programów, zobacz - [programy opracowanie MapReduce Java dla platformy Hadoop w usłudze HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

**toosubmit zadania MapReduce liczba programu word**

1. Otwórz **programu Windows PowerShell ISE**. Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell][powershell-install-configure].
2. Wklej hello następującego skryptu programu PowerShell:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    Witaj zadania MapReduce tworzy plik o nazwie *części r-00000*, który zawiera wyrazy i hello liczby. skrypt Hello używa hello **findstr** polecenie toolist wszystkie hello wyrazy, które zawiera *"Brak"*.
3. Ustaw hello pierwsze trzy zmienne i uruchom skrypt hello.

## <a name="hdinsight-sample-csharp-streaming"></a>Liczba - C# przesyłania strumieniowego w programie Word
Hadoop zapewnia przesyłania strumieniowego tooMapReduce interfejsu API, który umożliwia mapy toowrite i zmniejszyć funkcje w językach innych niż Java.

> [!NOTE]
> Witaj czynności w tym samouczku dotyczą tylko na podstawie tooWindows klastrów usługi HDInsight. Na przykład przesyłania strumieniowego dla klastrów usługi HDInsight opartych na systemie Linux, zobacz [opracowanie Python przesyłania strumieniowego programów dla usługi HDInsight](hdinsight-hadoop-streaming-python.md).

Przykład Witaj, mapowania hello i reduktor hello są plikami wykonywalnymi odczytać dane wejściowe hello [stdin] [ stdin-stdout-stderr] (wiersz po wierszu) i wyemituj dane wyjściowe hello zbyt[stdout] [stdin-stdout-stderr]. Hello program zlicza wszystkich wyrazów hello w tekście hello.

Gdy plik wykonywalny jest określona dla **mapowań**, każde zadanie mapowania uruchamia hello plik wykonywalny jako oddzielny proces po zainicjowaniu hello mapowania. Hello mapowania zadanie jest uruchamiane, jego dane wejściowe są konwertowane na linie i źródła hello wierszy toohello [stdin] [ stdin-stdout-stderr] hello procesu.

W hello międzyczasie mapowania hello zbiera hello w wierszu w danych wyjściowych stdout hello hello procesu. Konwertuje każdego wiersza w parę klucza i wartości, które są zbierane jako dane wyjściowe hello hello mapowania. Domyślnie hello prefiks wyrównać toohello pierwszy znak tabulacji jest kluczem hello i hello pozostałej części (z wyjątkiem hello znak tabulacji) wiersza hello jest wartością hello. Jeśli w wierszu hello nie ma żadnych znak tabulacji, cały wiersz jest uznawany za hello klucza i hello wartość jest równa null.

Gdy plik wykonywalny jest określona dla **reduktory**, każde zadanie reduktor uruchamia hello plik wykonywalny jako oddzielny proces po zainicjowaniu reduktor hello. Jak hello reduktor zadanie jest uruchamiane, jego pary klucza/wartości wejściowe są konwertowane na linie i jego źródła toohello wierszy hello [stdin] [ stdin-stdout-stderr] hello procesu.

W hello międzyczasie reduktor hello zbiera hello w wierszu w danych wyjściowych z hello [stdout] [ stdin-stdout-stderr] hello procesu. Konwertuje każdy wiersz tooa para klucza i wartości, które są zbierane jako dane wyjściowe hello reduktor hello. Domyślnie hello prefiks wyrównać toohello pierwszy znak tabulacji jest kluczem hello i hello pozostałej części (z wyjątkiem hello znak tabulacji) wiersza hello jest wartością hello.

**zadanie liczba word przesyłania strumieniowego toosubmit C#**

* Wykonaj procedurę hello w [Word liczba - Java](#word-count-java)i Zastąp definicji zadania hello powitania po wierszu:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    Plik wyjściowy Hello jest:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>Narzędzia do szacowania PI
narzędzia do szacowania pi Hello używa statystycznego (quasi Monte Carlo) metoda tooestimate hello wartość liczby pi. Punkty losowo umieszczone wewnątrz jednostki kwadratowa również objęty koło wpisanego w tym kwadratowy z obszarem równy toohello prawdopodobieństwo okręgu hello pi/4. od wartości hello 4R, gdzie R jest stosunek hello hello liczbę punktów, które znajdują się wewnątrz hello koło toohello łączną liczbę punktów znajdujące się w ramach kwadratowe hello można oszacować Hello wartość liczby pi. Hello większego przykładu hello punktów używana, jest lepiej oszacować hello hello.

skrypt Hello podany dla tego przykładu przesyła zadania jar usługi Hadoop i skonfigurowano toorun o wartości 16 mapy, z których każdy jest wymagane toocompute 10 milionów punktów próbki przez hello wartości parametrów. Parametr, te wartości mogą być zmieniony tooimprove hello Szacowana wartość liczby pi. Odwołanie hello 10 pierwszych miejsc dziesiętnych pi są 3.1415926535.

**zadania narzędzia do szacowania pi toosubmit**

* Wykonaj procedurę hello w [Word liczba - Java](#word-count-java)i Zastąp definicji zadania hello powitania po wierszu:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>Graysort 10 GB
W przykładzie użyto niewielkie 10GB danych, aby można było uruchomić stosunkowo szybko. Używa ona hello MapReduce aplikacje opracowane przez Owen O'Malley oraz organizacji i Arun Murthy, który won hello roczne ogólnego przeznaczenia ("daytona") terabajt sortowania testu porównawczego w 2009 ze stawką 0.578 TB na minutę (100 TB 173 minut). Aby uzyskać więcej informacji na ten temat oraz innych sortowania testów porównawczych, zobacz hello [Sortbenchmark](http://sortbenchmark.org/) lokacji.

W tym przykładzie używa trzech zestawów MapReduce programów:

1. **TeraGen** to program MapReduce służy wiersze hello toogenerate toosort danych.
2. **TeraSort** próbek danych wejściowych hello i używa danych hello toosort MapReduce do całkowitej zamówienia. TeraSort jest standardowe sortowania funkcji MapReduce, z wyjątkiem niestandardowych partycjonerem, który używa posortowaną listę kluczy N-1 próbkowany, definiujące hello klucza zakresu dla każdego Zmniejsz. W szczególności, wszystkie klucze takie przykładowe [i-1] < klucz = < próbki [i] są wysyłane tooreduce i. To gwarantuje, że elementy wyjściowe hello zmniejszyć i wyświetlane są wszystkie mniejszej niż dane wyjściowe hello zmniejszyć i + 1.
3. **TeraValidate** jest program MapReduce, która weryfikuje te dane wyjściowe hello globalnie jest sortowana. Tworzy jeden mapy dla każdego pliku w katalogu wyjściowego hello, a każda mapa zapewnia, że każdy klucz jest mniejsza lub równa toohello poprzedni. najpierw funkcja mapy Hello rekordów hello generuje również i ostatniego klucze każdego pliku oraz hello reduce — funkcja zapewnia, że hello pierwszy klucz pliku jest większy niż hello ostatniego klucza i-1 pliku. Problemów są zgłaszane jako dane wyjściowe hello zmniejszyć z kluczami hello, które są poza kolejnością.

argument wejściowy Hello i format wyjściowy, używany przez wszystkie trzy aplikacje, odczytywać i zapisywać pliki tekstowe hello w prawidłowym formacie hello. dane wyjściowe Hello hello zmniejszyć replikacji ustawił too1 zamiast domyślnych hello 3, ponieważ hello testu porównawczego kontekstem nie jest wymagane, czy dane wyjściowe hello być replikowane na węzłach toomultiple.

Trzy zadania są wymagane przez hello próbki, każdy odpowiedni tooone hello MapReduce opisanym w wprowadzenie hello:

1. Generowanie danych hello sortowania, uruchamiając hello **TeraGen** zadania MapReduce.
2. Sortowanie danych hello uruchamiając hello **TeraSort** zadania MapReduce.
3. Upewnij się, że hello dane zostały poprawnie sortowane uruchamiając hello **TeraValidate** zadania MapReduce.

**toosubmit hello zadania**

* Wykonaj procedurę hello w [Word liczba - Java](#word-count-java), i użyj hello następujące definicje zadań:

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Następne kroki
Z tego artykułu i artykuły hello w każdej z próbek hello wiesz, jak przykłady hello toorun dołączonego hello klastrów usługi HDInsight przy użyciu programu Azure PowerShell. Samouczki dotyczące przy użyciu Pig, Hive i MapReduce z usługą HDInsight zobacz następujące tematy hello:

* [Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive HDInsight tooanalyze przenośnych słuchawki używana][hdinsight-get-started]
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]
* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]
* [Przesyłanie zadań Hadoop w usłudze HDInsight][hdinsight-submit-jobs]
* [Dokumentację platformy Azure HDInsight SDK][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Dodatek A - hello kodu źródłowego liczba programu Word

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Dodatek B — Witaj wyrazów przesyłania strumieniowego kodu źródłowego
Hello MapReduce program używa hello cat.exe aplikacji jako tekst hello toostream interfejsu mapowania do konsoli hello i wc.exe hello hello zmniejszyć interfejsu toocount hello liczbę słowa, które są przesyłane strumieniowo z dokumentu. Zarówno mapowania hello i reduktor znaków, wiersz po wierszu, od hello Standardowy strumień wejściowy (stdin) i zapis toohello Standardowy strumień wyjściowy (stdout).

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Witaj mapowania kodu używa pliku cat.cs hello [StreamReader] [ streamreader] obiekt znaków hello tooread hello przychodzących strumienia toohello konsoli, który następnie zapisuje dane hello strumienia toohello Standardowy strumień wyjściowy z hello statycznych [elementu Console.Writeline] [ console-writeline] metody.

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Witaj reduktor kod używa pliku wc.cs hello [StreamReader] [ streamreader] obiekt tooread znaków z hello Standardowy strumień wejściowy że zostały danych wyjściowych przez hello cat.exe mapowania. Jak odczytuje hello znaków z hello [elementu Console.Writeline] [ console-writeline] metody, liczy słowa hello poprzez zliczanie spacje i znaki końca wiersza na koniec hello każdego wyrazu. Następnie zapisuje hello całkowita toohello Standardowy strumień wyjściowy z hello [elementu Console.Writeline] [ console-writeline] metody.

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Dodatek C — Witaj kodu źródłowego narzędzia do szacowania Pi
narzędzia do szacowania pi Hello kod języka Java, który zawiera funkcje mapowania i reduktor hello jest dostępna dla kontroli poniżej. program mapowania Hello następnie liczby hello liczbę tych punktów, które są okręgu hello i generuje określoną liczbę punktów, w losowo wybranym umieszczone wewnątrz kwadrat jednostki. program reduktor Hello akumuluje punktów zliczane przez mapowań hello i następnie szacuje hello wartość pi z hello 4R formuły, gdzie R jest hello stosunek liczby hello punktów zliczane wewnątrz hello koło toohello łączną liczbę punktów znajdujące się w ramach hello kwadratowe.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Dodatek D - kod źródłowy graysort 10gb hello
Kod Hello hello TeraSort MapReduce programu jest widoczne dla kontroli w tej sekcji.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
