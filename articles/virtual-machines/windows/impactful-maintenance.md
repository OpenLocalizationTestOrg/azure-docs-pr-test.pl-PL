---
title: "Obsługa aaaImpactful dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 98afaea0fdca796177e075b33615b03f1e7a0fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Obsługa istotna dla maszyn wirtualnych

Istnieje kilka przypadków, gdy maszyny wirtualne są ponownie uruchamiane powodu tooplanned toohello utrzymania podstawowej infrastruktury. Trwa istotna toothe dostępność maszyn wirtualnych hostowanych na platformie Azure, następujące hello są teraz dostępne dla toouse możesz:

-   Powiadomienia wysyłane co najmniej 30 dni przed hello wpływu.

-   Widoczność toohello okna obsługi dla każdej maszyny Wirtualnej.

-   Elastyczność i kontrolę podczas ustawiania hello dokładny czas konserwacji wpływu maszyn wirtualnych.

Konserwacji na platformie Microsoft Azure jest zaplanowane w iteracji. Początkowa liczba iteracji ma mniejszy zakresu w kolejności tooreduce hello zagrożenia w procesie rozmieszczania nowe poprawki i funkcje. Nowsze iteracji może obejmować wielu regionach (nigdy nie z hello tego samego regionu pary). Maszyna wirtualna znajduje się w iteracji jednego konserwacji. Jeśli iteracji została przerwana, pozostałe maszyny wirtualne znajdują się w innym, przyszłych, iteracji.

Witaj iteracji zaplanowanej konserwacji ma dwie fazy: Pre-emptive okna obsługi i okno zaplanowanej konserwacji.

Witaj **okna obsługi Pre-emptive** zapewnia hello elastyczność tooinitiate hello konserwacji na maszyny wirtualne. W ten sposób można określić, gdy maszyny wirtualne są w pełni funkcjonalne, hello sekwencji aktualizacji hello i czas powitania od każdej maszyny Wirtualnej już poddawana konserwacji. Można zapytania toosee każdej maszyny Wirtualnej, czy jest planowane konserwacji i sprawdzić hello wynik ostatniego żądania obsługi zainicjowane.

Witaj **zaplanowanego okna obsługi** jest harmonogramem Azure ma maszyn wirtualnych na powitania konserwacji. W tym oknie, następującego okna obsługi uprzedzające, możesz nadal kwerendy hello okna obsługi, ale nie będą mogli tooorchestrate hello konserwacji.

## <a name="availability-considerations-during-planned-maintenance"></a>Zagadnienia dotyczące dostępności podczas zaplanowanej konserwacji 

### <a name="paired-regions"></a>Sparowanego regionów

Każdy region platformy Azure jest łączyć się z innego regionu w hello tej samej lokalizacji geograficznej, razem wprowadzeniem regionalnych pary. Podczas wykonywania konserwacji, Azure będzie aktualizować tylko hello wystąpień maszyn wirtualnych w pojedynczym regionie jego pary. Na przykład podczas aktualizowania hello maszyn wirtualnych w północno-środkowe stany, Azure nie może zaktualizować wszystkie maszyny wirtualne w południowo-środkowe stany na powitania tym samym czasie. Takie aktualizacje zostaną zaplanowane na inny termin, co pozwoli na korzystanie z trybu failover lub równoważenie obciążenia między regionami. Jednak innych regionów, takie jak Europa Północna, Europa może być w trakcie konserwacji na hello sam czas jako wschodnie stany USA.
Przeczytaj więcej na temat [pary regionu Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Vs pojedynczego wystąpienia maszyn wirtualnych. Zestaw dostępności lub maszyny Wirtualnej zestawu skali

W przypadku wdrażania obciążenia przy użyciu maszyn wirtualnych na platformie Azure, możesz utworzyć hello maszyn wirtualnych w ramach zestawem dostępności w kolejności tooprovide wysokiej dostępności tooyour aplikacji. Taka konfiguracja powoduje, że podczas awarii albo obsługi zdarzeń, jest dostępny co najmniej jednej maszyny wirtualnej.

W zestawie dostępności poszczególnych maszyn wirtualnych są rozkładane między się too20 domen aktualizacji. Podczas zaplanowanej konserwacji pogarsza tylko jedną aktualizację domeny w danym momencie. kolejność Hello jest w pełni funkcjonalne domen aktualizacji nie można kontynuować sekwencyjnie podczas zaplanowanej konserwacji. Dla pojedynczego wystąpienia maszyn wirtualnych (nie jest częścią zestawu dostępności), nie istnieje żadne toopredict sposób lub oraz wpływ razem na liczbę maszyn wirtualnych.

Zestawy skalowania maszyny wirtualnej są zasobami obliczeń platformy Azure umożliwiającą toodeploy i zarządzać zestawem identycznych maszyn wirtualnych jako pojedynczy zasób.
zestaw skali Hello zawiera podobne gwarancje tooan zestawem dostępności w formie domeny aktualizacji. 

Aby uzyskać więcej informacji na temat konfigurowania maszyn wirtualnych wysokiej dostępności, zobacz [ *Zarządzanie dostępność maszyn wirtualnych systemu Windows hello*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Zaplanowane zdarzenia

Usługa Azure metadanych umożliwia toodiscover informacji na temat maszyna wirtualna hostowana na platformie Azure. Zaplanowane zdarzenia, kategorie hello widoczne, powierzchni informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu.

Aby uzyskać więcej informacji o zdarzeniach zaplanowane odwoływać się za[Azure metadanych usługi — zaplanowanego zdarzenia](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Odnajdywanie konserwacji i powiadomienia

Harmonogram konserwacji jest widoczne toocustomers na poziomie hello poszczególnych maszyn wirtualnych. Można użyć Azure portal, tooquery interfejsu API, programu PowerShell lub interfejsu wiersza polecenia systemu windows uprzedzające i zaplanowanej konserwacji. Ponadto oczekuje się powiadomienie (poczta e-mail) w przypadku hello w przypadku, gdy jeden lub więcej maszyn wirtualnych, które ma wpływ podczas procesu hello.

Zarówno uprzedzające konserwacji, jak i fazy zaplanowanej konserwacji zaczynają się powiadomienie. Oczekiwane tooreceive pojedyncze powiadomienia dla subskrypcji platformy Azure. Hello jest wysyłane powiadomienie administratora i współadministrator subskrypcji toohello domyślnie. Można również skonfigurować hello odbiorców, powiadomienia konserwacji.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Wyświetl hello okna obsługi w portalu hello 

Można użyć hello portalu Azure i poszukaj zaplanowane do obsługi maszyn wirtualnych.

1.  Zaloguj się toohello portalu Azure.

2.  Kliknij przycisk i otwórz hello **maszyn wirtualnych** bloku.

3.  Kliknij przycisk hello **kolumn** przycisk tooopen hello lista dostępnych kolumn toochoose z

4.  Wybierz i Dodaj hello **okna obsługi** kolumn. Maszyny wirtualne, które są planowane do konserwacji ma okna obsługi hello udostępniane. Po konserwacji zostanie ukończona lub zostało przerwane dla okna obsługi, nie jest widoczne.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Szczegóły obsługi zapytania przy użyciu interfejsu API Azure hello

Użyj hello [uzyskać informacji o maszyny Wirtualnej interfejsu API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) i poszukaj hello wystąpienia widoku toodiscover hello konserwacji szczegółowe informacje o poszczególnych maszyn wirtualnych. odpowiedź Hello zawiera hello następujące elementy:

  - isCustomerInitiatedMaintenanceAllowed: wskazuje, czy można teraz zainicjować uprzedzające ponownego wdrażania na powitania maszyny Wirtualnej.

  - preMaintenanceWindowStartTime: hello/godzina rozpoczęcia okna obsługi uprzedzające hello.

  - preMaintenanceWindowEndTime: hello godzina zakończenia okna obsługi uprzedzające hello. Po upływie tego czasu będzie już możliwe tooinitiate konserwacji na tej maszynie Wirtualnej.
    
  - maintenanceWindowStartTime: hello Uruchom czasu hello zaplanowanego okna obsługi, gdy wpływ na maszynie Wirtualnej.

  - maintenanceWindowEndTime: hello godzina zakończenia hello zaplanowanego okna obsługi.
  
  - lastOperationResultCode: hello wyników ostatnią operację ponownego wdrażania konserwacji.
 
  - lastOperationMessage: opisujące wynik hello ostatnią operację ponownego wdrażania obsługi komunikatów.

## <a name="pre-emptive-redeploy"></a>Uprzedzające ponownego wdrażania

Akcja uprzedzające ponownego wdrażania zawiera hello elastyczność toocontrol hello godzinę obsługi maszyn wirtualnych tooyour zastosowane na platformie Azure. Planowana konserwacja rozpoczyna się od uprzedzające konserwacyjne, gdzie można określić hello dokładnie raz dla każdego z toobe sieci maszyn wirtualnych, ponowny rozruch. Przypadki użycia, gdzie przydaje się takie funkcje są następujące:

-   Toobe konieczność obsługi skoordynować z hello końcowych klienta.

-   Witaj zaplanowanego okna obsługi oferowanych na platformie Azure nie jest wystarczający.
    Możliwe, że okna hello sytuacji toobe na czas zajętej hello tygodnia lub jest zbyt długa.

-   Wystąpienie usługi lub aplikacje wielowarstwowe należy wystarczającą ilość czasu między dwoma maszyn wirtualnych lub toofollow sekwencji.

Podczas wywoływania dla uprzedzające ponownego wdrażania maszyny wirtualnej przenosi hello tooan maszyny Wirtualnej już zaktualizowany węzeł, a następnie włącza go ponownie, zachowując opcji konfiguracji i skojarzonych zasobów. Dzięki temu dysku tymczasowym hello zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane.

Uprzedzające ponownego wdrażania włączeniu raz dla maszyny Wirtualnej. Jeśli występuje błąd podczas procesu hello, hello operacja została przerwana, hello, który nie ma wpływu na maszyny Wirtualnej i został wykluczony z hello planowanych konserwacji iteracji. Będzie można z Tobą kontaktu w późniejszym czasie z nowego harmonogramu i oferowane nowe możliwości tooschedule i sekwencji hello wpływu na maszyny wirtualne.