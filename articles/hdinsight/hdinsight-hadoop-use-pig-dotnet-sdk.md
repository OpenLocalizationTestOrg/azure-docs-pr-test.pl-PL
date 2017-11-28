---
title: "Apache Pig aaaRun zadania przy użyciu zestawu .NET SDK dla platformy Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello zestawu .NET SDK dla platformy Hadoop toosubmit Pig zadania tooHadoop w usłudze HDInsight."
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
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="16c8c-103">Uruchamianie zadań Pig przy użyciu hello zestawu .NET SDK dla platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c8c-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="16c8c-104">Dowiedz się, jak toouse hello zestawu .NET SDK dla platformy Hadoop toosubmit Apache Pig zadania tooHadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c8c-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="16c8c-105">Witaj zestawu .NET SDK usługi HDInsight udostępnia biblioteki klienta .NET, które umożliwia łatwiejsze toowork z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="16c8c-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="16c8c-106">Pig umożliwia toocreate MapReduce operacji za pomocą modelowania szereg przekształcenia danych.</span><span class="sxs-lookup"><span data-stu-id="16c8c-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="16c8c-107">W tym dokumencie możesz dowiedzieć się, jak toosubmit aplikacji toouse podstawowe C# Pig zadania tooan klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c8c-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16c8c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16c8c-108">Prerequisites</span></span>

<span data-ttu-id="16c8c-109">toocomplete hello kroki opisane w tym artykule, należy hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="16c8c-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="16c8c-110">Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight) (Windows lub opartych na systemie Linux).</span><span class="sxs-lookup"><span data-stu-id="16c8c-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="16c8c-111">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="16c8c-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="16c8c-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="16c8c-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="16c8c-113">Program Visual Studio 2012, 2013, 2015 lub 2017 r.</span><span class="sxs-lookup"><span data-stu-id="16c8c-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="16c8c-114">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="16c8c-114">Create hello application</span></span>

<span data-ttu-id="16c8c-115">Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET.</span><span class="sxs-lookup"><span data-stu-id="16c8c-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="16c8c-116">Z hello **pliku** menu w programie Visual Studio, wybierz **nowy** , a następnie wybierz **projektu**.</span><span class="sxs-lookup"><span data-stu-id="16c8c-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="16c8c-117">Dla nowego projektu hello wpisz lub wybierz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="16c8c-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="16c8c-118">Właściwość</span><span class="sxs-lookup"><span data-stu-id="16c8c-118">Property</span></span> | <span data-ttu-id="16c8c-119">Wartość</span><span class="sxs-lookup"><span data-stu-id="16c8c-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="16c8c-120">Kategoria</span><span class="sxs-lookup"><span data-stu-id="16c8c-120">Category</span></span> | <span data-ttu-id="16c8c-121">Szablony/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="16c8c-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="16c8c-122">Szablon</span><span class="sxs-lookup"><span data-stu-id="16c8c-122">Template</span></span> | <span data-ttu-id="16c8c-123">Aplikacja konsolowa</span><span class="sxs-lookup"><span data-stu-id="16c8c-123">Console Application</span></span> |
   | <span data-ttu-id="16c8c-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="16c8c-124">Name</span></span> | <span data-ttu-id="16c8c-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="16c8c-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="16c8c-126">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="16c8c-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="16c8c-127">Z hello **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** lub **Menedżera pakietów Nuget**, a następnie wybierz **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="16c8c-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="16c8c-128">tooinstall hello zestawu .NET SDK pakietów, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="16c8c-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="16c8c-129">W Eksploratorze rozwiązań kliknij dwukrotnie **Program.cs** tooopen go.</span><span class="sxs-lookup"><span data-stu-id="16c8c-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="16c8c-130">Zastąp istniejący kod hello hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="16c8c-130">Replace hello existing code with hello following.</span></span>

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
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
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

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="16c8c-131">Aplikacja hello toostart, naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="16c8c-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="16c8c-132">Aplikacja hello tooexit, naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="16c8c-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="16c8c-133">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="16c8c-133">Summary</span></span>

<span data-ttu-id="16c8c-134">Jak widać, hello zestawu .NET SDK dla platformy Hadoop umożliwia aplikacje .NET toocreate przesłać klastra usługi HDInsight tooan zadań Pig i monitorować stan zadania hello.</span><span class="sxs-lookup"><span data-stu-id="16c8c-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c8c-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16c8c-135">Next steps</span></span>

<span data-ttu-id="16c8c-136">Aby uzyskać informacji na temat Pig w usłudze HDInsight, zobacz [Use Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="16c8c-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="16c8c-137">Aby uzyskać więcej informacji na temat używania usługi Hadoop w usłudze HDInsight Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="16c8c-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="16c8c-138">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c8c-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="16c8c-139">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c8c-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
