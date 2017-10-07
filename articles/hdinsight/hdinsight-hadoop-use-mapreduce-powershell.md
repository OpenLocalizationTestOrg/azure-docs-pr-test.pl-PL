---
title: "aaaUse MapReduce i programu PowerShell z usługą Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse PowerShell tooremotely Uruchom zadań MapReduce z Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu PowerShell

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Ten dokument zawiera przykładowy przy użyciu programu Azure PowerShell toorun zadania MapReduce w usługi Hadoop w klastrze usługi HDInsight.

## <a id="prereq"></a>Wymagania wstępne

* **Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight)**

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* **Stacja robocza z programem Azure PowerShell**.

## <a id="powershell"></a>Uruchomienie zadania MapReduce przy użyciu programu Azure PowerShell

Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą tooremotely uruchomienie zadania MapReduce w usłudze HDInsight. Wewnętrznie, w tym celu za pomocą wywołania REST[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (nazywanych Templeton) systemem hello klastra usługi HDInsight.

Witaj następujące polecenia cmdlet są używane podczas uruchamiania zadań MapReduce w zdalnym klastrze usługi HDInsight.

* **Login-AzureRmAccount**: tooyour uwierzytelnia programu Azure PowerShell subskrypcji platformy Azure.

* **Nowy AzureRmHDInsightMapReduceJobDefinition**: tworzy nowy *definicji zadania* przy użyciu hello określone informacje o MapReduce.

* **Start-AzureRmHDInsightJob**: wysyła tooHDInsight definicji zadania hello, uruchamia zadanie hello i zwraca *zadania* obiektów, które mogą być używane toocheck hello stan zadania hello.

* **Czekaj-AzureRmHDInsightJob**: używa stan obiektu zadania hello hello toocheck hello zadania. Oczekuje, aż do ukończenia zadania hello lub przekroczono czas oczekiwania hello.

* **Get-AzureRmHDInsightJobOutput**: używane dane wyjściowe hello tooretrieve hello zadania.

Witaj następująca procedura przedstawia sposób toouse toorun te polecenia cmdlet zadania w klastrze usługi HDInsight.

1. Za pomocą edytora, Zapisz hello następującego kodu jako **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Otwórz nowe **programu Azure PowerShell** wiersza polecenia. Zmień lokalizację toohello katalogów hello **mapreducejob.ps1** pliku, a następnie użyj następującego skryptu hello toorun polecenia hello:

        .\mapreducejob.ps1

    Po uruchomieniu skryptu hello monit o nazwę hello hello klastra usługi HDInsight i hello HTTPS/Admin konta nazwę i hasło dla klastra hello. Mogą być również zostanie wyświetlony monit o tooauthenticate tooyour subskrypcji platformy Azure.

3. Po zakończeniu zadania hello, pojawi się toohello podobne dane wyjściowe następującego tekstu:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Te dane wyjściowe wskazuje zadania hello ukończona pomyślnie.

    > [!NOTE]
    > Jeśli hello **ExitCode** jest wartością innego niż 0, zobacz [Rozwiązywanie problemów](#troubleshooting).

    W tym przykładzie przechowuje także hello pobrane pliki tooan **output.txt** pliku w katalogu hello Uruchom skrypt hello.

### <a name="view-output"></a>Widok danych wyjściowych

Otwórz hello **output.txt** pliku w hello toosee Edytor tekstu liczby utworzonych przez zadanie hello i wyrazów.

> [!NOTE]
> pliki wyjściowe Hello zadania MapReduce są niezmienne. Jeśli uruchomisz tego przykładu należy więc toochange hello nazwa pliku wyjściowego hello.

## <a id="troubleshooting"></a>Rozwiązywanie problemów

Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania hello, może mieć wystąpił błąd podczas przetwarzania. informacje o błędzie tooview dla tego zadania, Dodaj polecenie toohello końca hello hello **mapreducejob.ps1** , zapisz go, a następnie uruchomić.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

To polecenie cmdlet zwraca informacje hello, które zostało zapisane tooSTDERR na powitania serwera po uruchomieniu zadania hello i może pomóc ustalić, dlaczego zadania hello kończy się niepowodzeniem.

## <a id="summary"></a>Podsumowanie

Jak widać, Azure PowerShell oferuje toorun łatwy sposób na klaster usługi HDInsight, stan zadania hello monitora i pobrać hello w danych wyjściowych zadań MapReduce.

## <a id="nextsteps"></a>Następne kroki

Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:

* [Korzystać z usługi MapReduce na HDInsight Hadoop](hdinsight-use-mapreduce.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
