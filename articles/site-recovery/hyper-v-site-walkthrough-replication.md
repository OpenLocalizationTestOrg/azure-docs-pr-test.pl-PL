---
title: "aaaSet się zasady replikacji dla maszyny Wirtualnej funkcji Hyper-V tooAzure replikacji (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooset się zasady replikacji podczas replikowania maszyn wirtualnych funkcji Hyper-V tooAzure magazynu"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Krok 9: Konfigurowanie zasady replikacji w przypadku tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V

W tym artykule opisano sposób tooset się zasady replikacji w przypadku replikacji tooAzure maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.


Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Temat migawek

Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie.
    - Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki.
    - Włącz migawki spójne z aplikacjami, wpłynie na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.

## <a name="set-up-a-replication-policy"></a>Konfigurowanie zasad replikacji

1. Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.

    ![Sieć](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.
3. W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).

    > [!NOTE]
    > 30 częstotliwość drugiego nie jest obsługiwane podczas replikowania toopremium magazynu. ograniczenie Hello jest określana przez hello liczby migawek dla obiekt blob (w 100) obsługiwane przez Magazyn w warstwie premium. [Dowiedz się więcej](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo jest hello okna przechowywania dla każdego punktu odzyskiwania. Maszyny wirtualne mogą zostać odzyskane tooany punktu, w tym oknie.
5. W **częstotliwość migawek spójności aplikacji**, określ, jak często (1 – 12 godzin) punkty odzyskiwania zawierające migawki spójne z aplikacjami są tworzone.
6. W **czas rozpoczęcia replikacji początkowej**, określ, kiedy toostart hello replikacji początkowej. Hello replikacja odbywa się za pośrednictwem przepustowości połączenia z Internetem, może być tooschedule ją poza najbardziej obciążonymi godzinami. Następnie kliknij przycisk **OK**.

    ![Zasady replikacji](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Podczas tworzenia nowych zasad, zostaną one automatycznie skojarzone z hello lokacji funkcji Hyper-V. Można skojarzyć z wieloma zasadami replikacji w lokacji funkcji Hyper-V (i hello maszyn wirtualnych w nim) **replikacji** > Nazwa zasady > **skojarzyć lokacji funkcji Hyper-V**.



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 10: Włączanie replikacji](hyper-v-site-walkthrough-enable-replication.md)
