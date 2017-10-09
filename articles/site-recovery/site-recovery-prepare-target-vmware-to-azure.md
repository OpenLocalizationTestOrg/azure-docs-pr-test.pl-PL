---
title: Przygotowanie docelowego (VMware tooAzure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób tooprepare Twojego toostart środowiska platformy Azure replikowanie tooAzure maszyny wirtualne VMware."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="cfa98-103">Przygotowanie docelowego (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="cfa98-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cfa98-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="cfa98-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="cfa98-105">TooAzure fizycznych</span><span class="sxs-lookup"><span data-stu-id="cfa98-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="cfa98-106">W tym artykule opisano sposób tooprepare Twojego toostart środowiska platformy Azure replikowanie tooAzure maszyny wirtualne VMware.</span><span class="sxs-lookup"><span data-stu-id="cfa98-106">This article describes how tooprepare your Azure environment toostart replicating VMware virtual machines tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfa98-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cfa98-107">Prerequisites</span></span>

<span data-ttu-id="cfa98-108">Artykuł Hello założono hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="cfa98-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="cfa98-109">Utworzono tooprotect magazynu usług odzyskiwania maszyn wirtualnych VMware.</span><span class="sxs-lookup"><span data-stu-id="cfa98-109">You have created a Recovery Services Vault tooprotect your VMware virtual machines.</span></span> <span data-ttu-id="cfa98-110">Można utworzyć magazyn usług odzyskiwania na podstawie hello [portalu Azure](http://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="cfa98-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="cfa98-111">Masz [konfiguracji środowiska lokalnego](./site-recovery-set-up-vmware-to-azure.md) tooAzure maszyny wirtualne VMware tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="cfa98-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware virtual machines tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="cfa98-112">Przygotowanie docelowego</span><span class="sxs-lookup"><span data-stu-id="cfa98-112">Prepare target</span></span>

<span data-ttu-id="cfa98-113">Po zakończeniu hello **cel ochrony krok 1** i **krok 2: przygotowanie źródła**, nastąpi za**krok 3: docelowy**</span><span class="sxs-lookup"><span data-stu-id="cfa98-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Przygotowanie docelowego](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="cfa98-115">**Subskrypcja:** z hello menu rozwijane, wybierz hello subskrypcji, które mają tooreplicate do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cfa98-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your virtual machines to.</span></span>
2. <span data-ttu-id="cfa98-116">**Model wdrażania:** hello wybierz model wdrażania (Classic lub Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="cfa98-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="cfa98-117">Oparte na powitania wybrany model wdrażania, sprawdzanie poprawności jest uruchamiane tooensure, który ma co najmniej jedno konto magazynu zgodny i siecią wirtualną tooreplicate subskrypcji docelowej hello i trybu failover maszyny wirtualnej do.</span><span class="sxs-lookup"><span data-stu-id="cfa98-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your virtual machine to.</span></span>

<span data-ttu-id="cfa98-118">Po hello operacji sprawdzania poprawności zakończy się pomyślnie, kliknij przycisk OK toogo toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="cfa98-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="cfa98-119">Jeśli nie masz zgodne konto magazynu Resource Manager lub sieci wirtualnej lub chcesz tooadd więcej, możesz to zrobić, klikając hello **+ konto magazynu** lub **+ sieć** przyciski na początku hello hello blok.</span><span class="sxs-lookup"><span data-stu-id="cfa98-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfa98-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cfa98-120">Next steps</span></span>
<span data-ttu-id="cfa98-121">[Konfigurowanie ustawień replikacji](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="cfa98-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
