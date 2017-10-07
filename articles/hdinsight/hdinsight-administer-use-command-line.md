---
title: "przy użyciu interfejsu wiersza polecenia Azure - Azure HDInsight klastrów Hadoop aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastrów toouse hello interfejsu wiersza polecenia platformy Azure toomanage Hadoop w usłudze Azure HDInsight. Witaj wiersza polecenia platformy Azure działa w przypadku systemu Windows, Mac i Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Zarządzanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello wiersza polecenia platformy Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Dowiedz się, jak toouse hello [interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md) klastrów toomanage Hadoop w usłudze Azure HDInsight. Witaj wiersza polecenia platformy Azure jest zaimplementowany w środowisku Node.js. Można go używać na dowolnej platformie, która obsługuje środowisko Node.js, w tym w systemie Windows, Mac i Linux.

W tym artykule opisano tylko przy użyciu hello wiersza polecenia platformy Azure z usługą HDInsight. Ogólne wskazówki na temat toouse wiersza polecenia platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure CLI** — zobacz [zainstalować i skonfigurować hello Azure CLI](../cli-install-nodejs.md) informacji o instalacji i konfiguracji.
* **Połącz tooAzure**za pomocą hello następujące polecenie:
  
        azure login
  
    Aby uzyskać więcej informacji na temat uwierzytelniania przy użyciu konta służbowego, zobacz [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../xplat-cli-connect.md).
* **Przełącz tryb usługi Azure Resource Manager toohello**za pomocą hello następujące polecenie:
  
        azure config mode arm

tooget uzyskać pomoc, użyj hello **-h** przełącznika.  Na przykład:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Tworzenie klastrów z hello interfejsu wiersza polecenia
Zobacz [Tworzenie klastrów usługi HDInsight przy użyciu hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Listy i pokazać szczegółów klastra
Użyj następującego polecenia toolist hello i pokazać szczegółów klastra:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Widok wiersza polecenia klastra listy][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Usuwanie klastrów
Użyj hello następujące polecenia toodelete klastra:

    azure hdinsight cluster delete <Cluster Name>

Można również usunąć klaster, usuwając hello grupę zasobów, która zawiera hello klastra. Należy pamiętać, spowoduje to usunięcie wszystkich zasobów hello w grupie hello w tym hello domyślne konto magazynu.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Skalowanie klastrów
Witaj toochange rozmiar klastra usługi Hadoop:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Włącz/Wyłącz dostęp HTTP dla klastra
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Włączanie/wyłączanie dostępu RDP dla klastra
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Następne kroki
W tym artykule wiesz już, jak tooperform różne HDInsight klastra zadania administracyjne. toolearn więcej, zobacz następujące artykuły hello:

* [Administrowanie HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]
* [Administrowanie HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]
* [Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]
* [Jak toouse hello wiersza polecenia platformy Azure][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Lista i Pokaż klastrów"
