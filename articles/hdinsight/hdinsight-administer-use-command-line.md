---
title: "Zarządzanie klastrami Hadoop przy użyciu interfejsu wiersza polecenia Azure - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać klastrów platformy Hadoop w usłudze Azure HDInsight za pomocą interfejsu wiersza polecenia platformy Azure. Interfejsu wiersza polecenia Azure działa w systemie Windows, Mac i Linux."
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
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="8b0a1-104">Zarządzanie klastrami Hadoop w HDInsight przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8b0a1-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="8b0a1-105">Dowiedz się, jak używać [interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md) do zarządzania klastrami Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="8b0a1-106">Interfejs wiersza polecenia platformy Azure został zaimplementowany w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="8b0a1-107">Można go używać na dowolnej platformie, która obsługuje środowisko Node.js, w tym w systemie Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="8b0a1-108">W tym artykule opisano tylko przy użyciu wiersza polecenia platformy Azure z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="8b0a1-109">Aby uzyskać ogólne wskazówki dotyczące sposobu używania interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="8b0a1-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="8b0a1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b0a1-110">Prerequisites</span></span>
<span data-ttu-id="8b0a1-111">Przed rozpoczęciem korzystania z informacji zawartych w tym artykule należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="8b0a1-112">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-112">**An Azure subscription**.</span></span> <span data-ttu-id="8b0a1-113">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8b0a1-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8b0a1-114">**Interfejs wiersza polecenia platformy Azure** — informacje na temat instalacji i konfiguracji można znaleźć w temacie [Instalowanie i konfigurowanie interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8b0a1-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="8b0a1-115">**Połączenia z platformą Azure**, za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="8b0a1-116">Więcej informacji na temat uwierzytelniania za pomocą konta służbowego lub szkolnego znajdziesz w temacie [Połączenie z subskrypcją platformy Azure z poziomu interfejsu wiersza polecenia platformy Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8b0a1-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="8b0a1-117">**Przełączenie w tryb usługi Azure Resource Manager** przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="8b0a1-118">Aby uzyskać pomoc, użyj **-h** przełącznika.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="8b0a1-119">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="8b0a1-120">Tworzenie klastrów z poziomu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="8b0a1-120">Create clusters with the CLI</span></span>
<span data-ttu-id="8b0a1-121">Zobacz [Tworzenie klastrów w usłudze HDInsight przy użyciu interfejsu wiersza polecenia Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b0a1-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="8b0a1-122">Listy i pokazać szczegółów klastra</span><span class="sxs-lookup"><span data-stu-id="8b0a1-122">List and show cluster details</span></span>
<span data-ttu-id="8b0a1-123">Użyj następujących poleceń do listy w celu wyświetlenia szczegółów klastra:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="8b0a1-124">![Widok wiersza polecenia klastra listy][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="8b0a1-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="8b0a1-125">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="8b0a1-125">Delete clusters</span></span>
<span data-ttu-id="8b0a1-126">Aby usunąć klaster, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="8b0a1-127">Można również usunąć klaster przez usunięcie grupy zasobów zawierającej klaster.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="8b0a1-128">Należy pamiętać, spowoduje to usunięcie wszystkich zasobów w grupie, w tym domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="8b0a1-129">Skalowanie klastrów</span><span class="sxs-lookup"><span data-stu-id="8b0a1-129">Scale clusters</span></span>
<span data-ttu-id="8b0a1-130">Aby zmienić rozmiar klastra usługi Hadoop:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="8b0a1-131">Włącz/Wyłącz dostęp HTTP dla klastra</span><span class="sxs-lookup"><span data-stu-id="8b0a1-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="8b0a1-132">Włączanie/wyłączanie dostępu RDP dla klastra</span><span class="sxs-lookup"><span data-stu-id="8b0a1-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="8b0a1-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8b0a1-133">Next steps</span></span>
<span data-ttu-id="8b0a1-134">W tym artykule zapoznaniu do wykonywania różnych zadań administracyjnych klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b0a1-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="8b0a1-135">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8b0a1-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="8b0a1-136">[Administrowanie HDInsight przy użyciu portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="8b0a1-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="8b0a1-137">[Administrowanie HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="8b0a1-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="8b0a1-138">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="8b0a1-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="8b0a1-139">[Sposób użycia interfejsu wiersza polecenia Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="8b0a1-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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
