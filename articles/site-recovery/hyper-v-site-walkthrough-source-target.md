---
title: "aaaSet hello źródła i celu tooAzure replikacji funkcji Hyper-V (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji maszyn wirtualnych funkcji Hyper-V tooAzure magazynu z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Krok 8: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji funkcji Hyper-V

W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure maszyn wirtualnych (bez programu System Center VMM) funkcji Hyper-V, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Skonfigurować witrynę hello funkcji Hyper-V, zainstaluj hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Azure hello na hostach funkcji Hyper-V i Zarejestruj w magazynie hello hello lokacji.

1. W **przygotowanie infrastruktury**, kliknij przycisk **źródła**. tooadd nowej lokacji funkcji Hyper-V jako kontener dla hostów funkcji Hyper-V lub klastry, kliknij przycisk **+ lokacja funkcji Hyper-V**.

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. W **lokacji funkcji Hyper-V Utwórz**, określ nazwę lokacji hello. Następnie kliknij przycisk **OK**. Teraz, wybierz witrynę hello utworzone i kliknij **+ serwer funkcji Hyper-V** tooadd toohello serwera lokacji.

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. W **Dodaj serwer** > **typ serwera**, sprawdź, czy **serwera funkcji Hyper-V** jest wyświetlany.

    - Sprawdź, czy ten serwer hello funkcji Hyper-V ma spełnia tooadd hello [wymagania wstępne](#on-premises-prerequisites), i jest w stanie tooaccess hello określonych adresów URL.
    - Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello. Uruchom ten plik tooinstall hello dostawcy i hello agenta usług odzyskiwania na każdym hoście funkcji Hyper-V.

    ![Konfiguracja źródła](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Zainstaluj hello dostawca i agent

1. Uruchom plik Instalatora dostawcy hello na każdym hoście po dodaniu lokacji toohello funkcji Hyper-V. Jeśli instalujesz w klastrze funkcji Hyper-V, uruchom Instalatora na każdym węźle klastra. Instalowanie i rejestrowanie w każdym węźle klastra funkcji Hyper-V zapewnia ochronę maszyn wirtualnych, nawet w przypadku migrowania między węzłami.
2. W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.
3. W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślną lokalizację instalacji dostawcy i kliknij przycisk **zainstalować**.
4. W **ustawienia magazynu**, kliknij przycisk **Przeglądaj** tooselect hello magazynu kluczy pobranego pliku. Określ subskrypcję usługi Azure Site Recovery hello, hello nazwę magazynu, i należy serwer hello funkcji Hyper-V toowhich hello funkcji Hyper-V w lokacji.

    ![Rejestracja serwera](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. W **ustawienia serwera Proxy**, określ, jak dostawca uruchomiony na hostach funkcji Hyper-V łączy tooAzure usługi Site Recovery za pośrednictwem hello hello internet.

    * Jeśli chcesz tooconnect dostawcy hello bezpośrednio wybierz **łączą się bezpośrednio tooAzure odzyskiwania lokacji bez serwera proxy**.
    * Zaznacz, jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy dla połączenia z dostawcą hello **połączyć tooAzure Przywracanie lokacji z użyciem serwera proxy**.
    * Jeśli używasz serwera proxy:
        - Określ adres hello, port i poświadczenia
        - Upewnij się, że hello adresy URL opisane w hello [wymagania wstępne](#prerequisites) mogą za pośrednictwem serwera proxy hello.

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister powitania serwera w magazynie hello.

    ![Lokalizacja instalacji](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Po zakończeniu rejestracji metadane z serwera funkcji Hyper-V hello są pobierane przez usługę Azure Site Recovery, a powitania serwera są wyświetlane w **infrastruktura usługi Site Recovery** > **hosty funkcji Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Określ konto magazynu Azure hello replikacji, a hello toowhich sieć platformy Azure, maszyny wirtualne Azure będą się łączyć po pracy awaryjnej.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowej**.
2. Wybierz hello subskrypcji i grupy zasobów hello mają toocreate hello Azure maszyn wirtualnych po pracy awaryjnej. Wybierz wdrożenia hello modelu mają toouse na platformie Azure (Zarządzanie zasobu lub classic) dla hello maszyn wirtualnych.

3. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

    - Jeśli nie masz konta magazynu, kliknij przycisk **i magazyn** toocreate wbudowanego konta Menedżera zasobów. 
    - Jeśli nie masz sieć platformy Azure, kliknij przycisk **+ sieć** toocreate wbudowanego sieci przy użyciu usługi Resource Manager.






## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](hyper-v-site-walkthrough-replication.md)
