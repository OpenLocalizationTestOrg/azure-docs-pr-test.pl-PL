---
title: "aaaProtect wdrażania aplikacji wielowarstwowych SAP NetWeaver przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooprotect SAP NetWeaver wdrożenia aplikacji za pomocą usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Ochrona wdrażania aplikacji wielowarstwowych SAP NetWeaver przy użyciu usługi Azure Site Recovery

Większości wdrożeń SAP duży i średnie ma rozwiązanie odzyskiwania po awarii.  znaczenie Hello rozwiązania w zakresie odzyskiwania po awarii niezawodny i testować wzrosło jako więcej biznesowych podstawowych, które procesy są przenoszone tooapplications, takie jak SAP.  Usługa Azure Site Recovery został przetestowane i zintegrowane z aplikacje SAP i przekracza możliwości hello większości lokalnymi rozwiązaniami odzyskiwania po awarii, w dolnym całkowity koszt posiadania (TCO) niż konkurencyjnych rozwiązania.
Za pomocą usługi Azure Site Recovery można wykonywać następujące czynności:
* Włącz ochronę SAP NetWeaver i produkcji NetWeaver aplikacje uruchamiane lokalnie, poprzez replikację tooAzure składników.
* Włącz ochronę SAP NetWeaver i produkcji NetWeaver aplikacje platformy Azure, poprzez replikację tooanother składniki centrum danych Azure.
* Uproszczenie migracja do chmury, za pomocą usługi Site Recovery toomigrate Twojego tooAzure wdrożenia SAP.
* Uprość uaktualnienia, testowanie i tworzenie prototypów projektu SAP, tworząc na żądanie klony środowiska produkcyjnego na potrzeby testowania aplikacji SAP.

W tym artykule opisano, jak tooprotect SAP NetWeaver wdrożeń aplikacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md). W tym artykule omówiono hello najlepsze rozwiązania dotyczące Zabezpieczanie wdrożenia SAP NetWeaver trójwarstwowa na platformie Azure przez replikowanie tooanother centrum danych Azure przy użyciu usługi Azure Site Recovery, konfiguracji i hello obsługiwane scenariusze i jak tooperform trybu failover, zarówno testowania Praca awaryjna (testowanie odzyskiwania po awarii), a rzeczywista praca awaryjna.


## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem upewnij się, że rozumiesz hello poniżej:

1. [Replikowanie tooAzure maszyny wirtualnej](azure-to-azure-walkthrough-enable-replication.md)
2. Jak zbyt[projektowania sieci odzyskiwania](site-recovery-azure-to-azure-networking-guidance.md)
3. [Ten test trybu failover tooAzure](azure-to-azure-walkthrough-test-failover.md)
4. [Sposób tooAzure trybu failover](site-recovery-failover.md)
5. Jak zbyt[replikacji kontrolera domeny](site-recovery-active-directory.md)
6. Jak zbyt[replikacji programu SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Z usługą Azure Site Recovery można wdrożyć rozwiązanie odzyskiwania po awarii dla hello następujące scenariusze:
* SAP komputerów z systemami w jednym centrum danych Azure, replikowanie tooanother centrum danych Azure (Azure do platformy Azure DR), ponieważ zaprojektowana [tutaj](https://aka.ms/asr-a2a-architecture).
* Systemy SAP działających na serwerach VMWare (lub fizycznych) lokalnej replikacji lokacji tooa odzyskiwania po awarii w centrum danych Azure (VMware do platformy Azure DR), wymagająca niektóre dodatkowe składniki zaprojektowana [tutaj](https://aka.ms/asr-v2a-architecture).
* Systemie SAP funkcji Hyper-V lokalnej replikacji lokacji tooa odzyskiwania po awarii w centrum danych Azure (funkcji Hyper-V-do Azure DR), wymagająca niektóre dodatkowe składniki zaprojektowana [tutaj](https://aka.ms/asr-h2a-architecture).

Ten dokument używa funkcji odzyskiwania po awarii programu SAP hello pierwszy case - Azure-Azure DR - toodemonstrate usługi Azure Site Recovery w. Replikacja usługi Azure Site Recovery jest niezależny od aplikacji, hello proces opisany jest oczekiwany toohold w innych sytuacjach również.

### <a name="required-foundation-services"></a>Foundation wymagane usługi
W tym scenariuszu dokumentacji wszystkich została wdrożona z powitania po wdrożeniu usługi foundation:
* ExpressRoute lub lokacja lokacja wirtualnej sieci prywatnej (VPN)
* Co najmniej jeden kontroler domeny usługi Active Directory i serwer DNS działające na platformie Azure

Zaleca się, że powyższe infrastruktury hello jest ustalonych toodeploying wcześniejsze usługi Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Typowe wdrożenie aplikacji SAP
Duże Klienci SAP zwykle wdrażać między 6 too20 poszczególne aplikacje SAP.  Większość tych aplikacji są oparte na powitania aparaty SAP NetWeaver ABAP lub Java.  Obsługa tych podstawowych NetWeaver aplikacji są wiele mniejszych aparaty autonomiczny określonego z systemem innym niż SAP NetWeaver - i zwykle niektóre aplikacje z systemem innym niż SAP.  

Jest krytyczne tooinventory wszystkich hello SAP aplikacji uruchamianych w orientacji poziomej i toodetermine hello wdrożeń w trybie (warstwy 2 lub 3-warstwowej), wersji, poprawki, rozmiary, churn — szybkości przetwarzania oraz wymagań dotyczących trwałości dysku.

![Wzorzec wdrożenia](./media/site-recovery-sap/sap-typical-deployment.png)

Warstwa trwałości bazy danych SAP Hello powinny być chronione za pomocą hello natywnych narzędzi bazami danych, takich jak AlwaysOn programu SQL Server, Oracle DataGuard lub HANA replikacji systemu. powitania klienta warstwy nie jest również chroniony za pomocą usługi Azure Site Recovery, ale jest ważne tooconsider tematy, które mają wpływ na tę warstwę, takich jak opóźnienie propagacji DNS, zabezpieczeń i dostępu zdalnego toohello odzyskiwania po awarii centrum danych.

Usługa Azure Site Recovery jest hello zalecane rozwiązania warstwy aplikacji hello, w tym SCS (). Inne aplikacje, takie jak aplikacje NetWeaver SAP i aplikacje z systemem innym niż SAP stanowią część hello ogólne SAP środowiska wdrażania, a także powinny być chronione przy użyciu usługi Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Replikowanie maszyn wirtualnych
Postępuj zgodnie z [w tych wskazówkach](azure-to-azure-walkthrough-enable-replication.md) toostart replikacji wszystkich hello SAP aplikacji maszyn wirtualnych toohello centrum danych Azure odzyskiwania po awarii.

Jeśli używasz statycznego adresu IP, można określić IP hello, interesujące hello tootake maszyny wirtualnej w hello sieci interfejsu karty sekcji w ustawieniach obliczeń i sieci.

![Adres IP obiektu docelowego](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Tworzenie planu odzyskiwania
Plan odzyskiwania umożliwia sekwencjonowania trybu failover hello różnych poziomów w wielowarstwowej aplikacji, w związku z tym zachowaniu spójności aplikacji. Wykonaj kroki hello opisane [tutaj](site-recovery-create-recovery-plans.md) podczas tworzenia planu odzyskiwania dla aplikacji sieci web w wielowarstwowych.

### <a name="adding-scripts-toohello-recovery-plan"></a>Dodawanie skryptów toohello planu odzyskiwania
Może być konieczne toodo niektóre operacje na powitania trybu failover trybu failover i testowanie post maszyn wirtualnych platformy Azure dla twojej aplikacji toofunction poprawnie. Można zautomatyzować hello post trybu failover operacji, takich jak aktualizacja wpisu DNS i zmiana skojarzenia i połączenia, dodając odpowiednie skrypty w planie odzyskiwania hello zgodnie z opisem w [w tym artykule](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>Aktualizację DNS
Jeśli hello DNS jest skonfigurowany do dynamicznej aktualizacji DNS, a następnie maszyn wirtualnych zwykle po rozpoczęciu aktualizacji hello DNS z hello nowego adresu IP. Tooadd tooupdate jawne krok DNS z hello nowe adresy IP maszyn wirtualnych hello następnie należy dodać to [skryptu tooupdate IP w systemie DNS](https://aka.ms/asr-dns-update) akcji post na grupach planu odzyskiwania.  

## <a name="example-azure-to-azure-deployment"></a>Przykład wdrożenia usługi Azure do platformy Azure
Na diagramie hello poniżej scenariusza odzyskiwania po awarii Azure do platformy Azure usługi Azure Site Recovery hello przedstawiono:
* Witaj podstawowego centrum danych znajduje się w Singapuru (Azja południowo-wschodnia Azure) i hello odzyskiwania po awarii centrum danych jest Hongkong (Azja Wschodnia Azure).  W tym scenariuszu lokalną wysoką dostępność są udostępniane przez mających dwie maszyny wirtualne uruchomione w trybie synchronicznym w Singapurze AlwaysOn programu SQL Server.
* Hello ASCS udziału pliku może być używane tooprovide wysokiej dostępności dla hello SAP pojedynczych punktów awarii. ASCS udziału plików nie wymaga udostępnionego dysku klastra, a aplikacje, takie jak SIOS nie są wymagane.
* Ochrony DR dla warstwy DBMS hello jest osiągane przy użyciu replikacji asynchronicznej.
* W tym scenariuszu pokazano "symetryczne DR" — termin używany toodescribe rozwiązanie odzyskiwania po awarii jest dokładny repliki produkcji, w związku z tym hello rozwiązanie odzyskiwania po awarii programu SQL Server ma lokalnego wysokiej dostępności. Użycie Hello symetryczne odzyskiwania po awarii nie jest obowiązkowe dla hello Warstwa bazy danych, a wielu klientów korzystać hello elastyczność toobuild wdrożeń chmury lokalnego węzła wysokiej dostępności szybko po zdarzeniu odzyskiwania po awarii.
* Witaj diagram przedstawia hello SAP NetWeaver ASCS i warstwy aplikacji serwera, replikowane za pomocą usługi Azure Site Recovery.

![Scenariusz replikacji](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Ten test trybu failover
Postępuj zgodnie z [w tych wskazówkach](azure-to-azure-walkthrough-test-failover.md) toodo test trybu failover.

1.  Przejdź tooAzure portalu i wybierz magazyn usług odzyskiwania.
2.  Polecenie hello planu odzyskiwania utworzone dla aplikacje SAP (s).
3.  Kliknij na "Test trybu Failover".
4.  Wybierz punkt odzyskiwania i procesu sieci wirtualnej platformy Azure toostart hello testowego trybu failover.
5.  Po skonfigurowaniu dodatkowej środowiska hello można wykonywać z operacji sprawdzania poprawności.
6.  Po zakończeniu operacji sprawdzania poprawności powitania kliknij pozycję "Oczyszczania testowy tryb failover" i pracy awaryjnej hello tooclean środowiska.

## <a name="doing-a-failover"></a>Podczas pracy w trybie failover
Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.

1.  Przejdź tooAzure portalu i wybierz magazyn usług odzyskiwania.
2.  Polecenie hello planu odzyskiwania utworzone dla aplikacje SAP.
3.  Kliknij pozycję "Failover".
4.  Wybierz proces pracy awaryjnej hello toostart punktu odzyskiwania.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o tworzeniu rozwiązanie odzyskiwania po awarii dla wdrożenia SAP NetWeaver przy użyciu usługi Azure Site Recovery w [dokumencie](http://aka.ms/asr-sap). oficjalny dokument Hello również zawiera omówienie zalecenia dla różnych architektur SAP, zawiera listę obsługiwanych aplikacji i typów maszyny Wirtualnej dla programu SAP na platformie Azure, a opisano możliwe planów testowych do rozwiązania do odzyskiwania po awarii.

Dowiedz się więcej o [replikowanie innych obciążeń](site-recovery-workload.md) przy użyciu usługi Site Recovery.
