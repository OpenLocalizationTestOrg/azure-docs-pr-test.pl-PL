---
title: "aaaRun zapytań Hive przy użyciu zestawu SDK programu .NET HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosubmit Hadoop zadania tooAzure HDInsight Hadoop przy użyciu zestawu SDK .NET usługi HDInsight."
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
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Uruchamianie zapytań Hive przy użyciu zestawu .NET SDK usługi HDInsight
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Dowiedz się, jak toosubmit Hive zapytań przy użyciu zestawu SDK .NET usługi HDInsight. Napisz zapytanie Hive wyświetlania list tabele programu Hive toosubmit program C# i wyświetlić wyniki hello.

> [!NOTE]
> Witaj czynności w tym artykule należy wykonać w kliencie systemu Windows. Dla informacji o korzystaniu z Hive Linux, OS X lub toowork klienta systemu Unix selektor hello kartę wyświetlany u góry hello hello artykułu.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć hello następujące elementy:

* **Klastra usługi Hadoop w usłudze HDInsight**. Zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Wysyłanie zapytań programu Hive za pomocą zestawu SDK .NET usługi HDInsight
Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET. 

**zadania tooSubmit**

1. Tworzenie aplikacji konsolowej C# w programie Visual Studio.
2. Z hello Konsola Menedżera pakietów Nuget uruchom następujące polecenie hello:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Użyj hello następującego kodu:

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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
4. Naciśnij klawisz **F5** toorun hello aplikacji.

dane wyjściowe aplikacji hello Hello są podobne do:

![Dane wyjściowe zadania HDInsight Hadoop Hive](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Następne kroki
W tym artykule uzyskanych kilka sposobów toocreate klastra usługi HDInsight. toolearn więcej, zobacz następujące artykuły hello:

* [Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]
* [Tworzenie klastrów Hadoop w usłudze HDInsight][hdinsight-provision]
* [Zarządzanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-management-portal.md)
* [Odwołanie do zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystanie z usługą HDInsight Sqoop](hdinsight-use-sqoop-mac-linux.md)
* [Tworzenie aplikacji usługi HDInsight platformy .NET z uwierzytelnianiem nieinterakcyjnym](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


