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
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="f2f8e-104">Zarządzanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f2f8e-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="f2f8e-105">Dowiedz się, jak toouse hello [interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md) klastrów toomanage Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="f2f8e-106">Witaj wiersza polecenia platformy Azure jest zaimplementowany w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="f2f8e-107">Można go używać na dowolnej platformie, która obsługuje środowisko Node.js, w tym w systemie Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="f2f8e-108">W tym artykule opisano tylko przy użyciu hello wiersza polecenia platformy Azure z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="f2f8e-109">Ogólne wskazówki na temat toouse wiersza polecenia platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="f2f8e-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="f2f8e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f2f8e-110">Prerequisites</span></span>
<span data-ttu-id="f2f8e-111">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="f2f8e-112">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-112">**An Azure subscription**.</span></span> <span data-ttu-id="f2f8e-113">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f2f8e-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f2f8e-114">**Azure CLI** — zobacz [zainstalować i skonfigurować hello Azure CLI](../cli-install-nodejs.md) informacji o instalacji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="f2f8e-115">**Połącz tooAzure**za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="f2f8e-116">Aby uzyskać więcej informacji na temat uwierzytelniania przy użyciu konta służbowego, zobacz [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f2f8e-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="f2f8e-117">**Przełącz tryb usługi Azure Resource Manager toohello**za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="f2f8e-118">tooget uzyskać pomoc, użyj hello **-h** przełącznika.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="f2f8e-119">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="f2f8e-120">Tworzenie klastrów z hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f2f8e-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="f2f8e-121">Zobacz [Tworzenie klastrów usługi HDInsight przy użyciu hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f2f8e-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="f2f8e-122">Listy i pokazać szczegółów klastra</span><span class="sxs-lookup"><span data-stu-id="f2f8e-122">List and show cluster details</span></span>
<span data-ttu-id="f2f8e-123">Użyj następującego polecenia toolist hello i pokazać szczegółów klastra:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="f2f8e-124">![Widok wiersza polecenia klastra listy][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="f2f8e-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="f2f8e-125">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="f2f8e-125">Delete clusters</span></span>
<span data-ttu-id="f2f8e-126">Użyj hello następujące polecenia toodelete klastra:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="f2f8e-127">Można również usunąć klaster, usuwając hello grupę zasobów, która zawiera hello klastra.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="f2f8e-128">Należy pamiętać, spowoduje to usunięcie wszystkich zasobów hello w grupie hello w tym hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="f2f8e-129">Skalowanie klastrów</span><span class="sxs-lookup"><span data-stu-id="f2f8e-129">Scale clusters</span></span>
<span data-ttu-id="f2f8e-130">Witaj toochange rozmiar klastra usługi Hadoop:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="f2f8e-131">Włącz/Wyłącz dostęp HTTP dla klastra</span><span class="sxs-lookup"><span data-stu-id="f2f8e-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="f2f8e-132">Włączanie/wyłączanie dostępu RDP dla klastra</span><span class="sxs-lookup"><span data-stu-id="f2f8e-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="f2f8e-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2f8e-133">Next steps</span></span>
<span data-ttu-id="f2f8e-134">W tym artykule wiesz już, jak tooperform różne HDInsight klastra zadania administracyjne.</span><span class="sxs-lookup"><span data-stu-id="f2f8e-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="f2f8e-135">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="f2f8e-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="f2f8e-136">[Administrowanie HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="f2f8e-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="f2f8e-137">[Administrowanie HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="f2f8e-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="f2f8e-138">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f2f8e-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="f2f8e-139">[Jak toouse hello wiersza polecenia platformy Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="f2f8e-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

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
