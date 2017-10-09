---
title: aaaPrepare programu System Center VMM dla funkcji Hyper-V replikacji tooAzure | Dokumentacja firmy Microsoft
description: "Opisuje sposób serwer programu System Center VMM tooprepare tooAzure replikacji funkcji Hyper-V, za pomocą usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="1037a-103">Krok 6: Przygotowanie serwerów programu VMM i hosty funkcji Hyper-V do tooAzure replikacji funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="1037a-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="1037a-104">Po skonfigurowaniu [Azure składniki](vmm-to-azure-walkthrough-prepare-azure.md) hello wdrożenia, użyj instrukcji hello w tym serwerów VMM lokalnych tooprepare artykułu i toointeract hosty funkcji Hyper-V z usługą Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1037a-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="1037a-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1037a-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="1037a-106">Przygotowanie serwerów programu VMM</span><span class="sxs-lookup"><span data-stu-id="1037a-106">Prepare VMM servers</span></span>

- <span data-ttu-id="1037a-107">Należy co najmniej jeden serwer VMM spełniające wymagania dotyczące obsługi hello replikacji usługi Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="1037a-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="1037a-108">Upewnij się, że zostały przygotowane powitania serwera VMM dla [mapowania sieci](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="1037a-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="1037a-109">Upewnij się, że na tym serwerze programu VMM hello mogą uzyskiwać dostęp do tych adresów URL</span><span class="sxs-lookup"><span data-stu-id="1037a-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="1037a-110">Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.</span><span class="sxs-lookup"><span data-stu-id="1037a-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="1037a-111">Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).</span><span class="sxs-lookup"><span data-stu-id="1037a-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="1037a-112">Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).</span><span class="sxs-lookup"><span data-stu-id="1037a-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="1037a-113">Podczas wdrażania usługi Site Recovery Pobierz hello dostawcy usługi Site Recovery i zainstalować ją na każdym serwerze programu VMM.</span><span class="sxs-lookup"><span data-stu-id="1037a-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="1037a-114">Serwer VMM Hello jest zarejestrowany w powitalne magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="1037a-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="1037a-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1037a-115">Next steps</span></span>

<span data-ttu-id="1037a-116">Przejdź do zbyt[kroku 7: Tworzenie magazynu](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="1037a-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

