---
title: "Tryb failover, a kończyć się niepowodzeniem z powrotem maszyn wirtualnych funkcji Hyper-V replikowany do centrum danych w dodatkowej z usługą Site Recovery | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działają maszyny wirtualne funkcji Hyper-V do lokacji dodatkowej lokalnymi i powrót po awarii do lokacji głównej, z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 44a662fa-2e7a-4996-86df-fdd6d6f5dedf
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 09/16/2017
ms.author: raynew
ms.openlocfilehash: 8f139070de99c4249207d048d445e86dd41e9060
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="fail-over-and-fail-back-hyper-v-vms-replicated-to-your-secondary-on-premises-site"></a>Tryb failover, a kończyć się niepowodzeniem z powrotem maszyn wirtualnych funkcji Hyper-V replikowany do lokacji dodatkowej lokalnymi

[Usługi Azure Site Recovery](site-recovery-overview.md) usługi zarządza i organizuje replikację, tryb failover i powrotu po awarii maszyn lokalnych i Azure maszynach wirtualnych (VM).

W tym samouczku opisano w tryb failover maszyny Wirtualnej funkcji Hyper-V zarządzane w chmurze programu System Center Virtual Machine Manager (VMM), do dodatkowej lokacji programu VMM. Po przez Ciebie nie powiodła się, możesz powrót po awarii do lokacji sieci lokalnej, gdy jest ona dostępna. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tryb failover maszyny Wirtualnej funkcji Hyper-V z głównej chmury VMM do dodatkowej chmury VMM
> * Włącz ponownie ochronę z lokacji dodatkowej do podstawowych i wykonaj powrót po awarii
> * Opcjonalnie rozpocząć replikację z podstawowej do dodatkowej ponownie

## <a name="overview"></a>Omówienie

Tryb failover i powrotu po awarii ma trzy etapy:

1. **Przełączyć do lokacji dodatkowej**: awaryjnie maszyny z lokacji podstawowej do lokacji dodatkowej.
2. **Niepowodzenie z lokacji dodatkowej**: replikowanie maszyn wirtualnych z pomocniczego podstawowym, a następnie uruchom planowany tryb failover do wykonaj powrót po awarii.
3. Po planowanego trybu failover opcjonalnie Uruchom replikacji z lokacji podstawowej do lokacji dodatkowej ponownie.


## <a name="fail-over-to-a-secondary-site"></a>Przełączyć do lokacji dodatkowej

### <a name="failover-prerequisites"></a>Wymagania wstępne dotyczące trybu failover

Upewnij się, że udało Ci się ukończyć [wyszczególniania odzyskiwania po awarii](tutorial-dr-drill-secondary.md) do sprawdzenia, czy wszystko działa zgodnie z oczekiwaniami.


### <a name="run-a-failover-from-primary-to-secondary"></a>Uruchom pracy awaryjnej z podstawowej do dodatkowej

Możesz uruchomić zwykłe i planowanego trybu failover dla maszyn wirtualnych funkcji Hyper-V.

- Użyj regularne pracy awaryjnej dla wystąpienia nieoczekiwanych awarii. Po uruchomieniu tej pracy awaryjnej usługi Site Recovery tworzy maszyny Wirtualnej w lokacji dodatkowej i uprawnień go w górę. Możesz uruchomić tryb failover przed określony punkt odzyskiwania. W zależności od tego punktu odzyskiwania, którego używasz, może wystąpić utrata danych.
- Planowany tryb failover może służyć konserwacji lub podczas oczekiwanych awarii. Ta opcja umożliwia zerowej utraty danych. Po wyzwoleniu planowanego trybu failover, źródłowe maszyny wirtualne są zamknięte. Niezsynchronizowane dane są synchronizowane i trybu failover zostanie wywołany. 
- 
W tej procedurze opisano sposób uruchamiania regularne trybu failover.


1. W **ustawienia** > **elementy replikowane** kliknij maszynę Wirtualną > **pracy awaryjnej**.
2. W **pracy awaryjnej** wybierz **punkt odzyskiwania** do trybu failover. Można użyć jednej z następujących opcji:
    - **Najnowsze** (domyślnie): Ta opcja najpierw przetwarza wszystkie dane wysyłane do usługi Site Recovery. Ponieważ repliki maszyna wirtualna utworzona po trybu failover ma wszystkie dane, które zostało replikowane do usługi Site Recovery pracę w trybie failover zostało wyzwolone zapewnia najniższy RPO (cel punktu odzyskiwania).
    - **Najnowsze przetworzone**: Ta opcja nie powiedzie się za pośrednictwem maszyn wirtualnych do ostatniego punktu odzyskiwania przetworzone przez usługę Site Recovery. Ta opcja umożliwia RTO niski (celu czasu odzyskiwania), ponieważ nie jest czas przetwarzania nieprzetworzonych danych.
    - **Najnowsza wersja aplikacji spójne**: Ta opcja nie powiedzie się na maszynie Wirtualnej, aby punkt najnowszych odzyskiwania zapewniających spójność aplikacji przetworzone przez usługę Site Recovery. 
3. Klucz szyfrowania nie jest ważna w tym scenariuszu.
4. Wybierz **Zamknij maszynę przed rozpoczęciem pracy awaryjnej** Jeśli chcesz, aby usługi Site Recovery, aby spróbować wykonać zamknięcie źródłowe maszyny wirtualne przed wyzwolenie pracy awaryjnej. Usługa Site Recovery również spróbować zsynchronizować danych lokalnych, które jeszcze nie zostało wysłane do lokacji dodatkowej, aby mogło nastąpić wyzwolenie pracy awaryjnej. Należy pamiętać, że czy tryb failover będzie kontynuowane, nawet w przypadku zamknięcia nie powiedzie się. Możesz śledzić postęp trybu failover **zadania** strony.
5. Teraz można wyświetlić maszynę Wirtualną w chmurze programu VMM dodatkowej.
6. Po zweryfikowaniu maszyny Wirtualnej, **zatwierdzić** pracy awaryjnej. Spowoduje to usunięcie wszystkich punktów odzyskiwania.

> [!WARNING]
> **Nie Anuluj trybu failover w toku**: przed uruchomieniem trybu failover zostanie zatrzymana replikację maszyny Wirtualnej. Jeśli anulujesz trybu failover w toku, zatrzymuje trybu failover, ale maszyna wirtualna nie będą replikowane ponownie.  


## <a name="reprotect-and-fail-back-from-secondary-to-primary"></a>Włącz ponownie ochronę i się nie powieść z podstawowym dodatkowej

### <a name="prerequisites-for-failback"></a>Wymagania wstępne dotyczące powrotu po awarii

Aby ukończyć powrotu po awarii, upewnij się, czy podstawowego i pomocniczego serwera programu VMM są podłączone do usługi Site Recovery.


### <a name="reprotect-and-fail-back"></a>Włącz ponownie ochronę i wykonaj powrót po awarii

Rozpoczęcia replikacji z lokacji dodatkowej do podstawowych i powrót po awarii do lokacji głównej. Po maszyny wirtualne są uruchomione ponownie w lokacji głównej, można replikować je do lokacji dodatkowej ponownie.  

1. W **ustawienia** > **elementy replikowane** kliknij maszynę Wirtualną i Włącz **odwrócić replikację**. Maszyna wirtualna zacznie replikację z powrotem do lokacji głównej.
2. Kliknij maszynę Wirtualną > **planowanego trybu Failover**.
3. W **potwierdzić planowanego trybu Failover**, sprawdź kierunek pracy awaryjnej (od dodatkowej chmury VMM) i wybierz lokalizacja źródłowa i docelowa. 
4. W **synchronizacji danych**, określ, jak mają być synchronizowane:
    - **Synchronizowanie danych przed pracy awaryjnej (należy zsynchronizować tylko zmiany różnicowe)**— ta opcja minimalizuje przestojów maszyn wirtualnych, ponieważ synchronizacji bez zamykania maszyny Wirtualnej. Oto, czego:
        - Tworzy migawkę repliki maszyny Wirtualnej i kopiuje go do podstawowego hosta funkcji Hyper-V. Replika kontynuowanie działania maszyny Wirtualnej.
        - Zamyka repliki maszyny Wirtualnej, dzięki czemu ma nowych zmian występuje. Ostateczny zestaw zmiany różnicowe są przesyłane do lokacji głównej i uruchomieniu maszyny Wirtualnej w lokacji głównej.
    - **Synchronizacja danych w trybie failover tylko (pełnego pobierania)**— Użyj tej opcji, jeśli działała w lokacji dodatkowej przez długi czas. Ta opcja jest szybsze, ponieważ będziemy spodziewać się wielu zmian dysku, a nie poświęcić czas na obliczenia sumy kontrolnej. Ta opcja wykonuje pobierania dysku. Jest również przydatne w przypadku podstawowej maszyny Wirtualnej został usunięty.
5. Klucz szyfrowania nie jest ważna w tym scenariuszu.
6. Inicjuj tryb failover. Możesz śledzić postęp trybu failover **zadania** kartę.
7. Jeśli został wybrany do synchronizacji danych przed przejście w tryb failover, po ukończeniu synchronizacji początkowej danych i wszystko jest gotowe zamknąć repliki maszyny Wirtualnej w lokacji dodatkowej, kliknij przycisk **zadania** > planowany tryb failover Nazwa zadania >  **Ukończ działanie trybu Failover**. Zamyka dodatkowej maszyny Wirtualnej, przesyła najnowsze zmiany z lokacją główną i uruchamia podstawowej maszyny Wirtualnej.
8. W głównej chmury VMM Sprawdź, czy maszyna wirtualna jest dostępna.
9. Podstawowej maszyny Wirtualnej jest teraz w stanie oczekiwania zatwierdzenia. Kliknij przycisk **zatwierdzania**, aby zatwierdzić pracy awaryjnej.
10. Jeśli chcesz rozpocząć replikację podstawowej maszyny Wirtualnej z powrotem do lokacji dodatkowej ponownie, Włącz **odwrócić replikację**.


> [!NOTE]
> Replikacja odwrotna replikuje tylko zmiany, które wystąpiły ponieważ repliki maszyna wirtualna została wyłączona i są wysyłane tylko zmiany różnicowe.

