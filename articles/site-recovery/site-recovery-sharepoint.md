---
title: "Wielowarstwowa aplikacja programu SharePoint przy użyciu usługi Azure Site Recovery aaaReplicate | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooreplicate wielowarstwowej aplikacji programu SharePoint przy użyciu możliwości usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Replikowanie wielowarstwowej aplikacji programu SharePoint przy użyciu usługi Azure Site Recovery odzyskiwania po awarii

W tym artykule opisano szczegółowo sposób tooprotect aplikacji programu SharePoint przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Omówienie

Microsoft SharePoint jest zaawansowanych aplikacji, które mogą ułatwić grupy lub działu organizowanie, współpracę i udostępnianie informacji. SharePoint zapewniają portali sieci intranet, Zarządzanie dokumentami i plikami, współpracy, sieci społecznościowych, sieci ekstranet, witryn sieci Web, wyszukiwania enterprise i business intelligence. Ma również integracji systemu, integracji procesów i możliwości automatyzacji przepływu pracy. Zazwyczaj organizacje uważają, że jako warstwy 1 aplikacji poufnych toodowntime i utraty danych.

Już dziś Microsoft SharePoint nie zawiera żadnych funkcji odzyskiwania po awarii poza pole. Niezależnie od typu hello i skali awarii odzyskiwanie obejmuje użycie hello centrum danych wstrzymania, które można odzyskać farmy hello. Centra danych wstrzymania są wymagane dla scenariuszy, w którym lokalnego nadmiarowych systemów i kopii zapasowych nie można odzyskać z hello przestoju w centrum danych podstawowych hello.

Rozwiązanie odzyskiwania po awarii dobrej powinien umożliwić modelowania planów odzyskiwania wokół hello architektury złożonych aplikacji, takich jak SharePoint. Należy również zaznaczyć hello możliwości tooadd dostosowane kroki toohandle aplikacji mapowań między różnych warstw i dlatego udostępnianie trybu failover z jednym kliknięciem w dolnym RTO w razie awarii hello.

W tym artykule opisano szczegółowo sposób tooprotect aplikacji programu SharePoint przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md). W tym artykule opisano najlepsze rozwiązania dotyczące replikacji tooAzure aplikacji SharePoint trzy warstwy, jak wyszczególniania odzyskiwania po awarii i sposób tooAzure aplikacji hello trybu failover.

Możesz obserwować hello poniżej wideo o odzyskiwaniu tooAzure multi warstwy aplikacji.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że rozumiesz hello poniżej:

1. [Replikowanie tooAzure maszyny wirtualnej](site-recovery-vmware-to-azure.md)
2. Jak zbyt[projektowania sieci odzyskiwania](site-recovery-network-design.md)
3. [Ten test trybu failover tooAzure](site-recovery-test-failover-to-azure.md)
4. [Sposób tooAzure trybu failover](site-recovery-failover.md)
5. Jak zbyt[replikacji kontrolera domeny](site-recovery-active-directory.md)
6. Jak zbyt[replikacji programu SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>Architektura programu SharePoint

Programu SharePoint można wdrożyć na jeden lub więcej serwerów przy użyciu topologii warstwowych i tooimplement ról serwera projektu farmy, który spełnia określonych celów. Typowy dużych, wysokiej jakości farmy programu SharePoint server obsługującego dużej liczby równoczesnych użytkowników i dużą liczbę elementów zawartości Użyj grupowania usługi w ramach strategii ich skalowalności. Ta metoda obejmuje uruchomione usługi na dedykowanych serwerach, grupowanie tych usług, a następnie skalowanie w poziomie serwerów hello jako grupa. Witaj następujących topologii zilustrowano hello usługi i grupowanie trzy warstwy farmy serwerów programu SharePoint server. Szczegółowe wskazówki dotyczące różnych topologiach programu SharePoint można znaleźć dokumentację tooSharePoint i architektury linii produktów. Można znaleźć więcej szczegółów na temat wdrażania programu SharePoint 2013 w [tego dokumentu](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Wzorzec wdrożenia 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Obsługa odzyskiwania lokacji

Do tworzenia w tym artykule, użyto maszyn wirtualnych VMware z systemem Windows Server 2012 R2 Enterprise. Użyto programu SharePoint 2013 Enterprise edition i programu SQL server 2014 Enterprise edition. Zgodnie z replikacji usługi Site Recovery jest niezależny od aplikacji, zalecenia hello podano tutaj oczekiwanego toohold na także następujących scenariuszach.

### <a name="source-and-target"></a>Źródłowa i docelowa

**Scenariusz** | **tooa lokacji dodatkowej** | **tooAzure**
--- | --- | ---
**Funkcja Hyper-V** | Tak | Tak
**VMware** | Tak | Tak
**Serwer fizyczny** | Tak | Tak

### <a name="sharepoint-versions"></a>Wersje programu SharePoint
Witaj następujących wersji serwera programu SharePoint są obsługiwane.

* Program SharePoint server 2013 standardowe
* Program SharePoint server 2013 Enterprise
* Serwer programu SharePoint 2016 standardowe
* Program SharePoint server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Tookeep rzeczy pamiętać

Jeśli używasz udostępniony klaster opartej na dysku jako wszystkie warstwy aplikacji, nie będzie można tooreplicate replikacji usługi Site Recovery może toouse tych maszyn wirtualnych. Można natywnego replikacji udostępnione przez aplikacji hello, a następnie użyć [planu odzyskiwania](site-recovery-create-recovery-plans.md) toofailover wszystkie warstwy.

## <a name="replicating-virtual-machines"></a>Replikowanie maszyn wirtualnych

Postępuj zgodnie z [w tych wskazówkach](site-recovery-vmware-to-azure.md) toostart replikowanie hello tooAzure maszyny wirtualnej.

* Po zakończeniu replikacji hello upewnij się, że Przejdź tooeach maszyny wirtualnej dla każdej warstwy i wybierz zestaw tej samej dostępności "elementu zreplikowane > Ustawienia > Właściwości > obliczenia i sieć". Na przykład jeśli warstwę web 3 maszyn wirtualnych, upewnij się, że wszystkie powitalne 3 maszyny wirtualne są skonfigurowane toobe częścią tej samej zestawem dostępności w usłudze Azure.

    ![Zestaw dostępności zestawu](./media/site-recovery-sharepoint/select-av-set.png)

* Aby uzyskać wskazówki dotyczące ochrony usługi Active Directory i DNS, można znaleźć za[ochrony usługi Active Directory i DNS](site-recovery-active-directory.md) dokumentu.

* Aby uzyskać wskazówki dotyczące ochrony warstwy bazy danych uruchomiony na serwerze SQL, można znaleźć za[ochrony programu SQL Server](site-recovery-active-directory.md) dokumentu.

## <a name="networking-configuration"></a>Konfiguracja sieci

### <a name="network-properties"></a>Właściwości sieci

* Hello aplikacji i warstwa sieci Web maszyn wirtualnych konfigurowania ustawień sieciowych w portalu Azure, tak aby hello maszyn wirtualnych pobierać dołączonych toohello prawo odzyskiwania po awarii sieci po pracy awaryjnej.

    ![Wybierz sieć](./media/site-recovery-sharepoint/select-network.png)


* Jeśli używasz statycznego adresu IP, określ IP hello, interesujące hello tootake maszyny wirtualnej w hello **docelowy adres IP** pola

    ![Ustawianie statycznego adresu IP](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS i routingu ruchu

Dla witryn, internetowy [tworzenia profilu usługi Traffic Manager typu 'Priority'](../traffic-manager/traffic-manager-create-profile.md) w hello subskrypcji platformy Azure. A następnie skonfiguruj profil DNS i usługi Traffic Manager w powitania po sposób.


| **Gdzie** | **Źródło** | **Docelowy**|
| --- | --- | --- |
| Publicznym systemie DNS | Publicznym systemie DNS dla witryny programu SharePoint <br/><br/> Przykład: sharepoint.contoso.com | Traffic Manager <br/><br/> contososharepoint.trafficmanager.NET |
| DNS lokalnego | sharepointonprem.contoso.com | Publiczny adres IP w farmie lokalne powitania |


W profilu usługi Traffic Manager hello [utworzyć hello podstawowymi i odzyskiwania punkty końcowe](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Użyj zewnętrznego punktu końcowego hello publicznego adresu IP dla punktu końcowego platformy Azure i lokalnego punktu końcowego. Upewnij się, że priorytet hello ustawiono wyższej tooon lokalnego punktu końcowego.

Host stronę testową na określonym porcie (np. 800) w warstwie sieci web programu SharePoint hello aby tooautomatically Traffic Manager wykryć dostępności post w tryb failover. W przypadku, gdy nie można włączyć uwierzytelnianie anonimowe dla poszczególnych witryn programu SharePoint jest obejście tego problemu.

[Konfigurowanie profilu usługi Traffic Manager hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md) z hello poniżej ustawienia.

* Metoda routingu - 'Priority'
* DNS czas toolive (TTL) - 30 sekund
* Ustawienia monitora punktu końcowego — Jeśli zostanie włączone uwierzytelnianie anonimowe można nadać punktu końcowego określonej witryny sieci Web. Lub za pomocą strony testu na określonym porcie (np. 800).

## <a name="creating-a-recovery-plan"></a>Tworzenie planu odzyskiwania

Plan odzyskiwania umożliwia sekwencjonowania trybu failover hello różnych poziomów w wielowarstwowej aplikacji, w związku z tym zachowaniu spójności aplikacji. Wykonaj hello kroki podczas tworzenia planu odzyskiwania dla aplikacji sieci web w wielowarstwowych. [Dowiedz się więcej o tworzeniu planu odzyskiwania](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Dodawanie grup toofailover maszyny wirtualne

1. Tworzenie planu odzyskiwania przez dodanie hello aplikacji i warstwa sieci Web maszyn wirtualnych.
2. Kliknij pozycję "Dostosuj" hello toogroup maszyn wirtualnych. Domyślnie wszystkie maszyny wirtualne są częścią "Grupa 1".

    ![Dostosowywanie planu odzyskiwania](./media/site-recovery-sharepoint/rp-groups.png)

3. Utwórz inną grupę (Grupa 2) i Przenieś warstwa sieci Web hello maszyn wirtualnych do hello nowej grupy. Warstwę aplikacji maszyn wirtualnych powinny być częścią "Grupa 1" i warstwa sieci Web maszyn wirtualnych powinny być częścią "Grupa 2". Jest to tooensure, który hello aplikacji maszyny wirtualne warstwy rozruchu najpierw następuje maszyny wirtualne warstwy sieci Web.


### <a name="adding-scripts-toohello-recovery-plan"></a>Dodawanie skryptów toohello planu odzyskiwania

Najczęściej używane hello skryptów usługi Azure Site Recovery można wdrożyć na koncie automatyzacji, klikając przycisk "Wdrażanie tooAzure" hello poniżej. Korzystając z dowolnego skryptu opublikowane, upewnij się, że Wykonaj wskazówki hello w skrypcie hello.

[![Wdrażanie tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Dodaj wstępne akcji skryptu too'Group 1' toofailover grupy dostępności funkcji SQL. Użyj skryptu "ASR-SQL-FailoverAG" hello, opublikowane w hello przykładowe skrypty. Upewnij się, postępując zgodnie z podanymi hello w skrypcie hello i zmieniać hello wymagane w skrypcie hello odpowiednio.

    ![Dodaj AG-skryptu krok-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Dodaj AG-skryptu krok-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Dodaj tooattach skryptu akcji post modułu równoważenia obciążenia na powitania przejścia w tryb failover maszyny wirtualne warstwy sieci Web (Grupa 2). Użyj skryptu "ASR AddSingleLoadBalancer" hello, opublikowane w hello przykładowe skrypty. Upewnij się, postępując zgodnie z podanymi hello w skrypcie hello i zmieniać hello wymagane w skrypcie hello odpowiednio.

    ![Dodaj LB-skryptu krok-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Dodaj LB-skryptu krok-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Dodaj krok wykonywany ręcznie tooupdate hello DNS rekordów toopoint toohello nowej farmy na platformie Azure.

    * Dla witryn internetowy nie DNS ma aktualizacji wymagane po pracy awaryjnej. Wykonaj kroki hello opisanego w tooconfigure sekcji "Wskazówki sieci" hello Menedżera ruchu. Jeśli hello profilu usługi Traffic Manager został skonfigurowany zgodnie z opisem w poprzedniej sekcji hello, należy dodać skrypt tooopen zastępczego (800 w przykładzie hello) na powitania maszyny Wirtualnej platformy Azure.

    * Dla wewnętrznych witryn należy dodać IP usługi równoważenia obciążenia ręcznego kroku tooupdate hello DNS rekordów toopoint toohello nowej sieci Web warstwy maszyny Wirtualnej.

4. Dodawanie aplikacji wyszukiwania toorestore ręcznego kroku z kopii zapasowej lub rozpocząć nową usługę wyszukiwania.

5. Przywracanie aplikacji usługi wyszukiwania z kopii zapasowej, wykonaj następujące czynności.

    * Ta metoda założono, że wykonano kopię zapasową hello aplikacji usługi wyszukiwania przed zdarzeniem krytycznego hello i możliwość tworzenia kopii zapasowych hello jest dostępny w witrynie hello odzyskiwania po awarii.
    * Łatwo można to osiągnąć Planowanie tworzenia kopii zapasowej hello (na przykład raz dziennie) i używając kopii zapasowej hello tooplace procedury w witrynie hello odzyskiwania po awarii. Procedury kopiowania mogą obejmować skryptową programów, takich jak AzCopy (kopiowania na platformę Azure) lub konfigurowania DFSR (Distributed pliku usługi replikacji).
    * Teraz tego hello programu SharePoint farmy jest uruchomiona, przejdź hello administracji centralnej "Kopia zapasowa i przywracanie" i wybierz przywracania. Witaj przywracania interrogates hello określona lokalizacja kopii zapasowej (może być wartością hello tooupdate). Wybierz chcesz toorestore tworzenia kopii zapasowej hello aplikacji usługi wyszukiwania.
    * Po przywróceniu wyszukiwania. Należy pamiętać, że hello przywracania oczekuje toofind hello same topologii (tej samej liczby serwerów) i te same dysk twardy litery przypisane toothose serwerów. Aby uzyskać więcej informacji, zobacz ["Aplikacji usługi przywrócić wyszukiwania w SharePoint 2013"](https://technet.microsoft.com/library/ee748654.aspx) dokumentu.


6. Począwszy od nowej aplikacji usługi wyszukiwania, wykonaj następujące czynności.

    * Ta metoda zakłada, że kopię zapasową bazy danych "Administracja wyszukiwania" hello dostępne w witrynie hello odzyskiwania po awarii.
    * Ponieważ hello innych baz danych aplikacji usługi wyszukiwania nie są replikowane, muszą one toobe utworzony ponownie. toodo tak, przejdź tooCentral administracji i Usuń hello aplikacji usługi wyszukiwania. Na wszystkich serwerach, które hello hosta indeksu wyszukiwania, Usuń pliki indeksu hello.
    * Utwórz ponownie hello aplikacji usługi wyszukiwania i to ponownie tworzy hello baz danych. Zalecane jest toohave przygotowane skrypt, który tworzy ponownie to aplikacja usługi, ponieważ nie jest możliwe tooperform wszystkie akcje za pośrednictwem hello graficznego interfejsu użytkownika. Na przykład lokalizacji dysku indeksu hello i Konfigurowanie topologii wyszukiwania hello są możliwe tylko przy użyciu poleceń cmdlet programu PowerShell programu SharePoint. Użyj polecenia cmdlet programu Windows PowerShell hello SPEnterpriseSearchServiceApplication przywracania, a następnie określ hello dziennikiem i replikowane Administracja wyszukiwania bazy danych, Search_Service__DB. To polecenie cmdlet udostępnia hello konfiguracji wyszukiwania, schemat właściwości zarządzanych, reguł i źródeł i tworzy domyślny zestaw hello innych składników.
    * Po powitalne aplikacji usługi wyszukiwania ma zostać utworzony ponownie, należy uruchomić pełne przeszukiwanie dla każdego źródła zawartości toorestore hello usługi wyszukiwania. Niektórych informacji analityka w farmie lokalne powitania, taką jak zalecenia wyszukiwania zostaną utracone.

7. Po wszystkich hello kroków, Zapisz hello planu odzyskiwania i planu odzyskiwania końcowego hello będą wyglądać jak poniżej.

    ![Zapisane planu odzyskiwania](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Ten test trybu failover
Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) toodo test trybu failover.

1.  Przejdź tooAzure portalu i wybierz magazyn usług odzyskiwania.
2.  Polecenie hello planu odzyskiwania utworzone dla aplikacji programu SharePoint.
3.  Kliknij na "Test trybu Failover".
4.  Wybierz punkt odzyskiwania i procesu sieci wirtualnej platformy Azure toostart hello testowego trybu failover.
5.  Po skonfigurowaniu dodatkowej środowiska hello można wykonywać z operacji sprawdzania poprawności.
6.  Po zakończeniu operacji sprawdzania poprawności hello możesz kliknąć pozycję "Oczyszczania testowy tryb failover" na powitania planu odzyskiwania i hello testowe środowisko trybu failover jest wyczyszczone.

Wskazówki na ten test trybu failover dla usługi AD i DNS, można znaleźć zbyt[Test pracy awaryjnej zagadnienia dotyczące AD i DNS](site-recovery-active-directory.md#test-failover-considerations) dokumentu.

Aby uzyskać wskazówki na ten test trybu failover dla SQL zawsze dotyczących grup dostępności, można znaleźć za[podczas testowego trybu failover dla programu SQL Server AlwaysOn](site-recovery-sql.md#steps-to-do-a-test-failover) dokumentu.

## <a name="doing-a-failover"></a>Podczas pracy w trybie failover
Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) do wykonywania pracy awaryjnej.

1.  Przejdź tooAzure portalu i wybierz magazyn usług odzyskiwania.
2.  Polecenie hello planu odzyskiwania utworzone dla aplikacji programu SharePoint.
3.  Kliknij pozycję "Failover".
4.  Wybierz proces pracy awaryjnej hello toostart punktu odzyskiwania.

## <a name="next-steps"></a>Następne kroki
Użytkownik może dowiedzieć się więcej o [replikowanie inne aplikacje](site-recovery-workload.md) przy użyciu usługi Site Recovery.
