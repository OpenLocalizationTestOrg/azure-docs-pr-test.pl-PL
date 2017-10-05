---
title: Przygotowanie docelowego (fizycznych do platformy Azure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób przygotowania środowiska Azure, aby uruchomić replikowania serwerów fizycznych z systemem Windows lub Linux na platformie Azure."
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
ms.openlocfilehash: aa7a32ace8354f615a8b8cc137f6bdf48fbadf48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="6f8f1-103">Przygotowanie docelowego (VMware do platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="6f8f1-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f8f1-104">Z programu VMware do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6f8f1-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="6f8f1-105">Fizycznych do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6f8f1-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="6f8f1-106">W tym artykule opisano sposób przygotowania środowiska Azure do rozpoczęcia replikacji serwery fizyczne (x 64) z systemu Windows lub Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f8f1-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6f8f1-107">Prerequisites</span></span>

<span data-ttu-id="6f8f1-108">Artykuł założono następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f8f1-108">The article assumes the following:</span></span>
- <span data-ttu-id="6f8f1-109">Utworzono magazyn usług odzyskiwania, aby chronić serwery fizyczne.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="6f8f1-110">Można utworzyć magazyn usług odzyskiwania z [portalu Azure](http://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="6f8f1-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="6f8f1-111">Masz [konfiguracji środowiska lokalnego](./site-recovery-set-up-physical-to-azure.md) do replikowania serwerów fizycznych do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="6f8f1-112">Przygotowanie docelowego</span><span class="sxs-lookup"><span data-stu-id="6f8f1-112">Prepare target</span></span>

<span data-ttu-id="6f8f1-113">Po zakończeniu **cel ochrony krok 1** i **krok 2: przygotowanie źródła**, zostają przeniesieni do **krok 3: docelowy**</span><span class="sxs-lookup"><span data-stu-id="6f8f1-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Przygotowanie docelowego](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="6f8f1-115">**Subskrypcja:** z menu rozwijanego Wybierz subskrypcję, która ma zostać zreplikowana na serwerach fizycznych.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="6f8f1-116">**Model wdrażania:** wybierz model wdrażania (Classic lub Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6f8f1-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="6f8f1-117">Oparte na modelu wdrażania wybranego, uruchomieniu aby upewnić się, że użytkownik ma co najmniej jedno konto magazynu zgodny i sieć wirtualną w docelowej subskrypcji replikacji i trybu failover serwerów fizycznych do weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="6f8f1-118">Po operacji sprawdzania poprawności zakończy się pomyślnie, kliknij przycisk OK, aby przejść do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="6f8f1-119">Jeśli nie masz zgodne konto magazynu Resource Manager lub sieci wirtualnej, lub czy chcesz dodać więcej, możesz to zrobić, klikając **+ konto magazynu** lub **+ sieć** przycisków w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="6f8f1-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f8f1-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f8f1-120">Next steps</span></span>
<span data-ttu-id="6f8f1-121">[Konfigurowanie ustawień replikacji](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="6f8f1-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
