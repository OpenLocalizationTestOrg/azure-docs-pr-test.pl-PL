---
title: "aaaOperations omówienie Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę.  W tym artykule opisano hello wartość OMS, identyfikuje hello różnych usług i ofert objęte OMS i udostępniono linki tootheir szczegółowe zawartości."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Co to jest pakiet Operations Management Suite (OMS)?
Ten artykuł zawiera wprowadzenie tooOperations Management Suite (OMS) tym krótki przegląd zawiera wartość biznesową hello, rozwiązań usług i zarządzania hello zawiera i ofert hello, które pakietu ze sobą różnych usług i rozwiązania.  Łącza są uwzględniane toohello szczegółowe dokumentacji na temat wdrażania wszystkie usługi i rozwiązania.

## <a name="from-on-premises-toohello-cloud"></a>Z lokalnymi toohello chmury
Firma Microsoft od dawna oferuje produkty do zarządzania środowiskami w przedsiębiorstwiach.  Wiele produktów zostały skonsolidowane w hello pakietu System Center management produktów w 2007.  Obejmuje programu Configuration Manager, która zapewnia takie funkcje jak dystrybucja oprogramowania i spisu, który zapewnia aktywnego monitorowania systemów i aplikacji, Orchestrator, w tym procesów ręcznych tooautomate elementów runbook programu Operations Manager , a Data Protection Manager kopii zapasowych i odzyskiwania danych o kluczowym znaczeniu.

Przenoszenie chmury toohello więcej zasobów obliczeniowych produktów System Center uzyskane więcej funkcji chmury, takich jak programu Operations Manager i zarządzania zasobami Azure programu Orchestrator.  Jednak nadal zasadniczo były to rozwiązania lokalne i wymagały znaczących inwestycji związanych z wdrożeniem i utrzymaniem lokalnego środowiska zarządzania.  toocompletely wykorzystać hello chmurze i obsługi przyszłych aplikacji, nowej toomanagement podejście była wymagana.

## <a name="introducing-operations-management-suite"></a>Wprowadzenie do pakietu Operations Management Suite
Operations Management Suite (znanej także jako OMS) to zbiór usług zarządzania, które zostały zaprojektowane w chmurze powitania od początku hello.  Składniki pakietu OMS są w pełni hostowane na platformie Azure, dzięki czemu nie trzeba wdrażać zasobów lokalnych ani zarządzać nimi.  Konfiguracja jest ograniczona do minimalnego zakresu, a pracę można rozpocząć dosłownie w ciągu kilku minut.  

- **Minimalne koszt i złożoność wdrożenia.**  Ponieważ wszystkie składniki hello i dane OMS są przechowywane na platformie Azure, może być w górę i uruchomiony w krótkim czasie bez hello złożoność i inwestycji w lokalnych składników.
- **Poziomy toocloud skali.**  Nie masz tooworry o płatność za zasoby obliczeniowe, które nie wymagają lub o kończy się miejsce do magazynowania od hello chmurze pozwala toopay tylko w przypadku co faktycznie używane i łatwo mogą być skalowane tooany obciążenia, które są wymagane.  Możesz rozpocząć zarządzając kilka tooget zasobów uruchomiona, a następnie skalowanie w górę tooyour całego środowiska.
- **Korzystać z najnowszych funkcji hello.**  Do pakietu OMS są stale dodawane nowe funkcje, a jego istniejące funkcje są nieustannie aktualizowane.  Stale masz dostęp do najnowszych funkcji toohello bez żadnych aktualizacji toodeploy wymaganie.
- **Zintegrowane usługi.**  Podczas każdej z usług OMS hello Podaj wartość na ich własnych, ich mogą współdziałać ze sobą toosolve zarządzania złożone scenariusze.  Na przykład element runbook automatyzacji Azure mogą dysków proces trybu failover z usługi Azure Site Recovery i następnie zalogowanie się informacji tooLog Analytics toogenerate alert.
- **Globalna wiedza.**  Rozwiązania do zarządzania w OMS stale mają dostęp toohello najnowsze informacje.  na przykład Hello rozwiązania zabezpieczeń i inspekcji można wykonać analizy zagrożeń przy użyciu najnowszych zagrożeniach hello wykrywane wokół hello world.
- **Dostęp z dowolnego miejsca.**  Możesz uzyskiwać dostęp do środowiska zarządzania z dowolnego miejsca za pomocą przeglądarki.  Zainstaluj aplikację OMS hello na smartfonie danych monitorowania tooyour łatwy dostęp.

### <a name="is-it-just-for-hello-cloud"></a>Jest to po prostu dla chmury hello?
Tak, ponieważ OMS usługi uruchamiane w chmurze hello nie oznacza, że nie można efektywnie zarządzać w lokalnym środowisku.  Umieść agenta w dowolnym systemie Windows lub komputera z systemem Linux w centrum danych która będzie wysyłać tooLog dane zbierane Analytics, gdzie może zostać przeanalizowana wraz z innymi danymi z usług w chmurze lub lokalnie.  Użyj chmury hello tooleverage kopia zapasowa Azure i usługi Azure Site Recovery dla kopii zapasowej i wysoka dostępność dla zasobów lokalnych.  
Elementy Runbook w chmurze hello zwykle nie dostęp do zasobów lokalnych, ale można zainstalować agenta na co najmniej jeden komputer za który będzie hostem elementów runbook w centrum danych.  Po uruchomieniu elementu runbook, należy po prostu określić, czy go toorun w chmurze hello lub na lokalnym procesu roboczego.

## <a name="hybrid-management-with-system-center"></a>Zarządzanie hybrydowe za pomocą programu System Center
Jeśli masz istniejącą instalację programu System Center można zintegrować te składniki z OMS usług tooprovide hybrydowego dla obu lokalną i środowisk wykorzystaniu hello specjalizacje względną każdego produktu w chmurze.  Połącz z istniejących agenty programu Operations Manager zarządzania grupy tooLog Analytics tooanalyze zarządzane w chmurze hello.  Za pomocą istniejącego procesu tworzenia kopii zapasowej programu Data Protection Manager toobackup chmury toohello danych.  


## <a name="oms-services"></a>Usługi pakietu OMS
podstawowe funkcje Hello OMS są udostępniane przez zestaw usług, które działają na platformie Azure.  Każda usługa udostępnia funkcję zarządzania określonymi i scenariusze zarządzania różnych tooachieve usług można łączyć.

|| Usługa | Opis |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Monitorowanie i analizowanie hello dostępności i wydajności różnych zasobów, w tym fizycznych i maszyn wirtualnych. |
| ![Azure Automation](media/operations-management-suite-overview/icon-automation.png) | Automatyzacja | Automatyzowanie procesów ręcznych oraz wymuszanie konfiguracji maszyn fizycznych i wirtualnych. |
| ![Azure Backup](media/operations-management-suite-overview/icon-backup.png) | Tworzenie kopii zapasowych | Wykonywanie kopii zapasowych i przywracanie kluczowych danych. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Zapewnianie wysokiej dostępności kluczowych aplikacji. |

### <a name="log-analytics"></a>Log Analytics
Usługa [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) umożliwia monitorowanie pakietu OMS przez zbieranie danych z zarządzanych zasobów w centralnym repozytorium.  Te dane mogą obejmować zdarzeń, danych wydajności lub niestandardowe dane przekazane za pośrednictwem hello interfejsu API. Po zebraniu danych, danych hello jest dostępna dla alertów, analizy i eksportowanie.  Ta metoda umożliwia tooconsolidate danych z różnych źródeł, można połączyć dane z usługami Azure z istniejącego środowiska lokalnego.  Oddziela również wyraźnie hello zbierania danych hello hello akcję podejmowaną w odniesieniu do danych tak, aby wszystkie akcje są dostępne tooall rodzajów danych z.  

![Omówienie usługi Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Zbieranie danych
Istnieją różne sposoby, który można pobrać danych do repozytorium hello tooanalyze analizy dzienników.

- **Maszyny wirtualne i komputery z systemem Windows lub Linux.**  Zainstaluj hello Microsoft Monitoring Agent na [Windows](../log-analytics/log-analytics-windows-agents.md) i [Linux](../log-analytics/log-analytics-linux-agents.md) komputerach lub maszynach wirtualnych, które mają toocollect danych z.  Hello agent będzie automatycznie pobierał z analizy dzienników konfiguracji, który definiuje zdarzenia i toocollect danych wydajności.  Można łatwo zainstalować agenta hello na maszynach wirtualnych działających na platformie Azure przy użyciu hello portalu Azure.  Jeśli masz istniejące środowisko programu Operations Manager, możesz łączyć tooLog grupy zarządzania hello Analytics i automatyczne uruchamianie zbierania danych ze wszystkich istniejących agentów.
- **Usługi platformy Azure.**  Analiza dzienników umożliwia zbieranie danych telemetrycznych z [diagnostyki Azure i monitorowania Azure](../log-analytics/log-analytics-azure-storage.md) do repozytorium hello, dzięki czemu można monitorować zasobów platformy Azure.
- **Interfejs API modułu zbierającego dane.**  Usługa Log Analytics zawiera [interfejs API REST umożliwiający wypełnianie danych z dowolnego klienta](../log-analytics/log-analytics-data-collector-api.md).  To pozwala toocollect danych z aplikacji innych firm, lub zaimplementuj scenariusze zarządzania niestandardowe.  Powszechnie używaną metodą jest toouse elementu runbook w automatyzacji Azure toocollect danych, a następnie użyć toowrite interfejsu API modułów zbierających dane hello go toohello repozytorium.

#### <a name="reporting-and-analyzing-data"></a>Raportowanie i analizowanie danych
Analiza dzienników obejmuje zaawansowane zapytania języka tooextract danych przechowywanych w repozytorium hello.  Dane ze wszystkich źródeł są przechowywane jako rekordy, dlatego można przeanalizować dane z wielu źródeł w ramach jednego zapytania.
  
Ponadto tooad hoc analizy, Log Analytics zapewnia wiele sposobów tooreport i analizowanie danych w wyniku zapytania.

- **Widoki i pulpity nawigacyjne.**  [Widoki](../log-analytics/log-analytics-view-designer.md) i [pulpity nawigacyjne](../log-analytics/log-analytics-dashboards.md) wizualizacja hello wyników kwerendy w portalu hello.  Rozwiązania do zarządzania zwykle zawiera widoki, które analizować dane hello hello rozwiązania.  Można także tworzenie własnych niestandardowych widoków danych tooanalyze i był łatwo dostępny w portalu niestandardowych.
- **Eksportowanie.**  Masz hello opcja tooexport hello wyniki wszelkie zapytania, aby można go analizować poza analizy dzienników.  Można także zaplanować regularne eksportu za[usługi Power BI](../log-analytics/log-analytics-powerbi.md) zapewniające ilustrujących możliwości wizualizacji i analizy.
- **Interfejs API funkcji przeszukiwania dzienników.**  Usługa Log Analytics zawiera [interfejs API REST umożliwiający zbieranie danych z dowolnego klienta](../log-analytics/log-analytics-log-search-api.md).  Umożliwia tooprogrammatically pracy z danymi zbieranymi w repozytorium hello, lub do niego dostęp z innego narzędzia do monitorowania.

#### <a name="alerting"></a>Generowanie alertów
Usługa Log Analytics może [proaktywnie generować alerty](../log-analytics/log-analytics-alerts.md) lub podejmować działania naprawcze po wykryciu problemu.  Tak jak w przypadku wszystkich pozostałych funkcji analizy w usłudze Log Analytics jest używane przeszukiwanie dzienników.  To wyszukiwanie jest uruchamiane zgodnie z ustalonym harmonogramem, a alert jest tworzony, jeśli hello wyników spełniających kryteria określonego.

![Alerty usługi Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

Ponadto toocreating alertu rekordu w repozytorium analizy dzienników hello alertów może zająć hello następujące akcje.

- **E-mail.**  Wyślij wiadomość e-mail tooproactively powiadamiał wykrytego problemu.
- **Runbook.**  Alert w usłudze Log Analytics może uruchomić element runbook w usłudze Azure Automation.  Jest to zazwyczaj wykonywane tooattempt toocorrect hello wykrył problem.  Witaj runbook może zostać uruchomiona w chmurze hello w hello przypadku problemu w programie Azure lub innej chmurze lub może zostać uruchomiony na agencie lokalnego problemu na maszynie fizycznej lub wirtualnej.
- **Webhook.**  Alert można uruchomić elementu webhook i przekaż go danych z wyników wyszukiwania dziennika hello hello.  Dzięki integracji z zewnętrznych usług, takich jak system alertów alternatywnego lub może podejmować działania naprawcze tootake do zewnętrznej witryny sieci web.

### <a name="azure-automation"></a>Azure Automation
[Automatyzacja Azure](http://azure.microsoft.com/documentation/services/automation) zapewnia tooOMS proces automatyzacji i konfiguracji zarządzania.  Go automatyzuje procesów ręcznych i pomaga tooenforce konfiguracji dla komputerów fizycznych i wirtualnych.  

#### <a name="process-automation"></a>Automatyzacja procesów
Usługa Azure Automation umożliwia automatyzowanie procesów ręcznych przy użyciu elementów [runbook](../automation/automation-runbook-types.md) opartych na skrypcie programu PowerShell lub przepływie pracy programu PowerShell.  Zawiera również zasoby obsługi elementów runbook, takie jak zmienne, które mogą być współużytkowane między wiele elementów runbook i poświadczeń i połączeń, które pozwalają toostore zaszyfrowane informacje, które mogą być wymagane dla elementu runbook do uwierzytelniania.
Elementy Runbook oferują automatyzacji procesu dla hello innych usług w zestawie hello.  Od każdego hello inne usługi są dostępne przy użyciu programu PowerShell lub za pośrednictwem interfejsu API REST, można utworzyć elementy runbook tooperform takie funkcje jak zbieranie danych zarządzania w analizy dzienników lub inicjowanie kopii zapasowej w usłudze Kopia zapasowa Azure.

##### <a name="accessing-resources"></a>Uzyskiwanie dostępu do zasobów
Elementy runbook są oparte na programie PowerShell, dlatego mogą zarządzać każdym zasobem, do którego można uzyskiwać dostęp za pomocą poleceń cmdlet programu PowerShell.  Gdy użytkownik [załadować moduł](../automation/automation-integration-modules.md) na koncie automatyzacji staje się dostępna tooall runbook na tym koncie. 
 
Gdy elementy runbook działają w chmurze hello, uzyskiwania dostępu do żadnych zasobów, dostępne z chmury hello.  Mogą to być zasoby w ramach Twojej subskrypcji platformy Azure, w innej chmurze, takiej jak usługi Amazon Web Services (AWS), lub w usłudze dostępnej za pośrednictwem interfejsu API REST.  Elementy Runbook w chmurze hello nie działają w ramach żadnych poświadczeń, ale można korzystać z automatyzacji zasobów, takich jak poświadczenia, połączeń i tooresources tooauthenticate certyfikaty, które będą mieć dostępu do.

Prawdopodobnie zasobów w centrum danych nie jest dostępny z poziomu elementu runbook w chmurze hello.  Można zainstalować jeden lub kilka [hybrydowych procesów roboczych Runbook](../automation/automation-hybrid-runbook-worker.md) danych, mimo że Centrum toorun elementy runbook, które wymagają dostępu do zasobów toolocal.  Podczas uruchamiania elementu runbook należy określić, czy należy wykonać w chmurze hello lub w określonych procesu roboczego.

![Elementy runbook usługi Azure Automation](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Uruchamianie elementu runbook
Elementy runbook mogą być [uruchamiane na wiele sposobów](../automation/automation-starting-a-runbook.md), dzięki czemu mogą być dołączane do różnych scenariuszy zarządzania.  

- **Azure Portal.**  Podobnie jak innymi usługami Azure automatyzacji Azure można zarządzać za pomocą hello portalu Azure.  Toostarting elementów runbook, można także zaimportować je lub tworzyć własne.
- **Planowanie.**  Można zaplanować toostart elementów runbook w regularnych odstępach czasu.  Dzięki temu można tooautomatically Powtórz proces zarządzania regularnych lub zbieranie danych tooLog Analytics.
- **Program PowerShell i interfejs API.**  Można uruchomić elementy runbook i przekazać je wymagane informacje o parametrach z polecenia cmdlet programu PowerShell lub hello interfejsu API REST usługi Automatyzacja Azure.  
- **Webhook.**  Można utworzyć elementu webhook dla każdego elementu runbook, aby mogła ona toobe rozpoczynający się od zewnętrznych aplikacji lub witryny sieci web.
- **Alert usługi Log Analytics.**  Alert w Log Analytics może automatycznie uruchomić element runbook tooattempt toocorrect hello zagadnienia zidentyfikowanego w wyniku hello alert.

#### <a name="configuration-management"></a>Zarządzanie konfiguracją
[Konfiguracji żądanego stanu środowiska PowerShell (DSC)](../automation/automation-dsc-overview.md) to platforma zarządzania w programie Windows PowerShell, który pozwala toodeploy i wymuszać hello konfiguracji fizycznych i maszyn wirtualnych.  Automatyzacja Azure zarządza konfiguracji DSC i udostępnia serwera ściągania w chmurze hello, że agenci mogą uzyskiwać dostęp do tooretrieve wymagane konfiguracje.

![Azure Automation DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure Backup i Azure Site Recovery
Azure Backup i Azure Site Recovery wpływ toobusiness ciągłości i odzyskiwanie po awarii.  Każdy z nich ma funkcje, które ułatwiają tooensure aplikacje pozostają dostępne po awarii wystąpić i zwracanie operacji toonormal systemów powróci.  Obie te usługi współtworzenia celów punktu toohello odzyskiwania (RPO) i cele czas odzyskiwania (Objective, RTO) zdefiniowany dla Twojej organizacji. Twoje RPO definiuje dopuszczalny limit hello, w którym dane są niedostępne podczas awarii i hello RTO ogranicza hello dopuszczalne ilość czasu, w którym usługa lub aplikacja nie jest dostępna podczas wystąpienia awarii.

#### <a name="azure-backup"></a>Azure Backup
Usługa [Azure Backup](http://azure.microsoft.com/documentation/services/backup) umożliwia wykonywanie kopii zapasowych i przywracanie danych w pakiecie OMS.  Chroni ona dane aplikacji i przechowuje je przez wiele lat bez konieczności ponoszenia jakichkolwiek inwestycji kapitałowych i przy minimalnych kosztach operacyjnych.  Dane z systemów Windows Server fizycznymi i wirtualnymi w dodanie tooapplication obciążeń, takich jak SQL Server i SharePoint jej kopii zapasowej.  Może również służyć przez System Center Data Protection Manager (DPM) tooreplicate chronionych danych tooAzure nadmiarowości i długoterminowego przechowywania.

Chronione dane w usłudze Azure Backup są przechowywane w magazynie kopii zapasowych, znajdującym się w określonym regionie geograficznym. Witaj, dane są replikowane w hello na tym samym regionie i, w zależności od typu hello magazynu, może być również region replikowanych tooanother dla dalszego odporności.

Usługa Azure Backup ma trzy podstawowe scenariusze.

- **Maszyna z systemem Windows z agentem usługi Azure Backup.** Wykonaj kopię zapasową plików i folderów z systemu Windows server lub klienta bezpośrednio tooyour magazynu kopii zapasowych systemu Azure.<br><br>![Maszyna z systemem Windows z agentem usługi Azure Backup](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) lub Microsoft Azure Backup Server.** Korzystać z programu DPM lub serwera kopii zapasowej Microsoft Azure toobackup pliki i foldery w dodanie tooapplication obciążeń, takie jak magazyn toolocal SQL i SharePoint, a następnie replikację tooyour magazynu kopii zapasowych systemu Azure. Obsługuje maszyny wirtualne z systemem Windows lub Linux korzystające z funkcji Hyper-V lub oprogramowania VMware.<br><br>![System Center Data Protection Manager (DPM) lub Microsoft Azure Backup Server](media/operations-management-suite-overview/overview-backup-02.png)
- **Rozszerzenia maszyny wirtualnej platformy Azure.** Kopia zapasowa systemu Windows lub Linux wirtualnych maszyn w Azure tooyour magazynu kopii zapasowych systemu Azure.<br><br>![Rozszerzenia maszyny wirtualnej platformy Azure](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Usługa Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) zapewnia ciągłość prowadzenia działalności biznesowej poprzez organizowanie replikacji lokalnych wirtualnego i tooAzure maszyn fizycznych lub tooa lokacji dodatkowej. Jeśli lokacji głównej jest niedostępny, należy przełączyć toohello dodatkowej lokalizacji dzięki czemu użytkownicy mogą przechowywać pracy i zakończyć się niepowodzeniem po tooworking zamówienie zwrotu systemów. 

Usługa Azure Site Recovery zapewnia wysoką dostępność serwerów i aplikacji.  Wspiera tooyour ciągłość i strategii odzyskiwania (BCDR) po awarii poprzez organizowanie replikacji, trybu failover i odzyskiwania na lokalne maszyny wirtualne funkcji Hyper-V, maszyny wirtualne VMware i serwery fizyczne systemu Windows i Linux. Można replikować maszyny tooa pomocniczego Centrum lub rozszerzyć poprzez replikację ich tooAzure centrum danych. Usługa Site Recovery udostępnia także prosty tryb failover oraz odzyskiwanie dla obciążeń. Integruje się z mechanizmami odzyskiwania po awarii, takimi jak SQL Server AlwaysOn, i udostępnia plany odzyskiwania w celu zapewnienia łatwego trybu failover dla obciążeń, które są rozmieszczone warstwowo na różnych maszynach.

Usługa Azure Site Recovery ma trzy podstawowe scenariusze replikacji.

- **Replikacja maszyn wirtualnych funkcji Hyper-V.**  Jeśli maszyny wirtualne funkcji Hyper-V są zarządzane w chmurach programu VMM, można replikować tooa zapasowy Centrum lub tooAzure magazyn danych. TooAzure replikacji jest za pośrednictwem bezpiecznego połączenia internetowego. Replikacja tooa dodatkowego centrum danych znajduje się nad hello sieci LAN.  Jeśli maszyny wirtualne funkcji Hyper-V nie są zarządzane przez program VMM, można replikować tylko tooAzure magazynu. TooAzure replikacji jest za pośrednictwem bezpiecznego połączenia internetowego.<br><br>![Replikacja maszyn wirtualnych funkcji Hyper-V](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Replikacja maszyn wirtualnych oprogramowania VMware.**  Można replikować VMware maszyn wirtualnych tooa dodatkowego centrum danych z magazynu VMware lub tooAzure. TooAzure replikacji może wystąpić w sieci VPN lokacja lokacja lub usługa Azure ExpressRoute lub za pośrednictwem bezpiecznego połączenia internetowego. Replikacja tooa dodatkowego centrum danych odbywa się za pośrednictwem hello InMage Scout kanału danych.<br><br>![Replikacja maszyn wirtualnych VMware](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Replikacja serwerów fizycznych z systemami Windows i Linux.**  Można replikować serwerów fizycznych tooa pomocniczego centrum danych lub tooAzure magazynu. TooAzure replikacji może wystąpić w sieci VPN lokacja lokacja lub usługa Azure ExpressRoute lub za pośrednictwem bezpiecznego połączenia internetowego. Replikacja tooa dodatkowego centrum danych odbywa się za pośrednictwem hello InMage Scout kanału danych. Usługa Azure Site Recovery zawiera rozwiązanie OMS, która wyświetla statystykami, ale muszą używać hello portalu Azure, dla wszystkich operacji.<br><br>![Replikacja serwerów fizycznych z systemami Windows i Linux](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Usługa Site Recovery przechowuje metadane w magazynach znajdujących się w określonym regionie geograficznym świadczenia usługi Azure. Nie replikowane dane są przechowywane przez hello usługi Site Recovery.

## <a name="management-solutions"></a>Rozwiązania do zarządzania
[Rozwiązania do zarządzania](operations-management-suite-solutions.md) to wstępnie spakowane zestawy logiki implementujące określony scenariusz zarządzania z użyciem co najmniej jednej usługi pakietu OMS.  Różnych rozwiązaniach dostępnych firmy Microsoft i partnerów, można łatwo dodać tooyour subskrypcji platformy Azure tooincrease hello wartości inwestycji w OMS.  Przez partnera można utworzyć własne toosupport rozwiązania, aplikacje i usługi i podaj toousers za pośrednictwem hello Azure Marketplace lub szablonów Szybki Start.

Dobrym przykładem rozwiązania, które korzysta z wielu usług tooprovide dodatkowe funkcje jest hello [rozwiązania do zarządzania aktualizacji](oms-solution-update-management.md).  To rozwiązanie wymaga hello analizy dzienników agenta dla systemu Windows i Linux toocollect informacje o wymaganych aktualizacji na każdego agenta.  Zapisuje danych repozytorium analizy dzienników toohello gdzie można analizować je z dołączone pulpitu nawigacyjnego.  Podczas tworzenia wdrożenia elementy runbook automatyzacji Azure są używane tooinstall wymagane aktualizacje.  Zarządzaj w portalu hello całego procesu i nie ma potrzeby tooworry o hello szczegółami.

![Rozwiązanie](media/operations-management-suite-overview/overview-solution.png)

Większość rozwiązań mogą działać w co najmniej jeden hello następujące funkcje.

- Zbieranie dodatkowych informacji.  Usługa Log Analytics zbiera różne dane z klientów i usług, w tym zdarzenia i dane wydajności.  Rozwiązanie do zarządzania może zbierać dodatkowe informacje, które nie są dostępne z innych źródeł danych — często przy użyciu elementów runbook usługi Azure Automation.
- Dodatkowa analiza zebranych informacji.  Rozwiązania do zarządzania zawierają pulpity nawigacyjne i widoki, które umożliwiają analizowanie i wizualizowanie danych.  Te dziennika wyszukiwania wstecz toopredefined łącze umożliwiające toodrill do hello szczegółowe dane.  Może również wykonywać analizy danych, które już zostały zebrane w repozytorium hello, na przykład wyszukiwanie w zdarzeń zabezpieczeń dla wzorców, które wskazują zagrożenie.
- Dodawanie funkcji.  Rozwiązania firmy Microsoft, zależą od możliwości hello hello core services tooprovide dodatkowe funkcje.  Na przykład mapy usługi zawiera toodiscover własnej konsoli i mapuje serwer i zależności procesów w czasie rzeczywistym.
Rozwiązania są regularnie dodawane tooOMS przez firmę Microsoft i partnerów, co pozwoli toocontinuously zwiększyć wartość hello inwestycji.  Można przeglądać i zainstalować rozwiązania firmy Microsoft za pośrednictwem hello katalogu rozwiązania w portalu OMS hello lub przeglądanie i instalowanie rozwiązania partnerskie i Microsoft za pośrednictwem hello Azure Marketplace w hello portalu Azure.  

![Galeria rozwiązań](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o usłudze [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Dowiedz się więcej o usłudze [Azure Automation](../automation/automation-intro.md).
* Dowiedz się więcej o usłudze [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Dowiedz się więcej o usłudze [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).
* Odnajdywanie hello [rozwiązania, które są dostępne](../log-analytics/log-analytics-add-solutions.md) w różnych ofert OMS hello. 

