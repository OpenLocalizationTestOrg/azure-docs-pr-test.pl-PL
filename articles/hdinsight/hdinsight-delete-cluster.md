---
title: "Jak usunąć klaster usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Informacje na różne sposoby, że możesz usunąć klaster usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 65dac529df15d2dd43eec17673d82a2832f7692e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="7919d-103">Usuwanie klastra usługi HDInsight przy użyciu przeglądarki, programu PowerShell lub wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7919d-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="7919d-104">Karta klastra usługi HDInsight zaczyna się po klastra jest tworzony i zatrzymuje po usunięciu klastra.</span><span class="sxs-lookup"><span data-stu-id="7919d-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="7919d-105">Są naliczane proporcjonalnie za minutę, więc zawsze należy usunąć klaster, gdy nie jest już używana.</span><span class="sxs-lookup"><span data-stu-id="7919d-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="7919d-106">W tym dokumencie Dowiedz się jak usunąć klaster za pomocą portalu Azure, programu Azure PowerShell i Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7919d-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7919d-107">Usunięcie klastra usługi HDInsight nie powoduje usunięcia konta magazynu Azure lub usługi Data Lake Store jest skojarzone z klastrem.</span><span class="sxs-lookup"><span data-stu-id="7919d-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="7919d-108">Można ponownie użyć danych przechowywanych w tych usług w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="7919d-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="7919d-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7919d-109">Azure portal</span></span>

1. <span data-ttu-id="7919d-110">Zaloguj się do [portalu Azure](https://portal.azure.com) i wybierz z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7919d-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="7919d-111">Jeśli z klastrem usługi HDInsight nie jest przypięty do pulpitu nawigacyjnego, możesz wyszukać jego według nazwy, korzystając z pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7919d-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![wyszukiwania portalu](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="7919d-113">Gdy zostanie otwarty blok dla klastra, wybierz **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="7919d-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="7919d-114">Po wyświetleniu monitu wybierz **tak** można usunąć klastra.</span><span class="sxs-lookup"><span data-stu-id="7919d-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![Ikona usuwania](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="7919d-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7919d-116">Azure PowerShell</span></span>

<span data-ttu-id="7919d-117">Z wiersza polecenia programu PowerShell wpisz następujące polecenie, aby usunąć klaster:</span><span class="sxs-lookup"><span data-stu-id="7919d-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="7919d-118">Zastąp **CLUSTERNAME** nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7919d-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="7919d-119">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="7919d-119">Azure CLI 1.0</span></span>

<span data-ttu-id="7919d-120">W wierszu należy użyć następującego można usunąć klastra:</span><span class="sxs-lookup"><span data-stu-id="7919d-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="7919d-121">Zastąp **CLUSTERNAME** nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7919d-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7919d-122">Azure CLI 2.0 nie obsługuje usuwania klastrów usługi HDInsight w tej chwili (31 lipca 2017 r.).</span><span class="sxs-lookup"><span data-stu-id="7919d-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>