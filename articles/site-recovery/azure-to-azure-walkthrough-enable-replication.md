---
title: "Włącz replikację dla maszyn wirtualnych platformy Azure do innego regionu Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków należy włączyć replikację do innego regionu Azure dla maszyn wirtualnych platformy Azure przy użyciu usługi Azure Site Recovery"
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
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Krok 5: Włączanie replikacji maszyn wirtualnych Azure


Po skonfigurowaniu [magazyn usług odzyskiwania i](azure-to-azure-walkthrough-vault.md), użyj w tym artykule, aby włączyć replikację maszyn wirtualnych (VM) do innego regionu Azure, z [usługi Azure Site Recovery](site-recovery-overview.md). Aby włączyć replikację, należy skonfigurować ustawienia źródłowym i docelowym, sprawdź zasady replikacji, a następnie wybierz maszyny wirtualne mają być replikowane.

- Po zakończeniu tego artykułu, maszynach wirtualnych platformy Azure należy replikację do dodatkowej regionu Azure.
- Opublikuj wszelkie komentarze u dołu w tym artykule, lub zadać pytania w [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.


## <a name="select-the-source"></a>Wybierz źródło 

1. Magazyny usług odzyskiwania, kliknij nazwę magazynu > **+ Replikuj**.
2. W **źródła**, wybierz pozycję **Azure — wersja ZAPOZNAWCZA**.
2. W **lokalizacja źródłowa**, wybierz źródło region platformy Azure, w którym są uruchomione maszyny wirtualne.
3. Wybierz **modelu wdrażania maszyny wirtualnej platformy Azure** dla maszyn wirtualnych: **Resource Manager** lub **klasycznego**.
4. Wybierz **źródłowa grupa zasobów** dla maszyn wirtualnych Menedżera zasobów lub **usługi w chmurze** klasycznych maszyn wirtualnych.
5. Kliknij pozycję **OK**, aby zapisać ustawienia.

    ![Skonfiguruj źródło](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a>Wybierz maszyny wirtualne

Usługa Site Recovery pobiera listę maszyn wirtualnych, związanych z subskrypcji i zasobu grupy/usługa w chmurze.

1. W **maszyn wirtualnych**, wybierz maszyny wirtualne mają być replikowane.
2. Kliknij przycisk **OK**.

    ![Wybierz maszyny wirtualne](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Konfigurowanie ustawień

Przepisy odzyskiwania lokacji domyślne ustawienia dla region docelowy (zgodnie z ustawieniami region źródłowego), a zasady replikacji:

   - **Lokalizacja docelowa**: region docelowy, którego chcesz użyć do odzyskiwania po awarii. Zaleca się, że lokalizacja docelowa odpowiada lokalizacji magazynu usługi Site Recovery.
   - **Docelowa grupa zasobów**: grupy zasobów, do których maszynach wirtualnych platformy Azure w celu region będzie należał po pracy awaryjnej. Domyślnie usługi Site Recovery tworzy nową grupę zasobów w regionie docelowych z sufiksem "asr". 
   - **Wirtualne sieci docelowej**: sieci, na których maszynach wirtualnych Azure w celu region zostaną umieszczone po pracy awaryjnej. Domyślnie usługa Site Recovery tworzy nową sieć wirtualną (i podsieci) w regionie docelowych z sufiksem "asr". Ta sieć jest zamapowana na sieć źródła. Należy pamiętać, przypisanie określonego adresu IP po przejściu w tryb failover maszyny wirtualnej, jeśli chcesz zachować ten sam adres IP w lokalizacji źródłowej i docelowej. 
   - **Buforowanie kont magazynu**: Usługa Site Recovery używa konta magazynu w regionie źródła. Zmiany w źródłowe maszyny wirtualne są wysyłane do tego konta, przed replikacji do lokalizacji docelowej. 
   - **Docelowa kont magazynu**: Domyślnie, Usługa Site Recovery tworzy nowe konto magazynu, w obszarze docelowym dublowanego źródła konta magazynu maszyny Wirtualnej.
   -  **Docelowa zestawów dostępności**: Domyślnie, Usługa Site Recovery tworzy nowy zestawem dostępności w region docelowy, wraz z sufiksem "asr". 
   - **Nazwa zasad replikacji**: Nazwa zasad.
   - **Przechowywania punktu odzyskiwania**: domyślnie Site Recovery przechowuje punkty odzyskiwania przez 24 godziny. Można skonfigurować wartość z zakresu od 1 do 72 godzin.
   - **Częstotliwość migawek spójności aplikacji**: domyślnie Site Recovery przyjmuje migawki dotyczącej spójności aplikacji co 4 godziny. Można skonfigurować dowolną wartość z zakresu od 1 do 12 godzin. Dane są replikowane w sposób ciągły:
    - Punktów odzyskiwania zapewniających spójność awarii zachowania spójności danych zapisu kolejności podczas tworzenia. Ten rodzaj punktu odzyskiwania jest zwykle wystarczające, jeśli aplikacja jest przeznaczona Aby dokonać odzyskiwania po awarii bez niespójności w danych
    - Punktów odzyskiwania zapewniających spójność awarii są generowane co kilka minut. Przy użyciu tych punktów odzyskiwania w tryb failover i odzyskiwania maszyn wirtualnych zapewnia odzyskiwania punktu cel (RPO) kolejności minut.
    - Punktów odzyskiwania zapewniających spójność aplikacji (oprócz spójności zapisu kolejności) zapewnić ukończenie wszystkich operacji uruchomionych aplikacji i opróżnienia buforów na dysku (przełączany w stan spoczynku aplikacji). Firma Microsoft zaleca korzystanie z tych punktów odzyskiwania dla bazy danych aplikacji, takich jak SQL Server, Oracle i Exchange.
        
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Modyfikowanie ustawień

Jeśli chcesz zmodyfikować ustawienia zasad docelowych i replikacji, wykonaj następujące czynności:

1. Aby wyświetlić lub zmodyfikować ustawienia obiektu docelowego, kliknij przycisk **ustawienia**.
2. Aby zastąpić domyślne ustawienia docelowych, kliknij przycisk **Dostosuj**. Można określić docelowa grupa zasobów, sieć wirtualną, zestawu dostępności i docelowe konto magazynu. Zestawy dostępności można dodawać tylko, jeśli maszyny wirtualne są częścią zestawu w regionie źródła.

    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. Aby zastąpić ustawienia replikacji dla punktów odzyskiwania i migawek spójności aplikacji, kliknij przycisk **Dostosuj** obok **zasad replikacji**.
 
    ![Konfigurowanie ustawień](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. Aby rozpocząć Inicjowanie obsługi zasobów docelowych, kliknij **Utwórz zasoby docelowe**. Inicjowanie obsługi administracyjnej ma minuty. Nie zamykaj bloku podczas inicjowania obsługi lub należy zacząć od początku.




## <a name="enable-replication"></a>Włączanie replikacji

1. W **ustawienia**, kliknij przycisk **włączyć replikację**. Dzięki temu replikacji początkowej wybranych maszyn wirtualnych. Stan replikacji początkowej może potrwać pewien czas, aby odświeżyć. Kliknij przycisk **Odśwież** można pobrać najnowszy stan.

2. Możesz śledzić postęp **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.

3. W **ustawienia** > **elementy replikowane**, można wyświetlić stan maszyn wirtualnych i postęp replikacji początkowej. Kliknij maszynę Wirtualną, aby przejść do jego ustawień.



## <a name="next-steps"></a>Następne kroki

Przejdź do [krok 6: testować tryb failover](azure-to-azure-walkthrough-test-failover.md)
