---
title: "Mapowanie sieci aaaConfigure replikowania maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure mapowania sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Krok 9: Konfigurowanie mapowania sieci dla funkcji Hyper-V tooAzure replikacji (w programie VMM)

Po skonfigurowaniu hello [źródłowa i docelowa ustawień replikacji](vmm-to-azure-walkthrough-source-target.md), użyj tego artykułu tooconfigure sieci mapowania toomap między sieciami maszyn wirtualnych VMM lokalnych i sieci platformy Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Przed rozpoczęciem

- Dowiedz się więcej o [mapowania sieci](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [Przygotowanie programu VMM do mapowania sieci](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Sprawdź, czy maszyny wirtualne na serwerze VMM hello tooa połączonych sieci maszyny Wirtualnej i czy utworzono przynajmniej jedną sieć wirtualną platformy Azure. Wiele sieci Vmnetwork może być zmapowane tooa pojedynczej sieci platformy Azure.

## <a name="configure-mapping"></a>Skonfiguruj mapowanie

Skonfiguruj mapowanie w następujący sposób:

1. W **infrastruktura usługi Site Recovery** > **mapowania sieci** > **mapowanie sieci**, kliknij przycisk hello **+ mapowanie sieci**  ikony.

    ![Mapowanie sieci](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. W **Dodaj mapowanie sieci**, wybierz pozycję hello źródłowy serwer VMM i **Azure** jako cel hello.
3. Sprawdź hello subskrypcji i modelu wdrażania powitania po pracy awaryjnej.
4. W **Sieć źródłowa**, wybierz pozycję hello źródłowej lokalnej sieci maszyny Wirtualnej ma toomap z listy hello skojarzone z serwerem VMM hello.
5. W **Sieć docelowa**, wybierz hello sieć platformy Azure, w którym replika Azure zostaną umieszczone podczas są tworzone. Następnie kliknij przycisk **OK**.

    ![Mapowanie sieci](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Oto, co się dzieje po rozpoczęciu mapowania sieci:

* Istniejące maszyny wirtualne w źródłowej sieci maszyny Wirtualnej hello są toohello połączonych sieci docelowej po rozpoczęciu mapowania. Nowych maszyn wirtualnych połączonych toohello źródłowej sieci maszyny Wirtualnej są połączone toohello mapowane sieć platformy Azure, podczas replikacji.
* Jeśli zmodyfikujesz istniejące mapowanie sieci maszyn wirtualnych repliki Połącz przy użyciu nowych ustawień hello.
* Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie maszyny wirtualnej repliki hello łączy toothat docelowej podsieci po pracy awaryjnej.
* Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello łączy toohello pierwszej podsieci w sieci hello.



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 10: Tworzenie zasad replikacji](vmm-to-azure-walkthrough-replication.md)
