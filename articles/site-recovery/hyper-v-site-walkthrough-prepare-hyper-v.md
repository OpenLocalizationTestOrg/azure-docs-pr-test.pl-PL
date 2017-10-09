---
title: "aaaPrepare funkcji Hyper-V obsługuje (bez programu System Center VMM) dla replikacji tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooprepare funkcji Hyper-V obsługuje dla tooAzure replikacji przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="0086f-103">Krok 6: Przygotowanie hosty funkcji Hyper-V do tooAzure replikacji</span><span class="sxs-lookup"><span data-stu-id="0086f-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="0086f-104">Użyj hello instrukcje w tym artykule tooprepare lokalnymi toointeract hosty funkcji Hyper-V z usługą Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0086f-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="0086f-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0086f-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="0086f-106">Przygotowywanie hostów</span><span class="sxs-lookup"><span data-stu-id="0086f-106">Prepare hosts</span></span>

- <span data-ttu-id="0086f-107">Upewnij się, że hello funkcji Hyper-V, hosty spełniają hello [wymagania wstępne](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="0086f-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="0086f-108">Upewnij się, że hosty hello dostęp hello wymagane adresów URL:</span><span class="sxs-lookup"><span data-stu-id="0086f-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="0086f-109">Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.</span><span class="sxs-lookup"><span data-stu-id="0086f-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="0086f-110">Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).</span><span class="sxs-lookup"><span data-stu-id="0086f-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="0086f-111">Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).</span><span class="sxs-lookup"><span data-stu-id="0086f-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="0086f-112">Podczas wdrażania usługi Site Recovery możesz dodać hostów funkcji Hyper-V, zawierających maszyny wirtualne mają tooreplicate lokacji tooa funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0086f-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="0086f-113">Witaj dostawcy usługi Site Recovery i agenta usług odzyskiwania są instalowane na każdym hoście.</span><span class="sxs-lookup"><span data-stu-id="0086f-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="0086f-114">Witryna Hello funkcji Hyper-V jest zarejestrowana w powitalne magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="0086f-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0086f-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0086f-115">Next steps</span></span>

<span data-ttu-id="0086f-116">Przejdź do zbyt[kroku 7: Tworzenie magazynu](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="0086f-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

