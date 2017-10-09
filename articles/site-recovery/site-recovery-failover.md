---
title: "aaaFailover w usłudze Site Recovery | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje hello replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Więcej informacji na temat trybu failover tooAzure lub dodatkowego centrum danych."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Praca w trybie failover w usłudze Site Recovery
W tym artykule opisano, jak toofailover maszyn wirtualnych i serwerów fizycznych chronione przez usługę Site Recovery.

## <a name="prerequisites"></a>Wymagania wstępne
1. Przed wykonaniem trybu failover, wykonaj [testowanie trybu failover](site-recovery-test-failover-to-azure.md) tooensure, czy wszystko działa zgodnie z oczekiwaniami.
1. [Przygotowanie sieci hello](site-recovery-network-design.md) w lokalizacji docelowej, przed wykonaniem trybu failover.  


## <a name="run-a-failover"></a>Tryb failover
W tej procedurze opisano sposób toorun w trybie failover [planu odzyskiwania](site-recovery-create-recovery-plans.md). Alternatywnie można uruchomić trybu failover powitania dla jednej maszyny wirtualnej lub serwerze fizycznym z hello **elementy replikowane** strony


![Tryb failover](./media/site-recovery-failover/Failover.png)

1. Wybierz **plany odzyskiwania** > *recoveryplan_name*. Kliknij przycisk **trybu Failover**
2. Na powitania **pracy awaryjnej** ekranu wybierz **punkt odzyskiwania** toofailover do. Można użyć jednej z hello następujące opcje:
    1.  **Najnowsze** (domyślnie): Ta opcja najpierw przetwarza wszystkie dane hello został wysłany tooSite odzyskiwania usługi toocreate punkt odzyskiwania dla każdej maszyny wirtualnej przed awaryjne tooit. Ta opcja zapewnia hello najniższy RPO (cel punktu odzyskiwania) jako hello maszyny wirtualnej utworzonej po wszystkich danych hello trybu failover, która została replikowane tooSite odzyskiwania usługi zostało wyzwolone hello trybu failover.
    1.  **Najnowsze przetworzone**: Ta opcja nie powiedzie się za pośrednictwem wszystkich maszyn wirtualnych hello odzyskiwania planu toohello najnowszy punkt odzyskiwania, który został już przetworzony przez usługę Site Recovery. Podczas wykonywania testu pracy w trybie failover maszyny wirtualnej, wyświetlane są również sygnaturę czasową hello najnowszy punkt odzyskiwania przetworzone. Jeśli przeprowadzasz trybu failover planu odzyskiwania, można przejść tooindividual maszyny wirtualnej i przyjrzyj się **najnowsze punkty odzyskiwania** kafelka tooget te informacje. Nie czas tooprocess hello nieprzetworzonych danych, ta opcja zapewnia niski opcja pracy awaryjnej RTO (celu czasu odzyskiwania).
    1.  **Najnowsza wersja aplikacji spójne**: Ta opcja nie powiedzie się za pośrednictwem wszystkich maszyn wirtualnych hello planu toohello najnowszej aplikacji odzyskiwania zapewniających spójność punkt odzyskiwania został już przetworzony przez usługę Site Recovery. Podczas wykonywania testu pracy w trybie failover maszyny wirtualnej, sygnaturę czasową ostatniego punktu odzyskiwania zapewniających spójność aplikacji hello jest także pokazany. Jeśli przeprowadzasz trybu failover planu odzyskiwania, można przejść tooindividual maszyny wirtualnej i przyjrzyj się **najnowsze punkty odzyskiwania** kafelka tooget te informacje.
    1.  **Najnowsze wielu maszyn wirtualnych przetwarzane**: Ta opcja jest dostępna tylko dla planów odzyskiwania, które mają co najmniej jedną maszynę wirtualną z wielu maszyn wirtualnych na. Maszyny wirtualne, które są częścią replikacji trybu failover toohello najnowsze wspólnej wielu maszyn wirtualnych spójne odzyskiwania grupy punktu. Inne maszyny wirtualne trybu failover tootheir najnowsze przetworzone punktu odzyskiwania.  
    1.  **Najnowsze wielu maszyn wirtualnych całej aplikacji**: Ta opcja jest dostępna tylko dla planów odzyskiwania, które mają co najmniej jedną maszynę wirtualną z ON spójności wielu maszyn wirtualnych. Maszyny wirtualne, które są częścią replikacji grupy pracy awaryjnej toohello najnowsze wspólnych wielu maszyn wirtualnych spójnych z aplikacją punktów odzyskiwania. Inne maszyny wirtualne trybu failover tootheir najnowsze spójnych z aplikacją punktu odzyskiwania.
    1.  **Niestandardowe**: Jeśli przeprowadzasz testowy tryb failover maszyny wirtualnej, a następnie można użyć tej opcji toofailover tooa odzyskiwania z określonego punktu.

    > [!NOTE]
    > Hello opcja toochoose punkt odzyskiwania jest dostępny tylko w przypadku, gdy kończy się niepowodzeniem, za pośrednictwem tooAzure.
    >
    >


1. Jeśli niektóre hello maszyny wirtualne w planie odzyskiwania hello nie zostały przez podczas poprzedniego uruchomienia, a teraz hello maszyny wirtualne są aktywne w miejscu źródłowym i docelowym, można użyć **zmianę kierunku** opcję Kierunek hello toodecide powinno się zdarzyć hello pracą w trybie failover.
1. W przypadku powrotu po awarii za pośrednictwem tooAzure i szyfrowanie danych jest włączone dla chmury hello (dotyczy tylko w przypadku ochrony maszyn wirtualnych funkcji Hyper-v z serwera programu VMM), w **klucza szyfrowania** hello wybierz certyfikat wystawiony podczas możesz włączone szyfrowanie danych podczas instalacji na serwerze VMM hello.
1. Wybierz **Zamknij maszynę przed rozpoczęciem pracy awaryjnej** Jeśli chcesz, aby Usługa Site Recovery tooattempt toodo zamykania maszyn wirtualnych źródła, aby mogło nastąpić wyzwolenie hello trybu failover. Tryb failover trwa nawet w przypadku zamknięcia nie powiedzie się.  

    > [!NOTE]
    > W przypadku maszyn wirtualnych funkcji Hyper-v ta opcja próbuje toosynchronize hello lokalne dane, które nie zostały wysłane toohello usługi przed wyzwalania hello trybu failover.
    >
    >

1. Pozwala śledzić postęp trybu failover hello w hello **zadania** strony. Nawet jeśli występują błędy podczas nieplanowanego trybu failover, planu odzyskiwania hello uruchamia do czasu ukończenia.
1. Po hello w tryb failover po zalogowaniu się tooit Sprawdź poprawność hello maszyny wirtualnej. Jeśli chcesz inny punkt odzyskiwania toogo hello maszyny wirtualnej, a następnie można użyć **zmienić punktu odzyskiwania** opcji.
1. Po zakończeniu przejścia w tryb failover maszyny wirtualnej hello możesz **zatwierdzić** hello trybu failover. Spowoduje to usunięcie wszystkich punktów odzyskiwania hello dostępne z usługą hello i **zmienić punktu odzyskiwania** opcja nie będzie już dostępna.

## <a name="planned-failover"></a>Planowany tryb failover
Oprócz przejścia w tryb Failover maszyny wirtualne funkcji Hyper-V chronione za pomocą usługi Site Recovery również obsługa **planowanego trybu failover**. Jest to zero danych utraty pracy awaryjnej opcja. Po wyzwoleniu planowanego trybu failover, najpierw hello źródło, które maszyny wirtualne są zamknięte, hello danych jeszcze toobe synchronizowane są synchronizowane, a następnie zostanie wywołany trybu failover.

> [!NOTE]
> Gdy użytkownik trybu failover funkcji Hyper-v maszyny wirtualne z jednego lokalnej lokacji tooanother lokacji lokalnej, lokacji głównej lokalnymi wstecz toohello toocome masz toofirst **replikacji odwrotnej** hello maszyny wirtualnej wstecz tooprimary lokacji i wyzwolić tryb failover. Jeśli hello podstawowej maszyny wirtualnej nie jest dostępne, przed uruchomieniem zbyt**replikacji odwrotnej** ma maszyny wirtualnej hello toorestore z kopii zapasowej.   
>
>

## <a name="failover-job"></a>Zadanie trybu failover

![Tryb failover](./media/site-recovery-failover/FailoverJob.png)

Po wyzwoleniu trybu failover obejmuje następujące kroki:

1. Sprawdzanie wymagań wstępnych: ten krok zapewnia, że spełniono wszystkie warunki wymagane do trybu failover
1. Tryb failover: Ten krok przetwarza dane hello i powoduje gotowy, że maszyna wirtualna platformy Azure można utworzyć poza jego. Jeśli wybrano **najnowsze** punkt odzyskiwania, w tym kroku tworzy punkt odzyskiwania z hello dane, które zostało wysłane toohello usługi.
1. Start: Ten krok umożliwia utworzenie maszyny wirtualnej platformy Azure przy użyciu danych hello przetwarzane w poprzednim kroku hello.

> [!WARNING]
> **Nie Anuluj toku pracy awaryjnej**: przed uruchomieniem trybu failover replikacji dla maszyny wirtualnej hello jest zatrzymana. Jeśli użytkownik **anulować** w zadaniu postępu zatrzymuje pracy awaryjnej, ale hello maszyny wirtualnej nie można uruchomić tooreplicate. Nie można ponownie rozpocząć replikacji.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Czas poświęcony na tooAzure trybu failover

W niektórych przypadkach pracy awaryjnej maszyn wirtualnych wymaga bardzo pośredniego kroku, który zazwyczaj trwa około 8 toocomplete minut too10. Te przypadki są następujące:

* Maszyny wirtualne VMware przy użyciu usługi mobilności w wersji starszej niż 9,8
* Serwerów fizycznych 
* Maszyny wirtualne VMware systemu Linux
* Maszyny wirtualne funkcji Hyper-V chronione jako serwerów fizycznych
* Maszyny wirtualne VMware, gdy następujące sterowniki nie są dostępne jako rozruchu sterowników 
    * storvsc 
    * magistralę maszyny wirtualnej 
    * storflt 
    * Intelide 
    * ATAPI
* Adresy IP maszyn wirtualnych VMware, które nie mają włączone niezależnie od tego, czy używasz DHCP lub statyczna usługi DHCP

W hello wszystkich innych przypadkach zdarza się to pośredniego kroku nie jest wymagana i hello czas pracy w trybie failover hello jest znacznie niższa. 





## <a name="using-scripts-in-failover"></a>Za pomocą skryptów w tryb Failover
Możesz tooautomate pewne akcje podczas wykonywania pracy awaryjnej. Za pomocą skryptów lub [elementy runbook automatyzacji Azure](site-recovery-runbook-automation.md) w [planów odzyskiwania](site-recovery-create-recovery-plans.md) toodo który.

## <a name="other-considerations"></a>Inne zagadnienia
* **Litera dysku** — literę dysku hello tooretain w przypadku maszyn wirtualnych po pracy awaryjnej można ustawić hello **zasad sieci SAN** dla hello wirtualnej maszynie zbyt**OnlineAll**. [Dowiedz się więcej](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Następne kroki
Gdy ma przejścia w tryb failover maszyny wirtualne i hello lokalnego centrum danych jest dostępna, wykonaj następujące czynności [ **ponownego włączenia ochrony** ](site-recovery-how-to-reprotect.md) maszyn wirtualnych VMware kopii toohello lokalnego centrum danych.

Użyj [ **planowanego trybu failover** ](site-recovery-failback-from-azure-to-hyper-v.md) opcję zbyt**powrotu po awarii** maszyn wirtualnych funkcji Hyper-v kopii lokalnej tooon z platformy Azure.

Jeśli nie powiodło się za pośrednictwem danych lokalnych tooanother maszyny wirtualnej funkcji Hyper-v zarządzanych przez program VMM centrum danych podstawowego serwera i hello center jest dostępny, następnie użyć **replikacja odwrotna** toohello wstecz opcja toostart hello replikacji Centrum danych podstawowych.
