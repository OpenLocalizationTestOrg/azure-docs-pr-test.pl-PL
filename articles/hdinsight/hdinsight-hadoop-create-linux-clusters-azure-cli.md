---
title: "klastry Hadoop aaaCreate przy użyciu wiersza polecenia - hello Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate klastrów usługi HDInsight przy użyciu hello 1.0 interfejsu wiersza polecenia platformy Azure i platform."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Tworzenie klastrów usługi HDInsight przy użyciu hello wiersza polecenia platformy Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Witaj czynnościach w ramach tego przewodnika dokumentu tworzenia klastra usługi HDInsight 3.5 przy użyciu hello Azure CLI w wersji 1.0.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).


## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Subskrypcja platformy Azure**. Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Interfejs wiersza polecenia platformy Azure**. z wiersza polecenia platformy Azure w wersji 0.10.14 ostatnio przetestowane Hello kroków w tym dokumencie.

    > [!IMPORTANT]
    > kroki Hello w tym dokumencie nie współpracujesz z 2.0 interfejsu wiersza polecenia platformy Azure. Azure CLI 2.0 nie obsługuje tworzenia klastra usługi HDInsight.

## <a name="log-in-tooyour-azure-subscription"></a>Zaloguj się za tooyour subskrypcji platformy Azure

Wykonaj kroki hello udokumentowane w [połączyć tooan subskrypcji platformy Azure z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)](../xplat-cli-connect.md) i nawiąż połączenie przy użyciu hello subskrypcji tooyour **logowania** — metoda.

## <a name="create-a-cluster"></a>Tworzenie klastra

Witaj, wykonaj czynności należy wykonać z poziomu wiersza polecenia, takich jak programu PowerShell lub Bash.

1. Witaj Użyj następującego polecenia tooauthenticate tooyour subskrypcji platformy Azure:

        azure login

    Możesz się zostanie wyświetlony monit o tooprovide swoją nazwę i hasło. Jeśli masz wiele subskrypcji Azure, użyj `azure account set <subscriptionname>` użyj polecenia tooset hello subskrypcji, która hello wiersza polecenia platformy Azure.

2. Przełącz tryb usługi Resource Manager tooAzure przy użyciu hello następujące polecenie:

        azure config mode arm

3. Utwórz grupę zasobów. Ta grupa zasobów zawiera hello klastra usługi HDInsight i skojarzone konto magazynu.

        azure group create groupname location

    * Zastąp `groupname` o unikatowej nazwie hello grupy.

    * Zastąp `location` z hello region geograficzny, który ma być toocreate hello grupy.

       Aby uzyskać listę prawidłowych lokalizacji, użyj hello `azure location list` polecenia, a następnie użyj jednej z lokalizacji hello z hello `Name` kolumny.

4. Utwórz konto magazynu. To konto magazynu jest używany jako hello domyślny magazyn dla klastra usługi HDInsight hello.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Zastąp `groupname` o nazwie hello hello grupy utworzony w poprzednim kroku hello.

    * Zastąp `location` z tej samej lokalizacji używany w poprzednim kroku hello hello.

    * Zastąp `storagename` o unikatowej nazwie hello konta magazynu.

        > [!NOTE]
        > Aby uzyskać więcej informacji o parametrach hello używane w tym poleceniu można używać `azure storage account create -h` tooview pomocy dla tego polecenia.

5. Pobieranie hello klucz używany konta magazynu hello tooaccess.

        azure storage account keys list -g groupname storagename

    * Zastąp `groupname` z nazwy grupy zasobów hello.
    * Zastąp `storagename` o nazwie hello hello konta magazynu.

     Witaj zwrócone dane, Zapisz hello `key` wartość `key1`.

6. Tworzenie klastra usługi HDInsight.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Zastąp `groupname` z nazwy grupy zasobów hello.

    * Zastąp `Hadoop` typu klastra hello, że chcesz toocreate. Na przykład `Hadoop`, `HBase`, `Kafka`, `Spark`, lub `Storm`.

     > [!IMPORTANT]
     > HDInsight klastry są dostępne w różnych typów, które odpowiadają toohello obciążenia lub technologii, która hello klastra dostosowana pod kątem. Brak toocreate nie obsługiwaną metodą klastra, który łączy wiele typów, takie jak Storm i bazy danych HBase w jednym klastrze.

    * Zastąp `location` z hello tej samej lokalizacji używane w poprzednich krokach.

    * Zastąp `storagename` nazwy konta magazynu hello.

    * Zastąp `storagekey` kluczem hello uzyskanych w poprzednim kroku hello.

    * Dla hello `--defaultStorageContainer` parametru, użyj hello sama nazwa jak używasz hello klastra.

    * Zastąp `admin` i `httppassword` hello nazwę i hasło mają toouse podczas uzyskiwania dostępu do klastra hello za pośrednictwem protokołu HTTPS.

    * Zastąp `sshuser` i `sshuserpassword` hello nazwy użytkownika i hasło mają toouse podczas uzyskiwania dostępu do klastra hello przy użyciu protokołu SSH

    > [!IMPORTANT]
    > W tym przykładzie jest tworzony klaster z dwoma notes procesu roboczego. Po utworzeniu klastra można również zmienić hello liczba węzłów procesu roboczego przez wykonanie operacji skalowania. Jeśli planujesz używanie więcej niż 32 węzłami procesów roboczych, następnie należy wybrać rozmiar węzła głównego z co najmniej 8 rdzeni i 14 GB pamięci RAM. Można ustawić rozmiaru węzła głównego hello przy użyciu hello `--headNodeSize` parametru podczas tworzenia klastra.
    >
    > Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

    Może upłynąć kilka minut toofinish procesu tworzenia klastra hello. Zazwyczaj około 15.

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki

Po pomyślnym utworzeniu klastra usługi HDInsight przy użyciu hello Azure CLI, za pomocą powitania po toolearn jak toowork z klastrem:

### <a name="hadoop-clusters"></a>Klastry Hadoop

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Klastrów HBase

* [Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Klastry STORM

* [Tworzenie topologii Java dla Storm w usłudze HDInsight](hdinsight-storm-develop-java-topology.md)
* [Użyj składników języka Python w Storm w usłudze HDInsight](hdinsight-storm-develop-python-topology.md)
* [Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
