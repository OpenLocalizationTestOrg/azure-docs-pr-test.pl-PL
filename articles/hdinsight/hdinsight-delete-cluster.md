---
title: "toodelete aaaHow klastra usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Informacje na temat hello różne sposoby, że możesz usunąć klaster usługi HDInsight."
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
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="1cda4-103">Usuwanie klastra usługi HDInsight przy użyciu przeglądarki, programu PowerShell lub interfejsu wiersza polecenia Azure hello</span><span class="sxs-lookup"><span data-stu-id="1cda4-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="1cda4-104">Karta klastra usługi HDInsight zaczyna się po klastra jest tworzony i zatrzymywana, gdy klaster hello jest usunięty.</span><span class="sxs-lookup"><span data-stu-id="1cda4-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="1cda4-105">Są naliczane proporcjonalnie za minutę, więc zawsze należy usunąć klaster, gdy nie jest już używana.</span><span class="sxs-lookup"><span data-stu-id="1cda4-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="1cda4-106">W tym dokumencie możesz dowiedzieć się, jak toodelete klastra przy użyciu hello portalu Azure, programu Azure PowerShell i hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="1cda4-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cda4-107">Usunięcie klastra usługi HDInsight nie powoduje usunięcia konta usługi Azure Storage hello lub Data Lake Store jest skojarzone z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="1cda4-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="1cda4-108">Można ponownie użyć danych przechowywanych w tych usług w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="1cda4-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="1cda4-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1cda4-109">Azure portal</span></span>

1. <span data-ttu-id="1cda4-110">Zaloguj się za toohello [portalu Azure](https://portal.azure.com) i wybierz z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1cda4-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="1cda4-111">Jeśli z klastrem usługi HDInsight nie jest przypięty toohello pulpitu nawigacyjnego, możesz wyszukać jego wg nazwy przy użyciu pola wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="1cda4-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![wyszukiwania portalu](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="1cda4-113">Gdy zostanie otwarty blok hello hello klastra, wybierz hello **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="1cda4-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="1cda4-114">Po wyświetleniu monitu wybierz **tak** toodelete hello klastra.</span><span class="sxs-lookup"><span data-stu-id="1cda4-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![Ikona usuwania](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="1cda4-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cda4-116">Azure PowerShell</span></span>

<span data-ttu-id="1cda4-117">Z wiersza polecenia programu PowerShell Użyj hello następujące polecenie toodelete hello klastra:</span><span class="sxs-lookup"><span data-stu-id="1cda4-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="1cda4-118">Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1cda4-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="1cda4-119">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="1cda4-119">Azure CLI 1.0</span></span>

<span data-ttu-id="1cda4-120">W wierszu Użyj powitania po toodelete hello klastra:</span><span class="sxs-lookup"><span data-stu-id="1cda4-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="1cda4-121">Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1cda4-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1cda4-122">Azure CLI 2.0 nie obsługuje usuwania klastrów usługi HDInsight w tej chwili (31 lipca 2017 r.).</span><span class="sxs-lookup"><span data-stu-id="1cda4-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>