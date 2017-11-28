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
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="7e4fa-103">Za pomocą języka C# MapReduce, przesyłanie strumieniowe na platformie Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4fa-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="7e4fa-104">Dowiedz się, jak toocreate toouse C# MapReduce rozwiązania w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e4fa-105">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7e4fa-106">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="7e4fa-107">Przesyłanie strumieniowe Hadoop to narzędzie umożliwiające zadań MapReduce toorun przy użyciu skryptu lub pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="7e4fa-108">W tym przykładzie .NET jest używane tooimplement hello mapowania i reduktor liczba rozwiązania programu word.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="7e4fa-109">.NET w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4fa-109">.NET on HDInsight</span></span>

<span data-ttu-id="7e4fa-110">__HDInsight opartych na systemie Linux__ klastrów użyj [Mono (https://mono-project.com)](https://mono-project.com) toorun aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="7e4fa-111">Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="7e4fa-112">Aby uzyskać więcej informacji na powitania wersji Mono dołączone do usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="7e4fa-113">toouse określonej wersji Mono, zobacz hello [instalacji lub aktualizacji Mono](hdinsight-hadoop-install-mono.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="7e4fa-114">Aby uzyskać więcej informacji na Mono zgodność z wersji systemu .NET Framework, zobacz [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="7e4fa-115">Jak działa przesyłanie strumieniowe Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e4fa-115">How Hadoop streaming works</span></span>

<span data-ttu-id="7e4fa-116">Witaj podstawowy proces używany do przesyłania strumieniowego w tym dokumencie jest następujący:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="7e4fa-117">Hadoop przekazuje STDIN mapowania toohello danych (mapper.exe w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="7e4fa-118">mapowania Hello przetwarza hello danych i emituje tooSTDOUT par klucz/wartość tabulacji.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="7e4fa-119">dane wyjściowe Hello odczytywane przez Hadoop, a następnie przekazywany STDIN reduktor toohello (reducer.exe w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="7e4fa-120">Reduktor Hello odczytuje pary klucz wartość hello tabulacji, przetwarza dane hello i następnie emituje hello wynik jako pary klucz wartość tabulacji ze strumienia STDOUT.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="7e4fa-121">dane wyjściowe Hello są odczytywane przez Hadoop i zapisywane toohello katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="7e4fa-122">Aby uzyskać więcej informacji dotyczących przesyłania strumieniowego, zobacz [Hadoop przesyłania strumieniowego (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e4fa-123">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e4fa-123">Prerequisites</span></span>

* <span data-ttu-id="7e4fa-124">Znajomość pisania i kompilowania kodu C#, przeznaczonego dla programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="7e4fa-125">Witaj kroków w tym dokumencie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="7e4fa-126">Sposób tooupload .exe pliki toohello klaster.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="7e4fa-127">Witaj kroki opisane w tym dokumencie Użyj hello Data Lake Tools dla programu Visual Studio tooupload hello pliki tooprimary magazynu dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="7e4fa-128">Program Azure PowerShell lub klient SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="7e4fa-129">Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="7e4fa-130">Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [tworzenia klastra usługi HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="7e4fa-131">Utwórz mapowania hello</span><span class="sxs-lookup"><span data-stu-id="7e4fa-131">Create hello mapper</span></span>

<span data-ttu-id="7e4fa-132">W programie Visual Studio Utwórz nową __aplikacja Konsolowa__ o nazwie __mapowania__.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="7e4fa-133">Użyj następującego kodu dla aplikacji hello hello:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-133">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="7e4fa-134">Po utworzeniu aplikacji hello skompiluj go tooproduce hello `/bin/Debug/mapper.exe` pliku w katalogu projektu hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="7e4fa-135">Utwórz reduktor hello</span><span class="sxs-lookup"><span data-stu-id="7e4fa-135">Create hello reducer</span></span>

<span data-ttu-id="7e4fa-136">W programie Visual Studio Utwórz nową __aplikacja Konsolowa__ o nazwie __reduktor__.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="7e4fa-137">Użyj następującego kodu dla aplikacji hello hello:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-137">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="7e4fa-138">Po utworzeniu aplikacji hello skompiluj go tooproduce hello `/bin/Debug/reducer.exe` pliku w katalogu projektu hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="7e4fa-139">Przekaż toostorage</span><span class="sxs-lookup"><span data-stu-id="7e4fa-139">Upload toostorage</span></span>

1. <span data-ttu-id="7e4fa-140">W programie Visual Studio Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="7e4fa-141">Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="7e4fa-142">Jeśli zostanie wyświetlony monit, wprowadź swoje poświadczenia subskrypcji platformy Azure, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="7e4fa-143">Rozwiń węzeł klastra usługi HDInsight hello, która ma toodeploy tej aplikacji w celu.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="7e4fa-144">Wpis tekstem hello __(domyślne konto magazynu)__ ma na liście.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Wyświetlanie hello konta magazynu dla klastra hello Eksploratora serwera](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="7e4fa-146">Jeśli tego wpisu można rozszerzać, używasz __konta magazynu Azure__ jako domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="7e4fa-147">Rozwiń pozycję hello tooview hello pliki hello domyślny magazyn dla klastra hello, a następnie kliknij dwukrotnie hello __(domyślny kontener)__.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="7e4fa-148">Jeśli tego wpisu nie można rozwijać, używasz __Azure Data Lake Store__ jako hello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="7e4fa-149">pliki hello tooview hello domyślny magazyn dla klastra hello, kliknij dwukrotnie hello __(domyślne konto magazynu)__ wpisu.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="7e4fa-150">pliki .exe hello tooupload, użyj jednej z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="7e4fa-151">Jeśli przy użyciu __konta magazynu Azure__, kliknij ikonę przekazywania hello, a następnie wyszukaj toohello **bin\debug** folder hello **mapowania** projektu.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="7e4fa-152">Na koniec wybierz hello **mapper.exe** plik i kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![Przekaż ikonę](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="7e4fa-154">Jeśli przy użyciu __Azure Data Lake Store__, kliknij prawym przyciskiem myszy pusty obszar liście hello zawartości pliku, a następnie wybierz __przekazać__.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="7e4fa-155">Na koniec wybierz hello **mapper.exe** plik i kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="7e4fa-156">Raz hello __mapper.exe__ przekazywania zakończył proces przekazywania powtarzania hello hello __reducer.exe__ pliku.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="7e4fa-157">Uruchom zadanie: przy użyciu sesji SSH</span><span class="sxs-lookup"><span data-stu-id="7e4fa-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="7e4fa-158">Użyj klastra usługi HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="7e4fa-159">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="7e4fa-160">Użyj jednej z hello następujące zadania MapReduce hello toostart polecenia:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="7e4fa-161">Jeśli przy użyciu __usługi Data Lake Store__ jako domyślnego magazynu:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="7e4fa-162">Jeśli przy użyciu __usługi Azure Storage__ jako domyślnego magazynu:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="7e4fa-163">następujące listy Hello opisano funkcję każdego parametru:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="7e4fa-164">`hadoop-streaming.jar`: plik jar hello, który zawiera hello przesyłania strumieniowego funkcji MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="7e4fa-165">`-files`: Dodaje hello `mapper.exe` i `reducer.exe` pliki toothis zadania.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="7e4fa-166">Witaj `adl:///` lub `wasb:///` przed każdego pliku jest głównym toohello ścieżka hello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="7e4fa-167">`-mapper`: Określa plik, który implementuje hello mapowania.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="7e4fa-168">`-reducer`: Określa plik, który implementuje reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="7e4fa-169">`-input`: hello dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="7e4fa-170">`-output`: katalog wyjściowy hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="7e4fa-171">Po zakończeniu zadania MapReduce hello, użyj powitania po tooview hello wyników:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="7e4fa-172">Witaj następujący tekst jest przykładem hello danych zwróconych przez to polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="7e4fa-173">Uruchom zadanie: przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e4fa-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="7e4fa-174">Użyj następującego toorun skrypt programu PowerShell zadania MapReduce hello i Pobierz hello wyników.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="7e4fa-175">Ten skrypt monituje o hello nazwa_klastra konto logowania i hasła, wraz z nazwą klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="7e4fa-176">Po zakończeniu zadania hello wyjście hello jest pobrany toohello `output.txt` pliku w skrypcie hello katalogu hello jest był uruchamiany z.</span><span class="sxs-lookup"><span data-stu-id="7e4fa-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="7e4fa-177">Witaj następujący tekst jest przykładem danych hello w hello `output.txt` pliku:</span><span class="sxs-lookup"><span data-stu-id="7e4fa-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="7e4fa-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e4fa-178">Next steps</span></span>

<span data-ttu-id="7e4fa-179">Aby uzyskać więcej informacji na temat używania MapReduce z usługą HDInsight, zobacz [Użyj MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="7e4fa-180">Aby uzyskać informacje o używaniu języka C# z Hive i Pig, zobacz [C# funkcja zdefiniowana przez użytkownika za pomocą technologii Hive i Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="7e4fa-181">Aby uzyskać informacje o używaniu języka C# z systemu Storm w usłudze HDInsight, zobacz [topologii opracowywania C# dla Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7e4fa-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>