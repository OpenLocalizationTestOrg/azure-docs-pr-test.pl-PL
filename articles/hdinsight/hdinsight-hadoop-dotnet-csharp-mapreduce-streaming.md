---
title: "aaaUse C# z MapReduce na platformie Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązania MapReduce toocreate toouse C# z platformą Hadoop w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Za pomocą języka C# MapReduce, przesyłanie strumieniowe na platformie Hadoop w usłudze HDInsight

Dowiedz się, jak toocreate toouse C# MapReduce rozwiązania w usłudze HDInsight.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).

Przesyłanie strumieniowe Hadoop to narzędzie umożliwiające zadań MapReduce toorun przy użyciu skryptu lub pliku wykonywalnego. W tym przykładzie .NET jest używane tooimplement hello mapowania i reduktor liczba rozwiązania programu word.

## <a name="net-on-hdinsight"></a>.NET w usłudze HDInsight

__HDInsight opartych na systemie Linux__ klastrów użyj [Mono (https://mono-project.com)](https://mono-project.com) toorun aplikacji .NET. Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5. Aby uzyskać więcej informacji na powitania wersji Mono dołączone do usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md). toouse określonej wersji Mono, zobacz hello [instalacji lub aktualizacji Mono](hdinsight-hadoop-install-mono.md) dokumentu.

Aby uzyskać więcej informacji na Mono zgodność z wersji systemu .NET Framework, zobacz [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Jak działa przesyłanie strumieniowe Hadoop

Witaj podstawowy proces używany do przesyłania strumieniowego w tym dokumencie jest następujący:

1. Hadoop przekazuje STDIN mapowania toohello danych (mapper.exe w tym przykładzie).
2. mapowania Hello przetwarza hello danych i emituje tooSTDOUT par klucz/wartość tabulacji.
3. dane wyjściowe Hello odczytywane przez Hadoop, a następnie przekazywany STDIN reduktor toohello (reducer.exe w tym przykładzie).
4. Reduktor Hello odczytuje pary klucz wartość hello tabulacji, przetwarza dane hello i następnie emituje hello wynik jako pary klucz wartość tabulacji ze strumienia STDOUT.
5. dane wyjściowe Hello są odczytywane przez Hadoop i zapisywane toohello katalogu wyjściowego.

Aby uzyskać więcej informacji dotyczących przesyłania strumieniowego, zobacz [Hadoop przesyłania strumieniowego (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Wymagania wstępne

* Znajomość pisania i kompilowania kodu C#, przeznaczonego dla programu .NET Framework 4.5. Witaj kroków w tym dokumencie Visual Studio 2017 r.

* Sposób tooupload .exe pliki toohello klaster. Witaj kroki opisane w tym dokumencie Użyj hello Data Lake Tools dla programu Visual Studio tooupload hello pliki tooprimary magazynu dla klastra hello.

* Program Azure PowerShell lub klient SSH.

* Hadoop w klastrze usługi HDInsight. Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [tworzenia klastra usługi HDInsight](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Utwórz mapowania hello

W programie Visual Studio Utwórz nową __aplikacja Konsolowa__ o nazwie __mapowania__. Użyj następującego kodu dla aplikacji hello hello:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Po utworzeniu aplikacji hello skompiluj go tooproduce hello `/bin/Debug/mapper.exe` pliku w katalogu projektu hello.

## <a name="create-hello-reducer"></a>Utwórz reduktor hello

W programie Visual Studio Utwórz nową __aplikacja Konsolowa__ o nazwie __reduktor__. Użyj następującego kodu dla aplikacji hello hello:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Po utworzeniu aplikacji hello skompiluj go tooproduce hello `/bin/Debug/reducer.exe` pliku w katalogu projektu hello.

## <a name="upload-toostorage"></a>Przekaż toostorage

1. W programie Visual Studio Otwórz **Eksploratora serwera**.

2. Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.

3. Jeśli zostanie wyświetlony monit, wprowadź swoje poświadczenia subskrypcji platformy Azure, a następnie kliknij przycisk **logowania**.

4. Rozwiń węzeł klastra usługi HDInsight hello, która ma toodeploy tej aplikacji w celu. Wpis tekstem hello __(domyślne konto magazynu)__ ma na liście.

    ![Wyświetlanie hello konta magazynu dla klastra hello Eksploratora serwera](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Jeśli tego wpisu można rozszerzać, używasz __konta magazynu Azure__ jako domyślny magazyn dla klastra hello. Rozwiń pozycję hello tooview hello pliki hello domyślny magazyn dla klastra hello, a następnie kliknij dwukrotnie hello __(domyślny kontener)__.

    * Jeśli tego wpisu nie można rozwijać, używasz __Azure Data Lake Store__ jako hello domyślny magazyn dla klastra hello. pliki hello tooview hello domyślny magazyn dla klastra hello, kliknij dwukrotnie hello __(domyślne konto magazynu)__ wpisu.

5. pliki .exe hello tooupload, użyj jednej z hello następujące metody:

    * Jeśli przy użyciu __konta magazynu Azure__, kliknij ikonę przekazywania hello, a następnie wyszukaj toohello **bin\debug** folder hello **mapowania** projektu. Na koniec wybierz hello **mapper.exe** plik i kliknij przycisk **Ok**.

        ![Przekaż ikonę](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Jeśli przy użyciu __Azure Data Lake Store__, kliknij prawym przyciskiem myszy pusty obszar liście hello zawartości pliku, a następnie wybierz __przekazać__. Na koniec wybierz hello **mapper.exe** plik i kliknij przycisk **Otwórz**.

    Raz hello __mapper.exe__ przekazywania zakończył proces przekazywania powtarzania hello hello __reducer.exe__ pliku.

## <a name="run-a-job-using-an-ssh-session"></a>Uruchom zadanie: przy użyciu sesji SSH

1. Użyj klastra usługi HDInsight toohello tooconnect SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj jednej z hello następujące zadania MapReduce hello toostart polecenia:

    * Jeśli przy użyciu __usługi Data Lake Store__ jako domyślnego magazynu:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Jeśli przy użyciu __usługi Azure Storage__ jako domyślnego magazynu:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    następujące listy Hello opisano funkcję każdego parametru:

    * `hadoop-streaming.jar`: plik jar hello, który zawiera hello przesyłania strumieniowego funkcji MapReduce.
    * `-files`: Dodaje hello `mapper.exe` i `reducer.exe` pliki toothis zadania. Witaj `adl:///` lub `wasb:///` przed każdego pliku jest głównym toohello ścieżka hello domyślny magazyn dla klastra hello.
    * `-mapper`: Określa plik, który implementuje hello mapowania.
    * `-reducer`: Określa plik, który implementuje reduktor hello.
    * `-input`: hello dane wejściowe.
    * `-output`: katalog wyjściowy hello.

3. Po zakończeniu zadania MapReduce hello, użyj powitania po tooview hello wyników:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Witaj następujący tekst jest przykładem hello danych zwróconych przez to polecenie:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Uruchom zadanie: przy użyciu programu PowerShell

Użyj następującego toorun skrypt programu PowerShell zadania MapReduce hello i Pobierz hello wyników.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Ten skrypt monituje o hello nazwa_klastra konto logowania i hasła, wraz z nazwą klastra usługi HDInsight hello. Po zakończeniu zadania hello wyjście hello jest pobrany toohello `output.txt` pliku w skrypcie hello katalogu hello jest był uruchamiany z. Witaj następujący tekst jest przykładem danych hello w hello `output.txt` pliku:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat używania MapReduce z usługą HDInsight, zobacz [Użyj MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md).

Aby uzyskać informacje o używaniu języka C# z Hive i Pig, zobacz [C# funkcja zdefiniowana przez użytkownika za pomocą technologii Hive i Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Aby uzyskać informacje o używaniu języka C# z systemu Storm w usłudze HDInsight, zobacz [topologii opracowywania C# dla Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).