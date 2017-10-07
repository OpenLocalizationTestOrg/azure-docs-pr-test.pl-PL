---
title: "aaaFailback w usłudze Azure Site Recovery dla maszyny wirtualnej funkcji Hyper-v | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje hello replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Więcej informacji na temat powrotu po awarii z platformy Azure tooon lokalnym centrum danych."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Powrót po awarii w usłudze Site Recovery dla maszyny wirtualnej funkcji Hyper-V

W tym artykule opisano, jak toofailback maszyny wirtualne chronione przez usługę Site Recovery.

## <a name="prerequisites"></a>Wymagania wstępne
1. Upewnij się, że ten hello lokacji głównej Menedżerem serwera/funkcji Hyper-V jest podłączony.
2. Użytkownik powinien wykonał **zatwierdzić** hello maszyny wirtualnej.

## <a name="why-is-there-no-button-called-failback"></a>Dlaczego jest ma przycisku o nazwie powrotu po awarii
W portalu hello jest nie jawnego gestu o nazwie powrotu po awarii. Powrót po awarii jest to krok, gdzie możesz wrócić toohello lokacji głównej. Zgodnie z definicją trybu failover jest w przypadku maszyn wirtualnych hello trybu failover z primary(on-premises) lokacji toorecovery (Azure) i powrotu po awarii jest podczas wykonywania pracy awaryjnej maszyn wirtualnych hello odzyskiwania kopii tooprimary.

Po zainicjowaniu tryb failover bloku hello informuje o kierunku hello hello zadania. W przypadku hello kierunek z lokalnej tooOn Azure jest powrót po awarii.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>Dlaczego jest tylko toofailback gestu planowanego trybu failover
Azure to środowisko o wysokiej dostępności i maszyn wirtualnych będą zawsze dostępne. Powrót po awarii jest planowane działanie, możesz zdecydować, tootake małych przestoju tak, aby uruchomić obciążeń hello ponownie uruchamiane lokalnie. To oczekuje bez utraty danych. Dlatego jest dostępna tylko gestu planowanego trybu failover, które wyłączyć maszyny wirtualne hello na platformie Azure, pobrać najnowsze zmiany hello i upewnij się, że istnieje nie powoduje utraty danych.

## <a name="initiate-failback"></a>Zainicjuj powrotu po awarii
Po przejściu w tryb failover lokalizacji głównej toosecondary hello replikowane maszyny wirtualne nie są chronione przez usługę Site Recovery, a lokalizacji dodatkowej hello obecnie działa jako lokalizacja active hello. Wykonaj te procedury toofail toohello wstecz oryginalnej lokacji głównej. W tej procedurze opisano sposób toorun planowanego trybu failover dla odzyskiwania plan. Alternatywnie można uruchomić jednej maszyny wirtualnej w trybie failover hello na powitania **maszyn wirtualnych** kartę.

1. Wybierz **plany odzyskiwania** > *recoveryplan_name*. Kliknij przycisk **pracy awaryjnej** > **planowanego trybu Failover**.
2. Na powitania ** potwierdzić planowanego trybu Failover ** wybierz hello lokalizacja źródłowa i docelowa. Należy zwrócić uwagę hello kierunek trybu failover. Jeśli hello w tryb failover z podstawowej pracy jako oczekiwać i wszystkich maszyn wirtualnych znajdują się w lokalizacji dodatkowej hello, jest to wyłącznie w celach informacyjnych.
3. W przypadku powrotu po awarii z platformy Azure, wybierz ustawienia w **synchronizacji danych**:

   * **Synchronizowanie danych przed pracy awaryjnej (tylko zmiany różnicowe Synchronizuj)**— tej opcji minimalizuje przestojów maszyn wirtualnych, jak synchronizacji bez zamykania je. Witaj, po:
     * Faza 1: Wykonuje migawkę hello maszyny wirtualnej na platformie Azure i kopiuje go hosta funkcji Hyper-V lokalnymi toohello. Witaj maszyny nadal działają na platformie Azure.
     * Faza 2: Hello maszyny wirtualnej platformy Azure spowoduje to zamknięcie ma nowych zmian występuje. ostateczny zestaw zmiany różnicowe Hello są toohello przeniesione na serwerze lokalnym i hello na lokalnej maszynie wirtualnej jest uruchomiony.

    - **Synchronizacja danych w trybie failover tylko (pełnego pobierania)**— Użyj tej opcji, jeśli działała na platformie Azure przez długi czas. Ta opcja jest szybsze, ponieważ oczekuje się, że większość hello dysku został zmieniony i nie chcemy czasu toospend obliczaniu sum kontrolnych. Wykonuje pobierania hello dysku. Jest również przydatne w przypadku maszyny wirtualnej lokalnego hello został usunięty.

    >[!NOTE]
    >Firma Microsoft zaleca, możesz użyć tej opcji, jeśli działała Azure jakiś czas (miesiąc lub więcej) lub maszyny wirtualnej lokalnego hello został usunięty. Ta opcja nie wykonać wszelkie obliczenia sumy kontrolnej.
    >
    >




4. Jeśli szyfrowanie danych jest włączone dla chmury hello w **klucza szyfrowania** hello wybierz certyfikat wystawiony po włączeniu szyfrowania danych podczas instalacji dostawcy na serwerze VMM hello.
5. Inicjuj tryb failover hello. Pozwala śledzić postęp trybu failover hello w hello **zadania** kartę.
6. W przypadku wybrania hello opcja toosynchronize hello danych przed hello przejścia w tryb failover raz hello początkowej synchronizacji danych i wszystko jest gotowe tooshut dół hello maszynach wirtualnych platformy Azure, kliknij przycisk **zadania** Nazwa zadania planowanego trybu failover **Przejdź w tryb Failover**. To zamknięcie hello Azure maszyny, hello transferów najnowsze zmiany toohello na lokalnej maszynie wirtualnej i uruchamia hello lokalne maszyny Wirtualnej.
7. Teraz można rejestrować na powitania toovalidate maszyny wirtualnej jest dostępna, zgodnie z oczekiwaniami.
8. Maszyna wirtualna Hello jest w stan oczekiwania na zatwierdzenie. Kliknij przycisk **zatwierdzić** toocommit hello w tryb failover.
9. Teraz w kolejności powrotu po awarii toocomplete powitania kliknij **odwrócić replikację** toostart ochrona powitalnych maszyny wirtualnej w lokacji głównej hello.

## <a name="failback-tooan-alternate-location"></a>Powrót po awarii tooan alternatywnej lokalizacji
Jeśli została wdrożona ochrona między [lokacji funkcji Hyper-V i Azure](site-recovery-hyper-v-site-to-azure.md) masz tooability toofailback z lokalizacji alternatywnej lokalnymi tooan platformy Azure. Jest to przydatne, jeśli potrzebujesz tooset się nowego sprzętu lokalnego. Oto jak to zrobić.

1. Jeśli podczas konfigurowania nowego sprzętu Zainstaluj system Windows Server 2012 R2 i roli Hyper-V na serwerze hello hello.
2. Utwórz przełącznik sieci wirtualnej z hello takie same nazwy, trzeba było na oryginalnym serwerze hello.
3. Wybierz **chronione elementy** -> **grupy ochrony**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> toofail ponownie, a następnie wybierz **planowane Tryb failover**.
4. W **potwierdzić planowanego trybu Failover** wybierz **Utwórz lokalną maszynę wirtualną, jeśli nie istnieje**.
5. W **nazwy hosta** wybierz hello nowy serwer hosta funkcji Hyper-V, na którym ma zostać maszyny wirtualnej hello tooplace.
6. W synchronizacji danych zaleca się opcja hello **synchronizować dane hello przed trybu failover hello**. Minimalizuje czas przestoju w przypadku maszyn wirtualnych, jak synchronizacji bez zamykania je. Witaj, po:

   * Faza 1: Wykonuje migawkę hello maszyny wirtualnej na platformie Azure i kopiuje go hosta funkcji Hyper-V lokalnymi toohello. Witaj maszyny nadal działają na platformie Azure.
   * Faza 2: Hello maszyny wirtualnej platformy Azure spowoduje to zamknięcie ma nowych zmian występuje. Witaj ostatecznego zestawu zmian są toohello przeniesione na serwerze lokalnym i hello na lokalnej maszynie wirtualnej zostanie uruchomiona.
7. Kliknij przycisk hello znacznikiem wyboru hello toobegin pracy awaryjnej (powrót po awarii).
8. Po zakończeniu synchronizacji początkowej hello i wszystko jest gotowe tooshut maszynę wirtualną hello na platformie Azure, kliknij przycisk **zadania** > <planned failover job> > **ukończenia pracy awaryjnej**. To kończy pracę hello Azure maszyny, transferów hello najnowsze zmiany toohello lokalnej maszyny wirtualnej i uruchamia go.
9. Możesz zalogować się na powitania lokalnej maszyny wirtualnej tooverify, który wszystko działa zgodnie z oczekiwaniami. Następnie kliknij przycisk **zatwierdzić** toofinish hello w tryb failover.
10. Kliknij przycisk **odwrócić replikację** toostart ochrona powitalnych na lokalnej maszynie wirtualnej.

    > [!NOTE]
    > Jeśli anulujesz hello zadaniem powrotu po awarii w synchronizacji danych kroku, hello lokalnej maszyny Wirtualnej będzie w stanie uszkodzenia. To dlatego synchronizacji danych kopiuje hello najnowszych danych z dysków danych lokalnych toohello dysków maszyny Wirtualnej platformy Azure, a dopiero po zakończeniu synchronizacji hello, hello dysku dane mogą nie być w stanie spójności. Jeśli hello lokalnej maszyny Wirtualnej został uruchomiony po synchronizacji danych zostało anulowane, może nie uruchomić. Ponownie uruchomić trybu failover toocomplete hello synchronizacji danych.
    >
    >



## <a name="next-steps"></a>Następne kroki

Po zakończeniu hello zadaniem powrotu po awarii, **zatwierdzić** hello maszyny wirtualnej. Zatwierdzanie usuwa hello Azure maszyny wirtualnej i jej dyski i przygotowuje hello wirtualna toobe objęte ochroną ponownie.

Po **zatwierdzić**, można zainicjować hello *odwrócić replikację*. Spowoduje to uruchomienie chroni hello maszyny wirtualnej z lokalnymi tooAzure Wstecz. Należy zwrócić uwagę na to będą tylko zmiany replikowania hello ponieważ hello maszyna wirtualna została wyłączona na platformie Azure i dlatego wysyła różnicowej tylko zmiany.
