---
title: "aaaRun Sqoop zadania przy użyciu platformy .NET i HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zestawu .NET SDK HDInsight toorun Sqoop importowania i eksportowania między klastrem Hadoop i bazy danych Azure SQL."
keywords: zadanie sqoop
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="6b7da-104">Uruchamianie zadań Sqoop przy użyciu zestawu .NET SDK dla platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b7da-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="6b7da-105">Dowiedz się, jak toouse zestawu .NET SDK HDInsight toorun Sqoop zadania w usłudze HDInsight tooimport i eksportowanie między klastrem usługi HDInsight i bazy danych Azure SQL lub bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b7da-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="6b7da-106">Witaj opisanych w tym artykule może służyć z obu komputerów z systemem Windows lub opartych na systemie Linux klastrem usługi HDInsight; Jednak te kroki działa tylko w kliencie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6b7da-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="6b7da-107">Selektor hello kartę na powitania górnej części tego artykułu toochoose innych metod.</span><span class="sxs-lookup"><span data-stu-id="6b7da-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="6b7da-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6b7da-108">Prerequisites</span></span>
<span data-ttu-id="6b7da-109">Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6b7da-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="6b7da-110">**Klastra usługi Hadoop w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6b7da-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="6b7da-111">Zobacz [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="6b7da-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="6b7da-112">Użyj Sqoop w klastrach HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6b7da-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="6b7da-113">Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="6b7da-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="6b7da-114">W tej sekcji utworzysz C# console aplikacji tooexport hello hivesampletable toohello bazy danych SQL tabelę utworzonego wcześniej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6b7da-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="6b7da-115">Prześlij zadanie Sqoop</span><span class="sxs-lookup"><span data-stu-id="6b7da-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="6b7da-116">Tworzenie aplikacji konsolowej C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b7da-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="6b7da-117">Z hello Konsola Menedżera pakietów programu Visual Studio Uruchom hello następującego pakietu hello tooimport polecenia Nuget.</span><span class="sxs-lookup"><span data-stu-id="6b7da-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="6b7da-118">Użyj następującego kodu w pliku Program.cs hello hello:</span><span class="sxs-lookup"><span data-stu-id="6b7da-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
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
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="6b7da-119">Naciśnij klawisz **F5** toorun hello program.</span><span class="sxs-lookup"><span data-stu-id="6b7da-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="6b7da-120">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="6b7da-120">Limitations</span></span>
* <span data-ttu-id="6b7da-121">Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="6b7da-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="6b7da-122">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop wykonuje wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="6b7da-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b7da-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b7da-123">Next steps</span></span>
<span data-ttu-id="6b7da-124">Teraz wiesz już, jak toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="6b7da-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="6b7da-125">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="6b7da-125">toolearn more, see:</span></span>

* <span data-ttu-id="6b7da-126">[Korzystanie z usługą HDInsight Oozie](hdinsight-use-oozie.md): Użyj Sqoop działań w przepływie pracy Oozie.</span><span class="sxs-lookup"><span data-stu-id="6b7da-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="6b7da-127">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight](hdinsight-analyze-flight-delay-data.md): Użyj Hive transmitowane tooanalyze opóźnienie danych, a następnie użyj bazy danych Azure SQL tooan Sqoop tooexport danych.</span><span class="sxs-lookup"><span data-stu-id="6b7da-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="6b7da-128">[Przekazywanie danych tooHDInsight](hdinsight-upload-data.md): znajdowanie innych metod do przekazywania danych tooHDInsight/usługi Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="6b7da-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

