---
title: "aaaEnable replikację dla maszyn wirtualnych platformy Azure tooanother region platformy Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello potrzebne tooenable replikacji tooanother region platformy Azure dla maszyn wirtualnych platformy Azure przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Krok 5: Włączanie replikacji maszyn wirtualnych Azure


Po skonfigurowaniu [magazyn usług odzyskiwania i](azure-to-azure-walkthrough-vault.md), za pomocą tego artykułu replikacji tooenable maszyn wirtualnych (VM), tooanother regionu Azure, [usługi Azure Site Recovery](site-recovery-overview.md). tooenable replikacji, należy skonfigurować ustawienia źródłowym i docelowym, sprawdź hello zasad replikacji, a następnie wybierz maszyny wirtualne mają tooreplicate.

- Po zakończeniu hello artykułu, maszynach wirtualnych platformy Azure powinna być replikacja toohello dodatkowej region platformy Azure.
- Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.


## <a name="select-hello-source"></a>Wybierz źródło hello 

1. Magazyny usług odzyskiwania, kliknij nazwę magazynu hello > **+ Replikuj**.
2. W **źródła**, wybierz pozycję **Azure — wersja ZAPOZNAWCZA**.
2. W **lokalizacja źródłowa**, wybierz źródło hello region platformy Azure, w którym są uruchomione maszyny wirtualne.
3. Wybierz hello **modelu wdrażania maszyny wirtualnej platformy Azure** dla maszyn wirtualnych: **Resource Manager** lub **klasycznego**.
4. Wybierz hello **źródłowa grupa zasobów** dla maszyn wirtualnych Menedżera zasobów lub **usługi w chmurze** klasycznych maszyn wirtualnych.
5. Kliknij przycisk **OK** toosave hello ustawienia.

    ![Konfigurowanie źródła hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Wybierz hello maszyny wirtualne

Usługa Site Recovery pobiera listę hello maszyn wirtualnych z którą skojarzona hello subskrypcji i zasobu grupy/usługa w chmurze.

1. W **maszyn wirtualnych**, wybierz hello maszyny wirtualne mają tooreplicate.
2. Kliknij przycisk **OK**.

    ![Wybierz maszyny wirtualne](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Konfigurowanie ustawień

Domyślne ustawienia dla region docelowy hello (na podstawie hello źródła region ustawień), udostępnia usługi Site Recovery i zasad replikacji hello:

   - **Lokalizacja docelowa**: hello region docelowy ma toouse odzyskiwania po awarii. Firma Microsoft zaleca zgodność hello lokalizację magazynu usługi Site Recovery hello hello lokalizacji docelowej.
   - **Docelowa grupa zasobów**: toowhich grupy zasobów maszyn wirtualnych Azure w region docelowy hello będą należeć po pracy awaryjnej. Domyślnie usługi Site Recovery tworzy nową grupę zasobów w regionie docelowym hello z sufiksem "asr". 
   - **Wirtualne sieci docelowej**: hello sieci, na których maszynach wirtualnych Azure w hello region docelowy zostaną umieszczone po pracy awaryjnej. Domyślnie usługa Site Recovery tworzy nową sieć wirtualną (i podsieci) region docelowy hello z sufiksem "asr". Ta sieć jest siecią źródła tooyour mapowane. Należy pamiętać, że po przejściu w tryb failover maszyny wirtualnej można przypisać określony adres IP, jeśli potrzebujesz tooretain hello sam adres IP w lokalizacji źródłowej i docelowej hello. 
   - **Buforowanie kont magazynu**: Usługa Site Recovery używa konta magazynu w regionie źródła hello. Zmiany dotyczące źródłowe maszyny wirtualne będą wysyłane konta toothis przed lokalizacji docelowej toohello replikacji. 
   - **Docelowa kont magazynu**: Domyślnie, Usługa Site Recovery tworzy nowe konto magazynu w regionie docelowym hello, toomirror hello źródła konta magazynu maszyny Wirtualnej.
   -  **Docelowa zestawów dostępności**: Domyślnie, Usługa Site Recovery tworzy nowy zestawem dostępności w hello region docelowy, z sufiksem "asr" hello. 
   - **Nazwa zasad replikacji**: Nazwa zasad.
   - **Przechowywania punktu odzyskiwania**: domyślnie Site Recovery przechowuje punkty odzyskiwania przez 24 godziny. Można skonfigurować wartość z zakresu od 1 do 72 godzin.
   - **Częstotliwość migawek spójności aplikacji**: domyślnie Site Recovery przyjmuje migawki dotyczącej spójności aplikacji co 4 godziny. Można skonfigurować dowolną wartość z zakresu od 1 do 12 godzin. Dane są replikowane w sposób ciągły:
    - Punktów odzyskiwania zapewniających spójność awarii zachowania spójności danych zapisu kolejności podczas tworzenia. Ten rodzaj punktu odzyskiwania jest zwykle wystarczające, jeśli aplikacja jest zaprojektowana toorecover z awarii bez niespójności danych
    - Punktów odzyskiwania zapewniających spójność awarii są generowane co kilka minut. Przy użyciu tych toofail punkty odzyskiwania przez i odzyskiwanie maszyn wirtualnych zapewnia odzyskiwania punktu cel (RPO) w kolejności hello minut.
    - Punktów odzyskiwania zapewniających spójność aplikacji (w spójności kolejności toowrite dodanie) zapewnić ukończenie wszystkich operacji uruchomionych aplikacji i opróżnienia buforów toodisk (przełączany w stan spoczynku aplikacji). Firma Microsoft zaleca korzystanie z tych punktów odzyskiwania dla bazy danych aplikacji, takich jak SQL Server, Oracle i Exchange.
        
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Modyfikowanie ustawień

Jeśli chcesz, aby ustawienia zasad replikacji i docelowe toomodify, hello następujące:

1. tooview lub zmodyfikować ustawienia obiektu docelowego, kliknij przycisk **ustawienia**.
2. toooverride hello domyślne ustawień obiektu docelowego, kliknij przycisk **Dostosuj**. Można określić docelowa grupa zasobów, sieć wirtualną, zestawu dostępności i docelowe konto magazynu. Zestawy dostępności można dodawać tylko, jeśli maszyny wirtualne są częścią zestawu w regionie źródła hello.

    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. ustawienia replikacji toooverride punktów odzyskiwania oraz migawki spójne z aplikacjami, kliknij przycisk **Dostosuj** dalej zbyt**zasad replikacji**.
 
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. toostart inicjowania obsługi administracyjnej hello zasobów docelowych, kliknij przycisk **Utwórz zasoby docelowe**. Inicjowanie obsługi administracyjnej ma minuty. Nie zamykaj bloku hello podczas inicjowania obsługi lub toostart będziesz mieć za pośrednictwem.




## <a name="enable-replication"></a>Włączanie replikacji

1. W **ustawienia**, kliknij przycisk **włączyć replikację**. Dzięki temu replikacji początkowej hello wybranych maszyn wirtualnych. Stan replikacji początkowej może potrwać kilka toorefresh czas. Kliknij przycisk **Odśwież** tooget hello najnowszy stan.

2. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.

3. W **ustawienia** > **elementy replikowane**, można wyświetlić stan hello maszyn wirtualnych i hello postęp replikacji początkowej. Kliknij przycisk hello toodrill maszyny Wirtualnej w dół do jego ustawień.



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 6: testować tryb failover](azure-to-azure-walkthrough-test-failover.md)
