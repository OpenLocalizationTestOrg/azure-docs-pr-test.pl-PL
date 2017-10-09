---
title: "aaaLog bezpieczeństwo danych Analytics | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu analizy dzienników prywatności i zabezpiecza dane."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Rejestrować analizy danych
Firma Microsoft zatwierdzone tooprotecting prywatności i zabezpieczania danych, podczas dostarczania oprogramowania i usług, które ułatwiają zarządzanie hello infrastrukturę IT w Twojej organizacji. Wiemy, że gdy powierzyć tooothers Twojego danych, tej relacji zaufania wymaga rygorystyczne zabezpieczeń. Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi.

Zabezpieczenia i ochrona danych ma najwyższy priorytet w firmie Microsoft. Skontaktuj się z nami z jakichkolwiek pytań, sugestie lub problemy o następujące informacje, w tym nasze zasady zabezpieczeń na powitania [opcje pomocy technicznej platformy Azure](http://azure.microsoft.com/support/options/).

W tym artykule opisano, jak dane są zbierane, przetwarzane i zabezpieczane przez usługi Analiza dzienników w hello Operations Management Suite (OMS). Można używać usługi web toohello tooconnect agentów, użyć danych operacyjnych toocollect System Center Operations Manager lub pobierania danych z diagnostyki Azure na potrzeby używania przez analizy dzienników. Witaj zebranych danych był wysyłany za pośrednictwem Internetu hello przy użyciu uwierzytelniania opartego na certyfikatach & toohello SSL 3 usługi analizy dzienników, która znajduje się w systemie Microsoft Azure. Dane są kompresowane przez agenta hello przed ich wysłaniem.

Witaj usługi analizy dzienników zarządza danych oparte na chmurze bezpiecznie przy użyciu hello następujące metody:

* Podział danych
* przechowywanie danych
* Zabezpieczenia fizyczne
* Zarządzanie zdarzeniami
* Zgodność
* Certyfikaty standardów zabezpieczeń

## <a name="data-segregation"></a>Podział danych
Dane klienta są przechowywane logicznie oddzielnie dla każdego składnika w całym hello usługę. Wszystkie dane są otagowane informacjami o organizacji. Znakowanie ten będzie nadal występował w całym cyklu życia danych hello i są wymuszane w każdej warstwie hello usługi. Każdy klient ma dedykowany blob systemu Azure, która przechowuje dane długoterminowo hello

## <a name="data-retention"></a>Przechowywanie danych
Indeksowane dziennik wyszukiwania danych są przechowywane i przechowywane zgodnie z tooyour cenową planu. Aby uzyskać więcej informacji, zobacz [cennik analizy dziennika](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft powoduje usunięcie danych klienta 30 dni, po zamknięciu hello obszarem roboczym pakietu OMS. Microsoft spowoduje również usunięcie konta magazynu Azure, gdzie znajdują się dane hello hello. Dane klienta zostanie usunięty, nie ma dysków fizycznych zostaną zniszczone.

Witaj w poniższej tabeli przedstawiono niektóre z dostępnych rozwiązań hello w OMS i przykłady hello typów danych, które pobierają.

| **Rozwiązania** | **Typy danych** |
| --- | --- |
| Ocena konfiguracji |Dane konfiguracji, metadane i dane o stanie |
| Planowanie pojemności |Dane dotyczące wydajności i metadane |
| Oprogramowanie chroniące przed złośliwym kodem |Dane konfiguracji i metadane |
| Ocena aktualizacji systemu |Metadane i stan danych. |
| Zarządzanie dziennikami |Zdefiniowane przez użytkownika dzienniki zdarzeń, dzienniki zdarzeń systemu Windows i/lub dzienniki programu IIS |
| Śledzenie zmian |Spis oprogramowania i metadanych usługi systemu Windows |
| SQL i oceny usługi Active Directory |Wyniki danych usługi WMI, dane rejestru dane dotyczące wydajności i dynamicznego zarządzania programu SQL Server |

Witaj w poniższej tabeli przedstawiono przykłady typów danych:

| **Typ danych** | **Pola** |
| --- | --- |
| Alerty |Alert nazwa, opis alertu, identyfikatorze BaseManagedEntityId, identyfikator problemu, IsMonitorAlert, RuleId, ResolutionState, priorytet, ważność, kategoria, właściciel, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, RepeatCount TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, |
| Konfiguracja |CustomerID, identyfikator agenta, identyfikator jednostki, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Wydarzenie |Identyfikator zdarzenia, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, numer, kategoria, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Uwaga:** podczas pisania zdarzenia za pomocą pola niestandardowe w dzienniku zdarzeń systemu Windows toohello OMS zbiera je. |
| Metadane |Identyfikatorze BaseManagedEntityId, ObjectStatus, jednostka organizacyjna, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, adres IP, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Adres, NetbiosDomainName, LogicalProcessors, DNSName, nazwa wyświetlana, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Wydajność |Nazwa obiektu, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| Stan |StateChangeEventId, StateId, NewHealthState, OldHealthState, kontekstu, TimeGenerated, TimeAdded, StateId2, identyfikatorze BaseManagedEntityId, elementu MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Zabezpieczenia fizyczne
Witaj analizy dzienników w usługę jest obsługiwanego przez personel firmy Microsoft i wszystkich działań są rejestrowane i może być sprawdzona. Usługa Hello całkowicie działa na platformie Azure i jest zgodny z hello Azure wspólne kryteria engineering. Możliwość wyświetlania szczegółów dotyczących zabezpieczeń fizycznych hello zasobów platformy Azure na stronie 18 hello [Przegląd zabezpieczeń systemu Microsoft Azure](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Fizyczny dostęp prawa toosecure obszarów są zmieniane w ciągu jednego dnia roboczego dla każdego, kto nie ma już odpowiedzialność za usługę hello, w tym transfer i kończenie działania. Informacje o hello globalnej infrastruktury fizycznej używamy w [Datacenters Microsoft](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Zarządzanie zdarzeniami
OMS ma procesu zarządzania zdarzeniami, które wszystkich usług firmy Microsoft jest zgodna. toosummarize, firma Microsoft:

* Użyj modelu udostępnionego odpowiedzialność, gdzie część odpowiedzialność zabezpieczeń należy tooMicrosoft i części należy toohello klienta
* Zarządzanie zdarzeniami zabezpieczeń platformy Azure
  * Uruchom postępowania w przypadku wykrycia zdarzenia
  * Oceń wpływ hello i ważność incydentu przez członków zespołu na wywołanie odpowiedzi na zdarzenia. Oparte na dowód, oceny hello może lub nie może powodować dalszych eskalacji toohello odpowiedzi zespołu pracowników ochrony obiektu.
  * Diagnozowanie zdarzenia przez zabezpieczeń odpowiedzi ekspertów tooconduct hello techniczne lub śledczej badania, określenie strategii zawierania, ograniczenia i obejście. Jeśli zespołu zabezpieczeń hello uznaje się, że dane klienta stały się narażonych tooan bezprawnego lub nieautoryzowane poszczególnych, równoległe wykonywanie hello procesu powiadomienie o zdarzeniu klienta rozpocznie się równolegle.  
  * Ustabilizowania i odzyskać hello incydentu. Witaj odpowiedzi na zdarzenia zespołu tworzy problemem hello toomitigate planu odzyskiwania. Kryzysami zawierania kroków, takich jak poddawania wpływ na systemy mogą wystąpić natychmiast i równolegle z diagnostyki. Dłuższy okres środki zaradcze mogą być planowane występujące po upływie hello bezpośrednie ryzyko.  
  * Zamknij zdarzenie hello i przeprowadzanie których post. Hello odpowiedzi na zdarzenia zespołu tworzy post których przedstawiono szczegóły hello hello zdarzenia, z hello zamiar toorevise zasady, procedury i procesy tooprevent cyklu hello zdarzenia.
* Powiadamia klientów o przypadki naruszenia zabezpieczeń
  * Określenie zakresu hello wpływ na klientów i tooprovide, każdy, kto jest w pełni funkcjonalne tak szczegółowe powiadomienia, jak to możliwe
  * Utwórz tooprovide powiadomień klientów z wystarczająco szczegółowe informacje, aby mogli wykonywać dochodzenia ich end i spełnia wszelkie wprowadzone tootheir użytkownicy końcowi podczas nie opóźnienia proces powiadamiania hello zobowiązania.
  * Potwierdź i zadeklarować zdarzenia hello, w razie potrzeby.
  * Powiadamia klientów o zdarzenia powiadomienia niezwłocznie nieuzasadnione i zgodnie z żadnych zobowiązań prawnych lub umownych. Powiadomienia o zdarzenia zabezpieczeń są dostępne w ramach tooone lub jeden z administratorów klienta w jakikolwiek sposób wybiera firmy Microsoft, w tym za pośrednictwem poczty e-mail.
* Należy przeprowadzić gotowości zespołu i szkolenia
  * Personel firmy Microsoft są wymagane toocomplete zabezpieczeń i szkolenia świadomości, co ułatwia ich tooidentify i raportu podejrzane problemy z zabezpieczeniami.  
  * Operatorzy pracuje hello usługi Microsoft Azure mają zobowiązań szkolenia dodanie otaczającego systemów toosensitive dostępu do hostowania danych klienta.
  * Specjalne szkolenia dotyczące ich ról odbierania personel odpowiedź zabezpieczeń firmy Microsoft

Gdy dojdzie do utraty danych klienta, powiadomimy każdego klienta w ciągu jednego dnia. Jednak utraty danych klienta nigdy nie wystąpił błąd związany z usługą OMS. Ponadto firma Microsoft zachowuje kopie danych, który został utworzony i jest geograficznie rozproszonych.

Aby uzyskać więcej informacji na temat sposób odpowiadania przez Microsoft zdarzenia toosecurity, zobacz [Response zabezpieczeń firmy Microsoft Azure w chmurze hello](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Zgodność
Witaj OMS oprogramowania rozwoju i usługi zespołu ochrony informacji i ładu program obsługuje jej wymagania biznesowe i stosuje toolaws i przepisami, zgodnie z opisem w [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) i [Zgodności Centrum zaufania Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Jak OMS ustanawia wymagania dotyczące zabezpieczeń, identyfikuje kontroli zabezpieczeń zarządza i monitoruje ryzyka są także opisane istnieje. Co rok, możemy przeglądu zasady, normy, procedury i wskazówek.

Każdego członka zespołu programowanie OMS odbiera szkolenia formalnego aplikacji w zakresie zabezpieczeń. Wewnętrznie używamy system kontroli wersji dla rozwoju oprogramowania. Każdy projekt oprogramowania jest chroniona przez system kontroli wersji powitania.

Firma Microsoft ma zabezpieczeń i zgodności zespołu nadzoruje i ocenia wszystkich usług firmy Microsoft. Zabezpieczenia informatyków uzupełnić hello zespołu i nie są one powiązane z hello inżynierii działów, które opracowanie OMS. Witaj zabezpieczeń ma swoje własne łańcuch zarządzania i przeprowadzenie oceny niezależnych produktów i usług tooensure zabezpieczeń i zgodności.

Zarząd firmy Microsoft jest powiadamiany o coroczny raport o wszystkie programy zabezpieczeń informacji w firmie Microsoft.

Witaj OMS oprogramowania rozwoju i usługi team aktywnie współpracuje z hello Legal firmy Microsoft i zgodność zespołów i innych tooacquire partnerów branży różne certyfikaty.

## <a name="certifications-and-attestations"></a>Certyfikaty i poświadczenia
Analiza dzienników OMS hello spełnia następujące wymagania:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Płatności karty Industry (PCI zgodne) Data Security Standard (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) przez Radę standardów zabezpieczeń PCI hello.
* [Typ usługi organizacji formantów (SOC) 1 1 i SOC 2 typu 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2) zgodne
* [HIPAA i HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) dla firm, które ma umowy skojarzyć HIPAA biznesowe
* Wspólne kryteria Engineering systemu Windows
* Wiarygodne technologie komputerowe firmy Microsoft (witryna może być w języku angielskim)
* Jako usługi Azure hello składników, które korzysta z pakietu OMS spełniać wymagania zgodności tooAzure. Więcej w [zgodności Centrum zaufania Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> W niektórych certyfikaty/poświadczenia, analizy dzienników jest wyświetlana w obszarze jego poprzednią nazwę *usługi Operational Insights*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Chmura obliczeniowa zabezpieczeń przepływu danych
Hello Poniższy diagram przedstawia architekturę zabezpieczeń chmury jako hello przepływ informacji w firmie i jak jest zabezpieczony, ponieważ jest przeniesienie usługi analizy dzienników toohello, ostatecznie odebrane przez użytkownika w portalu OMS hello. Więcej informacji na temat każdego kroku następuje hello diagramu.

![Obraz OMS zbierania danych i zabezpieczeń](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Zarejestruj się, aby zbieranie danych i analizy dzienników
Dla Twojej organizacji toosend danych tooLog Analytics możesz skonfigurować agentów systemu Windows, uruchomionych na maszynach wirtualnych platformy Azure lub OMS agentów dla systemu Linux. Jeśli używasz agenty programu Operations Manager, a następnie użyj Kreatora konfiguracji w tooconfigure konsoli operacje hello je. Użytkownicy (które mogą być, inne poszczególnych użytkowników lub grupy osób) Utwórz co najmniej jednego konta OMS (OMS obszarów roboczych) i zarejestrować agentów przy użyciu jednej z następujących kont hello:

* [Identyfikator organizacji](../active-directory/sign-up-organization.md)
* [Konto Microsoft - Outlook pakietu Office na żywo, MSN](http://www.microsoft.com/account/default.aspx)

Obszar roboczy OMS jest gdzie dane są zbierane, zagregowane, poddane analizie i przedstawiony. Obszar roboczy przede wszystkim jest używany jako dane toopartition oznacza i każdego obszaru roboczego jest unikatowa. Na przykład można toohave danych produkcyjnych zarządzanych za pomocą jednego obszarem roboczym pakietu OMS i badanie danych zarządzanych za pomocą innego obszaru roboczego. Obszary robocze zmniejszają również dane kontroli toohello dostępu użytkownika administrator. Każdy obszar roboczy może mieć wiele kont użytkowników skojarzonych z nim, a wszystkie konta użytkowników mogą uzyskiwać dostęp do wielu obszarów roboczych OMS. Możesz utworzyć obszarów roboczych na podstawie regionu centrum danych. Każdy obszar roboczy jest centrów danych replikowanych tooother w regionie hello, przede wszystkim dotyczące dostępności usług OMS.

Po ukończeniu pracy Kreatora konfiguracji hello, każdej grupie zarządzania programu Operations Manager dla programu Operations Manager, ustanawia połączenie z hello usługi analizy dzienników. Następnie należy użyć hello toochoose Kreatora dodawania komputerów, które komputery w grupie zarządzania hello mogą toosend danych toohello usługi. Dla innych typów agenta każda łączy bezpiecznie toohello usługę.

Cała komunikacja między połączonych systemów i hello usługi analizy dzienników jest zaszyfrowany.  Witaj TLS protokołu (HTTPS) jest używany do szyfrowania.  proces Microsoft SDL Hello nastąpią tooensure analizy dzienników jest aktualny i hello najnowsze osiągnięcia w protokołów kryptograficznych.

Każdy typ agenta zbiera dane analizy dziennika. Hello typu zbieranych danych jest zależy od typów hello rozwiązań używane. Wyświetlane podsumowanie zbierania danych w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Ponadto bardziej szczegółowe informacje o kolekcji jest dostępna w przypadku większości rozwiązań. Rozwiązanie to pakiet wstępnie zdefiniowanych widoków, zapytania wyszukiwania dziennika zasady zbierania danych i przetwarzania logiki. Tylko administratorzy mogą używać tooimport analizy dzienników rozwiązania. Po zaimportowaniu rozwiązania hello jest przeniesionego toohello serwerów zarządzania programu Operations Manager (jeśli jest używany), a następnie tooany agentów, które wybrano. W efekcie agentów hello zbieranie danych hello.

## <a name="2-send-data-from-agents"></a>2. Wysyłanie danych z agentów
Zarejestruj wszystkie typy agenta przy użyciu klucza rejestracji i jest ustanowić bezpiecznego połączenia między agentem hello a hello usługi analizy dzienników przy użyciu uwierzytelniania opartego na certyfikatach oraz protokołu SSL z portem 443. OMS używa toogenerate tajny magazynu i Obsługa kluczy. Klucze prywatne są obracane co 90 dni i są przechowywane na platformie Azure i są zarządzane przez hello Azure operacje, którzy postępuj zgodnie z ograniczeniami praktyk przepisami i zgodności.

Z programem Operations Manager należy zarejestrować obszaru roboczego z usługą analizy dzienników hello i jest ustanowić bezpiecznego połączenia HTTPS między serwerem zarządzania programu Operations Manager hello.

W przypadku agentów z systemem Windows uruchomionych na maszynach wirtualnych platformy Azure klucz magazynu tylko do odczytu jest zdarzeń diagnostycznych tooread używane w tabelach platformy Azure.

Każdy agent w przypadku usługi toohello toocommunicate jakiejkolwiek przyczyny, hello zbierane dane są przechowywane lokalnie w pamięci podręcznej tymczasowego i hello serwer zarządzania próbuje tooresend hello danych co osiem minut przez 2 godziny. Hello agenta buforowane dane są chronione przez system operacyjny hello magazynu poświadczeń. Jeśli usługa hello nie może przetworzyć danych powitania po dwóch godzinach, hello agentów może umieścić w kolejce hello danych. Jeśli zapełnienia kolejki hello OMS uruchamia porzucenie typy danych, począwszy od danych dotyczących wydajności. limit kolejki agenta Hello jest klucz rejestru, można modyfikować, jeśli to konieczne. Zebrane dane jest skompresowany i wysyłane do usługi toohello, pomijanie lokalnych baz danych, więc nie dodaje żadnych toothem obciążenia. Po zebraniu hello dane są wysyłane, zostanie ono usunięte z pamięci podręcznej hello.

Jak opisano powyżej, dane z agentów są wysyłane za pośrednictwem protokołu SSL tooMicrosoft centrach danych platformy Azure. Opcjonalnie można użyć dodatkowych zabezpieczeń tooprovide ExpressRoute hello danych. ExpressRoute jest toodirectly sposób łączenia tooAzure z istniejącej sieci WAN, takich jak wiele protokołów etykietę przełączania sieci VPN (MPLS), pochodzącymi z dostawcą usługi sieciowej. Aby uzyskać więcej informacji, zobacz [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. hello usługi analizy dzienników odbiera i przetwarza dane
Hello usługi Log Analytics zapewnia, że dane przychodzące jest z zaufanego źródła, weryfikując certyfikaty i hello integralności danych za pomocą uwierzytelniania systemu Azure. Witaj nieprzetworzonych danych pierwotnych jest następnie przechowywane jako obiekt blob w [magazyn Microsoft Azure](../storage/common/storage-introduction.md) i nie jest zaszyfrowany. Jednak każdy obiekt blob magazynu Azure ma zestaw unikatowego zestawu kluczy, który jest dostępny tylko toothat użytkownika. Typ Hello danych przechowywanych zależy od typów hello rozwiązań, które zostały zaimportowane i używać toocollect danych. Usługi analizy dzienników hello przetwarza hello danych pierwotnych dla obiektu blob magazynu Azure hello.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Użyj danych hello tooaccess analizy dzienników
TooLog Analytics w portalu OMS hello można zalogować się za pomocą konta organizacyjnego hello lub konta Microsoft, które należy wcześniej skonfigurować. Cały ruch między portalu OMS hello i analizy dzienników w OMS są wysyłane za pośrednictwem bezpiecznego kanału HTTPS. Za pomocą portalu OMS hello, identyfikator sesji jest generowany na powitania klienta użytkownika (przeglądarki sieci web), a dane są przechowywane w lokalnej pamięci podręcznej, dopóki hello sesja została przerwana. Gdy zakończony, pamięć podręczna hello zostanie usunięta. Pliki cookie po stronie klienta, które nie zawierają informacji umożliwiających identyfikację użytkownika, nie są automatycznie usuwane. Pliki cookie dotyczące sesji są oznaczane HTTPOnly i są zabezpieczone. Po upływie wstępnie określoną bezczynności sesji portalu OMS hello zostało przerwane.

Za pomocą portalu OMS hello, możesz wyeksportować plik CSV tooa danych i może uzyskać dostępu do danych przy użyciu interfejsy API wyszukiwania. Eksport CSV jest ograniczona too50, 000 wierszy na eksportu i danych interfejsu API jest ograniczony too5, 000 wierszy na wyszukiwania.

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do analizy dzienników](log-analytics-get-started.md) toolearn więcej informacji na temat analizy dzienników i get do pracy w minutach.
