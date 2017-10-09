---
title: "wymagania wstępne hello aaaReview dla funkcji Hyper-V tooAzure replikacji (bez programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje warunki wstępne hello do replikacji, trybu failover i odzyskiwania lokalnych maszyn wirtualnych funkcji Hyper-V tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="61ea8-103">Krok 2: Przejrzyj wymagania wstępne hello replikacji tooAzure funkcji Hyper-V (bez VMM)</span><span class="sxs-lookup"><span data-stu-id="61ea8-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="61ea8-104">wymagania wstępne Hello są podsumowane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="61ea8-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="61ea8-105">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="61ea8-105">**Prerequisite**</span></span> | <span data-ttu-id="61ea8-106">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="61ea8-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="61ea8-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="61ea8-107">**Azure**</span></span> | <span data-ttu-id="61ea8-108">Dowiedz się więcej na temat [wymagań platformy Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="61ea8-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="61ea8-109">**Serwery lokalne**</span><span class="sxs-lookup"><span data-stu-id="61ea8-109">**On-premises servers**</span></span> | <span data-ttu-id="61ea8-110">[Dowiedz się więcej](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) o wymaganiach dla hostów funkcji Hyper-V lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="61ea8-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="61ea8-111">**Lokalne maszyny wirtualne funkcji Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="61ea8-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="61ea8-112">Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="61ea8-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="61ea8-113">**Adresy URL platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="61ea8-113">**Azure URLs**</span></span> | <span data-ttu-id="61ea8-114">Hosty funkcji Hyper-V muszą uzyskać dostęp do toothese adresów URL:</span><span class="sxs-lookup"><span data-stu-id="61ea8-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="61ea8-115">Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.</span><span class="sxs-lookup"><span data-stu-id="61ea8-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="61ea8-116">Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).</span><span class="sxs-lookup"><span data-stu-id="61ea8-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="61ea8-117">Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).</span><span class="sxs-lookup"><span data-stu-id="61ea8-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="61ea8-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61ea8-118">Next steps</span></span>

- <span data-ttu-id="61ea8-119">Jeśli pełne wdrożenie robimy, przejdź zbyt[krok 3: Planowanie pojemności](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="61ea8-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="61ea8-120">Jeśli podczas wykonywania testu proste wdrożenie, należy przejść za[krok 4: Planowanie sieci](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="61ea8-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
