---
title: "klastry aaaManage Hadoop w usłudze HDInsight przy użyciu programu PowerShell - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform administracyjne zadań hello klastrów platformy Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Program Azure PowerShell jest zaawansowane środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania obciążeń na platformie Azure. W tym artykule dowiesz się, jak używać toomanage klastrów platformy Hadoop w usłudze Azure HDInsight przy użyciu konsoli programu Azure PowerShell do lokalnej za pośrednictwem hello programu Windows PowerShell. Lista hello hello poleceń cmdlet programu PowerShell w usłudze HDInsight, zobacz [dokumentacji poleceń cmdlet usługi HDInsight][hdinsight-powershell-reference].

**Wymagania wstępne**

Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Instalowanie programu Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Jeśli zainstalowano program Azure PowerShell w wersji 0,9 x, należy go odinstalować przed zainstalowaniem nowszej wersji.

Wersja hello toocheck hello zainstalowane środowiska PowerShell:

    Get-Module *azure*

toouninstall hello starszą wersję, uruchom programy i funkcje w Panelu sterowania hello.

## <a name="create-clusters"></a>Tworzenie klastrów
Zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu programu Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Lista klastrów
W bieżącej subskrypcji hello, należy użyć następującego polecenia toolist hello wszystkich klastrów:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Pokaż klastra
Użyj hello poniższe polecenie tooshow informacje określonego klastra w bieżącej subskrypcji hello:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Usuwanie klastrów
Użyj hello następujące polecenia toodelete klastra:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

Można również usunąć klaster przez usunięcie hello grupę zasobów, która zawiera hello klastra. Należy pamiętać, spowoduje to usunięcie wszystkich zasobów hello w grupie hello w tym hello domyślne konto magazynu.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Skalowanie klastrów
Skalowanie funkcji klastra Hello umożliwia toochange hello liczba węzłów procesu roboczego, używane przez klaster działa w usłudze Azure HDInsight bez konieczności toore — Tworzenie klastra hello.

> [!NOTE]
> Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane. Jeśli masz pewności, jaka wersja hello klastra, można sprawdzić hello stronę właściwości.  Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

wpływ Hello Zmienianie hello liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:

* Usługa Hadoop

    Można zwiększyć bezproblemowo hello liczba węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania. W trakcie operacji hello również można przesłać nowe zadania. Błędy w operacji skalowania bezpiecznie obsługi tak, aby hello klastra zawsze pozostanie w stanie funkcjonalności.

    Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby hello węzły danych są ponownie uruchamiane niektórych usług hello hello klastra. Powoduje to wszystkich uruchomionych i oczekujących zadań toofail na zakończenie hello hello operacji skalowania. Można jednak Prześlij ponownie hello zadania po zakończeniu operacji hello.
* HBase

    Można bezproblemowo dodać lub usunąć klaster HBase tooyour węzłów, jest uruchomiona. Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia hello operacji skalowania. Można jednak również ręcznie saldo serwerów regionalnych hello po zalogowaniu się headnode toohello klastra i uruchomione hello poniższych poleceń z poziomu okna wiersza polecenia:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Można bezproblemowo dodać lub usunąć klaster Storm tooyour węzłów danych jest uruchomiona. Jednak po pomyślnym zakończeniu hello operacji skalowania, konieczne będzie toorebalance hello topologii.

    Ponowne równoważenie można zrobić na dwa sposoby:

  * STORM interfejsu użytkownika sieci web
  * Narzędzia interfejsu wiersza polecenia (CLI)

    Zobacz toohello [dokumentację Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) więcej szczegółów.

    Witaj interfejsu użytkownika sieci web platformy Storm w klastrze jest dostępny hello HDInsight:

    ![Zrównoważ skali storm w usłudze HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Poniżej przedstawiono przykładowy sposób hello toouse interfejsu wiersza polecenia polecenie topologii Storm hello toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Witaj toochange rozmiar klastra usługi Hadoop przy użyciu programu Azure PowerShell, uruchom następujące polecenie na komputerze klienckim hello:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Dostęp do przydzielenia/odwołania
Klastry HDInsight są powitania po HTTP usługi sieci web (wszystkie te usługi mają RESTful punkty końcowe):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Domyślnie te usługi są przyznawane dostępu. Możesz można odwołać/Udziel dostępu hello. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Przez przyznawanie/odwoływanie dostępu hello, spowoduje zresetowanie hello klastra nazwę i hasło użytkownika.
>
>

Ponadto można to zrobić za pomocą hello portalu. Zobacz [administrowania HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Zaktualizuj poświadczenia użytkownika HTTP
To samo hello procedury jako [dostępu Grant/revoke HTTP](#grant/revoke-access). Jeśli klaster hello przyznano hello dostęp HTTP, należy je najpierw odwołać.  A następnie przyznać dostęp hello z nowymi poświadczeniami użytkownika HTTP.

## <a name="find-hello-default-storage-account"></a>Znajdź hello domyślne konto magazynu
Witaj następującego skryptu programu Powershell pokazano, jak tooget hello domyślna nazwa konta magazynu i hello domyślny klucz konta magazynu dla klastra.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Znajdź hello grupy zasobów
W trybie Menedżera zasobów hello każdego klastra usługi HDInsight należy tooan grupy zasobów platformy Azure.  Grupa zasobów hello toofind:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Przesyłanie zadań
**zadania MapReduce toosubmit**

Zobacz [próbek Uruchom MapReduce z Hadoop w HDInsight opartych na systemie Windows](hdinsight-run-samples.md).

**toosubmit zadań Hive**

Zobacz [uruchamianie zapytań Hive przy użyciu programu PowerShell](hdinsight-hadoop-use-hive-powershell.md).

**toosubmit zadań Pig**

Zobacz [Pig uruchomienie zadania przy użyciu programu PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**toosubmit Sqoop zadania**

Zobacz [Sqoop za pomocą usługi HDInsight](hdinsight-use-sqoop.md).

**toosubmit Oozie zadania**

Zobacz [Oozie Użyj Hadoop toodefine i Uruchom przepływ pracy w usłudze HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Przekazywanie danych tooAzure obiektu Blob magazynu
Zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Zobacz też
* [Dokumentację referencyjną polecenia cmdlet usługi HDInsight][hdinsight-powershell-reference]
* [Administrowanie HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]
* [Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]
* [Tworzenie klastrów usługi HDInsight][hdinsight-provision]
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Przesyłanie zadań Hadoop programowo][hdinsight-submit-jobs]
* [Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
