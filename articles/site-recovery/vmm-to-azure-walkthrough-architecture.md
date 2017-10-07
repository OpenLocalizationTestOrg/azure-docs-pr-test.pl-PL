---
title: "Architektura hello aaaReview dla funkcji Hyper-V tooAzure replikacji (z programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie składników i architektura używana podczas replikowania lokalnych maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM, przy użyciu usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: ee1f2775b0c929894933b639464176d7a0441519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture"></a>Krok 1: Przegląd architektury hello


W tym artykule opisano składniki hello i procesy używane podczas replikowania lokalnych maszyn wirtualnych funkcji Hyper-V w chmurach programu System Center Virtual Machine Manager (VMM), przy użyciu hello tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Opublikuj wszelkie komentarze u dołu hello tego artykułu lub hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Składniki architektury

Istnieje wiele składników związanych podczas replikowania maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM.

**Składnik** | **Wymaganie** | **Szczegóły**
--- | --- | ---
**Azure** | W przypadku platformy Azure konieczne jest posiadanie konta platformy Microsoft Azure, konta usługi Azure Storage i sieci platformy Azure. | Replikowane dane są przechowywane na koncie magazynu hello i maszyn wirtualnych platformy Azure są tworzone z danymi hello replikowane czasie pracy awaryjnej z lokacji lokalnej.<br/><br/> Hello maszynach wirtualnych platformy Azure połączyć toohello sieci wirtualnej platformy Azure, gdy są tworzone.
**Serwer VMM** | Serwer VMM Hello ma co najmniej jedną chmurę zawierających hosty funkcji Hyper-V. | Na serwerze VMM hello instalowanie hello dostawcy usługi Site Recovery tooorchestrate replikacji przy użyciu usługi Site Recovery i Zarejestruj serwer hello w powitalne magazyn usług odzyskiwania.
**Host funkcji Hyper-V** | Co najmniej jeden host/klaster funkcji Hyper-V zarządzany przez program VMM. |  Należy zainstalować agenta usług odzyskiwania hello w każdym członku klastra lub hosta.
**Maszyny wirtualne funkcji Hyper-V** | Co najmniej jedna maszyna wirtualna uruchomiona na serwerze hosta funkcji Hyper-V. | Nic nie musi tooexplicitly zainstalowanych na maszynach wirtualnych.
**Sieć** |Logiczne i sieci maszyny Wirtualnej, skonfiguruj na powitania serwera VMM. Sieć maszyny Wirtualnej powinny być połączone tooa sieci logicznej, która ma powiązanego z chmurą hello. | Sieci maszyn wirtualnych są tooAzure mapowanej sieci wirtualnych, aby maszynach wirtualnych platformy Azure znajdują się w sieci, gdy są tworzone po pracy awaryjnej.

Dowiedz się więcej o wymaganiach wstępnych dotyczących wdrożenia hello i wymagania dla każdego z tych składników w hello [macierz obsługi](site-recovery-support-matrix-to-azure.md).


**Rysunek 1: Replikowanie maszyn wirtualnych na hostach funkcji Hyper-V w tooAzure chmury VMM**

![Składniki](./media/vmm-to-azure-walkthrough-architecture/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Proces replikacji

**Rysunek 2: Proces replikacji i odzyskiwania dla tooAzure replikacji funkcji Hyper-V**

![przepływ pracy](./media/vmm-to-azure-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Włączanie ochrony

1. Po włączeniu ochrony dla maszyny Wirtualnej funkcji Hyper-V w hello portalu Azure lub lokalnie, hello **Włącz ochronę** uruchamia.
2. Witaj zadanie sprawdza, czy maszyna hello spełnia wymagania wstępne, przed wywołaniem hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset replikacji z ustawieniami hello skonfigurowano.
3. zadanie Hello rozpoczyna się Replikacja początkowa wywołując hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) — metoda, tooinitialize Pełna replikacja maszyny Wirtualnej i wysyłania hello wirtualna tooAzure dysków wirtualnych.
4. Można monitorować zadanie hello w hello **zadania** kartę.      ![Lista zadań](media/vmm-to-azure-walkthrough-architecture/image1.png) ![Szczegóły zadania Włącz ochronę](media/vmm-to-azure-walkthrough-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Replikacji początkowej danych hello

1. Po wyzwoleniu replikacji początkowej tworzona jest [migawka maszyny wirtualnej funkcji Hyper-V](https://technet.microsoft.com/library/dd560637.aspx).
2. Wirtualne dyski twarde są replikowane pojedynczo, dopóki nie są one wszystkich skopiowanych tooAzure. Go może potrwać kilka minut w zależności od hello rozmiar maszyny Wirtualnej, a przepustowość sieci. toooptimize użycie sieci, zobacz [jak toomanage lokalnymi użycia przepustowości sieci ochrony tooAzure](https://support.microsoft.com/kb/3056159).
3. Jeśli zmiany dysku są wykonywane, gdy Replikacja początkowa jest w toku, hello Tracker replikacji repliki funkcji Hyper-V będzie śledził te zmiany jako dzienniki replikacji funkcji Hyper-V (hrl). Te pliki znajdują się w hello tym samym folderze co dyski hello. Każdy dysk ma skojarzony plik hrl wysyłanej toosecondary magazynu.
4. Witaj pliki migawki i dziennika zużywają zasoby dysku w trakcie replikacji początkowej.
5. Po zakończeniu replikacji początkowej hello, hello migawki maszyny Wirtualnej jest usuwana. Przyrostowe zmiany dysków w dzienniku hello są zsynchronizowane i scalone toohello dysku nadrzędnego.


### <a name="finalize-protection"></a>Finalizowanie ochrony

1. Po replikacji początkowej hello zakończeniu hello **Finalizuj ochronę na maszynie wirtualnej hello** zadania konfiguruje ustawienia sieciowe i inne ustawienia po replikacji, aby hello maszyna wirtualna jest chroniona.
    ![Zadanie Finalizuj ochronę](media/vmm-to-azure-walkthrough-architecture/image3.png)
2. Jeśli replikujesz tooAzure, może być konieczne tootweak hello ustawień dla maszyny wirtualnej hello tak, aby była gotowa do pracy awaryjnej. W tym momencie możesz uruchomić test toocheck trybu failover, który wszystko działa zgodnie z oczekiwaniami.

### <a name="replicate-hello-delta"></a>Replikowanie hello delta

1. Po replikacji początkowej hello synchronizacja przyrostowa rozpoczyna się, zgodnie z ustawieniami replikacji.
2. Witaj Tracker replikacji repliki funkcji Hyper-V śledzi hello zmiany tooa wirtualnego dysku twardego jako pliki hrl. Z każdym dyskiem skonfigurowanym pod kątem replikacji jest skojarzony plik hrl. Ten dziennik jest wysyłany konta magazynu toohello klienta po zakończeniu replikacji początkowej. Kiedy dziennika tooAzure przesyłania, hello zmiany dysku podstawowego hello są śledzone w innym pliku dziennika, w hello tego samego katalogu.
3. Podczas replikacji początkowej i różnicowych można monitorować hello maszyny Wirtualnej w hello widok maszyny Wirtualnej. [Dowiedz się więcej](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Synchronizowanie replikacji

1. Jeśli replikacja różnicowa nie powiedzie się, a pełna replikacja byłaby kosztowna pod względem przepustowości lub czasu, maszyna wirtualna jest oznaczana do ponownej synchronizacji. Na przykład jeśli pliki hrl będą zajmować hello dostępu 50% rozmiaru dysku hello, następnie hello maszyny Wirtualnej zostaną oznaczone ponownej synchronizacji.
2.  Ponowna synchronizacja minimalizuje hello ilość danych przesyłanych przez obliczaniu sum kontrolnych hello źródłowych i docelowych maszyn wirtualnych oraz wysyłaniu tylko danych różnicowych hello. Ponowna synchronizacja używa algorytmu dzielenia na fragmenty o stałym bloku. Za jego pomocą pliki źródłowe i docelowe są dzielone na stałe fragmenty. Sumy kontrolne dla każdego fragmentu są generowane, a następnie porównuje toodetermine, która blokuje z miejsca docelowego hello źródła potrzeby toobe toohello zastosowane.
3. Po ukończeniu ponownej synchronizacji replikacja różnicowa powinna zostać wznowiona. Domyślnie ponowna synchronizacja jest zaplanowane toorun automatycznie poza godzinami pracy, ale możesz ponownie ręcznie zsynchronizować maszyny wirtualnej. Na przykład możesz wznowić ponowną synchronizację, jeśli wystąpi awaria sieci lub inna awaria. toodo, wybierz opcję hello maszyny Wirtualnej w portalu hello > **ponownie zsynchronizować**.

    ![Ręczna ponowna synchronizacja](media/vmm-to-azure-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a>Logika ponowień

Jeśli wystąpi błąd replikacji, może zostać użyty wbudowany mechanizm ponawiania. Tę logikę można podzielić na dwie kategorie:

**Kategoria** | **Szczegóły**
--- | ---
**Błąd nieodwracalny** | Nie jest podejmowana próba ponowienia. Maszyna wirtualna będzie mieć stan **Krytyczny** i będzie wymagana interwencja administratora. Przykłady te błędy: przerwany łańcuch wirtualnego dysku twardego; Nieprawidłowy stan dla repliki hello wirtualna; Błędy uwierzytelnianie sieciowe: błędy autoryzacji; Maszyna wirtualna nie znaleziono błędy (w przypadku autonomicznych serwerów funkcji Hyper-V)
**Błędy odwracalne** | Wykonywane co interwał replikacji, przy użyciu wykładniczej wycofania zwiększającą interwał ponawiania prób powitania od początku hello hello pierwsza próba 1, 2, 4, 8, a następnie 10 minut. Jeśli błąd będzie się powtarzać, ponowne próby będą wykonywane co 30 minut. Są to na przykład błędy sieci, błędy małej ilości miejsca na dysku i warunki małej ilości pamięci |



## <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

1. Można uruchomić planowane lub nieplanowane [pracy awaryjnej](site-recovery-failover.md) z lokalnymi tooAzure maszyn wirtualnych funkcji Hyper-V. Jeśli realizacja planowanego trybu failover, a następnie źródłowe maszyny wirtualne są zamknięte tooensure bez utraty danych.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md) tooorchestrate pracy w trybie failover wiele maszyn.
4. Po uruchomieniu trybu failover hello należy hello toosee można utworzyć repliki maszyn wirtualnych na platformie Azure. W razie potrzeby można przypisać publicznego toohello adres IP maszyny Wirtualnej.
5. Można następnie przekazać hello toostart trybu failover podczas uzyskiwania dostępu do obciążenia hello z hello repliki maszyny Wirtualnej platformy Azure.
6. Po ponownym udostępnieniu lokalnej lokacji głównej można do niej [powrócić po awarii](site-recovery-failback-from-azure-to-hyper-v.md). Należy rozpocząć poza planowanego trybu failover z lokacji głównej toohello platformy Azure. Dla planowanego trybu failover, można toohello wybierz toofailback tej samej maszyny Wirtualnej lub tooan alternatywnej lokalizacji i zsynchronizować zmiany między Azure i lokalnego, tooensure bez utraty danych. Po utworzeniu lokalnych maszyn wirtualnych należy zatwierdzić hello trybu failover.




## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 2: Przejrzyj wymagania wstępne dotyczące wdrażania hello](vmm-to-azure-walkthrough-prerequisites.md)
