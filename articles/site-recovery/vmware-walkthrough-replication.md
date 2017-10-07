---
title: "aaaSet się zasady replikacji dla maszyny Wirtualnej VMware tooAzure replikacji z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się zasady replikacji podczas replikowania maszyn wirtualnych VMware tooAzure magazynu"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>Krok 9: Konfigurowanie zasad replikacji dla maszyny Wirtualnej VMware tooAzure replikacji


W tym artykule opisano sposób tooset się zasady replikacji w przypadku replikacji maszyn wirtualnych VMware tooAzure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.


Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Konfigurowanie zasad

Uzyskać szybkie omówienie wideo, przed rozpoczęciem:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Kliknij przycisk toocreate nowe zasady replikacji, **infrastruktura usługi Site Recovery** > **zasady replikacji** > **+ zasad replikacji**.
2. W **Utwórz zasady replikacji**, określ nazwę zasady.
3. W **próg RPO**, określ hello RPO limit. Ta wartość określa, jak często są tworzone punkty odzyskiwania danych. Alert jest generowany, gdy ciągłej replikacji przekracza ten limit.
4. W **przechowywania punktu odzyskiwania**, określ czas (w godzinach) jest hello okna przechowywania dla każdego punktu odzyskiwania. Replikowane maszyny wirtualne można odzyskać punktu tooany w oknie. Zapasowej too24 godzin przechowywania jest obsługiwana dla maszyn replikowane toopremium magazynu i 72 godziny dla magazynu w warstwie standardowa.
5. W **częstotliwość migawek spójności aplikacji**, określ częstotliwość (w minutach) będą tworzone punkty odzyskiwana zawierające migawki spójne z aplikacjami. Kliknij przycisk **OK** toocreate hello zasad.

    ![Zasady replikacji](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Podczas tworzenia nowej zasady zostaną one automatycznie skojarzone z serwerem konfiguracji hello. Domyślnie zasady uzgadniania jest tworzony automatycznie powrotu po awarii. Na przykład jeśli hello zasad replikacji jest **rep zasad** będzie zasady powrotu po awarii hello **rep zasad-powrotu po awarii**. Ta zasada nie jest używany, dopiero po zainicjowaniu powrotu po awarii z platformy Azure.

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 10: zainstalować usługi mobilności hello](vmware-walkthrough-install-mobility.md)
