---
title: "aaaHow wykonuje pracę tooAzure replikacji funkcji Hyper-V w usłudze Site Recovery? | Microsoft Docs"
description: "Ten artykuł zawiera omówienie sposobu działania replikacji funkcji Hyper-V w usłudze Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Jak działa tooAzure replikacji funkcji Hyper-V?

Przeczytaj ten artykuł toounderstand hello architektury i przepływy pracy dotyczące tooAzure replikacji funkcji Hyper-V za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Opublikuj wszelkie komentarze u dołu hello tego artykułu lub hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Można replikować powitania po tooAzure:
- **Funkcja Hyper-V z programem VMM**: Maszyny wirtualne znajdujące się na lokalnych hostach funkcji Hyper-V zarządzanych w chmurach programu System Center Virtual Machine Manager (VMM). Na hostach może działać dowolny [obsługiwany system operacyjny](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Replikować możesz maszyny wirtualne funkcji Hyper-V, na których działa dowolny system operacyjny gościa [obsługiwany przez funkcję Hyper-V i platformę Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).
- **Funkcja Hyper-V bez programu VMM**: Lokalne maszyny wirtualne znajdujące się na hostach funkcji Hyper-V, które nie są zarządzane w chmurach programu VMM. Hostów można uruchomić dowolną hello [obsługiwanych systemów operacyjnych](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Replikować możesz maszyny wirtualne funkcji Hyper-V, na których działa dowolny system operacyjny gościa [obsługiwany przez funkcję Hyper-V i platformę Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="architectural-components"></a>Składniki architektury

**Obszar** | **Składnik** | **Szczegóły**
--- | --- | ---
**Azure** | W przypadku platformy Azure konieczne jest posiadanie konta platformy Microsoft Azure, konta usługi Azure Storage i sieci platformy Azure. | Konta magazynu i sieci mogą być kontami opartymi na usłudze Resource Manager lub kontami klasycznymi.<br/><br/> Replikowane dane są przechowywane na koncie magazynu hello i maszyn wirtualnych platformy Azure są tworzone z danymi hello replikowane czasie pracy awaryjnej z lokacji lokalnej.<br/><br/> Hello maszynach wirtualnych platformy Azure połączyć toohello sieci wirtualnej platformy Azure, gdy są tworzone.
**Serwer VMM** | Hosty funkcji Hyper-V znajdujące się w chmurach programu VMM | Jeśli hosty funkcji Hyper-V są zarządzane w chmurach programu VMM, należy zarejestrować serwer VMM hello w powitalne magazyn usług odzyskiwania.<br/><br/> Na serwerze VMM hello zainstalowaniu hello dostawcy usługi Site Recovery tooorchestrate replikacji z platformy Azure.<br/><br/> Należy logiczne i sieci maszyn wirtualnych skonfigurowanie mapowania sieci tooconfigure. Sieć maszyny Wirtualnej powinny być połączone tooa sieci logicznej, która ma powiązanego z chmurą hello.
**Host funkcji Hyper-V** | Serwery funkcji Hyper-V można wdrożyć z użyciem serwera VMM lub bez niego. | Jeśli serwer VMM nie jest, hello dostawcy usługi Site Recovery jest zainstalowany na powitania hosta tooorchestrate replikacji z usługą Site Recovery za pośrednictwem hello internet. W przypadku serwera programu VMM, hello dostawca jest zainstalowany na nim, a nie na powitania hosta.<br/><br/> agent usług odzyskiwania Hello jest zainstalowany na powitania hosta toohandle danych replikacji.<br/><br/> Komunikacja z hello dostawca i hello agent jest bezpieczna i szyfrowana. Zreplikowane dane w usłudze Azure Storage również są szyfrowane.
**Maszyny wirtualne funkcji Hyper-V** | Należy na serwerze hosta funkcji Hyper-V hello przynajmniej jednej maszyny wirtualnej. | Nic nie wymaga tooexplicitly zainstalowanych na maszynach wirtualnych

## <a name="deployment-steps"></a>Kroki wdrażania

1. **Azure**: skonfigurowaniu hello Azure składników. Przed rozpoczęciem wdrażania usługi Site Recovery zaleca się skonfigurowanie kont magazynu i sieci.
2. **Magazyn**: Utwórz magazyn usługi Recovery Services na potrzeby usługi Site Recovery i skonfiguruj ustawienia magazynu, co obejmuje skonfigurowanie ustawień źródła i celu, skonfigurowanie zasad replikacji i włączenie replikacji.
3. **Źródło i cel**:
    - **Hosty funkcji Hyper-V w chmurach VMM**: W ramach określania ustawień źródła, można pobrać i zainstalować hello dostawcy usługi Azure Site Recovery na serwerze VMM hello i hello agenta usług odzyskiwania Azure na każdym hoście funkcji Hyper-V. Źródło Hello będzie powitania serwera VMM. obiekt docelowy Hello jest Azure.
    - Hosty funkcji Hyper-V bez programu VMM: po określeniu ustawienia źródła można pobrać i zainstalować hello dostawca i agent na każdym hoście funkcji Hyper-V. Podczas wdrażania zebrać hello hostów do lokacji funkcji Hyper-V i określić tę lokację jako źródło hello. obiekt docelowy Hello jest Azure.

    ![Replikacja VMM/funkcji Hyper-V tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![tooAzure replikacji lokacji funkcji Hyper-V](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Zasady replikacji**: Utwórz zasady replikacji dla chmury VMM lub lokacji hello funkcji Hyper-V. Hello zasady są stosowane tooall maszyn wirtualnych znajdujących się na hostach w witrynie hello lub w chmurze.
5. **Włącz replikację**: Włącz replikację maszyn wirtualnych funkcji Hyper-V. Zgodnie z ustawieniami zasad replikacji hello następuje Replikacja początkowa. Dane zmiany są śledzone, i replikacji tooAzure zmiany różnicowe uruchamia się po zakończeniu replikacji początkowej hello. Śledzone zmiany elementu są przechowywane w pliku hrl.
6. **Testowanie trybu failover**: Uruchamianie testu toomake trybu failover, czy wszystko działa zgodnie z oczekiwaniami.

Dowiedz się więcej o wdrażaniu:
- [Rozpoczynanie pracy z tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V — z programem VMM](site-recovery-vmm-to-azure.md)
- [Rozpoczynanie pracy z tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V - bez programu VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Przepływ pracy replikacji funkcji Hyper-V

### <a name="enable-protection"></a>Włączanie ochrony

1. Po włączeniu ochrony dla maszyny Wirtualnej funkcji Hyper-V w hello portalu Azure lub lokalnie, hello **Włącz ochronę** uruchamia.
2. Witaj zadanie sprawdza, czy maszyna hello spełnia wymagania wstępne, przed wywołaniem hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset replikacji z ustawieniami hello skonfigurowano.
3. zadanie Hello rozpoczyna się Replikacja początkowa wywołując hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) — metoda, tooinitialize Pełna replikacja maszyny Wirtualnej i wysyłania hello wirtualna tooAzure dysków wirtualnych.
4. Można monitorować zadanie hello w hello **zadania** kartę.      ![Lista zadań](media/site-recovery-hyper-v-azure-architecture/image1.png) ![Szczegóły zadania Włącz ochronę](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>Replikacja początkowa

1. Po wyzwoleniu replikacji początkowej tworzona jest [migawka maszyny wirtualnej funkcji Hyper-V](https://technet.microsoft.com/library/dd560637.aspx).
2. Wirtualne dyski twarde są replikowane pojedynczo, dopóki nie są one wszystkich skopiowanych tooAzure. Go może potrwać kilka minut w zależności od hello rozmiar maszyny Wirtualnej, a przepustowość sieci. toooptimize użycie sieci, zobacz [jak toomanage lokalnymi użycia przepustowości sieci ochrony tooAzure](https://support.microsoft.com/kb/3056159).
3. Jeśli zmiany dysku są wykonywane, gdy Replikacja początkowa jest w toku, hello Tracker replikacji repliki funkcji Hyper-V będzie śledził te zmiany jako dzienniki replikacji funkcji Hyper-V (hrl). Te pliki znajdują się w hello tym samym folderze co dyski hello. Każdy dysk ma skojarzony plik hrl wysyłanej toosecondary magazynu.
4. Witaj pliki migawki i dziennika zużywają zasoby dysku w trakcie replikacji początkowej.
5. Po zakończeniu replikacji początkowej hello, hello migawki maszyny Wirtualnej jest usuwana. Przyrostowe zmiany dysków w dzienniku hello są zsynchronizowane i scalone toohello dysku nadrzędnego.


### <a name="finalize-protection"></a>Finalizowanie ochrony

1. Po replikacji początkowej hello zakończeniu hello **Finalizuj ochronę na maszynie wirtualnej hello** zadania konfiguruje ustawienia sieciowe i inne ustawienia po replikacji, aby hello maszyna wirtualna jest chroniona.
    ![Zadanie Finalizuj ochronę](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Jeśli replikujesz tooAzure, może być konieczne tootweak hello ustawień dla maszyny wirtualnej hello tak, aby była gotowa do pracy awaryjnej. W tym momencie możesz uruchomić test toocheck trybu failover, który wszystko działa zgodnie z oczekiwaniami.

### <a name="delta-replication"></a>Replikacja różnicowa

1. Po replikacji początkowej hello synchronizacja przyrostowa rozpoczyna się, zgodnie z ustawieniami replikacji.
2. Witaj Tracker replikacji repliki funkcji Hyper-V śledzi hello zmiany tooa wirtualnego dysku twardego jako pliki hrl. Z każdym dyskiem skonfigurowanym pod kątem replikacji jest skojarzony plik hrl. Ten dziennik jest wysyłany konta magazynu toohello klienta po zakończeniu replikacji początkowej. Kiedy dziennika tooAzure przesyłania, hello zmiany dysku podstawowego hello są śledzone w innym pliku dziennika, w hello tego samego katalogu.
3. Podczas replikacji początkowej i różnicowych można monitorować hello maszyny Wirtualnej w hello widok maszyny Wirtualnej. [Dowiedz się więcej](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>Synchronizacja replikacji

1. Jeśli replikacja różnicowa nie powiedzie się, a pełna replikacja byłaby kosztowna pod względem przepustowości lub czasu, maszyna wirtualna jest oznaczana do ponownej synchronizacji. Na przykład jeśli pliki hrl będą zajmować hello dostępu 50% rozmiaru dysku hello, następnie hello maszyny Wirtualnej zostaną oznaczone ponownej synchronizacji.
2.  Ponowna synchronizacja minimalizuje hello ilość danych przesyłanych przez obliczaniu sum kontrolnych hello źródłowych i docelowych maszyn wirtualnych oraz wysyłaniu tylko danych różnicowych hello. Ponowna synchronizacja używa algorytmu dzielenia na fragmenty o stałym bloku. Za jego pomocą pliki źródłowe i docelowe są dzielone na stałe fragmenty. Sumy kontrolne dla każdego fragmentu są generowane, a następnie porównuje toodetermine, która blokuje z miejsca docelowego hello źródła potrzeby toobe toohello zastosowane.
3. Po ukończeniu ponownej synchronizacji replikacja różnicowa powinna zostać wznowiona. Domyślnie ponowna synchronizacja jest zaplanowane toorun automatycznie poza godzinami pracy, ale możesz ponownie ręcznie zsynchronizować maszyny wirtualnej. Na przykład możesz wznowić ponowną synchronizację, jeśli wystąpi awaria sieci lub inna awaria. toodo, wybierz opcję hello maszyny Wirtualnej w portalu hello > **ponownie zsynchronizować**.

    ![Ręczna ponowna synchronizacja](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Ponowne próby

Jeśli wystąpi błąd replikacji, może zostać użyty wbudowany mechanizm ponawiania. Tę logikę można podzielić na dwie kategorie:

**Kategoria** | **Szczegóły**
--- | ---
**Błąd nieodwracalny** | Nie jest podejmowana próba ponowienia. Maszyna wirtualna będzie mieć stan **Krytyczny** i będzie wymagana interwencja administratora. Przykłady te błędy: przerwany łańcuch wirtualnego dysku twardego; Nieprawidłowy stan dla repliki hello wirtualna; Błędy uwierzytelnianie sieciowe: błędy autoryzacji; Maszyna wirtualna nie znaleziono błędy (w przypadku autonomicznych serwerów funkcji Hyper-V)
**Błędy odwracalne** | Wykonywane co interwał replikacji, przy użyciu wykładniczej wycofania zwiększającą interwał ponawiania prób powitania od początku hello hello pierwsza próba 1, 2, 4, 8, a następnie 10 minut. Jeśli błąd będzie się powtarzać, ponowne próby będą wykonywane co 30 minut. Są to na przykład błędy sieci, błędy małej ilości miejsca na dysku i warunki małej ilości pamięci |

## <a name="protection-and-recovery-lifecycle"></a>Cykl życia ochrony i odzyskiwania

![przepływ pracy](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Następne kroki

- [Check deployment prerequisites](site-recovery-prereq.md) (Sprawdzanie wymagań wstępnych dotyczących wdrożenia)
- Rozwiązywanie problemów:
    - [Monitorowanie i rozwiązywanie problemów z ochroną](site-recovery-monitoring-and-troubleshooting.md)
    - [Help from Microsoft support](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support) (Pomoc techniczna od firmy Microsoft)
    - [Common errors and resolutions](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions) (Typowe błędy i rozwiązania)
