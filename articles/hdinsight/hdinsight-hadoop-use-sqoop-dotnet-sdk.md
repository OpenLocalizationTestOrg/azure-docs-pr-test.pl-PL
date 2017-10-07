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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Uruchamianie zadań Sqoop przy użyciu zestawu .NET SDK dla platformy Hadoop w usłudze HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Dowiedz się, jak toouse zestawu .NET SDK HDInsight toorun Sqoop zadania w usłudze HDInsight tooimport i eksportowanie między klastrem usługi HDInsight i bazy danych Azure SQL lub bazy danych SQL Server.

> [!NOTE]
> Witaj opisanych w tym artykule może służyć z obu komputerów z systemem Windows lub opartych na systemie Linux klastrem usługi HDInsight; Jednak te kroki działa tylko w kliencie systemu Windows. Selektor hello kartę na powitania górnej części tego artykułu toochoose innych metod.
> 
> 

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:

* **Klastra usługi Hadoop w usłudze HDInsight**. Zobacz [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Użyj Sqoop w klastrach HDInsight przy użyciu zestawu .NET SDK
Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET. W tej sekcji utworzysz C# console aplikacji tooexport hello hivesampletable toohello bazy danych SQL tabelę utworzonego wcześniej w tym samouczku.

## <a name="submit-a-sqoop-job"></a>Prześlij zadanie Sqoop

1. Tworzenie aplikacji konsolowej C# w programie Visual Studio.
2. Z hello Konsola Menedżera pakietów programu Visual Studio Uruchom hello następującego pakietu hello tooimport polecenia Nuget.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Użyj następującego kodu w pliku Program.cs hello hello:
   
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
4. Naciśnij klawisz **F5** toorun hello program. 

## <a name="limitations"></a>Ograniczenia
* Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.
* Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop wykonuje wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.

## <a name="next-steps"></a>Następne kroki
Teraz wiesz już, jak toouse Sqoop. toolearn więcej, zobacz:

* [Korzystanie z usługą HDInsight Oozie](hdinsight-use-oozie.md): Użyj Sqoop działań w przepływie pracy Oozie.
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight](hdinsight-analyze-flight-delay-data.md): Użyj Hive transmitowane tooanalyze opóźnienie danych, a następnie użyj bazy danych Azure SQL tooan Sqoop tooexport danych.
* [Przekazywanie danych tooHDInsight](hdinsight-upload-data.md): znajdowanie innych metod do przekazywania danych tooHDInsight/usługi Azure Blob storage.

