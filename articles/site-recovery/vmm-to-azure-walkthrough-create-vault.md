---
title: "aaaSet się magazynu dla funkcji Hyper-V tooAzure replikacji (z programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooset się magazynu dla funkcji Hyper-V tooAzure replikacji (w programie VMM) przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Krok 7: Konfigurowanie magazynu dla replikacji funkcji Hyper-V

W tym artykule opisano sposób tooset Konfigurowanie magazynu i określ sposób tooreplicate z lokalizacji lokalnej, za pomocą hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.


Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Wybierz cel ochrony

Wybierz, co ma tooreplicate, i miejsce tooreplicate do.

1. Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.
2. W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.
3. W **cel ochrony**, wybierz pozycję **tooAzure** > **tak, z funkcją Hyper-V**. Wybierz **tak** tooconfirm jesteś %1./nOdnosi VMM. 

     ![Wybieranie celów](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 8: Konfigurowanie źródłowa i docelowa](vmm-to-azure-walkthrough-source-target.md)
