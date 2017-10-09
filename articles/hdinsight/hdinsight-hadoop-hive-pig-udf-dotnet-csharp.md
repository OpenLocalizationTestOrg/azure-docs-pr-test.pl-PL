---
title: "aaaUse C# z Hive i Pig na platformie Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse C# zdefiniowane przez użytkownika (UDF) funkcje za pomocą technologii Hive i Pig przesyłania strumieniowego w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="9a7da-103">C# zdefiniowane przez użytkownika funkcji za pomocą technologii Hive i Pig przesyłania strumieniowego na platformie Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="9a7da-104">Dowiedz się, jak toouse C# funkcje zdefiniowane przez użytkownika (UDF) z Apache Hive i Pig w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a7da-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a7da-105">Hello kroków w tym dokumencie pracy z klastrami usługi HDInsight opartych na systemie Linux, a także z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="9a7da-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9a7da-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9a7da-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9a7da-107">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9a7da-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="9a7da-108">Zarówno Hive i Pig można przekazać danych tooexternal aplikacje do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="9a7da-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="9a7da-109">Ten proces jest nazywany _przesyłania strumieniowego_.</span><span class="sxs-lookup"><span data-stu-id="9a7da-109">This process is known as _streaming_.</span></span> <span data-ttu-id="9a7da-110">Podczas korzystania z aplikacji .NET, hello przekazywania danych aplikacji toohello STDIN, a aplikacja hello zwraca wyniki hello ze strumienia STDOUT.</span><span class="sxs-lookup"><span data-stu-id="9a7da-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="9a7da-111">tooread i zapisu z STDIN i STDOUT, można użyć `Console.ReadLine()` i `Console.WriteLine()` z aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="9a7da-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a7da-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9a7da-112">Prerequisites</span></span>

* <span data-ttu-id="9a7da-113">Znajomość pisania i kompilowania kodu C#, przeznaczonego dla programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="9a7da-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="9a7da-114">Użyj dowolnej IDE ma.</span><span class="sxs-lookup"><span data-stu-id="9a7da-114">Use whatever IDE you want.</span></span> <span data-ttu-id="9a7da-115">Firma Microsoft zaleca [programu Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, lub [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="9a7da-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="9a7da-116">Witaj kroków w tym dokumencie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9a7da-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="9a7da-117">.Exe tooupload sposób pliki toohello klastra i wykonywania zadań Pig i Hive.</span><span class="sxs-lookup"><span data-stu-id="9a7da-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="9a7da-118">Zalecamy hello Data Lake Tools dla programu Visual Studio, programu Azure PowerShell i interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="9a7da-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="9a7da-119">Witaj kroki opisane w tym dokumencie użycia hello Data Lake Tools dla Visual Studio tooupload hello plików i uruchom hello przykładowe zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="9a7da-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="9a7da-120">Informacji na temat innych sposobów zapytań programu Hive toorun i zadań Pig Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="9a7da-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="9a7da-121">Use Apache Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="9a7da-122">Use Apache Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="9a7da-123">Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a7da-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="9a7da-124">Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [tworzenia klastra usługi HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9a7da-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="9a7da-125">.NET w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-125">.NET on HDInsight</span></span>

* <span data-ttu-id="9a7da-126">__HDInsight opartych na systemie Linux__ klastrów za pomocą [Mono (https://mono-project.com)](https://mono-project.com) toorun aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="9a7da-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="9a7da-127">Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="9a7da-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="9a7da-128">Aby uzyskać więcej informacji na Mono zgodność z wersji systemu .NET Framework, zobacz [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="9a7da-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="9a7da-129">toouse określonej wersji Mono, zobacz hello [instalacji lub aktualizacji Mono](hdinsight-hadoop-install-mono.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="9a7da-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="9a7da-130">__HDInsight opartych na systemie Windows__ klastrom aplikacji .NET toorun Microsoft .NET CLR hello.</span><span class="sxs-lookup"><span data-stu-id="9a7da-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="9a7da-131">Aby uzyskać więcej informacji o wersji hello hello .NET framework i Mono dołączone do wersji usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9a7da-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="9a7da-132">Utwórz hello C\# projektów</span><span class="sxs-lookup"><span data-stu-id="9a7da-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="9a7da-133">Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="9a7da-133">Hive UDF</span></span>

1. <span data-ttu-id="9a7da-134">Otwórz program Visual Studio i utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="9a7da-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="9a7da-135">Typ projektu hello wybierz **aplikacji konsoli (.NET Framework)**i nazwę hello nowy projekt **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9a7da-136">Wybierz __.NET Framework 4.5__ korzystania z klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="9a7da-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9a7da-137">Aby uzyskać więcej informacji na Mono zgodność z wersji systemu .NET Framework, zobacz [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="9a7da-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="9a7da-138">Zamień zawartość hello **Program.cs** hello następujący:</span><span class="sxs-lookup"><span data-stu-id="9a7da-138">Replace hello contents of **Program.cs** with hello following:</span></span>

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. <span data-ttu-id="9a7da-139">Tworzenie projektu hello.</span><span class="sxs-lookup"><span data-stu-id="9a7da-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="9a7da-140">Pig funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="9a7da-140">Pig UDF</span></span>

1. <span data-ttu-id="9a7da-141">Otwórz program Visual Studio i utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="9a7da-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="9a7da-142">Typ projektu hello wybierz **aplikacji konsoli**i nowy projekt hello nazwa **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="9a7da-143">Zamień zawartość hello hello **Program.cs** pliku z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="9a7da-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="9a7da-144">Ta aplikacja analizuje wierszy hello wysłanych z Pig i ponownego formatowania wierszy, które zaczynają się od `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="9a7da-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="9a7da-145">Zapisz **Program.cs**i późniejszego kompilowania hello projektu.</span><span class="sxs-lookup"><span data-stu-id="9a7da-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="9a7da-146">Przekaż toostorage</span><span class="sxs-lookup"><span data-stu-id="9a7da-146">Upload toostorage</span></span>

1. <span data-ttu-id="9a7da-147">W programie Visual Studio Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="9a7da-148">Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="9a7da-149">Jeśli zostanie wyświetlony monit, wprowadź swoje poświadczenia subskrypcji platformy Azure, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="9a7da-150">Rozwiń węzeł klastra usługi HDInsight hello, która ma toodeploy tej aplikacji w celu.</span><span class="sxs-lookup"><span data-stu-id="9a7da-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="9a7da-151">Wpis tekstem hello __(domyślne konto magazynu)__ ma na liście.</span><span class="sxs-lookup"><span data-stu-id="9a7da-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Wyświetlanie hello konta magazynu dla klastra hello Eksploratora serwera](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="9a7da-153">Jeśli tego wpisu można rozszerzać, używasz __konta magazynu Azure__ jako domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="9a7da-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="9a7da-154">Rozwiń pozycję hello tooview hello pliki hello domyślny magazyn dla klastra hello, a następnie kliknij dwukrotnie hello __(domyślny kontener)__.</span><span class="sxs-lookup"><span data-stu-id="9a7da-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="9a7da-155">Jeśli tego wpisu nie można rozwijać, używasz __Azure Data Lake Store__ jako hello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="9a7da-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="9a7da-156">pliki hello tooview hello domyślny magazyn dla klastra hello, kliknij dwukrotnie hello __(domyślne konto magazynu)__ wpisu.</span><span class="sxs-lookup"><span data-stu-id="9a7da-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="9a7da-157">pliki .exe hello tooupload, użyj jednej z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="9a7da-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="9a7da-158">Jeśli przy użyciu __konta magazynu Azure__, kliknij ikonę przekazywania hello, a następnie wyszukaj toohello **bin\debug** folder hello **HiveCSharp** projektu.</span><span class="sxs-lookup"><span data-stu-id="9a7da-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="9a7da-159">Na koniec wybierz hello **HiveCSharp.exe** plik i kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![Przekaż ikonę](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="9a7da-161">Jeśli przy użyciu __Azure Data Lake Store__, kliknij prawym przyciskiem myszy pusty obszar liście hello zawartości pliku, a następnie wybierz __przekazać__.</span><span class="sxs-lookup"><span data-stu-id="9a7da-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="9a7da-162">Na koniec wybierz hello **HiveCSharp.exe** plik i kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="9a7da-163">Raz hello __HiveCSharp.exe__ przekazywania zakończył proces przekazywania powtarzania hello hello __PigUDF.exe__ pliku.</span><span class="sxs-lookup"><span data-stu-id="9a7da-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="9a7da-164">Uruchomienie zapytania programu Hive</span><span class="sxs-lookup"><span data-stu-id="9a7da-164">Run a Hive query</span></span>

1. <span data-ttu-id="9a7da-165">W programie Visual Studio Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="9a7da-166">Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="9a7da-167">Kliknij prawym przyciskiem myszy klaster hello wdrożonymi hello **HiveCSharp** do aplikacji, a następnie wybierz **Napisz zapytanie Hive**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="9a7da-168">Użyj następującego tekstu dla zapytania Hive hello hello:</span><span class="sxs-lookup"><span data-stu-id="9a7da-168">Use hello following text for hello Hive query:</span></span>

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="9a7da-169">Usuń znaczniki komentarza hello `add file` instrukcji, która odpowiada hello typu magazyny domyślne używane dla klastra.</span><span class="sxs-lookup"><span data-stu-id="9a7da-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="9a7da-170">To zapytanie wybiera hello `clientid`, `devicemake`, i `devicemodel` pola z `hivesampletable`i przekazuje pola hello toohello HiveCSharp.exe aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9a7da-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="9a7da-171">Zapytanie Hello oczekuje hello aplikacji tooreturn trzy pola, które są przechowywane jako `clientid`, `phoneLabel`, i `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="9a7da-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="9a7da-172">Zapytanie Hello oczekuje również toofind HiveCSharp.exe w katalogu głównym hello hello domyślnego kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="9a7da-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="9a7da-173">Kliknij przycisk **przesyłania** klastra usługi HDInsight toohello toosubmit hello zadania.</span><span class="sxs-lookup"><span data-stu-id="9a7da-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="9a7da-174">Witaj **Podsumowanie zadania Hive** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="9a7da-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="9a7da-175">Kliknij przycisk **Odśwież** toorefresh hello podsumowania do **stan zadania** zmiany zbyt**Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="9a7da-176">dane wyjściowe zadania hello tooview, kliknij przycisk **dane wyjściowe zadania**.</span><span class="sxs-lookup"><span data-stu-id="9a7da-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="9a7da-177">Uruchom zadanie Pig</span><span class="sxs-lookup"><span data-stu-id="9a7da-177">Run a Pig job</span></span>

1. <span data-ttu-id="9a7da-178">Użyj jednej z powitania po klastra usługi HDInsight tooyour tooconnect metod:</span><span class="sxs-lookup"><span data-stu-id="9a7da-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="9a7da-179">Jeśli używasz __opartych na systemie Linux__ HDInsight klastra, należy użyć protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="9a7da-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="9a7da-180">Na przykład `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9a7da-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="9a7da-181">Aby uzyskać więcej informacji, zobacz [withHDInsight używanie protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="9a7da-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="9a7da-182">Jeśli używasz __opartych na systemie Windows__ klastra usługi HDInsight [Connect toohello klastra przy użyciu pulpitu zdalnego](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="9a7da-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="9a7da-183">Użyj hello jednym następującego wiersza polecenia Pig hello toostart polecenia:</span><span class="sxs-lookup"><span data-stu-id="9a7da-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="9a7da-184">Jeśli korzystasz z klastra z systemem Windows, należy użyć hello zamiast tego następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="9a7da-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="9a7da-185">A `grunt>` zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="9a7da-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="9a7da-186">Wprowadź następujące toorun zadanie Pig, które korzysta z aplikacji .NET Framework hello hello:</span><span class="sxs-lookup"><span data-stu-id="9a7da-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="9a7da-187">Witaj `DEFINE` instrukcja tworzy alias `streamer` w przypadku aplikacji hello pigudf.exe i `CACHE` ładuje go z domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="9a7da-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="9a7da-188">Później `streamer` jest używany z hello `STREAM` operator tooprocess hello pojedynczych wierszy zawartych w DZIENNIKÓW i danych hello zwracany jako serię kolumn.</span><span class="sxs-lookup"><span data-stu-id="9a7da-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a7da-189">Nazwa aplikacji Hello, który służy do przesyłania strumieniowego musi być ujęte w hello \` (backtick) gdy znak, ponieważ i ' (pojedynczy cudzysłów) w przypadku użycia z `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="9a7da-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="9a7da-190">Po wprowadzeniu hello ostatni wiersz, należy zacząć hello zadania.</span><span class="sxs-lookup"><span data-stu-id="9a7da-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="9a7da-191">Zwraca dane wyjściowe toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="9a7da-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="9a7da-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a7da-192">Next steps</span></span>

<span data-ttu-id="9a7da-193">W tym dokumencie wiesz już, jak toouse aplikacji .NET Framework, Hive i Pig w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a7da-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="9a7da-194">Jeśli chcesz toolearn toouse Python z Hive i Pig, zobacz temat [Użyj Python z Hive i Pig w usłudze HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="9a7da-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="9a7da-195">Inne sposoby toouse Pig i Hive i toolearn o korzystaniu z MapReduce Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="9a7da-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="9a7da-196">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9a7da-197">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9a7da-198">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a7da-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
