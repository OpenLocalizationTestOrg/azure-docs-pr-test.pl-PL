---
title: "Uruchom próbek Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z próbek określone przy użyciu usługi Azure HDInsight. Za pomocą skryptów środowiska PowerShell, które uruchamiać programy MapReduce w klastrach danych."
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
ms.openlocfilehash: 6e4dbf1fa32f916a206e4f8d796218ab809835ad
ms.sourcegitcommit: f8437edf5de144b40aed00af5c52a20e35d10ba1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Uruchom przykłady MapReduce z Hadoop w HDInsight opartych na systemie Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Zestaw przykładów są przekazywane do ułatwienia Ci uruchomiono uruchomionych zadań MapReduce na klastrów platformy Hadoop za pomocą usługi Azure HDInsight. Te przykłady są udostępniane na każdym klastry usługi HDInsight zarządzanych, które można utworzyć. Uruchamianie przykładów zapoznanie się z za pomocą poleceń cmdlet programu Azure PowerShell do uruchamiania zadań na klastrów platformy Hadoop.

* [**Word liczba**][hdinsight-sample-wordcount]: liczby wystąpień programu word w pliku tekstowym.
* [**C# przesyłania strumieniowego wyrazów**][hdinsight-sample-csharp-streaming]: liczby wystąpień programu word w pliku tekstowym przy użyciu interfejsu przesyłania strumieniowego usługi Hadoop.
* [**Narzędzia do szacowania pi**][hdinsight-sample-pi-estimator]: używa statystycznego (quasi Monte Carlo) metodę, aby oszacować wartość liczby pi.
* [**10 GB Graysort**][hdinsight-sample-10gb-graysort]: Uruchom ogólnego przeznaczenia GraySort pliku 10 GB, za pomocą usługi HDInsight. Istnieją trzy zadania do uruchomienia: Teragen do generowania danych Terasort, aby posortować dane i Teravalidate, aby potwierdzić prawidłowo posortowane dane.

> [!NOTE]
> Kod źródłowy znajduje się w dodatku.

Istnieje wiele dodatkową dokumentację w sieci web dla technologii związanych z platformy Hadoop, takich jak programowania MapReduce opartych na języku Java i przesyłanie strumieniowe i dokumentację dotyczącą poleceń cmdlet, które są używane w programie Windows PowerShell skryptów. Aby uzyskać więcej informacji na temat tych zasobów Zobacz:

* [Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight](hadoop/apache-hadoop-develop-deploy-java-mapreduce-linux.md)
* [Przesyłanie zadań Hadoop w usłudze HDInsight](hadoop/submit-apache-hadoop-jobs-programmatically.md)
* [Wprowadzenie do usługi Azure HDInsight][hdinsight-introduction]

Dzisiaj wiele osób wybiera Hive i Pig na MapReduce.  Aby uzyskać więcej informacji, zobacz:

* [Korzystanie z programu Hive w usłudze HDInsight](hadoop/hdinsight-use-hive.md)
* [Korzystanie z języka Pig w usłudze HDInsight](hadoop/hdinsight-use-pig.md)

**Wymagania wstępne**:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **klaster usługi HDInsight**. Aby uzyskać instrukcje na różne sposoby, w których można tworzyć takie klastry, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Stacja robocza z programem Azure PowerShell**.

    > [!IMPORTANT]
    > Obsługa środowiska Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i zostanie usunięta z dniem 1 stycznia 2017 r. W czynnościach opisanych w niniejszym dokumencie są używane nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Postępuj zgodnie z instrukcjami [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) do zainstalowania najnowszej wersji programu Azure PowerShell. Jeśli masz skrypty wymagające modyfikacji w celu użycia nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [Migrowanie do narzędzi programistycznych opartych na usłudze Azure Resource Manager dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Liczba - Java w programie Word
Aby przesłać projektu MapReduce, należy najpierw utworzyć definicji zadania MapReduce. W definicji zadania można określić plik jar programu MapReduce i lokalizację pliku jar, który jest **wasb:///example/jars/hadoop-mapreduce-examples.jar**, nazwę klasy i argumenty.  Wordcount MapReduce program przyjmuje dwa argumenty: plik źródłowy, który służy do Zliczanie słów i lokalizację danych wyjściowych.

Kod źródłowy znajduje się w [dodatek a](#apendix-a---the-word-count-MapReduce-program-in-java).

Procedurę tworzenia Java MapReduce programów, zobacz - [programy opracowanie MapReduce Java dla platformy Hadoop w usłudze HDInsight](hadoop/apache-hadoop-develop-deploy-java-mapreduce-linux.md)

**Aby przesłać zadania MapReduce liczba programu word**

1. Otwórz **programu Windows PowerShell ISE**. Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell][powershell-install-configure].
2. Wklej poniższy skrypt programu PowerShell:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define the MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit the job and wait for job completion
    $cred = Get-Credential -Message "Enter the HDInsight cluster HTTP user credential:"
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

    # Get the job output
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

    # Download the job output to the workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display the output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    Zadania MapReduce tworzy plik o nazwie *części r-00000*, który zawiera wyrazy i liczby elementów. Skrypt używa **findstr** polecenie, aby wyświetlić listę wszystkich wyrazów zawierający *"Brak"*.
3. Ustaw zmienne pierwsze trzy, a następnie uruchom skrypt.

## <a name="hdinsight-sample-csharp-streaming"></a>Liczba - C# przesyłania strumieniowego w programie Word
Hadoop zapewnia interfejs API przesyłania strumieniowego MapReduce, dzięki czemu można zapisać mapy i ograniczyć funkcje w językach innych niż Java.

> [!NOTE]
> Kroki opisane w tym samouczku dotyczą tylko komputerów z systemem Windows w usłudze hdinsight. Na przykład przesyłania strumieniowego dla klastrów usługi HDInsight opartych na systemie Linux, zobacz [opracowanie Python przesyłania strumieniowego programów dla usługi HDInsight](hadoop/apache-hadoop-streaming-python.md).

W tym przykładzie mapowania i reduktor są plikami wykonywalnymi odczytać dane wejściowe z [stdin] [ stdin-stdout-stderr] (wiersz po wierszu) i wyemituj dane wyjściowe do [stdout][stdin-stdout-stderr]. Program zlicza wszystkich wyrazów w tekście.

Gdy plik wykonywalny jest określona dla **mapowań**, każde zadanie mapowania uruchamia plik wykonywalny jako osobne proces po zainicjowaniu mapowania. Podczas działania zadania mapowania, konwertuje przychodzących do wierszy i źródła wierszy do [stdin] [ stdin-stdout-stderr] procesu.

Tymczasem mapowania zbiera dane wyjściowe wiersza ze strumienia wyjściowego stdout procesu. Konwertuje każdego wiersza w parę klucza i wartości, które są zbierane jako dane wyjściowe mapowania. Domyślnie prefiks wiersza do pierwszy znak tabulacji jest kluczem, a do końca wiersza (z wyjątkiem znak tabulacji) to wartość. Jeśli w wierszu nie ma żadnych znak tabulacji, cały wiersz jest uznawany za klucz i ma wartość null.

Gdy plik wykonywalny jest określona dla **reduktory**, każde zadanie reduktor uruchamia pliku wykonywalnego jako osobne proces po zainicjowaniu reduktor. Uruchamia zadanie reduktor, jego pary klucza/wartości wejściowe są konwertowane na linie i jego źródła wierszy do [stdin] [ stdin-stdout-stderr] procesu.

Tymczasem reduktor zbiera dane wyjściowe wiersza z [stdout] [ stdin-stdout-stderr] procesu. Konwertuje każdy wiersz na parę klucza i wartości, które są zbierane jako dane wyjściowe reduktor. Domyślnie prefiks wiersza do pierwszy znak tabulacji jest kluczem, a do końca wiersza (z wyjątkiem znak tabulacji) to wartość.

**Aby przesłać C# przesyłania strumieniowego zadanie liczba word**

* Postępuj zgodnie z procedurą w [Word liczba - Java](#word-count-java)i Zastąp definicji zadania o następujący wiersz:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    Plik wyjściowy jest:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>Narzędzia do szacowania PI
Narzędzia do szacowania pi używa statystycznego (quasi Monte Carlo) metodę, aby oszacować wartość liczby pi. Punkty losowo umieszczone wewnątrz jednostki kwadratowa również objęty koło wpisanego w tym kwadratowy z powierzchnią okręgu, prawdopodobieństwem pi/4. Wartość liczby pi można oszacować od wartości 4R, gdzie R jest współczynnik liczby punktów, które znajdują się wewnątrz okręgu całkowitą liczbę punktów, które znajdują się w kwadrat. Im większa próbka punkty używane jest lepsze szacowania.

Skryptów dla tego przykładu przesyła zadanie jar Hadoop i jest ustawiona do uruchamiania o wartości 16 mapy, z których każdy jest wymagane do obliczenia 10 milionów punktów próbki przez wartości parametrów. Wartości tych parametrów można zmienić zwiększające szacowaną wartość pi. Odwołanie są 3.1415926535 10 pierwszych miejsc dziesiętnych pi.

**Aby przesłać zadanie narzędzia do szacowania pi**

* Postępuj zgodnie z procedurą w [Word liczba - Java](#word-count-java)i Zastąp definicji zadania o następujący wiersz:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>Graysort 10 GB
W przykładzie użyto niewielkie 10GB danych, aby można było uruchomić stosunkowo szybko. Używa aplikacji MapReduce opracowane przez Owen O'Malley oraz organizacji i Arun Murthy, który won roczne testu porównawczego sortowania terabajt ogólnego przeznaczenia ("daytona") w 2009 ze stawką 0.578 TB na minutę (100 TB 173 minut). Aby uzyskać więcej informacji na ten temat oraz innych sortowania testów porównawczych, zobacz [Sortbenchmark](http://sortbenchmark.org/) lokacji.

W tym przykładzie używa trzech zestawów MapReduce programów:

1. **TeraGen** to program MapReduce, który służy do generowania wiersze danych do sortowania.
2. **TeraSort** próbek danych wejściowych i używa MapReduce, aby posortować dane w kolejności całkowitej. TeraSort jest standardowe sortowania funkcji MapReduce, z wyjątkiem niestandardowych partycjonerem, który używa posortowaną listę kluczy N-1 próbkowany, definiujące klucza zakresu dla każdego Zmniejsz. W szczególności, wszystkie klucze takie przykładowe [i-1] < klucz = < próbki [i] są wysyłane do i zmniejszyć. To gwarantuje, że dane wyjściowe zmniejszyć i wyświetlane są wszystkie mniejszej niż dane wyjściowe zmniejszyć i + 1.
3. **TeraValidate** to program MapReduce, który sprawdza, czy dane wyjściowe są sortowane globalnie. Tworzy jeden mapy dla każdego pliku w katalogu wyjściowego, a każda mapa zapewnia, że każdy klucz jest mniejsza niż lub równa poprzedniej. Funkcja mapy generuje również rekordy kluczy imię i nazwisko każdego pliku, a funkcja Zmniejsz zapewnia, że pierwszy klucz pliku i jest większy niż ostatni klucz i-1 pliku. Wszelkie problemy będą raportowane jako dane wyjściowe Zmniejsz z kluczami, które są poza kolejnością.

Format wejścia i wyjścia, używany przez wszystkie trzy aplikacje, odczytuje i zapisuje pliki tekstowe w prawidłowym formacie. Dane wyjściowe Zmniejsz ma ustawioną wartość 1, zamiast domyślnej 3, replikacji ponieważ kontekstem testu porównawczego nie wymaga, aby danych wyjściowych zostać zreplikowane na wielu węzłach.

Trzy zadania są wymagane przez próbki każdego odpowiadającego jednego z programów MapReduce opisano we wprowadzeniu:

1. Wygenerowane dane do sortowania, uruchamiając **TeraGen** zadania MapReduce.
2. Posortuj dane, uruchamiając **TeraSort** zadania MapReduce.
3. Upewnij się, że dane zostały poprawnie sortowane uruchamiając **TeraValidate** zadania MapReduce.

**Aby przesłać zadania**

* Postępuj zgodnie z procedurą w [Word liczba - Java](#word-count-java)i użyć następujących definicje zadań:

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
Z tego artykułu i artykułów w tych przykładach przedstawiono sposób uruchamiania przykładów dołączone klastry usługi HDInsight przy użyciu programu Azure PowerShell. Samouczki dotyczące przy użyciu Pig, Hive i MapReduce z usługą HDInsight zobacz następujące tematy:

* [Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight do analizy użycia przenośnych słuchawki][hdinsight-get-started]
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]
* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]
* [Przesyłanie zadań Hadoop w usłudze HDInsight][hdinsight-submit-jobs]
* [Dokumentację platformy Azure HDInsight SDK][hdinsight-sdk-documentation]

## <a name="appendix-a---the-word-count-source-code"></a>Dodatek A - kod źródłowy liczba programu Word

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

## <a name="appendix-b---the-word-count-streaming-source-code"></a>Dodatek B — wyrazów przesyłania strumieniowego kodu źródłowego
MapReduce używana aplikacja cat.exe jako interfejs mapowania strumienia tekstu w konsoli i aplikacji wc.exe jako interfejs Zmniejsz liczbę słowa, które są przesyłane strumieniowo z dokumentu. Mapowania i reduktor znaków, wiersz po wierszu, od Standardowy strumień wejściowy (stdin) do odczytu i zapisu w standardowym strumieniu wyjściowym (stdout).

```csharp
// The source code for the cat.exe (Mapper).

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

Używa mapowania kodu w pliku cat.cs [StreamReader] [ streamreader] obiektu do odczytania znaki strumienia przychodzącego do konsoli, który następnie zapisuje dane strumienia do standardowego strumienia wyjściowego z statycznych [elementu Console.Writeline] [ console-writeline] — metoda.

```csharp
// The source code for wc.exe (Reducer) is:

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

Używa reduktor kod w pliku wc.cs [StreamReader] [ streamreader] obiektu odczytywanie znaków z Standardowy strumień wejściowy, że zostały danych wyjściowych przez cat.exe mapowania. Jak odczytuje znaków z [elementu Console.Writeline] [ console-writeline] metody, liczy wyrazy poprzez zliczanie spacje i znaki końca wiersza na koniec każdego wyrazu. Następnie zapisuje łączną liczbę do standardowego strumienia wyjściowego z [elementu Console.Writeline] [ console-writeline] metody.

## <a name="appendix-c---the-pi-estimator-source-code"></a>Dodatek C — kod źródłowy narzędzia do szacowania Pi
Narzędzia do szacowania pi kodu języka Java, który zawiera funkcje mapowania i reduktor jest dostępna dla kontroli poniżej. Program mapowania punktów generuje określoną liczbę punktów, w losowo wybranym umieszczone wewnątrz kwadrat jednostki, a następnie oblicza liczbę punktów, które znajdują się wewnątrz okręgu. Program reduktor akumuluje punktów zliczane przez mapowań i następnie oszacowuje wartość pi z 4R formuły, gdzie R jest stosunkiem liczby punktów zliczane okręgu całkowitą liczbę punktów, które znajdują się w kwadrat.

```java
/**
* Licensed to the Apache Software Foundation (ASF) under one
* or more contributor license agreements. See the NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. The ASF licenses this file
* to you under the Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with the License. You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See the License for the specific language governing permissions and
* limitations under the License.
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

//A Map-reduce program to estimate the value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of the inscribed circle of the square.
//
//Reducer:
//Accumulate points inside/outside results from the mappers.
//Let numTotal = numInside + numOutside.
//The fraction numInside/numTotal is a rational approximation of
//the value (Area of the circle)/(Area of the square),
//where the area of the inscribed circle is Pi/4
//and the area of unit square is 1.
//Then, Pi is estimated value to be 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is the index.
//Halton sequence is used to generate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize to H(startindex),
//so the sequence begins with H(startindex+1).
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
//Assume the current point is H(index).
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
//count points inside/outside of the inscribed circle of the square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from the (offset+1)th sample.
//@param size the number of samples for this map
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

//count points inside/outside of the inscribed circle of the square
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
//Accumulate points inside/outside results from the mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing the file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from the mappers.
// @param isInside Is the points inside?
// @param values An iterator to a list of point counts
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

//Reduce task done, write output to a file.
@Override
public void close() throws IOException {
//write output to a file
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
//@return the estimated value of Pi.
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
// multiple writers to the same file.
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

## <a name="appendix-d---the-10gb-graysort-source-code"></a>Dodatek D - kod źródłowy graysort 10gb
Kod TeraSort MapReduce programu jest przedstawiane do kontroli w tej sekcji.

```java
/**
    * Licensed to the Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See the NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  The ASF licenses this file
    * to you under the Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with the License.  You may obtain a copy of the License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed to in writing, software
    * distributed under the License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See the License for the specific language governing permissions and
    * limitations under the License.
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
    * Generates the sampled split points, launches the job,
    * and waits for it to finish.
    * <p>
    * To run the program:
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
        * An inner trie node that contains 256 children based on the next
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
        * A leaf trie node that does string compares to figure out where the given
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
        * Read the cut points from the given sequence file.
        * @param fs the file system
        * @param p the path to read
        * @param job the job config
        * @return the strings to split the partitions on
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
        * Given a sorted set of cut points, build a trie that will find the correct
        * partition quickly.
        * @param splits the list of cut points
        * @param lower the lower bound of partitions 0..numPartitions-1
        * @param upper the upper bound of partitions 0..numPartitions-1
        * @param prefix the prefix that we have already checked against
        * @param maxDepth the maximum depth we will build a trie for
        * @return the trie node that will divide the splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on to the prefix
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
        // pick up the rest
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

[hdinsight-submit-jobs]: hadoop/submit-apache-hadoop-jobs-programmatically.md
[hdinsight-introduction]:hadoop/apache-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hadoop/hdinsight-use-hive.md
[hdinsight-use-pig]: hadoop/hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
