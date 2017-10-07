---
title: "przy użyciu zestawu SDK programu .NET HDInsight - Azure zadań MapReduce aaaSubmit | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosubmit MapReduce zadania tooAzure HDInsight Hadoop przy użyciu zestawu SDK .NET usługi HDInsight."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="1a59f-103">Uruchamianie zadań MapReduce przy użyciu zestawu SDK .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a59f-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="1a59f-104">Dowiedz się, jak toosubmit MapReduce zadania przy użyciu zestawu SDK .NET usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a59f-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="1a59f-105">HDInsight klastrów pochodzą z pliku jar z niektóre przykłady MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1a59f-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="1a59f-106">Plik jar Hello jest */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="1a59f-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="1a59f-107">Jednym z przykładów hello jest *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="1a59f-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="1a59f-108">Opracowywania C# console application toosubmit zadania wordcount.</span><span class="sxs-lookup"><span data-stu-id="1a59f-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="1a59f-109">zadanie Hello odczytuje hello */example/data/gutenberg/davinci.txt* plików i danych wyjściowych hello wyniki za*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="1a59f-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="1a59f-110">Jeśli chcesz, aby aplikacja hello toorerun, musi wyczyścić hello folder wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="1a59f-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="1a59f-111">Witaj czynności w tym artykule należy wykonać w kliencie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1a59f-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="1a59f-112">Dla informacji o korzystaniu z Hive Linux, OS X lub toowork klienta systemu Unix selektor hello kartę wyświetlany u góry hello hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="1a59f-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1a59f-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a59f-113">Prerequisites</span></span>
<span data-ttu-id="1a59f-114">Przed rozpoczęciem tego artykułu, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1a59f-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="1a59f-115">**Klastra usługi Hadoop w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1a59f-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="1a59f-116">Zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1a59f-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="1a59f-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="1a59f-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="1a59f-118">Przesyłanie zadań MapReduce przy użyciu zestawu SDK .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a59f-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="1a59f-119">Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="1a59f-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="1a59f-120">**zadania tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="1a59f-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="1a59f-121">Tworzenie aplikacji konsolowej C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a59f-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="1a59f-122">Z hello Konsola Menedżera pakietów Nuget uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1a59f-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="1a59f-123">Użyj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="1a59f-123">Use hello following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="1a59f-124">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a59f-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="1a59f-125">zadanie hello toorun ponownie, należy zmienić hello zadania dane wyjściowe nazwę folderu, w przykładowym hello, jest "/ przykład/data/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="1a59f-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="1a59f-126">Po pomyślnym zakończeniu zadania hello aplikacji hello drukuje hello zawartość pliku wyjściowego hello "części r-00000".</span><span class="sxs-lookup"><span data-stu-id="1a59f-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a59f-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1a59f-127">Next steps</span></span>
<span data-ttu-id="1a59f-128">W tym artykule uzyskanych kilka sposobów toocreate klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a59f-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="1a59f-129">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="1a59f-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="1a59f-130">Do przesyłania zadań Hive, zobacz [uruchamianie zapytań Hive przy użyciu zestawu SDK .NET usługi HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1a59f-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="1a59f-131">Do tworzenia klastrów usługi HDInsight, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1a59f-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="1a59f-132">Zarządzanie klastrami usługi HDInsight, zobacz [klastrów zarządzania Hadoop w HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1a59f-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="1a59f-133">Do uczenia hello zestawu .NET SDK usługi HDInsight, zobacz [odwołania do zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a59f-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="1a59f-134">Dla podejścia nieinterakcyjnego tooAzure uwierzytelniania, zobacz [tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinteraktywne](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="1a59f-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

