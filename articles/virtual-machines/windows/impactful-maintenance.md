---
title: "Obsługa istotna dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: Istotna konserwacji dla maszyn wirtualnych systemu Windows.
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 75cd4d567deb98e5d2498dc607b43dae483f1c94
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Obsługa istotna dla maszyn wirtualnych

Istnieje kilka przypadków, gdy maszyny wirtualne są ponownie uruchamiane z powodu zaplanowanej konserwacji do podstawowej infrastruktury. Trwa istotna dostępności maszyn wirtualnych hostowanych na platformie Azure, poniżej są teraz dostępne do użycia:

-   Powiadomienia wysyłane co najmniej 30 dni przed wpływu.

-   Wgląd do okna obsługi dla każdej maszyny Wirtualnej.

-   Elastyczność i kontrolę podczas ustawiania dokładny czas konserwacji wpływu maszyn wirtualnych.

Konserwacji na platformie Microsoft Azure jest zaplanowane w iteracji. Początkowa liczba iteracji ma mniejszy zakresu w celu zmniejszenia ryzyka związanego w wprowadza nowe poprawki i funkcje. Nowsze iteracji może obejmować wielu regionach (nigdy nie z tej samej pary regionu). Maszyna wirtualna znajduje się w iteracji jednego konserwacji. Jeśli iteracji została przerwana, pozostałe maszyny wirtualne znajdują się w innym, przyszłych, iteracji.

Iteracja zaplanowanej konserwacji ma dwie fazy: Pre-emptive okna obsługi i okno zaplanowanej konserwacji.

**Okna obsługi Pre-emptive** zapewnia elastyczność do inicjowania obsługi na maszyny wirtualne. W ten sposób można określić, gdy maszyny wirtualne są w pełni funkcjonalne, sekwencji aktualizacji i czas między każdej maszyny Wirtualnej już poddawana konserwacji. Można zapytania do każdej maszyny Wirtualnej, aby zobaczyć, czy jest planowane konserwacji i sprawdź wynik ostatniego żądania obsługi zainicjowane.

**Zaplanowanego okna obsługi** jest podczas Azure zostało zaplanowane na obsługę maszyn wirtualnych. W tym oknie, następującego okna obsługi uprzedzające, można nadal zapytania dla okna obsługi, ale nie można już do organizowania konserwacji.

## <a name="availability-considerations-during-planned-maintenance"></a>Zagadnienia dotyczące dostępności podczas zaplanowanej konserwacji 

### <a name="paired-regions"></a>Sparowanego regionów

Każdy region platformy Azure jest skojarzone z innego regionu w tej samej lokalizacji geograficznej, razem wprowadzeniem regionalnych pary. Podczas wykonywania konserwacji, Azure będzie aktualizować tylko wystąpień maszyn wirtualnych w pojedynczym regionie jego pary. Na przykład podczas aktualizowania maszyn wirtualnych w regionie Północno-środkowe stany USA platforma Azure nie będzie jednocześnie przeprowadzać aktualizacji żadnych maszyn wirtualnych w regionie Południowo-środkowe stany USA. Takie aktualizacje zostaną zaplanowane na inny termin, co pozwoli na korzystanie z trybu failover lub równoważenie obciążenia między regionami. Inne regiony, takie jak Europa Północna, mogą być jednak w trakcie konserwacji w tym samym czasie, co region Wschodnie stany USA.
Przeczytaj więcej na temat [pary regionu Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Vs pojedynczego wystąpienia maszyn wirtualnych. Zestaw dostępności lub maszyny Wirtualnej zestawu skali

W przypadku wdrażania obciążenia przy użyciu maszyn wirtualnych na platformie Azure, można tworzyć maszyn wirtualnych w ramach dostępności ustawiona, aby zapewnić wysoką dostępność aplikacji. Taka konfiguracja powoduje, że podczas awarii albo obsługi zdarzeń, jest dostępny co najmniej jednej maszyny wirtualnej.

W zestawie dostępności poszczególnych maszyn wirtualnych są rozkładane między domenami aktualizacji do 20. Podczas zaplanowanej konserwacji pogarsza tylko jedną aktualizację domeny w danym momencie. Kolejność jest w pełni funkcjonalne domen aktualizacji nie można kontynuować sekwencyjnie podczas zaplanowanej konserwacji. Dla maszyn wirtualnych jednego wystąpienia (nie jest częścią zestawu dostępności) Brak nie można przewidzieć lub oraz wpływ razem na liczbę maszyn wirtualnych.

Zestawy skalowania maszyny wirtualnej są zasobów obliczeń platformy Azure, która umożliwia wdrażanie i zarządzanie nimi zestaw identycznych maszyn wirtualnych jako pojedynczy zasób.
Zestaw skali zawiera podobne gwarancje dostępności ustawiony w formie domeny aktualizacji. 

Aby uzyskać więcej informacji na temat konfigurowania maszyn wirtualnych wysokiej dostępności, zobacz [ *Zarządzaj dostępnością maszyn wirtualnych systemu Windows*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Zaplanowane zdarzenia

Usługa Azure metadanych umożliwia odnajdywanie informacji o maszyna wirtualna hostowana na platformie Azure. Zaplanowane zdarzenia, w jednej z następujących kategorii narażonych powierzchni informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu.

Aby uzyskać więcej informacji o zdarzeniach zaplanowane dotyczą [Azure metadanych usługi — zaplanowanego zdarzenia](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Odnajdywanie konserwacji i powiadomienia

Harmonogram konserwacji jest widoczne dla klientów na poziomie poszczególnych maszyn wirtualnych. Portalu Azure, interfejsu API, programu PowerShell lub interfejsu wiersza polecenia można użyć w zapytaniu dla systemu windows uprzedzające i zaplanowanej konserwacji. Ponadto oczekuje się powiadomienie (poczta e-mail) w przypadku, gdy jeden lub więcej maszyn wirtualnych, które ma wpływ podczas procesu.

Zarówno uprzedzające konserwacji, jak i fazy zaplanowanej konserwacji zaczynają się powiadomienie. Oczekuje się pojedyncze powiadomienia dla subskrypcji platformy Azure. Powiadomienia są wysyłane do administratora subskrypcji i współadministratora domyślnie. Można również skonfigurować odbiorców, powiadomienia konserwacji.

### <a name="view-the-maintenance-window-in-the-portal"></a>Wyświetl okno obsługi w portalu 

Można korzystać z portalu Azure i wyszukaj zaplanowane do obsługi maszyn wirtualnych.

1.  Zaloguj się do Portalu Azure.

2.  Kliknij przycisk i Otwórz **maszyn wirtualnych** bloku.

3.  Kliknij przycisk **kolumn** przycisk, aby otworzyć listę dostępnych kolumn, które można wybierać

4.  Wybierz i Dodaj **okna obsługi** kolumn. Maszyny wirtualne, które są planowane do konserwacji ma udostępniane okna obsługi. Po konserwacji zostanie ukończona lub zostało przerwane dla okna obsługi, nie jest widoczne.

### <a name="query-maintenance-details-using-the-azure-api"></a>Szczegóły obsługi zapytań przy użyciu interfejsu API platformy Azure

Użyj [uzyskać informacji o maszyny Wirtualnej interfejsu API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) i poszukaj widok wystąpienia odnaleźć szczegółowe informacje konserwacji w poszczególnych maszyn wirtualnych. Odpowiedź zawiera następujące elementy:

  - isCustomerInitiatedMaintenanceAllowed: wskazuje, czy można teraz zainicjować uprzedzające ponownego wdrażania na maszynie Wirtualnej.

  - preMaintenanceWindowStartTime: godzina rozpoczęcia okna obsługi uprzedzające.

  - preMaintenanceWindowEndTime: godzina zakończenia okna obsługi uprzedzające. Po upływie tego czasu nie można zainicjować obsługi na tej maszynie Wirtualnej.
    
  - maintenanceWindowStartTime: godzina rozpoczęcia okna zaplanowanej konserwacji w przypadku maszyny Wirtualnej są w pełni funkcjonalne.

  - maintenanceWindowEndTime: godzina zakończenia okna zaplanowanej konserwacji.
  
  - lastOperationResultCode: wynik ostatnią operację ponownego wdrażania konserwacji.
 
  - lastOperationMessage: opisujące wynik ostatnią operację ponownego wdrażania obsługi wiadomości.

## <a name="pre-emptive-redeploy"></a>Uprzedzające ponownego wdrażania

Akcja uprzedzające ponownego wdrażania zapewnia elastyczność kontrolować czas stosowania konserwacji do maszyn wirtualnych na platformie Azure. Rozpoczyna się oknem obsługi uprzedzające, w którym można określić dokładnie raz dla każdego z maszyn wirtualnych, należy ponownie uruchomić od planowanej konserwacji. Przypadki użycia, gdzie przydaje się takie funkcje są następujące:

-   Konserwacja konieczne z odbiorcy końcowego.

-   Nie wystarcza czasu zaplanowanego okna obsługi oferowanych na platformie Azure.
    Możliwe, że okna dzieje się na czas zajętej tygodnia lub jest zbyt długa.

-   Wystąpienie usługi lub aplikacje wielowarstwowe należy wystarczającą ilość czasu między dwóch maszyn wirtualnych lub niektórych sekwencji, które należy wykonać.

Podczas wywoływania dla uprzedzające ponownego wdrażania maszyny wirtualnej maszyny Wirtualnej są przenoszone do już zaktualizowany węzeł i uprawnień go ponownie na zachowaniu opcji konfiguracji i skojarzonych zasobów. Ten sposób tymczasowego dysku zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane.

Uprzedzające ponownego wdrażania włączeniu raz dla maszyny Wirtualnej. Jeśli występuje błąd podczas procesu, operacja została przerwana, nie ma wpływu na Maszynie wirtualnej i jest ona wykluczana z iteracji zaplanowanej konserwacji. Będzie można z Tobą kontaktu w późniejszym czasie z nowego harmonogramu i oferowane nowych możliwościach zaplanować i sekwencjonowaniu wpływu na maszyny wirtualne.