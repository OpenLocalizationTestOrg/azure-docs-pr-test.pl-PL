---
title: "Przegląd zabezpieczeń operacyjne aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie hello operacyjne zabezpieczeń platformy Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Omówienie usługi Azure operational zabezpieczeń
Azure bezpieczeństwa operacyjnego odwołuje się toohello usług, kontrolek i toousers dostępne funkcje ochrony danych, aplikacji i innych zasobów na platformie Microsoft Azure. [Azure bezpieczeństwa operacyjnego](https://docs.microsoft.com/azure/security/azure-operational-security) jest platforma, która zawiera wiedzy hello uzyskane za pomocą różnych funkcji, które są unikatowe tooMicrosoft, w tym hello Microsoft Security Development Lifecycle (SDL), hello Microsoft Security Program Response Center i głębokie świadomości hello przez zabezpieczeń zagrożeń.

W tym artykule operacyjne Omówienie zabezpieczeń usługi Azure koncentruje się na powitania w następujących obszarach:

- Azure Operations Management Suite
-   Azure Security Center
-   Azure Monitor
-   Azure obserwatora sieciowego
-   Analizy usługi Azure Storage
-   Usługa Azure Active directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
Dział operacji IT jest odpowiedzialny za zarządzanie infrastruktury centrum danych, aplikacji i danych, w tym hello stabilności i bezpieczeństwa tych systemów. Jednak uzyskania szczegółowych informacji o zabezpieczeniach przez zwiększenie złożonych środowiskach IT często wymaga organizacje toocobble razem danych z wielu systemów zabezpieczeń i zarządzania.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) firmy Microsoft w chmurze IT rozwiązanie do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze.

OMS jest oparta na chmurze IT rozwiązania do zarządzania z wielu oferty, takie jak ich automatyzacji, zabezpieczeń i zgodności, analizy dzienników i tworzenia kopii zapasowej i odzyskiwania. W efekcie jest toomanage doskonałą pomoc i chronić infrastrukturę informatyczną — lokalnie i w chmurze hello.

podstawowe funkcje Hello OMS są udostępniane przez zestaw usług, które działają na platformie Azure. Każda usługa udostępnia funkcję zarządzania określonymi i scenariusze zarządzania różnych tooachieve usług można łączyć. W tym:

-   Log Analytics
-   Automatyzacja
-   Backup
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
Usługa [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) umożliwia monitorowanie pakietu OMS przez zbieranie danych z zarządzanych zasobów w centralnym repozytorium. Te dane mogą obejmować zdarzeń, danych wydajności lub niestandardowe dane przekazane za pośrednictwem hello interfejsu API. Po zebraniu danych, danych hello jest dostępna dla alertów, analizy i eksportowanie. Ta metoda umożliwia tooconsolidate danych z różnych źródeł, można połączyć dane z usługami Azure z istniejącego środowiska lokalnego. Oddziela również wyraźnie hello zbierania danych hello hello akcję podejmowaną w odniesieniu do danych tak, aby wszystkie akcje są dostępne tooall rodzajów danych z.

### <a name="automation"></a>Automatyzacja
Microsoft [usługi Automatyzacja Azure](https://docs.microsoft.com/azure/automation/automation-intro) umożliwia użytkownikom tooautomate hello ręczne, długotrwałą podatne na błędy i często powtarzanych często wykonywane zadania w środowisku cloud i enterprise. Zaoszczędzić czas i zwiększa niezawodność hello regularnych zadań administracyjnych i nawet planuje je toobe automatycznie wykonywane w regularnych odstępach czasu. Można automatyzować procesy za pomocą elementów Runbook lub automatyzować zarządzanie konfiguracją za pomocą konfiguracji żądanego stanu.

### <a name="backup"></a>Tworzenie kopii zapasowych
[Kopia zapasowa Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) hello bazujących na platformie Azure usługa może zużywać tooback (lub ochrona) i przywracanie danych w hello firmy Microsoft w chmurze. Usługa Azure Backup pozwala zastąpić dotychczasowe rozwiązania tworzenia kopii zapasowych, istniejące lokalnie lub poza siedzibą firmy, rozwiązaniem opartym na chmurze, które jest niezawodne, bezpieczne i konkurencyjne cenowo. Kopia zapasowa Azure oferuje wiele składników, które można pobrać i zainstalować na komputerze, odpowiednie hello, serwera, lub w chmurze hello. składnik Hello lub agenta, który można wdrożyć zależy od co tooprotect. Wszystkie składniki usługi Kopia zapasowa Azure (niezależnie od tego, czy są one chronione danych w sieci lokalnej lub w chmurze hello) mogą być używane tooback zapasowej magazyn usług odzyskiwania tooa danych na platformie Azure. Zobacz hello [tabeli składników usługi Kopia zapasowa Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Usługa Site recovery
[Usługa Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) zapewnia ciągłość prowadzenia działalności biznesowej poprzez organizowanie replikacji lokalnych wirtualnego i tooAzure maszyn fizycznych lub tooa lokacji dodatkowej. Jeśli lokacji głównej jest niedostępny, należy przełączyć toohello dodatkowej lokalizacji dzięki czemu użytkownicy mogą przechowywać pracy i zakończyć się niepowodzeniem po tooworking zamówienie zwrotu systemów. wykrywanie zagrożeń inteligentnego i skuteczne.

## <a name="azure-active-directory"></a>Usługa Azure Active Directory
[Usługa Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) jest kompleksowe tożsamość firmy Microsoft jako rozwiązaniem Service (IDaaS) który:

-   Włącza IAM jako usługa w chmurze
-   Umożliwia zarządzanie dostępu, jednokrotnego (SSO) i raportowania
-   Obsługuje zarządzanie zintegrowanego dostępu dla [tysięcy aplikacji](https://azure.microsoft.com/marketplace/active-directory/) w galerii aplikacji hello, w tym usług Salesforce, Google Apps, pole i Concur.

Usługi Azure AD zawiera również pełny pakiet [możliwości zarządzania tożsamościami](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports) tym [uwierzytelnianie wieloskładnikowe](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), [Rejestracja urządzenia]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [zarządzania hasłami samoobsługi](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [uprzywilejowane konto zarządzania](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [kontroli dostępu opartej na rolach](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [monitorowania użycia aplikacji](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [sformatowanego inspekcji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), i [monitorowania i alertów zabezpieczeń](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Z usługą Azure Active Directory, wszystkie aplikacje publikowania dla partnerów i klientów (biznesowe lub klienta) ma hello takie same możliwości zarządzania tożsamościami i dostępem. Ta umożliwia toosignificantly można zmniejszyć koszty operacyjne.

## <a name="azure-security-center"></a>Azure Security Center
[Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started) pomaga zapobiegania, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Umożliwia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami dla wszystkich subskrypcji, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań zabezpieczających.

[Centrum zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) pomaga chronić danych maszyny wirtualnej na platformie Azure, zapewniając wgląd w ustawienia zabezpieczeń na komputerze wirtualnym i monitorowanie zagrożeń. Usługa Security Center może monitorować maszyny wirtualne pod kątem następujących elementów:

-   Ustawienia zabezpieczeń systemu operacyjnego (OS) z hello zalecane reguły konfiguracji
-   Informacje o brakujących zabezpieczeniach systemu i aktualizacjach krytycznych
-   Zalecenia dotyczące ochrony punktów końcowych
-   Weryfikowanie szyfrowania dysków
-   Ataki sieciowe

Centrum zabezpieczeń Azure używa [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), która zapewnia [wbudowane role](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) mogą być przypisane toousers, grup i usług Azure.

Centrum zabezpieczeń ocenia konfiguracji hello problemy z zabezpieczeniami tooidentify zasobów i luk w zabezpieczeniach. W Centrum zabezpieczeń widoczne są tylko informacje dotyczące zasobów tooa po przypisaniu roli hello właściciela, współautora lub czytelnika dla grupy zasobów lub subskrypcji hello należącą do zasobu.

>[!Note]
>Zobacz [uprawnienia w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn więcej informacji na temat ról i akcji dozwolonych w Centrum zabezpieczeń.

Centrum zabezpieczeń używa hello Microsoft Monitoring Agent — jest to hello samego agenta używane przez usługę Operations Management Suite i analizy dzienników hello. Dane zbierane z tego agenta są przechowywane w istniejących analizy dzienników [obszaru roboczego](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) skojarzone z subskrypcją platformy Azure lub nowych obszarów roboczych, uwzględniając używanie funkcji geolokalizacji hello maszyny Wirtualnej na powitania konta.

## <a name="azure-monitor"></a>Azure Monitor
Problemy z wydajnością w Twojej aplikacji w chmurze może wpłynąć na Twojej firmy. Z wielu powiązanych elementów i częste wersjach degradations może nastąpić w dowolnej chwili. I w przypadku tworzenia aplikacji, użytkowników, zazwyczaj odnajdywanie problemy, które nie udało się znaleźć podczas testowania. Należy od razu wiedzieć o tych problemów i narzędzia do diagnozowania i rozwiązywania problemów hello.

[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) jest podstawowym narzędziem do monitorowania usługi działające na platformie Azure. Udostępnia poziomie infrastruktury danych o przepływności hello usługi i hello otaczającego środowiska. W przypadku zarządzania aplikacjami w usłudze Azure podejmowaniu decyzji, czy tooscale w górę lub w dół zasobów, Azure Monitor daje służą toostart.

Ponadto można użyć monitorowania danych toogain szczegółowych informacji o aplikacji. Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji. Obejmuje on:

-   Dziennik aktywności platformy Azure
-   Dzienniki diagnostyczne platformy Azure
-   Metryki
-   Diagnostyka Azure

### <a name="azure-activity-log"></a>Dziennik aktywności platformy Azure
Jest dziennika, który zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji. Witaj [dziennik aktywności](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) była wcześniej znana jako "Dzienników inspekcji" lub "Operacyjne dzienniki", ponieważ zgłasza płaszczyzny kontroli zdarzeń dla subskrypcji.

### <a name="azure-diagnostic-logs"></a>Dzienniki diagnostyczne platformy Azure
[Azure dzienników diagnostycznych](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) są emitowane przez zasób i zawierają rozbudowane, często dane dotyczące operacji hello tego zasobu. zawartość Hello te dzienniki zależy od typu zasobu.

Na przykład dzienniki systemu zdarzeń systemu Windows są jedną kategorię dzienników diagnostycznych dla maszyn wirtualnych i obiektów blob, tabeli, a dzienniki kolejki są kategorii dzienników diagnostycznych dla kont magazynu.

Dzienniki diagnostyczne różnią się od hello [dziennik aktywności (wcześniej znane jako dziennik inspekcji lub dziennik operacyjny)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). Dziennik aktywności Hello zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji. Dzienniki diagnostyczne zapewniają wgląd w operacje, w zasobie wykonanie samego.

### <a name="metrics"></a>Metryki
Azure Monitor umożliwia tooconsume telemetrii toogain wgląd w hello wydajności i kondycji obciążeń na platformie Azure. Typ najważniejszych Hello danych telemetrycznych platformy Azure jest metryki hello (nazywanych również liczniki wydajności) emitowane przez zasoby najbardziej platformy Azure. Azure Monitor udostępnia kilka sposobów tooconfigure i korzystać z tych [metryki](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) do monitorowania i rozwiązywania problemów.

### <a name="azure-diagnostics"></a>Diagnostyka Azure
Istnieje możliwość hello w ramach platformy Azure, która umożliwia hello zbieranie danych diagnostycznych o wdrożonej aplikacji. Można użyć rozszerzenia diagnostyki hello z różnych różnych źródeł. Obecnie obsługiwane są [Azure Cloud Service w sieci Web i proces roboczy](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [maszyny wirtualne Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) systemu Microsoft Windows i [sieci szkieletowej usług](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Network Watcher
Klienci kompilacji na trasie sieci na platformie Azure poprzez organizowanie i tworzenia różnych zasobów poszczególnych sieci, takich jak sieci wirtualnej, ExpressRoute, bramy aplikacji i usług równoważenia obciążenia. Monitorowanie jest dostępne na każdym z zasobów sieciowych hello.

Witaj zakończenia tooend sieci może mieć złożonych konfiguracji i interakcje między zasobami, tworzenie złożonych scenariuszy, które wymagają oparta na scenariuszu monitorowanie za pomocą Monitora sieci.

[Monitor sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) będzie upraszcza monitorowania i diagnozowania sieci platformy Azure. Dostępne z Włącz obserwatora sieciowego, który można tootake zdalnego Przechwytywanie pakietów na maszynie wirtualnej platformy Azure, narzędzia diagnostyki i wizualizacji uzyskać wgląd w korzystanie z dzienników przepływu ruchu sieciowego oraz przeprowadzania jego diagnostyki bramy sieci VPN i połączeń.

Obserwatora sieciowego ma obecnie hello następujące możliwości:

- [Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) — zapewnia hello przedstawiający widok poziomu sieci różnych połączeń i skojarzenia między zasobami sieci w grupie zasobów.
-   [Zmienna przechwytywania pakietów](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) -przechwytuje pakiet danych do i z maszyny wirtualnej. Zaawansowane filtrowanie opcje i dostosować formanty, takie jak trwa stanie tooset czasu i wszechstronność Podaj ograniczenia rozmiaru. Witaj pakietu danych mogą być przechowywane w magazynie obiektów blob lub na dysku lokalnym hello w formacie CAP.
-   [Sprawdź przepływów IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) — sprawdza, czy pakiet jest dozwolony lub niedozwolony na podstawie przepływ informacji 5-elementowej pakietu parametrów (docelowy adres IP, źródłowy adres IP, Port docelowy, Port źródłowy i Protocol). Jeśli pakietów hello jest zabroniony przez grupę zabezpieczeń, hello reguły i grup, które odmowa pakietów hello jest zwracana.
-   [Następny przeskok](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) — określa hello następnego skoku dla pakietów przesyłane w hello Azure sieci szkieletowej, umożliwiając tras toodiagnose any nieprawidłowo zdefiniowane przez użytkownika.
-   [Widok grupy zabezpieczeń](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -pobiera hello zabezpieczeń skuteczne i zastosowanej reguły, które są stosowane na maszynie Wirtualnej.
-   [Przepływ NSG rejestrowania](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) — dzienniki przepływu dla grup zabezpieczeń sieci Włącz toocapture dzienniki pokrewne tootraffic, który ma być dozwolony lub odrzucany przez reguły zabezpieczeń hello hello grupy. Przepływ Hello jest zdefiniowana przez informacji 5-elementowej — źródłowy adres IP, docelowy adres IP, Port źródłowy, Port docelowy i protokołu.
-   [Brama sieci wirtualnej i rozwiązywanie problemów z połączenia](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) — zapewnia hello tootroubleshoot możliwości połączenia i bramy sieci wirtualnej.
-   [Limity subskrypcji sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) — umożliwia użycie zasobów sieciowych tooview ograniczeń.
-   [Konfigurowanie dziennika diagnostyki](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) — zapewnia tooenable jednego okienka lub wyłącz dzienników diagnostycznych do zasobów sieciowych w grupie zasobów.

toolearn więcej jak Zobacz obserwatora sieciowego tooconfigure [skonfigurować obserwatora sieciowego](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Operacje Developer (DevOps)
Programowanie aplikacji dla wcześniejszego tooDevOps, zespoły zostały odpowiedzialnym za gromadzenie wymagań firmy dotyczących oprogramowania i pisanie kodu. Następnie oddzielny zespół pytań i odpowiedzi testy hello program w środowisku projektowym izolowanym, jeśli zostały spełnione wymagania i wersjach hello kod toodeploy operacji. zespoły Hello są dodatkowo pofragmentowane ze grup, takich jak sieci i bazy danych. Zawsze oprogramowanie jest "zgłoszony przez hello tablicy" tooan zespołu niezależne dodaje wąskich gardeł.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) toodeliver zespołów umożliwia bardziej bezpieczne, wyższej jakości rozwiązania szybsze i tańsze. Klienci oczekują dynamiczne i niezawodne środowisko w przypadku uzyskiwania dostępu do oprogramowania i usług.  Zespoły musi szybko przejść na aktualizacji oprogramowania, środki hello skutków aktualizacji hello i szybko reagować z nowe problemy tooaddress iteracji rozwoju lub zapewnić większą wartość.  Platformami chmury, takich jak Microsoft Azure zostały usunięte tradycyjnych wąskich gardeł i pomogła commoditize infrastruktury. W każdej branży reigns oprogramowania, jak hello główną różnicą i czynnikiem wyników biznesowych. Nie organizacji, developer lub procesu roboczego IT można lub należy unikać przenoszenia DevOps hello.

Dojrzała lekarze DevOps przyjmuje kilka hello wskazówek. Praktyki te [obejmują osób](https://www.visualstudio.com/learn/what-is-devops-culture/) strategii tooform oparte na powitania różnych scenariuszy biznesowych.  Narzędzia ułatwiają Automatyzowanie hello różnych rozwiązań:

-   [Elastyczne planowanie i zarządzanie projektami](https://www.visualstudio.com/learn/what-is-agile/) techniki są używane tooplan i izolowania pracy do przebiegów, zarządzania obciążenia zespołu i szybko dostosowania potrzeb biznesowych toochanging zespoły pomocy.
-   [Kontrola wersji, zwykle za pomocą narzędzia Git](https://www.visualstudio.com/learn/what-is-git/), umożliwia zespołom znajdujących się w dowolnym hello world tooshare źródła i zintegrować z oprogramowania programowanie narzędzia tooautomate hello wersji potoku.
-   [Ciągła integracja](https://www.visualstudio.com/learn/what-is-continuous-integration/) dysków hello systematyczne scalanie i testowanie kodu, co prowadzi wady toofinding wcześniej.  Inne zalety oszczędności na walka scalania problemy i szybkie opinii dla zespołów deweloperów czasu.
-   [Ciągłego dostarczania](https://www.visualstudio.com/learn/what-is-continuous-delivery/) rozwiązań oprogramowania tooproduction i środowisk testowych pomagające organizacjom szybko błędów i odpowiadać zmiana tooever biznesowe wymagania.
-   [Monitorowanie](https://www.visualstudio.com/learn/what-is-monitoring/) uruchomionych aplikacji, również w środowiskach produkcyjnych dla kondycji aplikacji jako także formularz organizacji pomocy użycia klienta hipoteza i szybko sprawdza, czy lub disprove strategii.  Zaawansowana dane zostaną zebrane i przechowywane w różnych formatach rejestrowania.
-   [Infrastruktura jako kodu (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) jest rozwiązaniem, dzięki czemu hello automatyzacji i sprawdzanie poprawności tworzenia i usuwania toohelp sieci i maszyn wirtualnych z dostarczania aplikacji bezpiecznego, stabilna hostingu platformami.
-   [Mikrousług](https://www.visualstudio.com/learn/what-are-microservices/) architektura jest wykorzystywana tooisolate przypadków użycia biznesowego w małych usług wielokrotnego użytku.  Taka architektura umożliwia stosowanie skalowalność i wydajność.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat zabezpieczeń OMS i inspekcji rozwiązania, zobacz następujące artykuły hello:

- [Operations Management Suite | Bezpieczeństwo i zgodność](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Monitorowania i odpowiada tooSecurity alerty w programie Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Monitorowanie zasobów Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources).
