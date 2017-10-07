---
title: "aaaUse Hadoop Hive przy użyciu programu PowerShell w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Użyj programu PowerShell zapytań programu Hive toorun w Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>Uruchamianie zapytań Hive przy użyciu programu PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Ten dokument zawiera przykładowy w hello grupy zasobów platformy Azure tryb toorun zapytań programu Hive w Hadoop w klastrze usługi HDInsight przy użyciu programu Azure PowerShell.

> [!NOTE]
> Niniejszy dokument nie daje szczegółowy opis wykonaj instrukcje HiveQL hello, które są używane w przykładach hello. Aby uzyskać informacje na powitania HiveQL, który jest używany w tym przykładzie, zobacz [używanie Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md).

**Wymagania wstępne**

* **Klaster Azure HDInsight**: nie ma znaczenia, czy klaster hello jest systemu Windows lub opartych na systemie Linux.

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* **Stacja robocza z programem Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Uruchamianie zapytań Hive przy użyciu programu Azure PowerShell

Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą tooremotely uruchamiania zapytań Hive w usłudze HDInsight. Wewnętrznie, poleceń cmdlet hello wywołań REST zbyt[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) na powitania klastra usługi HDInsight.

Witaj następujące polecenia cmdlet są używane podczas uruchamiania zapytań Hive w zdalnym klastrze usługi HDInsight:

* **Dodaj-AzureRmAccount**: tooyour uwierzytelnia programu Azure PowerShell subskrypcji platformy Azure
* **Nowy AzureRmHDInsightHiveJobDefinition**: tworzy *definicji zadania* przy użyciu hello określone instrukcje HiveQL
* **Start-AzureRmHDInsightJob**: wysyła tooHDInsight definicji zadania hello, uruchamia zadanie hello i zwraca *zadania* obiektów, które mogą być używane toocheck hello stan zadania hello
* **Czekaj-AzureRmHDInsightJob**: używa stan obiektu zadania hello hello toocheck hello zadania. Oczekuje, aż do ukończenia zadania hello lub przekroczono czas oczekiwania hello.
* **Get-AzureRmHDInsightJobOutput**: używane tooretrieve hello dane wyjściowe zadania hello
* **Wywołanie AzureRmHDInsightHiveJob**: używane toorun instrukcje HiveQL. To polecenie cmdlet bloki hello zapytanie kończy, a następnie zwraca wyniki hello
* **Użyj AzureRmHDInsightCluster**: ustawia hello bieżącego toouse klastra dla hello **Invoke AzureRmHDInsightHiveJob** polecenia

Witaj następująca procedura przedstawia sposób toouse toorun te polecenia cmdlet zadania w klastrze usługi HDInsight:

1. Za pomocą edytora, Zapisz hello następującego kodu jako **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Otwórz nowe **programu Azure PowerShell** wiersza polecenia. Zmień lokalizację toohello katalogów hello **hivejob.ps1** pliku, a następnie użyj następującego skryptu hello toorun polecenia hello:

        .\hivejob.ps1

    Po uruchomieniu skryptu hello jest monitem tooenter hello klastra nazwę i hello HTTPS/poświadczeń konta administratora klastra hello. Mogą być również zostanie wyświetlony monit o toolog w tooyour subskrypcji platformy Azure.

3. Po ukończeniu zadania hello zwraca toohello podobne informacje po thext:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Jak wspomniano wcześniej, **Invoke-Hive** można toorun używane zapytanie i poczekaj, aż hello odpowiedzi. Użyj następującego skryptu toosee działanie Invoke-Hive hello:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    dane wyjściowe Hello wygląda hello następującego tekstu:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Dłużej HiveQL zapytań, można użyć hello Azure PowerShell **ciągów tutaj** polecenia cmdlet lub HiveQL pliki skryptów. powitania po fragment kodu przedstawia sposób toouse hello **Invoke-Hive** toorun polecenia cmdlet skrypt HiveQL. Witaj HiveQL pliku skryptu muszą być przekazywane toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Aby uzyskać więcej informacji na temat **ciągów tutaj**, zobacz <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">przy użyciu systemu Windows PowerShell tutaj — ciągi</a>.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania hello, może mieć wystąpił błąd podczas przetwarzania. informacje o błędzie tooview dla tego zadania, Dodaj hello toohello końca hello **hivejob.ps1** , zapisz go, a następnie uruchomić.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

To polecenie cmdlet zwraca hello informacji zapisywanych tooSTDERR na powitania serwera po uruchomieniu zadania hello.

## <a name="summary"></a>Podsumowanie

Jak widać, Azure PowerShell oferuje łatwe toorun zapytań programu Hive w klastrze usługi HDInsight, monitor hello stan zadania i pobrać dane wyjściowe hello.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)
