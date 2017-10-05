---
title: "Uruchamianie zapytań Hive przy użyciu zestawu SDK programu .NET HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak umożliwiają przesyłanie zadań Hadoop do usługi Azure HDInsight Hadoop przy użyciu zestawu SDK .NET usługi HDInsight."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 7b1a5f7ea3b2bda438727dc75a85557ea7930280
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="9cc5d-103">Uruchamianie zapytań Hive przy użyciu zestawu .NET SDK usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cc5d-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="9cc5d-104">Dowiedz się, jak wysyłanie zapytań programu Hive za pomocą zestawu SDK .NET usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="9cc5d-105">Napisz program C# do przesyłania zapytań programu Hive, wyświetlania list tabele programu Hive i wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc5d-106">W kliencie systemu Windows należy wykonać czynności opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-106">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="9cc5d-107">Informacji o korzystaniu z systemem Linux, OS X lub klienta systemu Unix do pracy z gałęzi selektor karty wyświetlany w górnej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9cc5d-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cc5d-108">Prerequisites</span></span>
<span data-ttu-id="9cc5d-109">Przed rozpoczęciem tego artykułu, musi mieć następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9cc5d-109">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="9cc5d-110">**Klastra usługi Hadoop w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="9cc5d-111">Zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9cc5d-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="9cc5d-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="9cc5d-113">Wysyłanie zapytań programu Hive za pomocą zestawu SDK .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cc5d-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="9cc5d-114">Zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co ułatwia do pracy z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-114">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="9cc5d-115">**Do przesyłania zadań**</span><span class="sxs-lookup"><span data-stu-id="9cc5d-115">**To Submit jobs**</span></span>

1. <span data-ttu-id="9cc5d-116">Tworzenie aplikacji konsolowej C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="9cc5d-117">Za pomocą konsoli Menedżera pakietów Nuget uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9cc5d-117">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="9cc5d-118">Użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="9cc5d-118">Use the following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the Hive job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="9cc5d-119">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-119">Press **F5** to run the application.</span></span>

<span data-ttu-id="9cc5d-120">Dane wyjściowe aplikacji jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="9cc5d-120">The output of the application shall be similar to:</span></span>

![Dane wyjściowe zadania HDInsight Hadoop Hive](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="9cc5d-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cc5d-122">Next steps</span></span>
<span data-ttu-id="9cc5d-123">W tym artykule uzyskanych kilka sposobów tworzenia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9cc5d-123">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="9cc5d-124">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="9cc5d-124">To learn more, see the following articles:</span></span>

* <span data-ttu-id="9cc5d-125">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9cc5d-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="9cc5d-126">[Tworzenie klastrów Hadoop w usłudze HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="9cc5d-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="9cc5d-127">Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9cc5d-127">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="9cc5d-128">Odwołanie do zestawu SDK .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cc5d-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="9cc5d-129">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cc5d-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9cc5d-130">Korzystanie z usługą HDInsight Sqoop</span><span class="sxs-lookup"><span data-stu-id="9cc5d-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="9cc5d-131">Tworzenie aplikacji usługi HDInsight platformy .NET z uwierzytelnianiem nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="9cc5d-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


