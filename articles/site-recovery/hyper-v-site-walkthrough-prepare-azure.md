---
title: "Przygotowanie zasobów platformy Azure do replikowania maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) na platformie Azure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co jest potrzebne w miejscu na platformie Azure przed rozpoczęciem replikacji maszyn wirtualnych funkcji Hyper-V (bez VMM) na platformie Azure przy użyciu usługi Azure Site Recovery"
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
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="e5676-103">Krok 5: Przygotowanie zasobów Azure dla replikacji funkcji Hyper-V do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5676-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="e5676-104">Wykonaj instrukcje w tym artykule, aby przygotować zasobów platformy Azure, dzięki czemu można replikować maszyny wirtualne funkcji Hyper-V lokalnymi (bez programu System Center VMM) do platformy Azure przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="e5676-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="e5676-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu i zadawaj pytania techniczne na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e5676-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e5676-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e5676-106">Before you start</span></span>

<span data-ttu-id="e5676-107">Upewnij się, że zostały przeczytane [wymagania wstępne](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="e5676-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="e5676-108">Konfigurowanie konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5676-108">Set up an Azure account</span></span>

- <span data-ttu-id="e5676-109">Pobierz [konta Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e5676-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="e5676-110">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5676-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="e5676-111">Sprawdź, czy obsługiwane regiony usługi Site Recovery, w obszarze dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e5676-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="e5676-112">Dowiedz się więcej o [cenach usługi Site Recovery](site-recovery-faq.md#pricing)i uzyskać [szczegóły cennika](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e5676-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="e5676-113">Konfiguracja sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5676-113">Set up an Azure network</span></span>

- <span data-ttu-id="e5676-114">Skonfiguruj sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5676-114">Set up an Azure network.</span></span> <span data-ttu-id="e5676-115">Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="e5676-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="e5676-116">Sieć powinna znajdować się w tym samym regionie co magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="e5676-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="e5676-117">Usługi Site Recovery w portalu Azure mogą być używane w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.</span><span class="sxs-lookup"><span data-stu-id="e5676-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="e5676-118">Zaleca się skonfigurowanie sieci przed rozpoczęciem dalszych działań.</span><span class="sxs-lookup"><span data-stu-id="e5676-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="e5676-119">Jeśli tego nie zrobisz, konfigurację będzie trzeba przeprowadzić podczas wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e5676-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="e5676-120">Dowiedz się więcej o [cennik sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="e5676-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="e5676-121">Konfigurowanie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e5676-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="e5676-122">Usługa Site Recovery replikuje maszyny lokalnej do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e5676-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="e5676-123">Maszyny wirtualne platformy Azure są tworzone z magazynu po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="e5676-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="e5676-124">Konfigurowanie standard/premium [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) do przechowywania danych replikowanych do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5676-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="e5676-125">[Magazyn w warstwie Premium](../storage/common/storage-premium-storage.md) jest zazwyczaj używana w przypadku maszyn wirtualnych, które wymagają wysoką wydajność We/Wy i małe opóźnienia do intensywnych obciążeń we/wy hosta.</span><span class="sxs-lookup"><span data-stu-id="e5676-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="e5676-126">Jeśli używasz konta Premium do przechowywania replikowanych danych, potrzebujesz też standardowego konta magazynu do przechowywania dzienników replikacji, które przechwytują zachodzące zmiany w danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="e5676-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="e5676-127">W zależności od modelu zasobu, którego chcesz użyć dla nie powiodło się na maszynach wirtualnych platformy Azure, należy skonfigurować konto w [tryb usługi Resource Manager](../storage/common/storage-create-storage-account.md), lub [trybu klasycznego](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e5676-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="e5676-128">Zalecamy skonfigurowanie konta magazynu przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="e5676-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="e5676-129">Jeśli tego nie zrobisz trzeba przeprowadzić podczas wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e5676-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="e5676-130">Konta muszą być w tym samym regionie co magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e5676-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="e5676-131">Nie można przenieść kont magazynu używane przez usługę Site Recovery, grupy zasobów w ramach tej samej subskrypcji lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5676-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5676-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5676-132">Next steps</span></span>

<span data-ttu-id="e5676-133">Przejdź do [krok 6: Przygotowanie funkcji Hyper-V zasobów](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="e5676-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
