---
title: "aaaDNS rozwiązania analizy w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Konfigurowanie i korzystanie z rozwiązania analizy DNS hello w analizy dzienników toogather wgląd w informacje infrastruktura DNS dotyczące zabezpieczeń, wydajności i operacji."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>Zbieranie informacji na temat infrastruktury DNS z hello rozwiązania Podgląd Analytics DNS

![Symbol DNS Analytics](./media/log-analytics-dns/dns-analytics-symbol.png)

W tym artykule opisano, jak tooset się i użyj hello rozwiązania Azure DNS analizy w Azure Log Analytics toogather wgląd w informacje infrastruktura DNS dotyczące zabezpieczeń, wydajności i operacji.

Analiza DNS ułatwia:

- Identyfikować klientów, którzy spróbuj tooresolve złośliwe domen.
- Zidentyfikuj starych rekordów.
- Określ nazwy domen często, którego dotyczy kwerenda i talkative klientów DNS.
- Wyświetl żądania obciążenia na serwerach DNS.
- Widok dynamiczny błędami rejestracji DNS.

rozwiązanie Hello gromadzi, analizuje i skorelowany analityczne DNS z systemem Windows i dzienników inspekcji i inne powiązane dane z serwerów DNS.

## <a name="connected-sources"></a>Połączone źródła

Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie:

| **Źródło połączenia** | **Pomoc techniczna** | **Opis** |
| --- | --- | --- |
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Tak | rozwiązania Hello zbiera informacje DNS z agentów systemu Windows. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje DNS z bezpośredniego agentów systemu Linux. |
| [Grupa zarządzania programu System Center Operations Manager](log-analytics-om-agents.md) | Tak | rozwiązanie Hello zbiera informacje DNS z agentów w podłączonej grupy zarządzania programu Operations Manager. Połączenie bezpośrednie z toohello agenta programu Operations Manager hello Operations Management Suite nie jest wymagane. Dane są przesyłane z hello zarządzania grupy toohello Operations Management Suite repozytorium. |
| [Konto usługi Azure Storage](log-analytics-azure-storage.md) | Nie | Usługa Azure storage nie jest używana przez rozwiązania hello. |

### <a name="data-collection-details"></a>Szczegóły danych kolekcji

rozwiązanie Hello zbiera DNS zapasów i dane dotyczące zdarzeń DNS z serwerów DNS hello zainstalowanym agentem analizy dzienników. Te dane, a następnie przekazać tooLog Analytics i wyświetlić na pulpicie nawigacyjnym rozwiązania hello. Dane dotyczące zapasów, takie jak liczba hello serwerów, stref i rekordów zasobów DNS są zbierane przez uruchomienie polecenia cmdlet programu PowerShell DNS hello. dane Hello są aktualizowane raz na dwa dni. dane dotyczące zdarzeń Hello są zbierane niemal w czasie rzeczywistym z hello [analityczne i dzienniki inspekcji](https://technet.microsoft.com/library/dn800669.aspx#enhanc) zapewniane przez udoskonalone rejestrowanie DNS i Diagnostyka systemu Windows Server 2012 R2.

## <a name="configuration"></a>Konfiguracja

Użyj hello następujące rozwiązania hello tooconfigure informacji:

- Musi mieć [Windows](log-analytics-windows-agents.md) lub [programu Operations Manager](log-analytics-om-agents.md) agenta na każdym serwerze DNS, które mają toomonitor.
- Obszar roboczy usługi Operations Management Suite tooyour hello DNS Analytics rozwiązania można dodać z hello [portalu Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace). Można również użyć hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).

rozwiązanie Hello rozpoczyna zbieranie danych, bez potrzeby hello dalszej konfiguracji. Można jednak użyć powitania po pobraniu danych toocustomize konfiguracji.

### <a name="configure-hello-solution"></a>Konfigurowanie rozwiązania hello

Na pulpicie nawigacyjnym rozwiązania hello, kliknij przycisk **konfiguracji** tooopen hello DNS konfiguracji analizy strony. Istnieją dwa typy zmian konfiguracji, które mogą ułatwić:

- **Nazwy domen białej**. rozwiązanie Hello nie przetwarza wszystkie hello zapytania wyszukiwania. Ta funkcja obsługuje dozwolonych sufiksów nazw domen. Hello zapytań wyszukiwania, które rozpoznawanie nazw domen toohello zgodne sufiksy nazw domen w tym listy dozwolonych adresów IP nie są przetwarzane przez rozwiązanie hello. Nie przetwarza nazwy domen białej pomaga toooptimize hello dane przesyłane tooLog Analytics. domyślne Hello listy dozwolonych adresów IP obejmuje nazw popularnych domeny publicznej, takich jak www.google.com i www.facebook.com. Hello domyślną pełną listę można wyświetlić, przewijając widok.

 Można zmodyfikować tooadd listy hello sufiks nazwy domeny, wszystkie interesujące tooview insights wyszukiwania dla. Można również usunąć wszelkie sufiks nazwy domeny, których nie chcesz tooview wyszukiwania insights dla usługi.

- **Próg talkative klienta**. Klienci DNS, którzy przekracza próg hello na powitania liczba żądań wyszukiwania są wyróżnione na powitania **klientów DNS** bloku. Witaj domyślny próg to 1000. Można edytować hello próg.

    ![Nazwy domen białej](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Pakiety administracyjne

Jeśli używasz obszaru roboczego usługi Operations Management Suite tooyour hello Microsoft Monitoring Agent tooconnect hello następujący pakiet administracyjny jest zainstalowany:

- Pakiet analizy modułu zbierającego dane DNS firmy Microsoft (Microsft.IntelligencePacks.Dns)

Jeśli grupę zarządzania programu Operations Manager jest obszar roboczy usługi Operations Management Suite połączonych tooyour, hello następujące pakiety administracyjne są zainstalowane w programie Operations Manager podczas dodawania tego rozwiązania. Nie jest wymagana konfiguracja ani obsługi tych pakietów administracyjnych:

- Pakiet analizy modułu zbierającego dane DNS firmy Microsoft (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS analizy konfiguracji (Microsoft.IntelligencePack.Dns.Configuration)

Aby uzyskać więcej informacji dotyczących sposobu aktualizowania rozwiązania pakietów administracyjnych, zobacz [tooLog połączenie programu Operations Manager Analytics](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Użyj hello rozwiązania analizy DNS

W tej sekcji opisano wszystkie funkcje pulpitu nawigacyjnego hello i w jaki sposób toouse je.

Po dodaniu obszar roboczy tooyour rozwiązania hello hello kafelka rozwiązania na stronie Operations Management Suite — Przegląd hello zawiera krótkie podsumowanie infrastruktury DNS. Obejmuje on hello liczba serwerów DNS, w których są zbierane dane hello. Obejmuje on też hello liczba żądań wysyłanych przez klientów domeny złośliwe tooresolve w hello ostatnich 24 godzin. Po kliknięciu kafelka hello otwiera hello pulpit nawigacyjny rozwiązania.

![Kafelek DNS Analytics](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Pulpit nawigacyjny rozwiązania

pulpit nawigacyjny rozwiązania Hello zawiera podsumowanie informacji dla hello różnych funkcji hello rozwiązania. Zawiera również linki toohello szczegółowe widoku dla analizy śledczej i diagnostyki. Domyślnie dane hello są wyświetlane dla hello ostatnich siedmiu dni. Zakres dat i godzin hello można zmienić za pomocą hello **formant wyboru daty i godziny**, jak pokazano w powitania po obrazu:

![Formant wyboru godziny](./media/log-analytics-dns/dns-time.png)

pulpit nawigacyjny rozwiązania Hello przedstawia hello następujące karty:

**Zabezpieczenia systemu DNS**. Raporty hello klientów DNS, które próbujesz toocommunicate z domenami złośliwe. Przy użyciu źródła analizy zagrożeń firmy Microsoft, DNS Analytics może wykryć adresów IP, który próbujesz tooaccess domen złośliwego klienta. W wielu przypadkach urządzeń zainfekowanych złośliwym oprogramowaniem "telefonowania" toohello "command and control" center hello domeny złośliwe rozwiązując hello nazwy domeny przed złośliwym oprogramowaniem.

![Blok zabezpieczenia systemu DNS](./media/log-analytics-dns/dns-security-blade.png)

Po kliknięciu IP klienta, na liście hello wyszukiwania dziennika otwiera i zawiera szczegóły wyszukiwania hello hello odpowiednich zapytania. W hello poniższy przykład, DNS Analytics wykrył, że komunikacja hello została wykonana z [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Wyniki wyszukiwania dziennika przedstawiający ircbot](./media/log-analytics-dns/ircbot.png)

informacje Hello pomaga tooidentify:

- Klient IP, który zainicjował hello komunikacji.
- Nazwa domeny jest rozpoznawany jako toohello IP złośliwego.
- Adresy IP, które hello nazwa domeny jest rozpoznawany jako.
- Złośliwe adres IP.
- Ważność problemu hello.
- Przyczyna list dozwolonych hello złośliwego IP.
- Czas wykrycia.

**Zapytanie domen**. Udostępnia hello najczęściej używane nazwy domeny odpytywane przez klientów DNS hello w danym środowisku. Można wyświetlić hello listę wszystkich nazw domen hello dotyczy zapytanie. Możesz również można przejść do szczegółów żądania wyszukiwania hello nazwy domeny określonej w dzienniku wyszukiwania.

![Blok Odpytano domen](./media/log-analytics-dns/domains-queried-blade.png)

**Klienci DNS**. Raporty hello klientów *naruszenie progu hello* liczby zapytań w programie hello wybrany okres czasu. Można wyświetlić listę hello wszystkich klientów DNS hello i szczegóły hello hello zapytania je w dzienniku wyszukiwania.

![Klienci DNS bloku](./media/log-analytics-dns/dns-clients-blade.png)

**Rejestracje dynamicznych DNS**. Raporty nazw błędami rejestracji. Wszystkie błędy rejestracji dla adresu [rekordy zasobów](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (typ A i AAAA) są wyróżniane wraz z powitania klienta adresów IP, który zgłosił hello żądań rejestracji. Tej informacji toofind hello głównej przyczyny awarii rejestracji hello można użyć, wykonując następujące czynności:

1. Znajdź strefy hello, który jest serwerem autorytatywnym dla nazwy hello hello klienta próbuje tooupdate.

2. Użyj hello toocheck hello spisu informacji o rozwiązaniu tej strefy.

3. Sprawdź, czy w tej aktualizacji dynamicznej hello strefy hello jest włączona.

4. Sprawdź, czy strefa hello jest konfigurowana zabezpieczone aktualizacje dynamiczne, czy nie.

    ![Dynamiczne bloku rejestracji DNS](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Nazwa żądania rejestracji**. Górny Kafelek Hello pokazuje linię trendu udane i nieudane żądania dynamicznej aktualizacji DNS. niższe kafelka Hello wymieniono hello pierwszych 10 klientów, którzy wysyłają żądania aktualizacji DNS nie powiodło się toohello serwerów DNS, posortowane według hello liczba błędów.

![Nazwa rejestrowania żądań bloku ](./media/log-analytics-dns/name-reg-req-blade.png)

**Przykładowe zapytania analityczne Interfejsu**. Zawiera listę hello najbardziej typowych kwerend wyszukiwania, które bezpośrednio pobierania danych pierwotnych analytics.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Przykładowe zapytania](./media/log-analytics-dns/queries.png)

Te zapytania można użyć jako punktu wyjścia do tworzenia zapytań niestandardowych raportowania. zapytania Hello łączy strony wyszukiwania dziennika analizy DNS toohello gdzie są wyświetlane wyniki:

- **Lista serwerów DNS**. Przedstawia listę wszystkich serwerów DNS z ich skojarzone nazwy FQDN, nazwy domeny, nazwa lasu i serwera adresów IP.
- **Lista stref DNS**. Przedstawia listę wszystkich stref DNS z nazwy strefy skojarzony hello, stan aktualizacji dynamicznych, serwery nazw i stan podpisania DNSSEC.
- **Rekordy zasobów nieużywane**. Przedstawia listę wszystkich rekordów zasobów nieużywane/nieodświeżona hello. Ta lista zawiera nazwę w rekordzie zasobu hello, typ rekordu zasobu hello skojarzone serwerem DNS, czas generowania rekordów i nazwę strefy. Możesz użyć tej listy tooidentify hello DNS rekordów zasobów, które nie są już w użyciu. Na podstawie tych informacji, można następnie usunąć te wpisy z hello serwerów DNS.
- **Serwery DNS zapytania obciążenia**. Przedstawia informacje, dzięki czemu można uzyskać punktu widzenia hello ładowania DNS na serwerach DNS. Te informacje mogą pomóc w planowaniu pojemności hello hello serwerów. Można przejść toohello **metryki** karcie toochange hello widoku tooa graficznego wizualizacji. Ten widok pomaga zrozumieć sposób hello ładowania DNS jest dystrybuowana do serwerów DNS. Przedstawia on zapytanie DNS trendów szybkości dla każdego serwera.

    ![Wyniki wyszukiwania dziennika zapytań serwerów DNS](./media/log-analytics-dns/dns-servers-query-load.png)

- **Strefy DNS zapytania obciążenia**. Pokazuje hello DNS strefy zapytania na sekundę statystyki wszystkich stref hello na serwerach DNS hello są zarządzane przez rozwiązanie hello. Kliknij przycisk hello **metryki** karcie toochange hello widoku z wizualizacji graficznego tooa szczegółowe dane hello wyników.
- **Zdarzenia konfiguracji**. Pokazuje wszystkie zdarzenia zmiany konfiguracji DNS hello i skojarzonych komunikatów. Następnie możesz filtrować te zdarzenia na podstawie czasu serwera DNS zdarzeń, identyfikator zdarzenia hello, lub kategorii zadań. Witaj danych może pomóc inspekcji serwerów DNS toospecific zmiany wprowadzone w określonym czasie.
- **Dziennik analityczne DNS**. Pokazuje wszystkie zdarzenia analityczne hello na wszystkich serwerach DNS hello są zarządzane przez rozwiązanie hello. Następnie można filtrować te zdarzenia na podstawie czasu serwera DNS hello zdarzeń, identyfikator zdarzenia IP klienta, który zgłosił hello zapytania wyszukiwania i można wyszukiwać w kategorii zadań typu. Zdarzenia analityczne DNS serwera Włącz działania śledzenia na powitania serwera DNS. Analityczne zdarzenie jest rejestrowane za każdym razem hello serwer wysyła lub odbiera informacje dotyczące systemu DNS.

### <a name="search-by-using-dns-analytics-log-search"></a>Wyszukiwanie za pomocą wyszukiwania dziennika analizy DNS

Na stronie dziennik wyszukiwania hello można utworzyć kwerendę. Wyniki wyszukiwania można filtrować za pomocą formantów zestawu reguł. Można też utworzyć tootransform zaawansowanych zapytań, filtrować i raportu na wyniki. Uruchom przy użyciu hello następujące zapytania:

1. W hello **pola zapytania wyszukiwania**, typ `Type=DnsEvents` tooview hello wszystkich DNS zdarzenia generowane przez serwery DNS hello są zarządzane przez rozwiązanie hello. wyniki Hello listy hello dane dziennika dla wszystkich zdarzeń powiązanych toolookup zapytań, dynamicznej rejestracji i zmiany konfiguracji.

    ![DnsEvents dziennik wyszukiwania](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. Wybierz dane dziennika hello tooview zapytań wyszukiwania **LookUpQuery** jako hello **podtypu** filtr z kontroli aspektu hello powitania po lewej stronie. Tabela zawierająca wszystkie zdarzenia zapytania wyszukiwania powitania dla hello wybrany okres czasu jest wyświetlany.

    b. Wybierz dane dziennika hello tooview dla rejestracji dynamicznych **DynamicRegistration** jako hello **podtyp** filtr z kontroli aspektu hello powitania po lewej stronie. Tabela zawierająca wszystkie zdarzenia dynamicznej rejestracji powitania dla hello wybrany okres czasu jest wyświetlany.

    c. dane dziennika hello tooview zmian konfiguracji, wybierz **Zmianakonfiguracji** jako hello **podtypu** filtr z kontroli aspektu hello powitania po lewej stronie. Zostanie wyświetlony tabelę, która zawiera listę wszystkich zdarzeń zmian konfiguracji hello na powitania w wybranym okresie.

2. W hello **pola zapytania wyszukiwania**, typ `Type=DnsInventory` tooview hello wszystkie dane dotyczące zapasów DNS serwerów DNS hello są zarządzane przez rozwiązanie hello. wyniki Hello listy hello dane dziennika dla serwerów DNS strefy DNS i rekordów zasobów.

    ![DnsInventory dziennik wyszukiwania](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Opinia

Istnieją dwa sposoby, które można przesłać opinię:

- **UserVoice**. Opublikuj pomysły dotyczące toowork funkcje DNS Analytics na. Odwiedź hello [strony Operations Management Suite UserVoice](https://aka.ms/dnsanalyticsuservoice).
- **Dołącz do naszych kohorty**. Zawsze możemy interesują Cię o nowych klientów, Dołącz do naszych stado tooget wczesne toonew funkcji dostępu i pomóc nam w ulepszaniu DNS Analytics. Jeśli interesuje Cię w dołączenie naszych stado, wypełnij [szybkie badanie](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Następne kroki

[Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowe DNS rekordów dziennika.
