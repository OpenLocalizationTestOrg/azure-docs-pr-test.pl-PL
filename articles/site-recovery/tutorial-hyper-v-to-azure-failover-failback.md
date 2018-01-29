---
title: "Tryb failover, a kończyć się niepowodzeniem z powrotem maszyn wirtualnych funkcji Hyper-V replikowany do platformy Azure z usługą Site Recovery | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działają maszyny wirtualne funkcji Hyper-V do platformy Azure i powrót po awarii do lokacji lokalnej, z usługą Azure Site Recovery"
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: article
ms.date: 12/31/2017
ms.author: raynew
ms.openlocfilehash: 390fe98bc718da4fe07f580bbf1dcbffbf8fc1ba
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/03/2018
---
# <a name="fail-over-and-fail-back-hyper-v-vms-replicated-to-azure"></a>Tryb failover, a kończyć się niepowodzeniem z powrotem maszyn wirtualnych funkcji Hyper-V zreplikowanej w systemie Azure

W tym samouczku opisano w tryb failover maszyny Wirtualnej funkcji Hyper-V do platformy Azure. Po przez Ciebie nie powiodła się, możesz powrót po awarii do lokacji sieci lokalnej, gdy jest ona dostępna. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Sprawdź, czy właściwości maszyny Wirtualnej funkcji Hyper-V, aby sprawdzić, który jest zgodny z wymaganiami platformy Azure
> * Uruchom tryb failover na platformie Azure
> * Włącz ponownie ochronę maszyn wirtualnych platformy Azure do lokacji lokalnej
> * Nie powiodło się platformy Azure z lokalnymi
> * Włącz ponownie ochronę lokalnych maszyn wirtualnych, aby uruchomić ponownie replikację do platformy Azure

To jest piąty samouczek w serii. Ten samouczek zakłada, zostały już wykonane zadania w poprzednim samouczki.

1. [Przygotowywanie platformy Azure](tutorial-prepare-azure.md)
2. [Przygotowywanie lokalnego wdrożenia oprogramowania VMware](tutorial-prepare-on-premises-hyper-v.md)
3. Konfigurowanie odzyskiwania po awarii dla [maszyn wirtualnych funkcji Hyper-V](tutorial-hyper-v-to-azure.md), lub [maszyn wirtualnych funkcji Hyper-V zarządzane w chmurach programu System Center VMM](tutorial-hyper-v-vmm-to-azure.md)
4. [Uruchamianie próbnego odzyskiwania po awarii](tutorial-dr-drill-azure.md)

## <a name="prepare-for-failover-and-failback"></a>Przygotowanie do trybu failover i powrotu po awarii

Upewnij się, na Maszynie wirtualnej nie ma żadnych migawek i że lokalnej maszyny Wirtualnej jest wyłączona podczas zastosowania. Pomaga to zapewnić spójność danych podczas replikacji. Nigdy nie włączaj maszyny Wirtualnej po zakończeniu zastosowania. 

Tryb failover i powrotu po awarii składa się z czterech etapów:

1. **Awaryjnie Azure**: awaryjnie maszyny z lokacji lokalnej na platformie Azure.
2. **Włącz ponownie ochronę maszyny wirtualne Azure**: Włącz ponownie ochronę maszyn wirtualnych platformy Azure, aby rozpoczynały się replikację z powrotem do lokalnych maszyn wirtualnych funkcji Hyper-V.
3. **Przełączyć się na lokalnych**: uruchomić trybu failover z platformy Azure do witryny lokalnej, gdy jest ona dostępna.
4. **Ponownej ochrony maszyn wirtualnych lokalnymi**: po danych nie powiodło się ponownie, włącz ponownie ochronę maszyn wirtualnych lokalnie do rozpoczęcia replikacji je do platformy Azure.

## <a name="verify-vm-properties"></a>Sprawdź właściwości maszyny Wirtualnej

Sprawdź właściwości maszyny Wirtualnej, a następnie upewnij się, że maszyna wirtualna jest zgodna z [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. W **chronione elementy**, kliknij przycisk **elementy replikowane** >< nazwę maszyny Wirtualnej >.

2. W **elementu zreplikowane** okienku przejrzyj informacje maszyny Wirtualnej, stan kondycji i najnowsze dostępne punkty odzyskiwania. Kliknij przycisk **właściwości** można zobaczyć więcej szczegółów.
     - W **obliczenia i sieć**, zmodyfikuj ustawienia maszyny Wirtualnej i ustawień, takich jak tej podsieci, w którym sieci maszyny Wirtualnej platformy Azure. Dyski zarządzane nie są obsługiwane dla powrotu po awarii z platformy Azure do funkcji Hyper-V.
   zostaną umieszczone po pracy awaryjnej i adres IP, który zostanie przypisany do niej.
    - W **dysków**, można wyświetlić informacje dotyczące systemu operacyjnego i dysków z danymi na Maszynie wirtualnej.

## <a name="fail-over-to-azure"></a>Przełączyć na platformie Azure

1. W **ustawienia** > **elementy replikowane** kliknij maszynę Wirtualną > **pracy awaryjnej**.
2. W **pracy awaryjnej** wybierz **najnowsze** punktu odzyskiwania. 
3. Wybierz **Zamknij maszynę przed rozpoczęciem pracy awaryjnej**. Usługa Site Recovery spróbuje zamknięcie źródłowe maszyny wirtualne przed wyzwolenie pracy awaryjnej. Tryb failover trwa nawet w przypadku zamknięcia nie powiedzie się. Możesz śledzić postęp trybu failover **zadania** strony.
4. Po zweryfikowaniu trybu failover kliknij **zatwierdzić**. Spowoduje to usunięcie wszystkich punktów odzyskiwania.

> [!WARNING]
> **Nie Anuluj trybu failover w toku**: przed uruchomieniem trybu failover zostanie zatrzymana replikację maszyny Wirtualnej. Jeśli anulujesz w toku, zatrzymuje trybu failover, ale maszyna wirtualna nie będą replikowane ponownie.

## <a name="reprotect-azure-vms"></a>Włącz ponownie ochronę maszyny wirtualne platformy Azure

1. W **AzureVMVault** > **elementy replikowane**, kliknij prawym przyciskiem myszy maszynę Wirtualną, która została przejścia w tryb failover i wybierz **ponownego włączenia ochrony**.
2. Sprawdź, czy kierunek ochrony jest ustawiony **Azure do środowiska lokalnego**.
3. Lokalnej maszyny Wirtualnej jest wyłączony w trakcie przełączonej w celu zapewnienia spójności danych. Nigdy nie włączaj ją po zakończeniu pracy zastosowania.
4. Po zakończeniu przełączonej maszyna wirtualna zacznie replikację z platformy Azure do lokacji lokalnej.



## <a name="fail-over-from-azure-and-reprotect-the-on-premises-vm"></a>Tryb failover z platformy Azure i włącz ponownie ochronę maszyny Wirtualnej na lokalnym

Przełączyć się z platformy Azure do lokacji lokalnej i Rozpocznij replikację maszyn wirtualnych z lokacji lokalnej do platformy Azure.

1. W **ustawienia** > **elementy replikowane**, kliknij maszynę Wirtualną > **planowanego trybu Failover**.
2. W **potwierdzić planowanego trybu Failover**Sprawdź kierunek pracy awaryjnej (na platformie Azure), a wybierz lokalizacja źródłowa i docelowa.
3. Wybierz **synchronizować dane przed pracy awaryjnej (należy zsynchronizować tylko zmiany różnicowe)**. Ta opcja minimalizuje przestojów maszyn wirtualnych, ponieważ synchronizacji bez zamykania maszyny Wirtualnej.
4. Inicjuj tryb failover. Możesz śledzić postęp trybu failover **zadania** kartę.
5. Po początkowej danych odbywa się synchronizacja i wszystko jest gotowe do zamykania maszyn wirtualnych platformy Azure kliknij **zadania** > planowanego trybu failover zadania nazwa-> **ukończenia pracy awaryjnej**. Zamyka maszyny Wirtualnej Azure, przesyła najnowsze zmiany w lokalnej instalacji programu i uruchamia lokalnej maszyny Wirtualnej.
6. Zaloguj się na lokalnej maszynie Wirtualnej, aby Sprawdź, czy jest dostępna, zgodnie z oczekiwaniami.
7. Lokalnej maszyny Wirtualnej znajduje się teraz w **zatwierdzania oczekującej** stanu. Kliknij przycisk **zatwierdzić**. To spowoduje usunięcie maszyn wirtualnych platformy Azure i jego dysków i przygotowuje lokalnej maszyny Wirtualnej do replikacji odwrotnej.
Aby rozpocząć replikację lokalnej maszyny Wirtualnej do platformy Azure, należy włączyć **odwrócić replikację**. Spowoduje to zainicjowanie replikacji zmiany różnicowe, które wystąpiły od maszyny Wirtualnej platformy Azure został wyłączony.  
