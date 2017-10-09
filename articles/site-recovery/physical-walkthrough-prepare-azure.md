---
title: "tooreplicate zasobów Azure aaaPrepare lokalnych serwerów fizycznych tooAzure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera informacje potrzebne w miejscu na platformie Azure przed rozpoczęciem replikacji lokalnych serwerów tooAzure, przy użyciu usługi Azure Site Recovery hello"
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
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="b3057-103">Krok 5: Przygotowanie zasobów Azure dla tooAzure replikacji serwera fizycznego</span><span class="sxs-lookup"><span data-stu-id="b3057-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="b3057-104">Użyj instrukcji hello, w tym artykule tooprepare Azure zasobów, dzięki czemu można replikować tooAzure serwerów lokalnych przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="b3057-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="b3057-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b3057-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b3057-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b3057-106">Before you start</span></span>

<span data-ttu-id="b3057-107">Upewnij się, że zostały przeczytane hello [wymagania wstępne](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="b3057-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="b3057-108">Konfigurowanie konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b3057-108">Set up an Azure account</span></span>

- <span data-ttu-id="b3057-109">Pobierz [konta Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="b3057-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="b3057-110">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3057-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="b3057-111">Sprawdź, czy hello obsługiwane regiony usługi Site Recovery w obszarze **dotyczącą dostępności geograficznej** w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="b3057-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="b3057-112">Dowiedz się więcej o [cenach usługi Site Recovery](site-recovery-faq.md#pricing)i uzyskać hello [szczegóły cennika](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="b3057-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="b3057-113">Konfiguracja sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b3057-113">Set up an Azure network</span></span>

- <span data-ttu-id="b3057-114">Skonfiguruj sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3057-114">Set up an Azure network.</span></span> <span data-ttu-id="b3057-115">Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="b3057-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="b3057-116">Usługi Site Recovery w portalu Azure hello mogą być używane w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.</span><span class="sxs-lookup"><span data-stu-id="b3057-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="b3057-117">Witaj sieć powinna znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello.</span><span class="sxs-lookup"><span data-stu-id="b3057-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="b3057-118">Dowiedz się więcej o [cennik sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="b3057-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="b3057-119">Dowiedz się więcej o [łączności maszyny Wirtualnej Azure](physical-walkthrough-network.md) po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="b3057-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="b3057-120">Konfigurowanie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b3057-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="b3057-121">Usługa Site Recovery replikacji lokalnych serwerów tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="b3057-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="b3057-122">Maszyny wirtualne platformy Azure są tworzone na podstawie magazynu powitania po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="b3057-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="b3057-123">Konfigurowanie [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) dla replikowanych danych.</span><span class="sxs-lookup"><span data-stu-id="b3057-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="b3057-124">Odzyskiwanie lokacji w hello portalu Azure można używać kont magazynu w Menedżerze zasobów lub w trybie klasycznym.</span><span class="sxs-lookup"><span data-stu-id="b3057-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="b3057-125">Konto magazynu Hello może być standardowe lub [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b3057-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="b3057-126">Skonfigurowanie konta premium, należy również dodatkowe konta standardowego dla danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="b3057-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b3057-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3057-127">Next steps</span></span>

<span data-ttu-id="b3057-128">Przejdź do zbyt[krok 6: Konfigurowanie magazynu](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="b3057-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
