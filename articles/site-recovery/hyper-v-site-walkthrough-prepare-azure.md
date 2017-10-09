---
title: "aaaPrepare zasobów Azure tooreplicate tooAzure maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera informacje potrzebne w miejscu na platformie Azure przed rozpoczęciem replikacji przy użyciu usługi Azure Site Recovery tooAzure maszyn wirtualnych funkcji Hyper-V (bez VMM)"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="1afb9-103">Krok 5: Przygotowanie zasobów Azure dla tooAzure replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="1afb9-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="1afb9-104">Użyj instrukcji hello, w tym artykule tooprepare Azure zasobów, dzięki czemu można replikować lokalne maszyny wirtualne funkcji Hyper-V (bez programu System Center VMM) przy użyciu hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="1afb9-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="1afb9-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1afb9-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1afb9-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1afb9-106">Before you start</span></span>

<span data-ttu-id="1afb9-107">Upewnij się, że zostały przeczytane hello [wymagania wstępne](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1afb9-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="1afb9-108">Konfigurowanie konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1afb9-108">Set up an Azure account</span></span>

- <span data-ttu-id="1afb9-109">Pobierz [konta Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1afb9-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="1afb9-110">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1afb9-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="1afb9-111">Sprawdź, czy hello obsługiwane regiony usługi Site Recovery, w obszarze dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="1afb9-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="1afb9-112">Dowiedz się więcej o [cenach usługi Site Recovery](site-recovery-faq.md#pricing)i uzyskać hello [szczegóły cennika](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="1afb9-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="1afb9-113">Konfiguracja sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1afb9-113">Set up an Azure network</span></span>

- <span data-ttu-id="1afb9-114">Skonfiguruj sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1afb9-114">Set up an Azure network.</span></span> <span data-ttu-id="1afb9-115">Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1afb9-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="1afb9-116">Witaj sieć powinna znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello</span><span class="sxs-lookup"><span data-stu-id="1afb9-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="1afb9-117">Usługi Site Recovery w portalu Azure hello mogą być używane w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.</span><span class="sxs-lookup"><span data-stu-id="1afb9-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="1afb9-118">Zaleca się skonfigurowanie sieci przed rozpoczęciem dalszych działań.</span><span class="sxs-lookup"><span data-stu-id="1afb9-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="1afb9-119">Jeśli nie, należy toodo go podczas wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1afb9-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="1afb9-120">Dowiedz się więcej o [cennik sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="1afb9-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="1afb9-121">Konfigurowanie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1afb9-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="1afb9-122">Usługa Site Recovery replikuje magazynu tooAzure maszyny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="1afb9-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="1afb9-123">Maszyny wirtualne platformy Azure są tworzone na podstawie magazynu powitania po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1afb9-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="1afb9-124">Konfigurowanie standard/premium [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dane replikowane tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1afb9-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="1afb9-125">[Magazyn w warstwie Premium](../storage/common/storage-premium-storage.md) jest zazwyczaj używana w przypadku maszyn wirtualnych, które wymagają wysoką wydajność We/Wy i intensywnych obciążeń we/wy toohost małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="1afb9-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="1afb9-126">Jeśli chcesz, aby toouse toostore konta premium zreplikowanych danych, należy również konta magazynu w warstwie standardowa toostore dzienników replikacji przechwytywania trwającą zmienia się tooon lokalne dane.</span><span class="sxs-lookup"><span data-stu-id="1afb9-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="1afb9-127">W zależności od modelu zasobu hello ma toouse nie powiodła się na maszynach wirtualnych platformy Azure, należy skonfigurować konto w [tryb usługi Resource Manager](../storage/common/storage-create-storage-account.md), lub [trybu klasycznego](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1afb9-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="1afb9-128">Zalecamy skonfigurowanie konta magazynu przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="1afb9-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="1afb9-129">Jeśli użytkownik nie należy toodo go podczas wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1afb9-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="1afb9-130">Witaj konta muszą być w hello magazyn usług odzyskiwania i tym samym regionie co hello.</span><span class="sxs-lookup"><span data-stu-id="1afb9-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="1afb9-131">Nie można przenieść magazynu konta używane przez usługę Site Recovery między grupami zasobów w ramach hello sam subskrypcji lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1afb9-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1afb9-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1afb9-132">Next steps</span></span>

<span data-ttu-id="1afb9-133">Przejdź zbyt[krok 6: Przygotowanie funkcji Hyper-V zasobów](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="1afb9-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
