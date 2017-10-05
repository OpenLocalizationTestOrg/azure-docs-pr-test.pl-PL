---
title: "Uruchamianie zadań Apache Pig przy użyciu zestawu .NET SDK dla platformy Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać zestawu .NET SDK dla platformy Hadoop do przesyłania zadań Pig do platformy Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="19bff-103">Uruchamianie zadań Pig przy użyciu zestawu .NET SDK dla platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="19bff-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="19bff-104">Dowiedz się, jak używać zestawu .NET SDK dla platformy Hadoop do przesyłania zadań Apache Pig do platformy Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19bff-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="19bff-105">Zestaw .NET SDK usługi HDInsight zapewnia bibliotek klienta .NET, które ułatwia pracy z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="19bff-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="19bff-106">Pig służy do tworzenia MapReduce operacji za pomocą modelowania szereg przekształcenia danych.</span><span class="sxs-lookup"><span data-stu-id="19bff-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="19bff-107">W tym dokumencie Dowiedz się jak używać podstawowej aplikacji C# można przesłać zadania programu Pig do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19bff-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19bff-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19bff-108">Prerequisites</span></span>

<span data-ttu-id="19bff-109">Aby wykonać kroki opisane w tym artykule, są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="19bff-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="19bff-110">Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight) (Windows lub opartych na systemie Linux).</span><span class="sxs-lookup"><span data-stu-id="19bff-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="19bff-111">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="19bff-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19bff-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="19bff-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="19bff-113">Program Visual Studio 2012, 2013, 2015 lub 2017 r.</span><span class="sxs-lookup"><span data-stu-id="19bff-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="19bff-114">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="19bff-114">Create the application</span></span>

<span data-ttu-id="19bff-115">Zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co ułatwia do pracy z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="19bff-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="19bff-116">Z **pliku** menu w programie Visual Studio, wybierz **nowy** , a następnie wybierz **projektu**.</span><span class="sxs-lookup"><span data-stu-id="19bff-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="19bff-117">Dla nowego projektu wpisz lub wybierz następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="19bff-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="19bff-118">Właściwość</span><span class="sxs-lookup"><span data-stu-id="19bff-118">Property</span></span> | <span data-ttu-id="19bff-119">Wartość</span><span class="sxs-lookup"><span data-stu-id="19bff-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="19bff-120">Kategoria</span><span class="sxs-lookup"><span data-stu-id="19bff-120">Category</span></span> | <span data-ttu-id="19bff-121">Szablony/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="19bff-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="19bff-122">Szablon</span><span class="sxs-lookup"><span data-stu-id="19bff-122">Template</span></span> | <span data-ttu-id="19bff-123">Aplikacja konsolowa</span><span class="sxs-lookup"><span data-stu-id="19bff-123">Console Application</span></span> |
   | <span data-ttu-id="19bff-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19bff-124">Name</span></span> | <span data-ttu-id="19bff-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="19bff-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="19bff-126">Kliknij przycisk **OK**, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="19bff-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="19bff-127">Z **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** lub **Menedżera pakietów Nuget**, a następnie wybierz **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="19bff-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="19bff-128">Aby zainstalować pakiety zestawu .NET SDK, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="19bff-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="19bff-129">W Eksploratorze rozwiązań kliknij dwukrotnie **Program.cs** go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="19bff-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="19bff-130">Zamień istniejący kod poniżej.</span><span class="sxs-lookup"><span data-stu-id="19bff-130">Replace the existing code with the following.</span></span>

    ```csharp
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
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="19bff-131">Aby uruchomić aplikację, naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="19bff-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="19bff-132">Aby zakończyć aplikację, naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="19bff-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="19bff-133">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="19bff-133">Summary</span></span>

<span data-ttu-id="19bff-134">Jak widać, zestawu .NET SDK dla platformy Hadoop umożliwia tworzenie aplikacji platformy .NET, które przesyłania zadań Pig do klastra usługi HDInsight i monitorowanie stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="19bff-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19bff-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19bff-135">Next steps</span></span>

<span data-ttu-id="19bff-136">Aby uzyskać informacji na temat Pig w usłudze HDInsight, zobacz [Use Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="19bff-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="19bff-137">Aby uzyskać więcej informacji na temat używania usługi Hadoop w usłudze HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="19bff-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="19bff-138">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="19bff-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="19bff-139">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="19bff-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
