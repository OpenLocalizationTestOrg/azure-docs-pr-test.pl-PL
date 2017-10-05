---
title: "Przygotowanie zasobów platformy Azure w ramach replikacji lokalnych serwerów fizycznych do platformy Azure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co jest potrzebne w miejscu na platformie Azure przed rozpoczęciem replikacji lokalnych serwerów na platformę Azure przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a><span data-ttu-id="e82e5-103">Krok 5: Przygotowanie zasobów Azure dla replikacji serwera fizycznego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e82e5-103">Step 5: Prepare Azure resources for physical server replication to Azure</span></span>


<span data-ttu-id="e82e5-104">Postępuj zgodnie z instrukcjami w tym artykule, aby przygotować zasobów platformy Azure, aby serwerów lokalnych można replikować do platformy Azure przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="e82e5-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="e82e5-105">Opublikuj komentarze i pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e82e5-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e82e5-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e82e5-106">Before you start</span></span>

<span data-ttu-id="e82e5-107">Upewnij się, że zostały przeczytane [wymagania wstępne](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="e82e5-107">Make sure you've read the [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="e82e5-108">Konfigurowanie konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e82e5-108">Set up an Azure account</span></span>

- <span data-ttu-id="e82e5-109">Pobierz [konta Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e82e5-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="e82e5-110">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e82e5-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="e82e5-111">Sprawdź, czy obsługiwane regiony usługi Site Recovery w obszarze **dotyczącą dostępności geograficznej** w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e82e5-111">Check the supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="e82e5-112">Dowiedz się więcej o [cenach usługi Site Recovery](site-recovery-faq.md#pricing)i uzyskać [szczegóły cennika](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e82e5-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="e82e5-113">Konfiguracja sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e82e5-113">Set up an Azure network</span></span>

- <span data-ttu-id="e82e5-114">Skonfiguruj sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e82e5-114">Set up an Azure network.</span></span> <span data-ttu-id="e82e5-115">Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="e82e5-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="e82e5-116">Usługi Site Recovery w portalu Azure mogą być używane w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.</span><span class="sxs-lookup"><span data-stu-id="e82e5-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="e82e5-117">Sieć powinna znajdować się w tym samym regionie co magazyn usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e82e5-117">The network should be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="e82e5-118">Dowiedz się więcej o [cennik sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="e82e5-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="e82e5-119">Dowiedz się więcej o [łączności maszyny Wirtualnej Azure](physical-walkthrough-network.md) po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="e82e5-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="e82e5-120">Konfigurowanie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e82e5-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="e82e5-121">Usługa Site Recovery replikuje serwerów lokalnych do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e82e5-121">Site Recovery replicates on-premises servers to Azure storage.</span></span> <span data-ttu-id="e82e5-122">Maszyny wirtualne platformy Azure są tworzone z magazynu po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="e82e5-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="e82e5-123">Konfigurowanie [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) dla replikowanych danych.</span><span class="sxs-lookup"><span data-stu-id="e82e5-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="e82e5-124">Usługi Site Recovery w portalu Azure można używać kont magazynu w Menedżerze zasobów lub w trybie klasycznym.</span><span class="sxs-lookup"><span data-stu-id="e82e5-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="e82e5-125">Konto magazynu może być standard lub [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e82e5-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="e82e5-126">Skonfigurowanie konta premium, należy również dodatkowe konta standardowego dla danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="e82e5-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e82e5-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e82e5-127">Next steps</span></span>

<span data-ttu-id="e82e5-128">Przejdź do [krok 6: Konfigurowanie magazynu](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="e82e5-128">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
