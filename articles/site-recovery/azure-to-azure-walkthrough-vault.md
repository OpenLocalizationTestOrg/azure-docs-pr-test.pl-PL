---
title: "aaaSet się magazynu dla maszyny Wirtualnej Azure repliction między regionami z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się magazynu Azure replikacji między regiony platformy Azure przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Krok 4: Konfigurowanie magazynu Azure tooAzure replikacji

Po [Planowanie sieci](azure-to-azure-walkthrough-network.md), użyj tego tooset artykułu zapasowej magazynu, maszyn wirtualnych platformy Azure (maszyny wirtualne) replikowanie tooanother region platformy Azure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

- Po zakończeniu artykułu hello powinny mieć Konfigurowanie magazynu usług odzyskiwania.
- Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.




## <a name="create-a-vault"></a>Tworzenie magazynu

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Zaleca się tworzenie magazynu usług odzyskiwania hello w hello lokalizację tooreplicate sieci maszyn wirtualnych. Na przykład, jeśli w lokalizacji docelowej jest hello centralnego nam, utwórz magazyn hello w **środkowe stany USA**.


## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 5: Włączanie replikacji](azure-to-azure-walkthrough-enable-replication.md)
