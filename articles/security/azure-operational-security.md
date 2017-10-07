---
title: "aaaAzure bezpieczeństwa operacyjnego | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat programu Microsoft Operations Management Suite (OMS), jego usług i jak działa."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Azure bezpieczeństwa operacyjnego
## <a name="introduction"></a>Wprowadzenie

### <a name="overview"></a>Omówienie
Wiemy, że zabezpieczeń jest jednego zadania w chmurze hello i jak ważne jest aby znaleźć dokładne i aktualne informacje na temat zabezpieczeń platformy Azure. Jednym z hello najlepsze toouse powodów Azure dla usług i aplikacji jest tootake zaletą hello szerokiej gamy narzędzi zabezpieczeń i możliwości są dostępne. Te narzędzia i funkcje dzięki możliwości toocreate bezpiecznych rozwiązań na powitania bezpiecznej platformie Azure. Windows Azure należy podać poufność, integralność i dostępność danych klienta, jednoczesnym accountability przezroczysty.

Klienci toohelp lepiej zrozumieć tablicy hello kontroli zabezpieczeń zaimplementowana w systemie Microsoft Azure z obu powitania klienta i Microsoft perspektywy operacyjnej, tym oficjalnym dokumencie "Azure bezpieczeństwa operacyjnego", jest zapisywany zapewnia kompleksowe wyświetlać hello operacyjne zabezpieczeń dostępnych w systemie Windows Azure.

### <a name="azure-platform"></a>Platformy Azure
Azure to platforma usługi chmury publicznej, która obsługuje szeroki wybór systemów operacyjnych, programowania języków, struktury, narzędzia, baz danych i urządzeń. Kontenery systemu Linux można uruchamiać z integracją rozwiązania Docker; Tworzenie aplikacji za pomocą języka JavaScript, Python, .NET, PHP, Java i Node.js; Kompilacja zapleczy dla systemu iOS, Android i Windows urządzeń. Usługa w chmurze Azure obsługuje hello już polegać na tej samej technologii miliony deweloperów i specjalistów IT i zaufania.

Podczas tworzenia lub migracji zasobów informatycznych do dostawcy usług chmury publicznej, są zależne tooprotect możliwości w organizacji, aplikacji i danych za pomocą usługi hello i formanty hello zapewniają toomanage hello bezpieczeństwa sieci opartej na chmurze zasoby.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą spełnić ich wymagań dotyczących zabezpieczeń. Ponadto Azure zapewnia szereg zabezpieczeń można skonfigurować opcje i hello toocontrol możliwości ich, dzięki czemu można dostosować toomeet hello unikatowe wymagania dotyczące zabezpieczeń wdrożenia w organizacji. Ten dokument zostanie pomaga w zrozumieniu sposobu Azure zabezpieczeń możliwości mogą pomóc spełnić te wymagania.

### <a name="abstract"></a>Abstrakcyjny
Azure bezpieczeństwa operacyjnego odwołuje się toohello usług, kontrolek i toousers dostępne funkcje ochrony danych, aplikacji i innych zasobów na platformie Microsoft Azure. Azure bezpieczeństwa operacyjnego w oparciu framework, która będzie zawierała wiedzę hello za pośrednictwem różnych funkcji, które są unikatowe tooMicrosoft, w tym hello Microsoft Security Development Lifecycle (SDL), hello Microsoft Security Response Center Program i głębokie świadomości hello bezpieczeństwa zagrożeń.

Ten dokument zawiera opis tooAzure podejście firmy Microsoft bezpieczeństwa operacyjnego hello platformy Microsoft Azure w chmurze i obejmuje następujące usługi:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure obserwatora sieciowego](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Analizy usługi Azure Storage](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Usługa Azure Active directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) jest hello IT rozwiązania do zarządzania hello chmura hybrydowa. Użyte bez parametrów lub tooextend, który zapewnia istniejącego wdrożenia programu System Center, OMS hello maksymalną elastyczność i kontrola zarządzania infrastruktury w chmurze.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Dzięki OMS mogą zarządzać wystąpienie w żadną chmurą, tym lokalnymi, Azure AWS, Windows Server, Linux, VMware i OpenStack, na niższe koszty niż konkurencyjnych rozwiązania. Skompilowany dla Witaj świecie pierwszy chmury, OMS oferuje nowe toomanaging podejście przedsiębiorstwie hello najszybsze i najbardziej ekonomiczny sposób toomeet nowych transakcji będzie wymagał i uwzględnić nowe obciążenia, aplikacji i środowisk chmury.

### <a name="oms-services"></a>Usługi pakietu OMS

podstawowe funkcje Hello OMS są udostępniane przez zestaw usług, które działają na platformie Azure. Każda usługa udostępnia funkcję zarządzania określonymi i scenariusze zarządzania różnych tooachieve usług można łączyć.

| Usługa  | Opis|
| :------------- | :-------------|
| Log Analytics | Monitorowanie i analizowanie hello dostępności i wydajności różnych zasobów, w tym fizycznych i maszyn wirtualnych. |
|Automatyzacja | Automatyzowanie procesów ręcznych oraz wymuszanie konfiguracji maszyn fizycznych i wirtualnych. |
| Tworzenie kopii zapasowych | Kopie zapasowe i przywracanie danych o kluczowym znaczeniu. |
| Site Recovery | Zapewnianie wysokiej dostępności kluczowych aplikacji. |

### <a name="log-analytics"></a>Log Analytics

Usługa [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) umożliwia monitorowanie pakietu OMS przez zbieranie danych z zarządzanych zasobów w centralnym repozytorium. Te dane mogą obejmować zdarzeń, danych wydajności lub niestandardowe dane przekazane za pośrednictwem hello interfejsu API. Po zebraniu danych, danych hello jest dostępna dla alertów, analizy i eksportowanie.


Ta metoda umożliwia tooconsolidate danych z różnych źródeł, więc można połączyć dane z usługami Azure z istniejącą lokalnego środowiska. Oddziela również wyraźnie hello zbierania danych hello hello akcję podejmowaną w odniesieniu do danych tak, aby wszystkie akcje są dostępne tooall rodzajów danych z.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

Witaj usługi analizy dzienników zarządza danych oparte na chmurze bezpiecznie przy użyciu hello następujące metody:
-   Podział danych
-   przechowywanie danych
-   Zabezpieczenia fizyczne
-   Zarządzanie zdarzeniami
-   Zgodność
-   Certyfikaty standardów zabezpieczeń

### <a name="azure-backup"></a>Azure Backup

[Kopia zapasowa Azure](http://azure.microsoft.com/documentation/services/backup) dostarcza dane kopii zapasowej i przywracania usługi i jest częścią pakietu OMS hello produktów i usług.
Chroni ona dane aplikacji i przechowuje je przez wiele lat bez konieczności ponoszenia jakichkolwiek inwestycji kapitałowych i przy minimalnych kosztach operacyjnych. Go można utworzyć kopię zapasową danych z fizycznymi i wirtualnymi systemów Windows Server dodatkowo tooapplication obciążeń, takich jak SQL Server i programu SharePoint. Może także służyć przez [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate chronionych danych tooAzure nadmiarowości i długoterminowego przechowywania.


Chronione dane w usłudze Azure Backup są przechowywane w magazynie kopii zapasowych, znajdującym się w określonym regionie geograficznym. Witaj, dane są replikowane w hello na tym samym regionie i, w zależności od typu hello magazynu, może być również region replikowanych tooanother dla dalszego odporności.

### <a name="management-solutions"></a>Rozwiązania do zarządzania
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) firmy Microsoft w chmurze IT rozwiązanie do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze.


[Rozwiązania do zarządzania](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) opakowaniach jednostkowych zestawy warunki logiczne implementujących scenariusza określonego zarządzania przy użyciu co najmniej jedną usługę OMS. Różnych rozwiązaniach dostępnych firmy Microsoft i partnerów, można łatwo dodać tooyour subskrypcji platformy Azure tooincrease hello wartości inwestycji w OMS. Przez partnera można utworzyć własne toosupport rozwiązania, aplikacje i usługi i podaj toousers za pośrednictwem hello Azure Marketplace lub Szybki Start szablonów.


![Rozwiązania do zarządzania](./media/azure-operational-security/azure-operational-security-fig4.png)

Dobrym przykładem rozwiązania obejmującego wiele usług tooprovide dodatkowe funkcje jest hello [rozwiązania do zarządzania aktualizacji](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). To rozwiązanie wymaga hello [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) agenta dla systemu Windows i Linux toocollect informacje o wymaganych aktualizacji na każdego agenta. Zapisuje danych repozytorium analizy dzienników toohello gdzie można analizować je z dołączone pulpitu nawigacyjnego.

Podczas tworzenia wdrożenia, elementy runbook w [usługi Automatyzacja Azure](https://docs.microsoft.com/azure/automation/automation-intro) są używane tooinstall wymagane aktualizacje. Zarządzaj w portalu hello całego procesu i nie ma potrzeby tooworry o hello szczegółami.

## <a name="azure-security-center"></a>Azure Security Center

Centrum zabezpieczeń Azure ułatwia ochronę zasobów platformy Azure. Zapewnia zabezpieczenia zintegrowane monitorowanie i zarządzanie zasadami subskrypcji platformy Azure. W ramach usługi hello jesteś w stanie toodefine zasady nie tylko z subskrypcjami platformy Azure, ale także przed [grup zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), dlatego może być bardziej szczegółowego.

### <a name="security-policies-and-recommendations"></a>Zasady zabezpieczeń i zalecenia w tym zakresie

Zasady zabezpieczeń definiuje zestaw hello formantów, które są zalecane dla zasobów w ramach hello określonej subskrypcji lub grupy zasobów.

W Centrum zabezpieczeń można zdefiniować zasady zgodnie z wymagań dotyczących zabezpieczeń tooyour firmy i typem aplikacji hello lub czułości hello danych.

![Zasady zabezpieczeń i zalecenia w tym zakresie](./media/azure-operational-security/azure-operational-security-fig5.png)


Zasady, które są włączone na poziomie subskrypcji hello automatycznie propagację tooall grup zasobów w ramach subskrypcji hello, jak pokazano na diagramie hello hello prawej strony:


### <a name="data-collection"></a>Zbieranie danych

Centrum zabezpieczeń zbiera dane z Twojego tooassess maszynach wirtualnych (VM) stanu zabezpieczeń, podaj zalecenia dotyczące zabezpieczeń i alertów toothreats. Po pierwszym dostęp do Centrum zabezpieczeń, zbierania danych jest włączona na wszystkich maszynach wirtualnych w ramach subskrypcji. Zbieranie danych jest zalecane, ale można zrezygnować z wyłączając zbierania danych w hello zasadami Centrum zabezpieczeń.

### <a name="data-sources"></a>Źródła danych

- Centrum zabezpieczeń Azure analizuje dane z powitania po widoczność tooprovide źródeł do Twojej stan zabezpieczeń, identyfikowanie luk w zabezpieczeniach i zaleca środki zaradcze oraz wykrywać zagrożenia active:

-   Usług Azure: Używa informacji o konfiguracji hello usług platformy Azure została wdrożona, komunikując się z dostawcą zasobów tej usługi.

- Ruch sieciowy: używa próbkowanych metadanych ruchu sieciowego z infrastruktury firmy Microsoft, takich jak źródłowy i docelowy adres IP, źródłowy i docelowy port, rozmiar pakietu i protokół sieciowy.

-   Rozwiązania partnerów: używa alertów zabezpieczeń z rozwiązań zintegrowanych partnerów, takich jak zapory i rozwiązania do ochrony przed złośliwym oprogramowaniem.

-   Maszyny wirtualne: używa informacji dotyczących konfiguracji oraz zdarzeń związanych z zabezpieczeniami, takich jak zdarzenia systemu Windows i dzienniki inspekcji, dzienniki programu IIS, komunikaty dziennika systemu i pliki zrzutu awaryjnego, z maszyn wirtualnych.

### <a name="data-protection"></a>Ochrona danych

Klienci toohelp zapobiegania, wykrywania i odpowiadać toothreats, Centrum zabezpieczeń Azure zbiera i przetwarza dane związane z zabezpieczeniami, w tym informacje o konfiguracji, metadane, dzienniki zdarzeń i pliki zrzutu awaryjnego. Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi.

-   **Podział danych**: dane są przechowywane logicznie oddzielnie dla każdego składnika w całym hello usługi. Wszystkie dane są otagowane informacjami o organizacji. Znakowanie ten będzie nadal występował w całym cyklu życia danych hello i są wymuszane w każdej warstwie hello usługi.

-   **Dostęp do danych**: tooprovide zalecenia dotyczące zabezpieczeń i Zbadaj możliwe zagrożenia bezpieczeństwa, personel firmy Microsoft mogą uzyskać dostęp do informacji zbieranych lub przeanalizowane przez usługi Azure, w tym pliki zrzutu awaryjnego, przetworzyć zdarzenia tworzenia dysku maszyny Wirtualnej migawki i artefaktów, które mogą przypadkowo obejmować dane klienta lub dane osobowe z maszyn wirtualnych. Firma Microsoft jest zgodna toohello [warunki dotyczące usług Online firmy Microsoft i zasady zachowania poufności informacji](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), których stan, który firma Microsoft nie ma używa danych klienta lub interpretowania go do celów reklamowych lub podobne komercyjnych.

-   **Użyj danych**: Firma Microsoft wykorzystuje wzorce i analizy zagrożeń widoczne w wielu dzierżawy tooenhance naszych możliwości wykrywania i zapobiegania; że odbywa się zgodnie z opisem w temacie zobowiązaniami prywatności hello naszych [prywatności Instrukcja](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Lokalizacja danych

Usługa Azure Security Center zbiera efemeryczne kopie plików zrzutu awaryjnego i analizuje je pod kątem dowodów na próby ich naruszenia i pomyślnie przeprowadzonych ataków. Centrum zabezpieczeń Azure wykonuje tę analizę w hello tej samej lokalizacji geograficznej, jak hello obszaru roboczego i usuwa hello tymczasowych kopii po zakończeniu analizy. Artefakty maszyny są przechowywane w centralnie hello tego samego regionu, jak hello maszyny Wirtualnej.

-   **Kont magazynu**: określono konto magazynu dla każdego regionu, w którym są uruchomione maszyny wirtualne. Ta umożliwia możesz toostore danych w hello tego samego regionu hello maszyny wirtualnej, z których hello zbieranych danych.

-   **Centrum zabezpieczeń Azure magazynu**: informacje o alertach zabezpieczeń, takich jak alerty partnera, zalecenia i stan kondycji zabezpieczeń są przechowywane w centralnie, w obecnie hello Stanów Zjednoczonych. Informacje te mogą obejmować informacji powiązanych z konfiguracji i zdarzenia zabezpieczeń zebranych z maszyn wirtualnych jako wymagane tooprovide możesz z hello zabezpieczeń alertu, zalecenie lub zabezpieczeń stan kondycji.


## <a name="azure-monitor"></a>Azure Monitor

Witaj [zabezpieczeń OMS](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) i umożliwia rozwiązanie inspekcji IT tooactively monitorowanie wszystkich zasobów, które mogą pomóc zminimalizować wpływ hello zdarzeń zabezpieczeń. Zabezpieczenia OMS i inspekcji ma domen zabezpieczeń, które mogą służyć do monitorowania zasobów. Domena zabezpieczeń Hello zapewnia szybki dostęp toooptions, zabezpieczeń hello następujące domeny są objęte więcej szczegółów:

-   oceny złośliwego oprogramowania
-   Ocena aktualizacji
-   Tożsamościami i dostępem.

Azure Monitor zawiera tooinformation wskaźniki dotyczące określonych typów zasobów. Zapewnia ona wizualizacji, zapytania, routingu, alerty, automatyczne skalowanie i automatyzacji na dane zarówno z hello infrastruktury platformy Azure (dziennik) i każdego pojedynczego zasobu platformy Azure (dzienników diagnostycznych).

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


Aplikacje w chmurze są złożonych z wielu części ruchu. Monitorowania udostępnia tooensure danych, która aplikacja pozostaje w górę i uruchomiona w dobrej kondycji. Pomaga również należy toostave wyłączone potencjalne problemy lub Rozwiązywanie problemów z przeszłości te.

Ponadto można użyć monitorowania danych toogain szczegółowych informacji o aplikacji. Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.

### <a name="azure-activity-log"></a>Dziennik aktywności platformy Azure


Jest dziennika, który zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji. Witaj dziennik aktywności była wcześniej znana jako "Dzienników inspekcji" lub "Operacyjne dzienniki", ponieważ zgłasza płaszczyzny kontroli zdarzeń dla subskrypcji.

![Dziennik aktywności platformy Azure](./media/azure-operational-security/azure-operational-security-fig7.png)

Korzystając z hello dziennik aktywności, można określić hello ", co, która i kiedy" dla żadnego zapisu (PUT, POST, DELETE) wykonywanych na powitania zasobów w ramach subskrypcji. Można także zrozumieć hello stanu operacji hello i inne odpowiednie właściwości. Hello dziennik aktywności nie zawiera operacje zasobów, które używają modelu klasycznym hello lub (GET) operacji odczytu.

### <a name="azure-diagnostic-logs"></a>Dzienniki diagnostyczne platformy Azure

Te dzienniki są emitowane przez zasób i zawierają rozbudowane, często dane dotyczące operacji hello tego zasobu. zawartość Hello te dzienniki zależy od typu zasobu.

Na przykład dzienniki systemu zdarzeń systemu Windows są jedną kategorię dzienników diagnostycznych dla maszyn wirtualnych i obiektów blob, tabeli, a dzienniki kolejki są kategorii dzienników diagnostycznych dla kont magazynu.

Dzienniki diagnostyczne różnią się od hello [dziennik aktywności (wcześniej znane jako dziennik inspekcji lub dziennik operacyjny)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). Dziennik aktywności Hello zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji. Dzienniki diagnostyczne zapewniają wgląd w operacje, w zasobie wykonanie samego.

### <a name="metrics"></a>Metryki

Azure Monitor umożliwia tooconsume telemetrii toogain wgląd w hello wydajności i kondycji obciążeń na platformie Azure. Typ najważniejszych Hello danych telemetrycznych platformy Azure jest metryki hello (nazywanych również liczniki wydajności) emitowane przez zasoby najbardziej platformy Azure. Azure Monitor udostępnia kilka sposobów tooconfigure i korzystać z tych [metryki](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) do monitorowania i rozwiązywania problemów. Metryki są cenne źródła danych telemetrycznych i umożliwiają hello toodo następujące zadania:

-   **Śledzenie wydajności hello** zasobu (np. maszyna wirtualna, witryny sieci Web lub logiki aplikacji) kreślenia jego metryki na wykresie portalu i przypinanie tego pulpitu nawigacyjnego tooa wykresu.

-   **Otrzymuj powiadomienia o problemie** czy wpływ metrykę przecina pewnej wartości progowej, hello wydajności zasobu.

-   **Konfigurowanie automatycznych akcji**, takie jak automatyczne skalowanie zasobu lub wyzwalania elementu runbook, gdy metryki przecina pewnej wartości progowej.

-   **Wykonywać zaawansowane analizy** lub zgłaszanie trendów wydajności lub użycia zasobu.

-   **Archiwum** hello historii wydajności lub kondycji zasobu zgodności i inspekcji.

### <a name="azure-diagnostics"></a>Diagnostyka Azure

Istnieje możliwość hello w ramach platformy Azure, która umożliwia hello zbieranie danych diagnostycznych o wdrożonej aplikacji. Można użyć rozszerzenia diagnostyki hello z różnych różnych źródeł. Obecnie obsługiwane są [Azure Cloud Service w sieci Web i proces roboczy](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [maszyny wirtualne Azure](https://docs.microsoft.com/azure/virtual-machines/windows/overview) systemu Microsoft Windows i [sieci szkieletowej usług](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Innymi usługami Azure mają własne oddzielne diagnostyki.

## <a name="azure-network-watcher"></a>Monitor sieci platformy Azure

Inspekcja zabezpieczeń sieci jest niezbędne do wykrycia luk w zabezpieczeniach sieci i zapewniania zgodności z przepisami ładu modelu i zabezpieczeń IT. Widok grupy zabezpieczeń można pobrać hello skonfigurowane reguły grupy zabezpieczeń sieci i zabezpieczeń i hello reguły efektywnym elementem systemu zabezpieczeń. Z listą hello zasady zastosowane należy określić hello portów, które są otwarte i oceny luk w zabezpieczeniach sieci.

[Monitor sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) to regionalnych usługa, która umożliwia toomonitor i diagnozowanie warunki na poziomie sieci w, do i z platformy Azure. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure. Ta usługa obejmuje przechwytywania pakietów, następnego przeskoku, przepływ IP Sprawdź widok grupy zabezpieczeń, dzienniki przepływu NSG. Scenariusz poziomu monitorowania udostępnia widok tooend zakończenia zasobów sieciowych w monitorowania zasobów sieciowych tooindividual kontrastu.

![Monitor sieci platformy Azure](./media/azure-operational-security/azure-operational-security-fig8.png)

Obserwatora sieciowego ma obecnie hello następujące możliwości:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Dzienniki inspekcji</a>**-operacje wykonywane w ramach konfiguracji hello sieci są rejestrowane. Dzienniki te mogą być wyświetlane w portalu Azure hello lub pobrany przy użyciu narzędzi firmy Microsoft, takich jak usługi Power BI lub narzędzi innych firm. Dzienniki inspekcji są dostępne za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia i interfejsu API Rest. Aby uzyskać więcej informacji na dziennikach inspekcji Zobacz operacje inspekcji za pomocą Menedżera zasobów. Dzienniki inspekcji są dostępne dla operacje wykonywane na wszystkich zasobów sieciowych.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">Przepływ IP weryfikuje </a>**  — sprawdza, czy pakiet jest dozwolony lub niedozwolony na podstawie przepływ informacji 5-elementowej pakietu parametrów (docelowy adres IP, źródłowy adres IP, Port docelowy, Port źródłowy i Protocol). Pakietów hello jest niedozwolone przez sieciowej grupy zabezpieczeń, reguła hello i sieciową grupę zabezpieczeń, którego pakietów hello jest zwracana.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Następny przeskok</a>**  — określa hello następnego skoku dla pakietów przesyłane w hello Azure sieci szkieletowej, umożliwiając tras toodiagnose any nieprawidłowo zdefiniowane przez użytkownika.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Widok grupy zabezpieczeń</a>**  -pobiera hello zabezpieczeń skuteczne i zastosowanej reguły, które są stosowane na maszynie Wirtualnej.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">Przepływ NSG rejestrowania</a>**  — dzienniki przepływu dla grup zabezpieczeń sieci Włącz toocapture dzienniki pokrewne tootraffic, który ma być dozwolony lub odrzucany przez reguły zabezpieczeń hello hello grupy. Przepływ Hello jest zdefiniowana przez informacji 5-elementowej — źródłowy adres IP, docelowy adres IP, Port źródłowy, Port docelowy i protokołu.

## <a name="azure-storage-analytics"></a>Analityka usługi Azure Storage

[Analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) może przechowywać metryki, które zawierają zagregowane transakcji statystyk i pojemności dane dotyczące usługi Magazyn tooa żądań. Transakcje są raportowane zarówno na poziomie operacji hello interfejsu API i na poziomie usługi magazynu hello i pojemności jest zgłaszany na poziomie usługi hello magazynu. Dane metryk można wykorzystania usługi magazynu używanych tooanalyze, diagnozowanie problemów z żądania wysyłane przed hello usługi magazynu i tooimprove hello wydajności aplikacji korzystających z usługi.

[Analizy usługi Azure Storage](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) wykonuje rejestrowanie i udostępnia metryki danych dla konta magazynu. Można użyć tego żądania tootrace danych, analizować trendy użycia i diagnozowanie problemów z kontem magazynu. Rejestrowanie analityka magazynu jest dostępne dla hello [usługi obiektów Blob, kolejki i tabeli](https://docs.microsoft.com/azure/storage/storage-introduction). Analityka magazynu rejestruje szczegółowe informacje na temat usługi Magazyn tooa udane i nieudane żądania.

Te informacje mogą być używane toomonitor poszczególnych żądań i toodiagnose problemy z usługą magazynu. Żądania są rejestrowane w sposób optymalny. Wpisy dziennika są tworzone tylko w przypadku żądań wysyłanych do punktu końcowego usługi hello. Na przykład jeśli konto magazynu ma działanie punktu końcowego obiektu Blob, ale nie w jej tabel lub kolejek punktów końcowych, tylko dzienniki dotyczące toohello usługi obiektów Blob jest tworzony.

toouse analityka magazynu, należy ją włączyć osobno dla każdej usługi ma toomonitor. Możesz je włączyć w hello [portalu Azure](https://portal.azure.com/); Aby uzyskać więcej informacji, zobacz [monitorować konta magazynu w portalu Azure hello](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Można również włączyć analityka magazynu programowo przy użyciu interfejsu API REST hello lub powitania klienta biblioteki. Użyj hello ustawić właściwości usługi operacji tooenable analityka magazynu osobno dla każdej usługi.

Hello zagregowane dane są przechowywane w dobrze znany obiekt blob (w przypadku rejestrowania) i dobrze znanego tabele (dla metryki), które mogą uzyskać dostęp za pomocą usługi Blob hello i tabeli interfejsów API.

Analityka magazynu ma limit 20 TB na powitania ilość przechowywanych danych, która jest niezależna od hello całkowitego limitu konta magazynu. Wszystkie dzienniki są przechowywane w [blokowe obiekty BLOB](https://docs.microsoft.com/azure/storage/storage-analytics) w kontenerze o nazwie $logs, które są automatycznie tworzone podczas analityka magazynu jest włączona dla konta magazynu.

następujące akcje wykonywane przez analityka magazynu Hello są rozliczeniowy:

-   Obiekty BLOB toocreate żądań logowania
-   Żądania toocreate jednostek tabeli dla metryki.

> [!Note]
> Aby uzyskać więcej informacji dotyczących rozliczeń i zasad przechowywania danych, zobacz [analizy magazynu i rozliczeń](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
> Aby uzyskać optymalną wydajność ma toolimit hello liczba dysków wysokiej wykorzystywanych dołączony toohello maszyny wirtualnej tooavoid możliwości ograniczania. Jeśli wszystkie dyski są nie jest wysoce włączona na powitania tym samym czasie hello konta magazynu może obsługiwać większy dysk numer.

> [!Note]
> Aby uzyskać więcej informacji o limity konta magazynu, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](https://docs.microsoft.com/azure/storage/storage-scalability-targets).


następujące typy żądań uwierzytelnionych i anonimowych Hello są rejestrowane.

| Uwierzytelniony  | Anonimowe|
| :------------- | :-------------|
| Liczba pomyślnych żądań | Liczba pomyślnych żądań |
|Nieudane żądania, w tym limitu czasu, ograniczania przepustowości sieci, autoryzacji i innych błędów | Żądania przy użyciu dostępu sygnatury dostępu Współdzielonego, włącznie z żądaniami nie powiodło się i pomyślne |
| Żądania przy użyciu dostępu sygnatury dostępu Współdzielonego, włącznie z żądaniami nie powiodło się i pomyślne |Błędy limitu czasu dla klienta i serwera |
|   Żądania tooanalytics danych |    Nieudane żądania GET z kodem błędu 304 (nie jest zmodyfikowany) |
| Żądania wysyłane przez analityka magazynu, takich jak dziennika utworzeniu lub usunięciu, nie są rejestrowane. Pełną listę hello zarejestrowane dane są udokumentowane WE hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) i [Format dziennika analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) tematów. | Inne nieudanych żądań anonimowych nie są rejestrowane. Pełną listę hello zarejestrowane dane są udokumentowane WE hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) i [Format dziennika analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |
## <a name="azure-active-directory"></a>Usługa Azure Active Directory

Usługi Azure AD umożliwia także całą gamę możliwości zarządzania tożsamościami, w tym uwierzytelniania wieloskładnikowego, rejestracji urządzenia, zarządzanie hasłami samoobsługi, Samoobsługowe zarządzanie grupami, uprzywilejowane konto zarządzania, kontroli dostępu opartej na rolach, monitorowania użycia aplikacji, sformatowanego inspekcji i zabezpieczeń, monitorowanie i alerty.

-   Poprawy zabezpieczeń aplikacji z usługi Azure AD, uwierzytelnianie wieloskładnikowe i dostępu warunkowego.

-   Monitorowanie użycia aplikacji oraz ochronę firmy przed zagrożeniami zaawansowanych zabezpieczeń, monitorowanie i raportowanie.

W usłudze Azure Active Directory (Azure AD) uwzględniono raporty dotyczące zabezpieczeń, działań i inspekcji dla katalogu. [Raport dotyczący usługi Azure Active Directory inspekcji Hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) pomaga klientom tooidentify uprzywilejowany akcje, które wystąpiły w usłudze Azure Active Directory. Uprzywilejowanych akcji obejmują zmiany podniesienia uprawnień (na przykład tworzenie roli lub resetowanie haseł), zmiana konfiguracji zasad (na przykład zasady haseł) lub zmiany konfiguracji toodirectory (na przykład zmiany toodomain federacyjnego ustawienia).

Witaj raporty zawierają hello rekordu inspekcji dla nazwy zdarzenia hello, aktora hello, który wykonał akcję hello, zasobu docelowego hello wpływ zmiany hello i hello daty i czasu (UTC). Klienci są w stanie tooretrieve hello listę zdarzeń inspekcji dla ich Azure Active Directory za pośrednictwem hello [portalu Azure](https://portal.azure.com/), zgodnie z opisem w [wyświetlanie dzienników inspekcji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Poniżej przedstawiono listę raportów hello uwzględnionych:

| Raporty dotyczące zabezpieczeń  | Raporty dotyczące działań| Raporty dotyczące inspekcji |
| :------------- | :-------------| :-------------|
|Logowania z nieznanych źródeł | Podsumowanie użycia aplikacji | Raport dotyczący inspekcji katalogu |
|Logowania po wielokrotnych niepowodzeniach | Szczegóły użycia aplikacji |   |
|Logowania z wielu lokalizacji geograficznych | Pulpit nawigacyjny aplikacji |  |
|Logowania z adresów IP związanych z podejrzanymi działaniami |Błędy aprowizacji kont |  |
|Nieregularne działania związane z logowaniem |Urządzenia indywidualnych użytkowników |  |
|Logowania z urządzeń, które mogą być zainfekowane |Działania indywidualnych użytkowników |   |
|Nietypowe działania użytkowników związane z logowaniem |Raport dotyczący działań grup |   |
| |Raport dotyczący działań związanych z rejestracją resetowania haseł |   |
| |Działania związane z resetowaniem haseł |   | |



Hello dane z tych raportów mogą być przydatne tooyour aplikacji, takich jak systemów SIEM, inspekcji i narzędzia do analizy biznesowej. Raportowanie Hello Azure AD [interfejsów API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) zapewniają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API. Te interfejsy API można wywołać z różnych języków programowania i narzędzi.

Zdarzenia w hello raport dotyczący usługi Azure AD inspekcji są zachowywane na okres 180 dni.

> [!Note]
> Aby uzyskać więcej informacji na temat przechowywania w raportach, zobacz [zasady przechowywania raportów Active Directory Azure](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Dla klientów do przechowywania ich [zdarzenia inspekcji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) przez dłuższy czas przechowywania, hello interfejsu API raportowania może być zdarzeń inspekcji ściągania tooregularly używanych w magazynie danych.

## <a name="summary"></a>Podsumowanie

Podsumowania tego artykułu, ochrony prywatności i zabezpieczania danych, dostarczając oprogramowania i usług, które ułatwiają zarządzanie hello infrastrukturę IT w Twojej organizacji. Firma Microsoft rozumie, że podczas ich powierzyć ich tooothers danych, tej relacji zaufania wymaga rygorystyczne zabezpieczeń. Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi. Zabezpieczenia i ochrona danych ma najwyższy priorytet w firmie Microsoft.

W tym artykule opisano

-   Jak dane są zbierane, przetwarzane i zabezpieczone w hello Operations Management Suite (OMS).

-   Szybko analizuj zdarzenia w wielu źródłach danych. Identyfikowanie zagrożenia bezpieczeństwa i zrozumieć zakres hello i wpływu na zagrożenia i ataków uszkodzenia hello toomitigate naruszenia zabezpieczeń.

-   Identyfikuj wzorce ataków dzięki wizualizowaniu wychodzącego złośliwego ruchu przez adresy IP i typów zagrożeń spowodowanych złośliwymi działaniami. Dowiedz się, stan zabezpieczeń hello całego środowiska niezależnie od platformy.

-   Przechwyć wszystkie hello dziennika i zdarzenie dane wymagane do inspekcji zabezpieczeń i zgodności. Ukośnika hello czasu i zasobów potrzebnych toosupply inspekcji zabezpieczeń z pełną, wyszukiwanie i można eksportować dziennika i zdarzenie zestawu danych.

<ul>
<li>Zbieranie zdarzeń zabezpieczeń, inspekcji i analizy naruszenia tookeep zamknięcia oczu zasobów:</li>
<ul>
<li>Stan zabezpieczeń</li>
<li>Godne problem</li>
<li>Zagrożenia podsumowania</li>
</ul>
</ul>

## <a name="next-steps"></a>Następne kroki

- [Projektowanie i bezpieczeństwa operacyjnego](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft projektuje jej usług i oprogramowania z zabezpieczeniami w uwadze toohelp zapewnienia jego infrastruktury chmury odporne i obrony, w odniesieniu przed atakami.

- [Operations Management Suite | Bezpieczeństwo i zgodność](https://www.microsoft.com/cloud-platform/security-and-compliance)

Użyj Microsoft zabezpieczeń danych i analiza tooperform bardziej inteligentne i skuteczne wykrywanie zagrożeń.

- [Planowanie Centrum zabezpieczeń Azure i operacje](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) zestaw kroków i zadań, które można wykonać toooptimize korzystanie z Centrum zabezpieczeń oparte na modelu zarządzania chmurą i wymagania dotyczące zabezpieczeń w organizacji.

