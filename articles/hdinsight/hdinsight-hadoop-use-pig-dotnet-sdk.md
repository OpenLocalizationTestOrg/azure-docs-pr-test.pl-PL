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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Uruchamianie zadań Pig przy użyciu hello zestawu .NET SDK dla platformy Hadoop w usłudze HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Dowiedz się, jak toouse hello zestawu .NET SDK dla platformy Hadoop toosubmit Apache Pig zadania tooHadoop w usłudze Azure HDInsight.

Witaj zestawu .NET SDK usługi HDInsight udostępnia biblioteki klienta .NET, które umożliwia łatwiejsze toowork z klastrami HDInsight ze środowiska .NET. Pig umożliwia toocreate MapReduce operacji za pomocą modelowania szereg przekształcenia danych. W tym dokumencie możesz dowiedzieć się, jak toosubmit aplikacji toouse podstawowe C# Pig zadania tooan klastra usługi HDInsight.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete hello kroki opisane w tym artykule, należy hello poniżej.

* Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight) (Windows lub opartych na systemie Linux).

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Program Visual Studio 2012, 2013, 2015 lub 2017 r.

## <a name="create-hello-application"></a>Tworzenie aplikacji hello

Hello zestawu .NET SDK HDInsight udostępnia biblioteki klienta .NET, co pozwala na łatwiejsze toowork z klastrami HDInsight ze środowiska .NET.

1. Z hello **pliku** menu w programie Visual Studio, wybierz **nowy** , a następnie wybierz **projektu**.

2. Dla nowego projektu hello wpisz lub wybierz hello następujące wartości:

   | Właściwość | Wartość |
   | ------ | ------ |
   | Kategoria | Szablony/Visual C#/Windows |
   | Szablon | Aplikacja konsolowa |
   | Nazwa | SubmitPigJob |

3. Kliknij przycisk **OK** toocreate hello projektu.

4. Z hello **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** lub **Menedżera pakietów Nuget**, a następnie wybierz **Konsola Menedżera pakietów**.

5. tooinstall hello zestawu .NET SDK pakietów, użyj hello następujące polecenie:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. W Eksploratorze rozwiązań kliknij dwukrotnie **Program.cs** tooopen go. Zastąp istniejący kod hello hello poniżej.

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

7. Aplikacja hello toostart, naciśnij klawisz **F5**.

8. Aplikacja hello tooexit, naciśnij klawisz **ENTER**.

## <a name="summary"></a>Podsumowanie

Jak widać, hello zestawu .NET SDK dla platformy Hadoop umożliwia aplikacje .NET toocreate przesłać klastra usługi HDInsight tooan zadań Pig i monitorować stan zadania hello.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać informacji na temat Pig w usłudze HDInsight, zobacz [Use Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md).

Aby uzyskać więcej informacji na temat używania usługi Hadoop w usłudze HDInsight Zobacz hello w następujących dokumentach:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
