---
title: toofail aaaHow z Azure tooVMware | Dokumentacja firmy Microsoft
description: "Po pracy w trybie failover tooAzure maszyn wirtualnych można zainicjować powrotu po awarii toobring maszyn wirtualnych wstecz tooon lokalnych. Dowiedz się, jak kopii toofail kroki hello."
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
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Niepowodzenie z lokacji lokalnej Azure tooan

W tym artykule opisano, jak toofail kopię maszyn wirtualnych z lokacji lokalnej toohello maszyn wirtualnych platformy Azure. Hello instrukcje w tym artykule toofail z powrotem z maszyn wirtualnych VMware lub serwerach fizycznych systemu Windows i Linux po ich już nie za pośrednictwem z tooAzure lokacji lokalne powitania przy użyciu hello [VMware replikowanie maszyn wirtualnych i fizycznych tooAzure serwerów z usługą Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) samouczka.

> [!WARNING]
> Jeśli masz [ukończone migracji](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)przeniesionego hello maszyny wirtualnej tooanother zasobów grupy lub został usunięty hello maszyny wirtualnej platformy Azure, nie powrotu po awarii po.

> [!NOTE]
> Jeśli ma przejścia w tryb failover maszyny wirtualne VMware można hosta funkcji Hyper-v tooa powrotu po awarii.

## <a name="overview-of-failback"></a>Omówienie powrotu po awarii
Oto, jak działa powrotu po awarii. Po za pośrednictwem tooAzure ma nie powiodła się, nie zostanie lokacji lokalnej tooyour Wstecz w kilku etapach:

1. [Włącz ponownie ochronę](site-recovery-how-to-reprotect.md) hello maszyn wirtualnych na platformie Azure, aby rozpoczynały się maszyny wirtualne tooVMware tooreplicate w lokacji lokalnej. W ramach tego procesu również należy:
    1. Skonfiguruj lokalny główny serwer docelowy: Windows głównego celu dla maszyny wirtualnej systemu Windows i [główny cel Linux](site-recovery-how-to-install-linux-master-target.md) dla maszyn wirtualnych systemu Linux.
    2. Konfigurowanie [serwera przetwarzania](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Zainicjuj [Wznów](site-recovery-how-to-reprotect.md). Spowoduje to wyłączyć hello na lokalnej maszynie wirtualnej i zsynchronizować hello Azure danych maszyny wirtualnej z hello lokalnych dysków.
5. Po lokacji lokalnej tooyour replikowania maszyn wirtualnych na platformie Azure, zainicjowaniu błędu za pośrednictwem z lokacji lokalnej toohello platformy Azure.

Po danych nie powiodło się ponownie, Wznów maszyn wirtualnych lokalnie hello, które nie powiodło się do, aby rozpoczynały się tooreplicate tooAzure.

Aby szybko zapoznać Obejrzyj powitania po klip wideo dotyczący sposobu toofail za pośrednictwem z Azure tooan lokalnej lokacji.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Niepowodzenie lokalizacji oryginalnej lub alternatywnej toohello Wstecz

Nie powiodło się na maszynie wirtualnej VMware, może się nie powieść toohello Wstecz, tego samego źródła lokalnej maszyny wirtualnej, gdy jego nadal istnieje. W tym scenariuszu hello są replikowane tylko ponownie. Ten scenariusz jest nazywany odzyskiwanie do oryginalnej lokalizacji. Jeśli nie istnieje hello na lokalnej maszynie wirtualnej, scenariusz hello jest odzyskiwania do lokalizacji alternatywnej.

> [!NOTE]
> Można tylko oryginalny vCenter toohello powrotu po awarii i serwer konfiguracji. Nie można wdrożyć nowy serwer konfiguracji i korzystania z niego powrotu po awarii. Ponadto nie można dodać nowego toohello istniejącej konfiguracji serwera vCenter i powrotu po awarii do hello nowe vCenter.

#### <a name="original-location-recovery"></a>Odzyskiwanie do oryginalnej lokalizacji

Jeśli nie zostanie toohello wstecz oryginalna maszyna wirtualna, wymagane są hello następujące warunki:
* Maszyna wirtualna hello jest zarządzana przez serwer vCenter, następnie hello hosta ESX główny serwer docelowy powinien mieć dostępu toohello maszyny wirtualnej w magazynie danych.
* Jeśli maszyna wirtualna hello znajduje się na hoście ESX, ale nie jest zarządzana przez vCenter, hello dysku twardego maszyny wirtualnej hello musi być w magazynie danych mogą uzyskiwać dostęp hello główny cel przez hosta.
* Jeśli maszyna wirtualna znajduje się na hoście ESX i nie używa vCenter, następnie należy wykonać odnajdywania hosta ESX hello hello głównego celu przed możesz Włącz ponownie ochronę. Dotyczy to powrót fizycznych serwerów powrotu po awarii zbyt.
* Użytkownik może zakończyć się niepowodzeniem wstecz tooa wirtualna sieć SAN (vSAN) lub dysk, który jest oparty na urządzeniu raw mapowania (RDM), jeśli dyski hello już istnieją i są połączone toohello na lokalnej maszynie wirtualnej.

#### <a name="alternate-location-recovery"></a>Odzyskiwanie do lokalizacji alternatywnej
Jeśli nie istnieje hello na lokalnej maszynie wirtualnej przed ponownej ochrony maszyny wirtualnej hello, hello scenariusz jest nazywany odzyskiwania do lokalizacji alternatywnej. przepływ pracy ponownej ochrony Hello ponownie tworzy hello na lokalnej maszynie wirtualnej. Spowoduje to również pobierania danych.

* Przechodzenia wstecz tooan alternatywnej lokalizacji hello maszyny wirtualnej zostanie odzyskany toohello tego samego hosta ESX, na które hello główny serwer docelowy jest wdrożona. Witaj magazynu danych, który został użyty dysk hello toocreate będzie hello tego samego magazynu danych, które zostały wybrane podczas ponownej ochrony maszyny wirtualnej hello.
* Może się nie powieść ponownie tylko tooa maszyny wirtualnej plików systemowych (VMFS) magazynu danych. Jeśli masz vSAN lub RDM ponownej ochrony i powrotu po awarii nie będzie działać.
* Ponownej ochrony obejmuje jedną początkowy transfer dużej ilości danych następuje hello zmiany. Ten proces nie istnieje, ponieważ hello maszyny wirtualnej nie istnieje lokalnie. pełne dane Hello musi toobe replikowane ponownie. Ta ponownej ochrony również zajmie więcej czasu niż odzyskiwanie do oryginalnej lokalizacji.
* Nie można przerwać ponownie toovSAN lub RDM opartych na dyskach. Na VMFS magazyn danych można tworzyć tylko nowe dyski maszyny wirtualnej (VMDKs).

Fizyczny komputer podczas przejścia w tryb failover tooAzure, można symulować powrotem tylko jako maszyny wirtualnej VMware (również określonego tooas P2A2V). Ten przepływ podlega hello odzyskiwanie do lokalizacji alternatywnej.

* Serwera fizycznego systemu Windows Server 2008 R2 z dodatkiem SP1, chronionych i przejścia w tryb failover tooAzure, nie może się nie powiodła się ponownie.
* Upewnij się, że można wykryć co najmniej jeden główny cel serwera i hello niezbędne ESX/ESXi hostów toowhich należy ponownie toofail.

## <a name="have-you-completed-reprotection"></a>Czy ukończono ponowne włączenie ochrony?
Przed kontynuowaniem pełną hello Wznów kroki hello maszyny wirtualne są w stanie zreplikowanych, a następnie można zainicjować lokalnej lokacji wstecz tooan trybu failover. Aby uzyskać więcej informacji, zobacz [jak tooreprotect z Azure lokalnych tooon](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Serwer konfiguracji jest wymagana lokalnie czy powrotu po awarii. Podczas powrotu po awarii hello maszyny wirtualnej musi istnieć w bazie danych serwera konfiguracji hello lub powrotu po awarii nie powiodło się. W związku z tym upewnij się, wykonanie zaplanowanego tworzenia kopii zapasowych serwera. Jeśli wystąpił awarii, konieczne będzie toorestore powitania serwera z hello tego samego adresu IP dla toowork powrotu po awarii.
* Witaj główny serwer docelowy nie powinna mieć żadnych migawek przed wyzwalania powrotu po awarii.

## <a name="steps-toofail-back"></a>Kroki toofail Wstecz

> [!IMPORTANT]
> Przed rozpoczęciem powrotu po awarii, upewnij się, że ukończono ponowne włączenie ochrony maszyn wirtualnych hello. maszyny wirtualne Hello powinna być w stanie chronionym i ich kondycję powinna być **OK**. maszyny wirtualne hello tooreprotect odczytu [jak tooreprotect](site-recovery-how-to-reprotect.md).

1. W hello zreplikowanych elementów strony, wybierz maszynę wirtualną hello i kliknij go prawym przyciskiem myszy tooselect **nieplanowany tryb Failover**.
2. W **potwierdzić trybu Failover**, sprawdź hello kierunek pracy awaryjnej (na platformie Azure), a następnie wybierz hello punktu odzyskiwania (Najnowsza lub najnowszą wersję aplikacji hello spójne) mają toouse hello pracy awaryjnej. punktu spójnego aplikacji Hello znajduje się za hello ostatniego punktu w czasie i powoduje utratę danych.
3. Podczas pracy w trybie failover Usługa Site Recovery zamyka hello maszyn wirtualnych na platformie Azure. Po sprawdzeniu, że powrót po awarii została ukończona, zgodnie z oczekiwaniami, można sprawdzić, zamknij hello maszyn wirtualnych na platformie Azure.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>punkt odzyskiwania toowhat wstecz hello maszyny wirtualne mogą nie?

Podczas powrotu po awarii masz dwie opcje toofail wstecz hello odzyskiwanie maszyny wirtualnej/plan.

W przypadku wybrania hello najnowsze przetworzone punktu w czasie wszystkich maszyn wirtualnych będzie można przełączyć tootheir najnowszego dostępnego punktu w czasie. W przypadku grupy replikacji w ramach planu odzyskiwania hello, a następnie każdej maszyny wirtualnej z grupy replikacji hello zostaną przełączone awaryjnie tooits niezależnie od ostatniego punktu w czasie.

Nie można przerwać powrót maszyny wirtualnej do momentu składa się z co najmniej jeden punkt odzyskiwania. Nie można przerwać wstecz planu odzyskiwania, dopóki wszystkie maszyny wirtualne mają co najmniej jednego punktu odzyskiwania.

> [!NOTE]
> Najnowszy punkt odzyskiwania jest punkt odzyskiwania spójna w razie awarii.

W przypadku wybrania punktu odzyskiwania na poziomie aplikacji hello awarii jednej maszyny wirtualnej zostanie odzyskana tooits najnowszego punktu odzyskiwania zapewniających spójność aplikacji. W przypadku hello planu odzyskiwania z grupą replikacji każda grupa replikacji odzyska tooits wspólnego punktu odzyskiwania.
Należy pamiętać, że punktów odzyskiwania zapewniających spójność aplikacji może być za w czasie i może być utrata danych.

### <a name="what-happens-toovmware-tools-post-failback"></a>Co się stanie, że narzędzia tooVMware post powrotu po awarii?

Podczas pracy awaryjnej tooAzure narzędzi VMware hello nie są uruchomione na powitania maszyny wirtualnej platformy Azure. W przypadku maszyny wirtualnej systemu Windows funkcja automatycznego odzyskiwania systemu wyłącza hello narzędzia VMware w trybie failover. W przypadku maszyny wirtualnej systemu Linux funkcja automatycznego odzyskiwania systemu odinstalowuje hello narzędzia VMware w trybie failover.

Podczas powrotu po awarii maszyny wirtualnej systemu Windows hello narzędzia VMware hello są ponownie włączyć po awarii. Podobnie w przypadku maszyny wirtualnej systemu linux narzędzi VMware hello są instalowane jeszcze raz na maszynie hello podczas powrotu po awarii.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu powrotu po awarii, należy toocommit hello tooensure maszyny wirtualnej, które odzyskane maszynach wirtualnych platformy Azure są usuwane.

### <a name="commit"></a>Zatwierdzenie
Zatwierdzenie jest wymagane tooremove hello przejścia w tryb failover maszyny wirtualnej z platformy Azure.
Kliknij prawym przyciskiem myszy element hello chroniony, a następnie kliknij przycisk **zatwierdzić**. Zadania spowoduje usunięcie hello przejścia w tryb failover maszyny wirtualne na platformie Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Włącz ponownie ochronę z lokalnymi tooAzure

Po zakończeniu przekazywania maszyny wirtualnej jest do lokacji lokalnej hello, ale nie będzie można go chronić. toostart tooreplicate tooAzure ponownie hello następujące:

1. W **magazynu** > **ustawienie** > **elementy replikowane**, wybierz hello maszyn wirtualnych, które nie zostały ponownie, a następnie kliknij przycisk  **Włącz ochronę ponownie**.
2. Nadaj wartość hello hello serwera przetwarzania, który wymaga toobe używana tooAzure wstecz toosend danych.
3. Kliknij przycisk **OK** toobegin hello ponownej ochrony zadania.

> [!NOTE]
> Po rozruchu maszyny wirtualnej lokalnymi, dopiero po pewnym czasie dla agenta hello tooregister wstecz toohello konfiguracji serwera (too15 minut). W tym czasie Wznów zakończy się niepowodzeniem i zwraca komunikat o błędzie informujący, że agent hello nie jest zainstalowany. Poczekaj kilka minut, a następnie spróbuj ponownie ponownej ochrony.

Po Wznów hello zakończenie zadania, hello maszyna wirtualna wykonuje replikację tooAzure Wstecz i możliwość pracy w trybie failover.

## <a name="common-issues"></a>Typowe problemy
Upewnij się, że ten vCenter hello jest w stanie połączenia przed wykonaniem powrotu po awarii. W przeciwnym razie rozłączanie dysków i dołączać wstecz toohello maszyny wirtualnej zakończy się niepowodzeniem.
