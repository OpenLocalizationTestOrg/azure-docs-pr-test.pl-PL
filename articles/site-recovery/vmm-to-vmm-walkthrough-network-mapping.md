---
title: "aaaMap sieci dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toomap sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Krok 7: Mapowanie sieci dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V


Po skonfigurowaniu [ustawienia źródłowe i docelowe](vmm-to-vmm-walkthrough-source-target.md) replikację funkcji Hyper-V maszynach wirtualnych (VM) tooa System Center Virtual Machine Manager (VMM) lokacji dodatkowej, użyć tego mapowania artykułu tooconfigure sieci wirtualnej funkcji Hyper-v Maszyna wirtualna replikacji tooa dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

- Dowiedz się więcej o [mapowania sieci](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) przed jego uruchomieniem.
- Sprawdź, czy maszyny wirtualne na serwerach VMM są połączone tooa sieci maszyny Wirtualnej.

## <a name="configure-network-mapping"></a>Konfiguracja mapowania sieci

1. W **mapowanie sieci** > **mapowania sieci**, kliknij przycisk **+ mapowanie sieci**.
2. W **Dodaj mapowanie sieci** , wybierz źródło hello i VMM serwery docelowe. Witaj sieci maszyny Wirtualnej skojarzone z serwerów VMM hello są pobierane.
3. W **Sieć źródłowa**, wybierz sieć hello ma toouse z listy hello sieci maszyny Wirtualnej skojarzone z hello podstawowy serwer VMM.
4. W **Sieć docelowa**, wybierz sieć hello ma toouse na powitania pomocniczy serwer programu VMM. Następnie kliknij przycisk **OK**.

    ![Mapowanie sieci](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Oto, co się dzieje po rozpoczęciu mapowania sieci:

* Wszystkie istniejące maszyny wirtualne repliki odpowiadające źródłowej sieci maszyny Wirtualnej toohello będzie sieć maszyny Wirtualnej podłączonej toohello docelowej.
* Nowe maszyny wirtualne, które są połączone toohello źródłowej sieci maszyny Wirtualnej będzie mapowanej sieci docelowej połączonych toohello po replikacji.
* Jeśli zmodyfikujesz istniejące mapowanie, uwzględniając nową sieć maszyn wirtualnych repliki zostaną podłączone z wykorzystaniem nowych ustawień hello.
* Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.



## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 8: Skonfiguruj zasady replikacji](vmm-to-vmm-walkthrough-replication.md).
