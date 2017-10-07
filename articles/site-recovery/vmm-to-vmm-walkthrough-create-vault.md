---
title: "aaaCreate magazynu dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate magazynu podczas replikowania maszyn wirtualnych funkcji Hyper-V tooa, lokacji dodatkowej programu System Center VMM, z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Krok 5: Tworzenie magazynu dla lokacji dodatkowej tooa replikacji funkcji Hyper-V

Po przygotowaniu lokalnymi [programu System Center Virtual Machine Manager (VMM) serwerów i klastrów hostów Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) dla funkcji Hyper-V replikacji tooa dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md), można utworzyć Magazyn usług odzyskiwania i wybierz hello scenariusza replikacji.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Wybierz cel ochrony

Wybierz, co ma tooreplicate i miejscu tooreplicate do.

1. Kliknij przycisk **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury** > **cel ochrony**.
2. Wybierz **lokacji toorecovery**i wybierz **tak, z funkcją Hyper-V**.
3. Wybierz **tak** tooindicate używasz hostów funkcji Hyper-V hello toomanage programu VMM.
4. Wybierz **tak** Jeśli pomocniczy serwer programu VMM. Jeśli wdrażasz replikacji między chmurami na jednym serwerze programu VMM, kliknij przycisk **nr**. Następnie kliknij przycisk **OK**.

    ![Wybieranie celów](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 6: Konfigurowanie hello replikacji źródłowa i docelowa](vmm-to-vmm-walkthrough-source-target.md).
