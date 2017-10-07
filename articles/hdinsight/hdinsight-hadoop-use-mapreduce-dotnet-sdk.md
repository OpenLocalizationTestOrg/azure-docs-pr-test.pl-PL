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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Uruchamianie zadań MapReduce przy użyciu zestawu SDK .NET usługi HDInsight
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Dowiedz się, jak toosubmit MapReduce zadania przy użyciu zestawu SDK .NET usługi HDInsight. HDInsight klastrów pochodzą z pliku jar z niektóre przykłady MapReduce. Plik jar Hello jest */example/jars/hadoop-mapreduce-examples.jar*.  Jednym z przykładów hello jest *wordcount*. Opracowywania C# console application toosubmit zadania wordcount.  zadanie Hello odczytuje hello */example/data/gutenberg/davinci.txt* plików i danych wyjściowych hello wyniki za*/example/data/davinciwordcount*.  Jeśli chcesz, aby aplikacja hello toorerun, musi wyczyścić hello folder wyjściowy.

> [!NOTE]
> Witaj czynności w tym artykule należy wykonać w kliencie systemu Windows. Dla informacji o korzystaniu z Hive Linux, OS X lub toowork klienta systemu Unix selektor hello kartę wyświetlany u góry hello hello artykułu.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć hello następujące elementy:

* **Klastra usługi Hadoop w usłudze HDInsight**. Zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Przesyłanie zadań MapReduce przy użyciu zestawu SDK .NET usługi HDInsight
Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET. 

**zadania tooSubmit**

1. Tworzenie aplikacji konsolowej C# w programie Visual Studio.
2. Z hello Konsola Menedżera pakietów Nuget uruchom następujące polecenie hello:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Użyj hello następującego kodu:
   
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
4. Naciśnij klawisz **F5** toorun hello aplikacji.

zadanie hello toorun ponownie, należy zmienić hello zadania dane wyjściowe nazwę folderu, w przykładowym hello, jest "/ przykład/data/davinciwordcount".

Po pomyślnym zakończeniu zadania hello aplikacji hello drukuje hello zawartość pliku wyjściowego hello "części r-00000".

## <a name="next-steps"></a>Następne kroki
W tym artykule uzyskanych kilka sposobów toocreate klastra usługi HDInsight. toolearn więcej, zobacz następujące artykuły hello:

* Do przesyłania zadań Hive, zobacz [uruchamianie zapytań Hive przy użyciu zestawu SDK .NET usługi HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Do tworzenia klastrów usługi HDInsight, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Zarządzanie klastrami usługi HDInsight, zobacz [klastrów zarządzania Hadoop w HDInsight](hdinsight-administer-use-portal-linux.md).
* Do uczenia hello zestawu .NET SDK usługi HDInsight, zobacz [odwołania do zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).
* Dla podejścia nieinterakcyjnego tooAzure uwierzytelniania, zobacz [tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinteraktywne](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

