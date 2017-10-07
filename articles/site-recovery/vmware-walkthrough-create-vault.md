---
title: "aaaSet się magazynu dla VMware tooAzure replikacji przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooset się magazynu dla VMware tooAzure replikacji przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>Krok 7: Konfigurowanie magazynu dla tooAzure replikacji VMware


W tym artykule opisano sposób tooset Konfigurowanie magazynu i określ sposób tooreplicate z lokalizacji lokalnej, za pomocą hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.


Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Wybierz cel ochrony

Wybierz, co ma tooreplicate, i miejsce tooreplicate do.

1. Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.
2. W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.
3. W **cel ochrony**, wybierz pozycję **tooAzure** > **tak, z programem VMware vSphere Hypervisor**.



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 8: Konfigurowanie źródłowa i docelowa](vmware-walkthrough-source-target.md)
