---
title: "aaaUse Hadoop Pig przy użyciu programu PowerShell w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastra tooa zadań Pig toosubmit Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Korzystanie z zadań Pig toorun programu Azure PowerShell z usługą HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Ten dokument zawiera przykładowy w klastrze usługi HDInsight przy użyciu programu Azure PowerShell toosubmit Pig zadania tooa Hadoop. Pig umożliwia zadań MapReduce toowrite przy użyciu modeli przekształcenia danych języka (Pig Latin), a nie mapy i zmniejszyć funkcji.

> [!NOTE]
> Niniejszy dokument nie daje szczegółowy opis wykonaj instrukcje Pig Latin hello używany w przykładach hello. Informacje o hello Pig Latin używana w tym przykładzie, zobacz [Use Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Wymagania wstępne

* **Klaster Azure HDInsight**

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* **Stacja robocza z programem Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Uruchamianie zadań Pig przy użyciu programu PowerShell

Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą tooremotely uruchamiania zadań Pig w usłudze HDInsight. Wewnętrznie, programu PowerShell używa wywołania REST zbyt[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) uruchomiona w klastrze HDInsight hello.

Witaj następujące polecenia cmdlet są używane podczas uruchamiania zadań Pig w zdalnym klastrze usługi HDInsight:

* **Login-AzureRmAccount**: tooyour uwierzytelnia programu Azure PowerShell subskrypcji platformy Azure
* **Nowy AzureRmHDInsightPigJobDefinition**: tworzy *definicji zadania* przy użyciu hello określony Pig Latin — instrukcje
* **Start-AzureRmHDInsightJob**: wysyła tooHDInsight definicji zadania hello, uruchamia zadanie hello i zwraca *zadania* obiektów, które mogą być używane toocheck hello stan zadania hello
* **Czekaj-AzureRmHDInsightJob**: używa stan obiektu zadania hello hello toocheck hello zadania. Go oczekuje, aż hello zadanie zostało zakończone, lub hello czas oczekiwania został przekroczony.
* **Get-AzureRmHDInsightJobOutput**: używane tooretrieve hello dane wyjściowe zadania hello

Witaj następująca procedura przedstawia sposób toouse toorun te polecenia cmdlet zadania w klastrze usługi HDInsight.

1. Za pomocą edytora, Zapisz hello następującego kodu jako **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Otwórz wiersz polecenia programu Windows PowerShell. Zmień lokalizację toohello katalogów hello **pigjob.ps1** pliku, a następnie użyj następującego skryptu hello toorun polecenia hello:

        .\pigjob.ps1

    Jesteś zostanie wyświetlony monit o toolog w tooyour subskrypcji platformy Azure. Następnie zostanie wyświetlona prośba o hello HTTPs/Admin konta nazwy i hasła dla klastra usługi HDInsight hello.

2. Po zakończeniu zadania hello, powinien on zwrócić informacje toohello podobne następującego tekstu:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Rozwiązywanie problemów

Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania hello, może mieć wystąpił błąd podczas przetwarzania. informacje o błędzie tooview dla tego zadania, Dodaj polecenie toohello końca hello hello **pigjob.ps1** , zapisz go, a następnie uruchomić.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

To polecenie zwróci hello informacje, które zostało zapisane tooSTDERR na powitania serwera po uruchomieniu zadania hello, a może pomóc ustalić, dlaczego zadania hello kończy się niepowodzeniem.

## <a id="summary"></a>Podsumowanie
Jak widać, Azure PowerShell oferuje toorun łatwy sposób na klaster usługi HDInsight, stan zadania hello monitora i pobrać hello w danych wyjściowych zadań Pig.

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)
