---
title: "aaaAzure operacyjne najlepsze rozwiązania w zakresie zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw najlepszych rozwiązań dla usługi Azure Operational zabezpieczeń."
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
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Usługa Azure Operational najlepsze rozwiązania
Azure bezpieczeństwa operacyjnego odwołuje się toohello usług, kontrolek i toousers dostępne funkcje ochrony danych, aplikacji i innych zasobów na platformie Microsoft Azure. Azure bezpieczeństwa operacyjnego w oparciu framework, która będzie zawierała wiedzę hello za pośrednictwem różnych funkcji, które są unikatowe tooMicrosoft, w tym hello Microsoft Security Development Lifecycle (SDL), hello Microsoft Security Response Center Program i głębokie świadomości hello bezpieczeństwa zagrożeń.

W tym artykule omówiono kolekcja najlepszych rozwiązań dotyczących zabezpieczeń bazy danych platformy Azure. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z zabezpieczeń bazy danych platformy Azure i doświadczenia hello klientów, takich jak samodzielnie.

Dla każdego najlepszym rozwiązaniem prezentujemy zasady:
-   Jakie hello najlepszym rozwiązaniem jest
-   Dlaczego chcesz tooenable tej najlepsze praktyki
-   Co może wynikać hello tooenable hello najlepszym rozwiązaniem w przeciwnym przypadku
- Jak można znaleźć tooenable hello najlepsze praktyki

W tym artykule Azure zabezpieczeń najlepsze rozwiązanie w zakresie jest na podstawie opinii konsensu i funkcji platformy Azure i zestawy funkcji istniejących w chwili hello, który został zapisany w tym artykule. Opinie i technologie ulegną zmianom i będą w tym artykule zaktualizowane na tooreflect regularnie tych zmian.

Usługa Azure Operational najlepsze rozwiązania omówione w tym artykule obejmują:

-   Monitorowanie, zarządzanie i ochrona infrastruktury chmury
-   Zarządzanie tożsamościami i implementować rejestracji jednokrotnej (SSO)
-   Śledzenie żądań, analizować trendy użycia i diagnozowanie problemów
-   Monitorowanie usług za pomocą scentralizowanego rozwiązania monitorowania
-   Zapobiegania, wykrywania i odpowiadać toothreats
-   Monitorowanie sieci oparta na scenariuszu end-to-end
-   Zabezpieczanie wdrożenia przy użyciu narzędzia do opracowywania oprogramowania sprawdzoną

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Monitorowanie, zarządzanie i ochrona infrastruktury chmury
Dział operacji IT jest odpowiedzialny za zarządzanie infrastruktury centrum danych, aplikacji i danych, w tym hello stabilności i bezpieczeństwa tych systemów. Jednak uzyskania szczegółowych informacji o zabezpieczeniach przez zwiększenie złożonych środowiskach IT często wymaga organizacje toocobble razem danych z wielu systemów zabezpieczeń i zarządzania.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) firmy Microsoft w chmurze IT rozwiązanie do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze.

[Rozwiązania pakietu OMS zabezpieczeń i inspekcji](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) umożliwia IT tooactively monitorowanie wszystkich zasobów, które mogą pomóc zminimalizować wpływ hello zdarzeń zabezpieczeń. Zabezpieczenia OMS i inspekcji ma domen zabezpieczeń, które mogą służyć do monitorowania zasobów.

Aby uzyskać więcej informacji na temat pakietu OMS, przeczytaj artykuł hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp zapobiegania, wykrywania i odpowiadać toothreats, [zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) zbiera i przetwarza dane dotyczące zasobów, w tym:

-   Dziennik zdarzeń zabezpieczeń
-   Zdarzenia funkcji Śledzenie zdarzeń systemu Windows (ETW)
-   Zdarzenia inspekcji funkcji AppLocker
-   Dziennik zapory systemu Windows
-   Zdarzenia rozwiązania Advanced Threat Analytics
-   Wyniki oceny linii bazowej
-   Wyniki oceny oprogramowania chroniącego przed złośliwym kodem
-   Wyniki oceny aktualizacji/poprawek
-   Strumienie SYSLOG, które są jawnie włączone w agencie hello


## <a name="manage-identity-and-implement-single-sign-on"></a>Zarządzanie tożsamościami i implementowanie logowania jednokrotnego
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) jest katalog wielu dzierżawców w chmurze firmy Microsoft i tożsamość usługi zarządzania.

[Usługi Azure AD](https://azure.microsoft.com/services/active-directory/) zawiera również pełny pakiet [Zarządzanie tożsamościami](https://docs.microsoft.com/azure/security/security-identity-management-overview) możliwości, w tym [uwierzytelnianie wieloskładnikowe](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), rejestracji urządzenia, zarządzanie hasłami samoobsługi, Samoobsługowe zarządzanie grupami, uprzywilejowane konto zarządzania, kontroli dostępu opartej na rolach, monitorowania, sformatowanego inspekcji i zabezpieczeń, monitorowanie i alerty użycia aplikacji.

Hello następujące możliwości można zabezpieczenia aplikacji opartej na chmurze, usprawnić procesów IT, zmniejszyć koszty i zapewnienia, że są spełnione cele zgodność z zasadami firmowymi:

-   Zarządzanie tożsamościami i dostępem hello chmury
-   Uproszczenie aplikacji w chmurze tooany dostępu użytkownika
-   Ochrona cennych danych i aplikacji
-   Samoobsługa dostępna dla wszystkich pracowników
-   Integracja z usługą Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Zarządzanie tożsamościami i dostępem hello chmury
Azure Active Directory (Azure AD) jest zaawansowane [rozwiązanie chmury zarządzania tożsamościami i dostępem](https://www.microsoft.com/cloud-platform/identity-management), które zapewnia niezawodny zestaw funkcji toomanage użytkowników i grup. Pomaga zabezpieczyć tooon dostępu lokalnego i w chmurze, aplikacji, w tym usług sieci web firmy Microsoft, takich jak Office 365 i znacznie oprogramowania firmy Microsoft jako aplikacje usługi (SaaS).
toolearn więcej sposobem tooenable ochronę tożsamości w usłudze Azure AD, zobacz [włączania usługi Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Uproszczenie aplikacji w chmurze tooany dostępu użytkownika
[Włącz rejestrację jednokrotną](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toothousands dostępu użytkownika toosimplify aplikacji w chmurze z urządzeń z systemem Windows, Mac, Android i iOS. Użytkownicy, można uruchomić aplikacji z poziomu panelu spersonalizowany dostęp za pośrednictwem sieci web lub aplikacji mobilnej przy użyciu swoich poświadczeń firmowych. Użyj toogo modułu serwera Proxy aplikacji usługi Azure AD hello poza aplikacji SaaS i opublikować lokalnej sieci web aplikacji tooprovide bardzo bezpieczny dostęp zdalny i logowania jednokrotnego.

### <a name="protect-sensitive-data-and-applications"></a>Ochrona cennych danych i aplikacji
Włącz [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent nieautoryzowany dostęp do tooon lokalnych i aplikacji w chmurze, zapewniając dodatkowy poziom uwierzytelniania. Chroń swoją firmę i eliminuj potencjalne zagrożenia dzięki funkcji monitorowania zabezpieczeń, alertom oraz raportom opartym na uczeniu maszynowym, które identyfikują niespójne wzorce dostępu.

### <a name="enable-self-service-for-your-employees"></a>Samoobsługa dostępna dla wszystkich pracowników
Delegowanie pracowników tooyour ważnych zadań, takich jak resetowanie haseł i tworzenie grup i zarządzanie nimi. [Włącz zmianę hasła samoobsługi](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), Resetuj i samoobsługi grupy zarządzania z usługą Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Integracja z usługą Azure Active Directory
Rozszerzanie [usługi Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) i wszystkimi innymi lokalnymi katalogów tooAzure AD tooenable rejestracji jednokrotnej dla wszystkich aplikacji opartej na chmurze. Atrybuty użytkownika może być katalogiem w chmurze tooyour automatycznie synchronizowane z różnych rodzajów w lokalnych katalogach.

więcej informacji na temat integracji Azure Active Directory toolearn i jak tooenable, przeczytaj artykuł hello [integrację katalogów lokalnych z usługą Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Śledzenie żądań, analizować trendy użycia i diagnozowanie problemów
[Analizy usługi Azure Storage](https://docs.microsoft.com/azure/storage/storage-analytics) wykonuje rejestrowanie i udostępnia metryki danych dla konta magazynu. Można użyć tego żądania tootrace danych, analizować trendy użycia i diagnozowanie problemów z kontem magazynu.

Metryki analityka magazynu są domyślnie włączone dla nowego konta magazynu. Można włączyć i skonfigurować metryki i rejestrowanie w portalu Azure; hello Aby uzyskać więcej informacji, zobacz [monitorować konta magazynu w portalu Azure hello](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Można również włączyć analityka magazynu programowo przy użyciu interfejsu API REST hello lub powitania klienta biblioteki. Użyj hello ustawić właściwości usługi operacji tooenable analityka magazynu osobno dla każdej usługi.

Szczegółowy przewodnik przy użyciu analizy magazynu i inne narzędzia tooidentify, diagnozowanie i rozwiązywanie problemów związanych z usługą Azure Storage, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

więcej informacji na temat integracji Azure Active Directory toolearn i jak tooenable, przeczytaj artykuł hello [Włączanie i konfigurowanie analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Monitorowanie usług
Aplikacje w chmurze są złożonych z wielu części ruchu. Monitorowania udostępnia tooensure danych, która aplikacja pozostaje w górę i uruchomiona w dobrej kondycji. Pomaga również należy toostave wyłączone potencjalne problemy lub Rozwiązywanie problemów z przeszłości te. Ponadto można użyć monitorowania danych toogain szczegółowych informacji o aplikacji. Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.

### <a name="monitor-azure-resources"></a>Monitorowanie zasobów platformy Azure
[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) to usługa platformy hello, która zapewnia jednego źródła do monitorowania zasobów platformy Azure. Z monitorem Azure można zwizualizować, zapytania, trasy, archiwizacji i podejmij akcję na powitania metryki i dzienników pochodzących z zasobami na platformie Azure. Możesz pracować z tych danych za pomocą bloku portalu Monitor hello, [poleceń cmdlet programu PowerShell Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [interfejsu wiersza polecenia i Platform](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), lub [interfejsów API REST Monitor Azure](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Włączanie automatycznego skalowania z Monitorem systemu Azure
Włącz [skalowania automatycznego Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) ma zastosowanie tylko zestawy skalowania maszyny toovirtual (VMSS), usługi w chmurze planów usługi aplikacji i środowiska usługi app service.

### <a name="manage-roles-permissions-and-security"></a>Zarządzaj rolami uprawnień i zabezpieczeń
Wiele zespołów muszą toostrictly [regulowania dostępu toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) danych i ustawień. Na przykład, jeśli masz członków zespołu, którzy używają wyłącznie na monitorowanie (pracowników działu pomocy technicznej, metodyki devops engineers) lub korzystając z dostawcą usługi zarządzanej, możesz je dostęp do danych monitorowania, jednocześnie ograniczając toocreate ich możliwości tooonly toogrant, należy zmodyfikować, lub Usuwanie zasobów.

Oznacza to, jak tooquickly zastosować wbudowane monitorowania RBAC roli tooa użytkownika na platformie Azure lub tworzenie własnych niestandardowych ról dla użytkownika, który wymaga ograniczonych uprawnień monitorowania. Następnie omówiono zagadnienia dotyczące zabezpieczeń dla zasobów związanych z monitora Azure i w jaki sposób można ograniczyć dostęp do danych toohello zawierają.

## <a name="prevent-detect-and-respond-toothreats"></a>Zapobiegania, wykrywania i odpowiadać toothreats
Wykrywanie zagrożeń Centrum zabezpieczeń polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych. Te informacje, często korelowanie informacji z wielu źródeł, zagrożenia tooidentify jego analizy. Alerty zabezpieczeń mają pierwszeństwo w Centrum zabezpieczeń wraz z zaleceniami w sposób tooremediate hello zagrożeń.

-   [Konfigurowanie zasad zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-policies) dla subskrypcji platformy Azure.
-   Użyj hello [zalecenia w Centrum zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp ochronę zasobów platformy Azure.
-   Przejrzyj i bieżące zarządzanie [alerty zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).

[Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) pomaga zapobiegania, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

Centrum zabezpieczeń zapewnia łatwe w użyciu i skuteczne zapobieganie, wykrywanie i odpowiedzi możliwości, które są wbudowane w tooAzure. Do najważniejszych możliwości należą:

-   Zrozumienie stan zabezpieczeń chmury
-   Przejmij kontrolę nad zabezpieczeniami chmury
-   Łatwe wdrażanie zintegrowanych rozwiązań zabezpieczeń w chmurze
-   Wykrywanie zagrożeń i szybkie reagowanie

### <a name="understand-cloud-security-state"></a>Zrozumienie stan zabezpieczeń chmury
Korzystanie z Centrum zabezpieczeń Azure tooget centralnej widok stanu zabezpieczeń hello wszystkich zasobów platformy Azure. Jeden rzut oka Sprawdź, czy hello odpowiednie środki zabezpieczające są stosowane i poprawnie skonfigurowana i szybką identyfikację wszelkich zasobów, które wymagają uwagi.

### <a name="take-control-of-cloud-security"></a>Przejmij kontrolę nad zabezpieczeniami chmury
Zdefiniuj [zasady zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-policies) dla Twojej subskrypcji platformy Azure zgodnie z firmy tooyour na chmurze zabezpieczeń wymaga, dostosowane toohello typem aplikacji oraz poufności danych hello w każdej subskrypcji. Użyj zaleceń oparte na zasadach tooguide zasobów właścicieli hello proces wdrażania wymagane formanty — podjęcia czynności hello poza zabezpieczeń chmury.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Łatwe wdrażanie zintegrowanych rozwiązań zabezpieczeń w chmurze
[Włącz rozwiązań zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) firmy Microsoft i jej partnerów, łącznie z branży zapory i ochrony przed złośliwym oprogramowaniem. Użyj uproszczone inicjowania obsługi administracyjnej rozwiązań zabezpieczeń toodeploy — zmiany nawet sieci są skonfigurowane dla Ciebie. Zdarzenia zabezpieczeń pochodzące od rozwiązań partnerów zostaną automatycznie zebrane na potrzeby analiz i alertów.

### <a name="detect-threats-and-respond-fast"></a>Wykrywanie zagrożeń i szybkie reagowanie
Wyprzedzanie bieżących i pojawiających się zagrożeń w chmurze dzięki zintegrowanemu podejściu, którego podstawą są analizy. Łącząc Microsoft globalne [analizy zagrożeń](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) i doświadczenia z informacjami dotyczącymi zdarzeń związanych z zabezpieczeniami w chmurze między wdrożeń platformy Azure, Centrum zabezpieczeń pomaga wykrywać zagrożenia rzeczywiste wczesne i redukować liczbę fałszywych alarmów. Alerty zabezpieczeń w chmurze zapewniają wgląd w kampanii atak powitania, w tym zdarzenia powiązane i wpływ na zasoby i sugestie sposobów tooremediate wystawia i szybkie odzyskiwanie.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Monitorowanie sieci oparta na scenariuszu end-to-end
Klienci kompilacji na trasie sieci na platformie Azure poprzez organizowanie i tworzenia różnych zasobów poszczególnych sieci, takich jak sieci wirtualnej, ExpressRoute, bramy aplikacji i usług równoważenia obciążenia. Monitorowanie jest dostępne na każdym z zasobów sieciowych hello.

[Monitor sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) to regionalnych usługa, która umożliwia toomonitor i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Automatyzowanie zdalnego monitorowania sieci przez przechwytywanie pakietów
Monitorowanie i diagnozowanie problemów sieciowych bez potrzeby logowania tooyour maszynach wirtualnych (VM) za pomocą Monitora sieci. Wyzwalacz [przechwytywania pakietów](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) przez ustawienia alertów i uzyskać dostęp do informacji o wydajności w czasie tooreal dostęp na poziomie pakietów hello. Możesz szczegółowo analizować problemy w celu lepszego ich diagnozowania.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Uzyskiwanie szczegółowych informacji dotyczących ruchu sieciowego przy użyciu dzienników przepływu
Tworzenie lepiej zrozumieć sieci ruchu wzorzec przy użyciu [dzienniki przepływu sieciowej grupy zabezpieczeń](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). Informacje o dziennikach przepływu pomaga zbierania danych dotyczących zgodności, inspekcja i monitorowanie profilu zabezpieczeń sieci.

### <a name="diagnose-vpn-connectivity-issues"></a>Diagnozowanie problemów z połączeniem sieci VPN
Zawiera obserwatora sieciowego zbyt hello możliwości[diagnozowanie najbardziej typowe problemy bramy sieci VPN i połączeń](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Pozwala nie tylko tooidentify hello problem, ale także toouse hello szczegółowe dzienniki utworzony toohelp dalszego zbadania.

więcej informacji na temat toolearn tooconfigure obserwatora sieciowego i jak tooenable, przeczytaj artykuł hello [skonfigurować obserwatora sieciowego](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Zabezpieczanie wdrożenia przy użyciu narzędzia do opracowywania oprogramowania sprawdzoną
Są to hello listy z Azure DevOps rozwiązań w tym miejscu Microsoft Cloud, co pozwala firmom i zespołom produktywności i wydajne.

-   **Infrastruktura jako kodu (IaC):** infrastruktury jako kod to zestaw metod i rozwiązań, które pomagają specjalistom IT Usuń hello obciążeń związanych z hello dzień tooday kompilacji i zarządzanie infrastrukturą moduły. Umożliwia toobuild specjalistom IT oraz obsługa środowisku nowoczesnych serwera w sposób przypominający ten sposób deweloperzy oprogramowania tworzenia i obsługi kodu aplikacji. Dla platformy Azure, mamy [usługi Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) pozwala tooprovision aplikacji przy użyciu szablonu deklaracyjnego. Pojedynczy szablon umożliwia wdrożenie wielu usług wraz z ich zależnościami. Użyj hello tego samego szablonu toorepeatedly wdrożenia aplikacji podczas każdego etapu cyklu życia aplikacji hello.
-   **Ciągłej integracji i wdrażania:** projektach zespołowych Visual Studio Online, można skonfigurować za[automatycznie twórz i wdrażaj](https://www.visualstudio.com/docs/build/overview) tooAzure sieci web aplikacji lub usług w chmurze. Usługi VSO automatycznie wdraża pliki binarne powitania po wykonaniu tooAzure kompilacji po każdym ewidencjonowania kodu. Hello procesu kompilacji pakietu opisane w tym miejscu jest równoważne toohello pakietu polecenie w programie Visual Studio i kroki publikowania hello są równoważne toohello polecenia Opublikuj w programie Visual Studio.
-   **Zarządzanie zleceniami:** programu Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) to doskonałe rozwiązanie do automatyzacji wieloetapowym wdrażania i zarządzania nimi hello wersji procesu. Szybkie, łatwe i często, należy utworzyć toorelease potoki zarządzanych ciągłego wdrażania. Możemy znacznie automatyzacji procesu wersji Release Management i firma Microsoft może wstępnie zdefiniowanych przepływów pracy. Wdrażanie lokalnej i toohello w chmurze, rozszerzanie i dostosowywanie zgodnie z potrzebami.
-   **Monitorowanie wydajności aplikacji:** wykrywania problemów, rozwiązywania problemów i stale poprawiaj swoje aplikacje. Szybko diagnozuj problemy w działającej aplikacji. Dowiedz się, do czego używają jej użytkownicy. Konfiguracja polega łatwe dodawanie kodu Javascript i wpis webconfig i wyświetlić wyniki w ciągu minut w portalu hello wszystkie szczegóły hello. [App insights](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) pomaga firmom dla szybsze wykrywanie problemów i korygowanie.
-   **Ładowanie testowanie & skalowania automatycznego:** firma Microsoft można znaleźć problemy z wydajnością w naszej aplikacji tooimprove wdrożenia jakości i toomake się naszej aplikacji jest zawsze potrzeb biznesowych toohello toocater się lub jest niedostępny. Upewnij się, że aplikacja może obsługiwać ruch kampanii następnego uruchomienia lub marketing. Uruchamianie oparte na chmurze [testy obciążenia](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) prawie czas z programu Visual Studio Online.

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [bezpieczeństwa operacyjnego Azure](https://docs.microsoft.com/azure/security/azure-operational-security).
- tooLearn więcej [Operations Management Suite | Bezpieczeństwo i zgodność](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Wprowadzenie do programu Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).
