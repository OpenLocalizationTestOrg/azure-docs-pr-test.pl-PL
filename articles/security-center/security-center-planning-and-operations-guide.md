---
title: Operacje przewodnik planowania i Centrum aaaSecurity | Dokumentacja firmy Microsoft
description: "Ten dokument ułatwia tooplan przed wdrożeniem Centrum zabezpieczeń Azure i zagadnienia dotyczące codziennych operacji."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Przewodnik planowania i obsługi usługi Azure Security Center
Ten przewodnik jest przeznaczony dla specjalistów technologii informatycznych (IT), architektów IT, analityków zabezpieczeń informacji i administratorów chmury, których organizacje planują wdrożenie Centrum zabezpieczeń Azure toouse.

>[!NOTE] 
>Począwszy od początku czerwca 2017, Centrum zabezpieczeń użyj toocollect Microsoft Monitoring Agent hello i przechowywania danych. Zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md) toolearn więcej. Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Przewodnik planowania
W tym przewodniku przedstawiono serię kroków i zadań, które można wykonać toooptimize korzystanie z Centrum zabezpieczeń opartych na wymagania dotyczące zabezpieczeń w organizacji oraz modelu zarządzania chmurą. tootake pełne korzystanie z Centrum zabezpieczeń, jest ważne toounderstand jak inne osoby lub zespoły w organizacji używać hello usługi toomeet bezpiecznego programowania i obsługi, monitorowaniem, zarządzaniem i reagowaniem na zdarzenia. Witaj kluczowe tooconsider podczas planowania toouse Centrum zabezpieczeń są:

* Role zabezpieczeń i kontrola dostępu
* Zasady zabezpieczeń i zalecenia w tym zakresie
* Zbieranie i przechowywanie danych
* Bieżące monitorowanie zabezpieczeń
* Reagowanie na zdarzenia

W następnej sekcji hello przedstawiono sposób tooplan dla każdego z tych obszarów i stosować te zalecenia w zależności od wymagań.

> [!NOTE]
> Odczyt [Centrum zabezpieczeń Azure — często zadawane pytania (FAQ)](security-center-faq.md) listę często zadawane pytania, które również mogą być przydatne podczas hello projektowania i planowania fazy.
> 

## <a name="security-roles-and-access-controls"></a>Role zabezpieczeń i kontrola dostępu
W zależności od rozmiaru hello i struktury organizacji wiele osób oraz zespołów może używać zadań związanych z zabezpieczeniami w Centrum zabezpieczeń tooperform inny. Powitania po diagram masz przykład zawierający fikcyjne osoby oraz ich role i obowiązki związane z zabezpieczeniami:

![Role](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Centrum zabezpieczeń umożliwia toomeet tych osób różnych obowiązków. Na przykład:

**Jan (właściciel obciążenia chmury)**

* Zarządza obciążeniem chmury i powiązanymi zasobami
* Odpowiada za zaimplementowanie i utrzymanie ochrony zgodnie z zasadami zabezpieczeń firmy

**Aneta (CISO/CIO)**

* Odpowiedzialne za wszystkie aspekty zabezpieczeń firmy hello
* Chce stan zabezpieczeń firmy hello toounderstand między obciążeń chmury
* Wymaga toobe o głównych ataków i zagrożeń

**Daniel (zabezpieczenia informatyczne)**

* Zasady zabezpieczeń, które tooensure hello odpowiednią ochronę firmy zestawów
* Monitoruje zgodność z zasadami
* Generuje raporty dla kierownictwa lub audytorów

**Magda (operacje zabezpieczeń)**

* Monitoruje i odpowiada alerty toosecurity 24/7
* Eskalowanie tooCloud właściciel obciążenia lub analityk działu zabezpieczeń IT

**Stanisław (analityk zabezpieczeń)**

* Bada ataki
* Praca z korygowania tooapply właściciel obciążenia chmury 

Centrum zabezpieczeń używa [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md), co umożliwia [wbudowane role](../active-directory/role-based-access-built-in-roles.md) mogą być przypisane toousers, grup i usług Azure. Po otwarciu Centrum zabezpieczeń, zobacz tylko informacje związane z tooresources mają oni dostęp. Oznacza to, że użytkownik hello jest przypisany hello rolę właściciela, współautora lub czytelnika toohello subskrypcji lub grupy zasobów należącą do zasobu. Dodanie ról toothese istnieją dwa określonych ról Centrum zabezpieczeń:

- **Czytnik zabezpieczeń**: użytkownika należącego do roli toothis jest możliwe tooview prawa tooSecurity Center, który zawiera zalecenia, alertów, zasad i kondycji, ale nie będzie możliwe toomake zmiany.
- **Administrator zabezpieczeń**: takie same jak czytnika zabezpieczeń, ale można także zaktualizować hello zasady zabezpieczeń, odrzucić zalecenia i alerty.

role Centrum zabezpieczeń Hello opisane powyżej nie mają dostępu do obszarów usługi tooother Azure, takiego jak magazyn, sieci Web i mobilnych lub Internetu rzeczy.  

> [!NOTE]
> Użytkownik musi toobe co najmniej subskrypcji, właściciel grupy zasobów lub współautora toobe stanie toosee Centrum zabezpieczeń Azure. 
> 
> 

Przy użyciu osoby hello wyjaśnione w hello poprzedni diagram hello, które są wymagane następujące funkcje RBAC:

**Jan (właściciel obciążenia chmury)**

* Właściciel/Współautor grupy zasobów

**Daniel (zabezpieczenia informatyczne)**

* Właściciel/współautor subskrypcji lub administrator zabezpieczeń

**Magda (operacje zabezpieczeń)**

* Czytelnik subskrypcji lub alerty dla czytelnika zabezpieczeń tooview
* Właściciel/Współautor subskrypcji lub administratora zabezpieczeń wymagane toodismiss alertów

**Stanisław (analityk zabezpieczeń)**

* Alerty dotyczące subskrypcji czytnika tooview
* Właściciel/Współautor subskrypcji wymagane toodismiss alertów
* Obszar roboczy toohello dostępu mogą być wymagane

Niektóre inne tooconsider ważne informacje:

* Tylko właściciele lub współautorzy subskrypcji i administratorzy zabezpieczeń mogą edytować zasady zabezpieczeń
* Tylko właściciele i współautorzy subskrypcji i grupy zasobów mogą stosować zalecenia dotyczące zabezpieczeń zasobu

Podczas planowania kontroli dostępu przy użyciu funkcji RBAC dla Centrum zabezpieczeń można toounderstand się, kto w organizacji będą używać Centrum zabezpieczeń. Ponadto musisz wiedzieć, jakiego rodzaju zadania będą wykonywały te osoby, a następnie odpowiednio skonfigurować kontrolę dostępu opartą na rolach.

> [!NOTE]
> Firma Microsoft zaleca, aby przypisać hello najbardziej ograniczająca rola potrzebne dla użytkowników toocomplete ich zadań. Na przykład użytkowników, którzy muszą tylko tooview informacji na temat hello stan zabezpieczeń zasobów, ale nie podejmować działań, np. stosować zaleceń ani edytować zasad, należy przypisać rolę czytelnika hello.
> 
> 

## <a name="security-policies-and-recommendations"></a>Zasady zabezpieczeń i zalecenia w tym zakresie
Zasady zabezpieczeń definiuje zestaw hello formantów, które są zalecane dla zasobów w ramach hello określonej subskrypcji. W Centrum zabezpieczeń można zdefiniować zasady zgodnie z wymagań dotyczących zabezpieczeń tooyour firmy i typem aplikacji hello lub czułości hello danych.

Zasady, które są włączone na poziomie subskrypcji hello automatycznie propagację tooall grup zasobów w ramach subskrypcji hello pokazane na powitania po diagramu:

![Zasady zabezpieczeń](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Jeśli potrzebujesz tooreview, które zasady zostały zmienione, możesz użyć [dzienników inspekcji platformy Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). Zmiany zasad są zawsze rejestrowane w Dziennikach inspekcji Azure.
> 
> 

### <a name="security-recommendations"></a>Zalecenia dotyczące zabezpieczeń
Przed skonfigurowaniem zasad zabezpieczeń, przejrzyj wszystkie hello [zalecenia dotyczące zabezpieczeń](security-center-recommendations.md)i określić, czy te zasady są odpowiednie dla różnych subskrypcji i grupy zasobów. Jest również ważne toounderstand jakie działania należy podjąć tooaddress [zalecenia dotyczące zabezpieczeń](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) i kto w organizacji będzie odpowiedzialna za monitorowanie dla nowe zalecenia dotyczące i podjęcie hello wymagane kroki.

Usługa Security Center zaleci podanie szczegółowych informacji dotyczących kontaktu zabezpieczeń dla Twojej subskrypcji platformy Azure. Te informacje będą używane przez Microsoft toocontact Jeśli hello Microsoft Security odpowiedzi Center (MSRC) wykrywa, że danych klienta uzyskaniu przez nieautoryzowanego lub nielegalnych stronę. Odczyt [podać szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure](security-center-provide-security-contact-details.md) Aby uzyskać więcej informacji na temat tooenable tego zalecenia.

## <a name="data-collection-and-storage"></a>Zbieranie i przechowywanie danych
Centrum zabezpieczeń Azure używa hello Microsoft Monitoring Agent — jest to hello używać tego samego agenta hello Operations Management Suite i usługi analizy dzienników — toocollect zabezpieczeń danych z maszyn wirtualnych. Dane zbierane z tego agenta będą przechowywane w obszarach roboczych usługi Log Analytics.

### <a name="agent"></a>Agent

Po włączeniu funkcji zbierania danych w zasadach zabezpieczeń hello hello Microsoft Monitoring Agent (dla [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) lub [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) jest zainstalowany na wszystkich obsługiwanych maszyn wirtualnych platformy Azure i nowe pliki, które są tworzone.  Jeśli hello maszyna wirtualna ma już hello Microsoft Monitoring Agent został zainstalowany, Centrum zabezpieczeń Azure będzie korzystać z bieżącej hello zainstalowany agent. Proces agenta Hello jest zaprojektowana toobe nieinwazyjna i mają bardzo minimalny wpływ na wydajność maszyny Wirtualnej.

Microsoft Monitoring Agent dla systemu Windows Hello wymaga użycia portu TCP 443. Zobacz hello [Rozwiązywanie problemów z artykułu](security-center-troubleshooting-guide.md) dodatkowe szczegóły.

Jeśli w pewnym momencie chcesz toodisable zbierania danych, można go wyłączyć w zasadach zabezpieczeń hello. Jednak ponieważ hello Microsoft Monitoring Agent może być używany przez inne zarządzania platformy Azure i monitorowanie usług, hello agent nie zostanie usunięta automatycznie po wyłączeniu zbierania danych w Centrum zabezpieczeń. Można ręcznie odinstalować agenta hello w razie potrzeby.

> [!NOTE]
> listę obsługiwanych maszyn wirtualnych, przeczytaj hello toofind [Centrum zabezpieczeń Azure — często zadawane pytania (FAQ)](security-center-faq.md).
> 

### <a name="workspace"></a>Obszar roboczy

Danych zbieranych z programu Microsoft Monitoring Agent (imieniu Centrum zabezpieczeń Azure) będą przechowywane w każdej istniejącej analizy dzienników obszarów roboczych powitalne skojarzone z subskrypcją platformy Azure lub nowych obszarów roboczych, uwzględniając hello konta geograficznie hello maszyny Wirtualnej. 

W hello portalu Azure możesz wyszukać toosee listę obszarów roboczych usługi Analiza dzienników, wraz ze wszystkimi utworzone przez Centrum zabezpieczeń Azure. W przypadku nowych obszarów roboczych zostanie utworzona powiązana grupa zasobów. W obu przypadkach stosowana będzie następująca konwencja nazewnictwa: 

* Obszar roboczy: *DefaultWorkspace-[identyfikator-subskrypcji]-[lokalizacja-geograficzna]*
* Grupa zasobów: *DefaultResouceGroup-[lokalizacja-geograficzna]*

W przypadku obszarów roboczych utworzonych przez usługę Azure Security Center dane są przechowywane przez 30 dni. Wyjścia obszarów roboczych, przechowywania jest oparta na roboczym hello warstwy cenowej.

> [!NOTE]
> Firma Microsoft daje silne zobowiązań tooprotect hello prywatności i bezpieczeństwa tych danych. Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi. Aby uzyskać więcej informacji na temat obsługi danych i poufności, należy przeczytać artykuł [Azure Security Center — bezpieczeństwo danych](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Bieżące monitorowanie zabezpieczeń
Po wstępnej konfiguracji i zastosowaniu zaleceń Centrum zabezpieczeń hello następny krok polega na uwzględnieniu procesów operacyjnych Centrum zabezpieczeń.

tooaccess Centrum zabezpieczeń z portalu Azure, możesz kliknąć hello **Przeglądaj** i typ **Centrum zabezpieczeń** w hello **filtru** pola. Widoki Hello czy pobiera użytkownika hello są zgodne toothese zastosowane filtry, w poniższym przykładzie hello przedstawia środowisko z wielu toobe problemy opisane:

![pulpit nawigacyjny](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Centrum zabezpieczeń nie zakłóca zwykłych procedur operacyjnych, będzie pasywnie monitoruje wdrożenia i podano zalecenia na podstawie zasad zabezpieczeń hello, który został włączony.

Podczas należy najpierw włączyć toouse Centrum zabezpieczeń bieżącego środowiska platformy Azure, upewnij się, że należy przejrzeć wszystkie zalecenia, które mogą być wykonywane w hello **zalecenia** Kafelek lub względem poszczególnych zasobów (**obliczeniowe** **Sieci**, **magazyn & danych**, **aplikacji**).

Po wykonaniu wszystkich zaleceń, hello **zapobiegania** sekcji powinna być zielona dla wszystkich przejrzanych zasobów. Ciągłe monitorowanie w tym momencie staje się łatwiejsze, ponieważ zajmie tylko działania na podstawie zmian w hello zasobu zabezpieczeń kondycji oraz Kafelki zaleceń.

Witaj **wykrywania** sekcja jest bardziej reaktywna. zawiera ona, alerty dotyczące problemów, które są albo miejsce teraz, lub w przeszłości hello i wykrytych przez kontrolki Centrum zabezpieczeń i 3 systemów firm. Kafelek alerty zabezpieczeń Hello są wyświetlane wykresy słupkowe, które reprezentują hello liczbę alertów wykrywania zagrożeń zidentyfikowanych w poszczególnych dniach oraz ich rozkład hello różnych kategorii ważności (niskiej, średniej, wysokiej). Aby uzyskać więcej informacji na temat alertów zabezpieczeń, przeczytaj [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> Można również wykorzystać toovisualize Microsoft Power BI danych Centrum zabezpieczeń. Przeczytaj artykuł [Get insights from Azure Security Center data with Power BI](security-center-powerbi.md) (Uzyskiwanie szczegółowych informacji na podstawie danych z Centrum zabezpieczeń Azure za pomocą usługi Power BI).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Monitorowanie nowych lub zmodyfikowanych zasobów
Większość środowisk Azure jest dynamiczna. Systematycznie tworzone są nowe zasoby i usuwane stare, zmieniają się konfiguracje itd. Centrum zabezpieczeń pomaga, upewnij się, że masz wgląd w hello stanu zabezpieczeń nowych zasobów.

Po dodaniu nowych zasobów (maszyn wirtualnych, baz danych SQL) tooyour środowiska Azure Centrum zabezpieczeń automatycznie odnajdzie tych zasobów i rozpocząć toomonitor ich zabezpieczeń. Obejmuje to także role procesu roboczego i role sieci Web usługi PaaS. Po włączeniu funkcji zbierania danych w hello [zasady zabezpieczeń](security-center-policies.md)dodatkowe możliwości monitorowania zostanie włączona automatycznie maszyn wirtualnych.

![Kluczowe obszary](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Dla maszyn wirtualnych kliknij pozycję **Obliczenia** w obszarze **Zapobieganie**. Wszystkie problemy z włączaniem danych lub powiązanymi zaleceniami zostaną wyświetlone w hello **omówienie** karcie i **zalecenia dotyczące monitorowania** sekcji.
2. Hello widoku **zalecenia** toosee co, jeśli zagrożenia bezpieczeństwa zostały zidentyfikowane dla nowego zasobu hello.
3. Często zdarza się, że po dodaniu tooyour środowiska nowych maszyn wirtualnych, tylko hello jest zainstalowany system operacyjny początkowo. właściciel zasobu Hello może być konieczne pewne toodeploy czasu inne aplikacje, które będą używane przez te maszyny wirtualne.  W idealnym przypadku należy wiedzieć hello zamiar końcowego danego obciążenia. Jest on przechodzi toobe serwera aplikacji? Oparte na jaki to będzie toobe jest nowe obciążenie, można włączyć odpowiednie hello **zasady zabezpieczeń**, czyli hello trzeci krok w tym przepływie pracy.
4. Jak tooyour środowiska Azure dodawane są nowe zasoby, jest to możliwe, że nowe alerty są wyświetlane w hello **alerty zabezpieczeń** kafelka. Zawsze Sprawdź, czy istnieją nowe alerty w tym kafelku i podejmuj działania zgodnie z zaleceniami Centrum tooSecurity.

Trzeba będzie także tooregularly hello stanu monitora z istniejących zasobów tooidentify zmian konfiguracji, które spowodowały zagrożenia bezpieczeństwa, odejście od zalecanych planów bazowych oraz alerty zabezpieczeń. Rozpocznij od hello pulpit nawigacyjny Centrum zabezpieczeń. Pulpit ma trzy główne obszary tooreview spójne przeglądanie.

![Operacje](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Witaj **zapobiegania** panelu sekcji zapewnia szybki dostęp tooyour kluczowych zasobów. Użyj tej opcji toomonitor obliczeniowych, sieci, magazynu i danych i aplikacji.
2. Witaj **zalecenia** panelu umożliwia tooreview zaleceń Centrum zabezpieczeń. Podczas ciągłego monitorowania może się okazać, że nie masz zalecenia codziennie, co jest zrozumiałe, ponieważ uwagę, że wszystkie zalecenia na powitania początkowej konfiguracji Centrum zabezpieczeń. Z tego powodu nie może mieć nowe informacje w tej sekcji codziennie i trzeba tooaccess go zgodnie z potrzebami.
3. Witaj **wykrywania** sekcji mogą ulec zmianie na podstawie bardzo często lub bardzo rzadko. Zawsze czytaj alerty zabezpieczeń i podejmuj działania na podstawie zaleceń usługi Security Center.

## <a name="incident-response"></a>Reagowanie na zdarzenia
Centrum zabezpieczeń wykryje i alerty toothreats miarę ich występowania. Organizacje powinny monitorować nowe alerty zabezpieczeń i podjąć działania jako dodatkowe wymagane tooinvestigate lub je korygować atak powitania. Aby uzyskać więcej informacji na temat sposobu działania funkcji wykrywania zagrożeń usługi Security Center, przeczytaj [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md).

Chociaż w tym artykule nie tooassist konwersji hello tworzenia własnego planu reagowania na zdarzenia, zamierzamy toouse Microsoft Azure Security Response w cyklu życia chmury hello jako hello foundation etapach odpowiedzi na zdarzenia. etapy Hello są przedstawione w powitania po diagramu:

![Podejrzane działania](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Można użyć hello National Institute of Standards and Technology (NIST) [Przewodnik obsługi zdarzenia zabezpieczeń komputera](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) jako tooassist odwołanie zostanie tworzenie własnych.
> 

Alerty Centrum zabezpieczeń można użyć podczas hello następujące etapy:

* **Wykrywanie**: zidentyfikuj podejrzane działanie w co najmniej jednym zasobie. 
* **Oceny**: wykonaj hello początkowej oceny tooobtain więcej informacji na temat hello podejrzanych działań.
* **Diagnozowanie**: Użyj hello korygowania kroki tooconduct hello procedury techniczne tooaddress hello problem.

Każdy Alert zabezpieczeń zawiera informacje, które mogą być używane toobetter zrozumieć charakter hello atak powitania i zasugerować możliwe ograniczenie jego skutków. Niektóre alerty zapewniają również tooeither łącza więcej informacji lub tooother źródeł informacji w systemie Azure. Korzystając z informacji hello dostępnych dalszych badań i środki zaradcze toobegin i można także przeszukać związanych z zabezpieczeniami danych przechowywanych w obszarze roboczym.

Witaj poniższym przykładzie pokazano podejrzane działania w protokole RDP:

![Podejrzane działania](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Jak widać, ten blok zawiera szczegóły dotyczące czasu hello, że atak powitania miało miejsce, hello nazwa hosta źródłowego, hello docelową maszynę Wirtualną i poszczególne kroki zaleceń. W niektórych sytuacjach hello informacji o źródle atak powitania może być pusta. Więcej informacji na temat działania tego typu znajduje się w artykule [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) (Brakujące informacje źródłowe w alertach Centrum zabezpieczeń Azure).

W hello [jak tooLeverage hello Centrum zabezpieczeń Azure i programu Microsoft Operations Management Suite dla reagowania na zdarzenia](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) wideo widać niektóre pokazów, które mogą pomóc Ci toounderstand sposobu użycia Centrum zabezpieczeń w każdym jeden z tych etapów.

> [!NOTE]
> Odczyt [Leveraging Centrum zabezpieczeń Azure do reagowania na zdarzenia](security-center-incident-response.md) Aby uzyskać więcej informacji dotyczących sposobu tooassist możliwości Centrum zabezpieczeń toouse możesz podczas reagowania na zdarzenia procesu. 
> 
> 

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób tooplan dla wdrożenia Centrum zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md)
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.

