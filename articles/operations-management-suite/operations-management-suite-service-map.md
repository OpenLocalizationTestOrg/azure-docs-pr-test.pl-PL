---
title: "Witaj aaaUse rozwiązania mapy usługi Operations Management Suite | Dokumentacja firmy Microsoft"
description: "Mapa usługi jest rozwiązaniem Operations Management Suite, który automatycznie odnajduje składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami. Ten artykuł zawiera szczegółowe informacje dotyczące wdrażania mapy usługi w danym środowisku i korzystania z niego w różnych scenariuszach."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Użyj rozwiązania mapy usługi hello w Operations Management Suite
Mapy usług automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapy hello komunikacji między usługami. Z mapy usługi można przeglądać serwery w sposób hello uważasz, że ich: jako połączonych systemy, które dostarczają usług krytycznych. Mapa usługi pokazuje połączeń między serwerami, procesów i portów w dowolnej architekturze połączenia TCP z innych niż wymagana żadna konfiguracja hello instalacji agenta.

W tym artykule opisano szczegóły hello przy użyciu mapy usługi. Informacje o konfigurowaniu mapy usługi i dołączania agentów, zobacz [rozwiązania Konfigurowanie mapy usługi Operations Management Suite](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Przypadki użycia: należy go przetwarza pamiętać zależności

### <a name="discovery"></a>Odnajdywania
Mapy usług automatycznie tworzy wspólnej mapę zależności odwołania na serwery, procesów i usług innych firm. Odnajduje, a mapuje wszystkie zależności TCP niespodziewanego połączeń, systemów zdalnych innych firm, które zależą od oraz zależności tootraditional ciemny obszarów sieci, takie jak Active Directory. Mapa usług odnajduje połączenia sieciowe nie powiodło się, że zarządzanych systemach próbujesz toomake, pomaga w identyfikacji potencjalnych konfiguracji serwera, awaria usługi i problemy z siecią.

### <a name="incident-management"></a>Zarządzanie zdarzeniami
Mapy usług pozwala wyeliminować czynności hello izolacji problem przedstawiające, jak połączenia systemów i wpływu na siebie. Ponadto tooidentifying nie powiodło się połączeń, pomaga zidentyfikować równoważenia obciążenia nieprawidłowo, zaskakująco lub zbyt duże obciążenie usług krytycznych i nieautoryzowane klientów, takich jak rozmowa systemów tooproduction komputerach deweloperów. Przy użyciu zintegrowanego przepływy pracy z Operations Management Suite zmienić śledzenia, można również sprawdzić, czy zdarzenie zmiany na maszynie zaplecza lub usługi wyjaśniono hello głównej przyczyny zdarzenia.

### <a name="migration-assurance"></a>Zapewnienie migracji
Przy użyciu mapy usługi, można efektywnie planowania, przyspieszanie i zweryfikować Azure migracji, które pomaga zapewnić, że nic pozostawione i nie występują awarie niespodziewanego. Może odnajdywać tego toomigrate potrzeby współzależne wszystkie systemy ze sobą, oceny konfiguracji systemu i pojemności, a ustalić, czy na komputerze z uruchomionym systemem nadal działa jako użytkowników lub kwalifikuje się do likwidacji zamiast migracji. Po zakończeniu przenoszenia hello można sprawdzić na tooverify obciążenia i tożsamości klienta, które systemy testowe i Klienci nawiązują połączenie. Jeśli definicje planowania i zapory podsieci problemy, połączenia nie powiodło się w społeczności maps mapy usługi punktu toohello systemów, które wymagają łączności.

### <a name="business-continuity"></a>Ciągłość działalności biznesowej
Jeśli używasz usługi Azure Site Recovery i musi pomocy Definiowanie hello odzyskiwania sekwencji dla środowiska aplikacji mapy usług, można automatycznie stwierdzić, jak systemy opierają się na siebie tooensure, że plan odzyskiwania jest niezawodne. Wybierając krytyczne serwera lub grupy i wyświetlanie jej klientów, należy zidentyfikować toorecover systemów frontonu, które po powitania serwera został przywrócony i jest dostępny. Z drugiej strony analizując krytyczne serwerów zaplecza zależności można zidentyfikować toorecover systemów, które przed systemów fokus zostaną przywrócone.

### <a name="patch-management"></a>Zarządzanie poprawkami
Mapy usług podnosi poziom użytkowania hello oceny aktualizacji systemu Operations Management Suite, pokazujące, które innych zespołów i serwery są zależne od usługi, więc można powiadomić je z wyprzedzeniem przed wyłączyć przez systemy w celu wdrożenia poprawki. Mapy usług zwiększa również poprawki zarządzania w programie Operations Management Suite poprzez wyświetlenie, czy usługi są dostępne i poprawnie połączone po zostaną poprawiono i ponownie uruchomione.


## <a name="mapping-overview"></a>Mapowanie — omówienie
Agenci mapy usługi zebrać informacje dotyczące wszystkich procesów połączenia TCP na serwerze hello, gdzie są one zainstalowane, a szczegóły hello połączeń przychodzących i wychodzących dla każdego procesu. Na liście hello w okienku po lewej stronie powitania możesz wybrać maszyny lub grupy, które mają ich zależności mapy usług agentów toovisualize za pośrednictwem określonego przedziału czasu. Zależności maszyny mapuje fokus na określonym komputerze i przedstawiają wszystkie maszyny hello, które są bezpośrednio TCP klientów lub serwerów tej maszynie.  Mapowanie grup maszyny Pokaż zestawy serwerów oraz ich zależności.

![Omówienie mapy usług](media/oms-service-map/service-map-overview.png)

Maszyny można skalować w hello tooshow mapy hello uruchomionego procesu za pomocą aktywnych połączeń sieciowych w zakresie czasu hello wybrane. Gdy komputer zdalny przy użyciu mapy usługi agenta jest rozwinięty tooshow szczegóły procesu, wyświetlane są tylko procesy, które komunikują się z maszyną fokus hello. po lewej stronie powitania hello procesów, które łączą się z określonej liczby Hello bez wykorzystania agentów maszyn frontonu, które łączą się hello fokus maszyny. Jeśli maszyna fokus hello jest połączenie tooa maszyny zaplecza, w której nie ma agenta, serwera zaplecza hello znajduje się w grupie Port serwera, wraz z innymi toohello połączeń sam numer portu.

Domyślnie mapy usługi mapuje hello Pokaż ostatnich 30 minut informacji o zależnościach. Za pomocą formantów czasu hello w lewym górnym rogu hello, można zbadać mapy dla zakresów historycznego się jak wyszukiwanego zależności w hello tooshow godzina tooone przeszłości (na przykład podczas zdarzenia lub zanim nastąpiła zmiana). Dane mapy usługi są przechowywane przez 30 dni roboczych płatną i 7 dni w bezpłatnych obszarów roboczych.

## <a name="status-badges-and-border-coloring"></a>Identyfikatory stanu i kolorowanie obramowania
Na powitania dołu każdego serwera w mapie hello można listę identyfikatory stan przekazywania informacji o stanie dotyczące powitania serwera. identyfikatory Hello oznacza, że niektóre istotne informacje dotyczące serwera hello z jednego z hello Operations Management Suite rozwiązania integracji. Klikając pozycję wskaźnika przejście bezpośrednio toohello Szczegóły stanu hello w okienku po prawej stronie powitania. Witaj stan dostępne identyfikatory zawierają alerty, działu, zmiany, zabezpieczeń i aktualizacje.

W zależności od ważności hello hello stan identyfikatory obramowanie węzła maszyny mogą być kolorowe czerwony (krytyczna), żółty (ostrzeżenie) lub niebieski (informacyjny). kolor Hello reprezentuje hello najpoważniejsze stan dowolnego hello identyfikatory stanu. Szare obramowanie wskazuje węzła, który ma wskaźników stanu.

![Identyfikatory stanu](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Grupy na komputerze
Grupy na komputerze Zezwalaj możesz toosee mapy skupia się wokół zestaw serwerów, nie tylko jedną pozwala zobaczyć, wszyscy członkowie hello wielowarstwowych aplikacji lub serwera klastra w jedną mapę.

Użytkownicy wybierają serwerów, które należą do grupy ze sobą i wybierz nazwę grupy hello.  Można następnie wybierz grupę hello tooview ze wszystkimi połączenia i procesy lub go wyświetlać tylko procesy hello i połączeń, które dotyczą bezpośrednio toohello innych członków grupy hello.

![Grupy na komputerze](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Tworzenie grupy na komputerze
toocreate grupę, wybierz hello maszyny lub maszyn ma w hello maszyny na liście, a następnie kliknij przycisk **dodać toogroup**.

![Tworzenie grupy](media/oms-service-map/machine-groups-create.png)

Istnieje, można wybrać **Utwórz nowy** i nadaj nazwę grupie hello.

![Nazwa grupy](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Grupy na komputerze są obecnie ograniczone too10 serwerów, ale planujemy tooincrease ten limit wkrótce.

### <a name="viewing-a-group"></a>Wyświetlanie grupy
Po utworzeniu niektórych grup, można je wyświetlić, wybierając kartę grupy hello.

![Karta grup](media/oms-service-map/machine-groups-tab.png)

Następnie wybierz hello grupy nazwa tooview hello mapy dla tej grupy na komputerze.
![Grupy na komputerze](media/oms-service-map/machine-group.png) hello maszyny, które należą do grupy toohello zostały opisane w białych hello mapy.

Powiększające hello grupa będzie zawierała listę hello maszyny, które tworzą hello grupy na komputerze.

![Grupy na komputerze maszyny](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filtruj według procesów
Możesz Przełącz do widoku mapy hello między przedstawiający wszystkich procesów i połączeń w hello grupy i tylko te, które dotyczą bezpośrednio toohello grupy na komputerze hello.  Witaj widok domyślny jest tooshow wszystkich procesów.  Widok hello można zmienić, klikając ikonę filtra hello powyżej hello mapy.

![Grupy filtru](media/oms-service-map/machine-groups-filter.png)

Gdy **wszystkie procesy** jest zaznaczone, mapy hello uwzględni wszystkie procesy i połączeń na wszystkich maszynach hello w hello grupy.

![Przetwarza wszystkie grupy na komputerze](media/oms-service-map/machine-groups-all.png)

Jeśli zmienisz hello widoku tylko tooshow **podłączone grupy procesów**, mapy hello będzie zawężony dół tooonly tych procesów i połączeń, które są bezpośrednio połączone maszyny tooother w grupie hello, tworzenie uproszczony widok.

![Procesy filtrowane grupy na komputerze](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Dodawanie grupy tooa maszyny
tooadd maszyny tooan istniejącą grupę, należy sprawdzić hello pola dalej toohello maszyny, a następnie kliknij przycisk **dodać toogroup**.  Następnie wybierz hello żądanej tooadd hello maszyny do grupy.
 
### <a name="removing-machines-from-a-group"></a>Usuwanie urządzenia z grupy
W hello listy grupy rozwiń węzeł hello grupy nazwa toolist hello maszyn w hello grupy na komputerze.  Następnie kliknij przycisk hello wielokropka menu dalej toohello maszyny mają tooremove i wybierz polecenie **Usuń**.

![Usuń maszynę z grupy](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Usuwanie lub zmiana nazwy grupy
Polecenie hello wielokropka menu dalej toohello Nazwa grupy w hello listy grup.

![Maszyna grupy menu](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Ikony ról
Niektóre procesy obsługi ról określonego na maszynach: serwery sieci web, serwerów aplikacji, bazy danych i tak dalej. Mapy usługi oznacza procesu i pola maszyny z roli ikony toohelp zidentyfikować na pierwszy rzut oka hello roli procesu lub serwera odtwarzania.

| Ikona roli | Opis |
|:--|:--|
| ![Serwer sieci Web](media/oms-service-map/role-web-server.png) | Serwer sieci Web |
| ![Serwer aplikacji](media/oms-service-map/role-application-server.png) | Serwer aplikacji |
| ![Serwer bazy danych](media/oms-service-map/role-database.png) | Serwer bazy danych |
| ![Serwer LDAP](media/oms-service-map/role-ldap.png) | Serwer LDAP |
| ![Serwer protokołu SMB](media/oms-service-map/role-smb.png) | Serwer protokołu SMB |

![Ikony ról](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Połączenia nie powiodło się
Nie powiodło się połączeń są wyświetlane w mapy usługi mapuje procesami i komputerami, linia przerywana red wskazujący, że system klienta kończy się niepowodzeniem tooreach procesu lub portu. Nieudane połączenia są zgłaszane z dowolnego systemu z wdrożonym agentem mapy usług w przypadku tego systemu hello jedno próby hello nie powiodło się połączenie. Mapy usług mierzy ten proces obserwując gniazda TCP, które nie są tooestablish połączenia. Ten błąd może wystąpić z zapory, błąd konfiguracji powitania klienta lub serwera, lub zdalnej usługi jest niedostępny.

![Połączenia nie powiodło się](media/oms-service-map/failed-connections.png)

Opis połączenia nie powiodło się może pomóc w rozwiązywaniu problemów, weryfikacji migracji, analizowania zabezpieczeń i zrozumienia ogólnej architektury. Czasami jest bezpieczna połączenia nie powiodło się, ale często wskazywały bezpośrednio problem tooa, takich jak środowisko trybu failover, nagle staje się niedostępny lub dwie warstwy aplikacji jest tootalk po migracji chmury.

## <a name="client-groups"></a>Grup klientów
Grup klienta są pola na mapie hello, które reprezentują komputery klienckie, które nie mają zależności agentów. Pojedynczej grupy klientów reprezentuje hello klientów dla poszczególnych procesu lub komputera.

![Grup klientów](media/oms-service-map/client-groups.png)

adresy IP hello toosee hello serwerów z grupy klientów, wybierz hello grupy. zawartość Hello grupy hello są wymienione w hello **właściwości grupy klienta** okienka.

![Właściwości grupy klientów](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Port serwera grup
Port serwera grupy są pola, które reprezentują portów na serwerach, które nie mają zależności agentów. pole Hello zawiera hello port serwera oraz liczbę hello liczby serwerów z portem toothat połączenia. Rozwiń hello pole toosee hello poszczególnych serwerów i połączeń. Jeśli istnieje tylko jeden serwer w polu hello, wyświetlana jest hello nazwę lub adres IP.

![Port serwera grup](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Menu Kontekst
Kliknięcie przycisku hello wielokropek (...) u góry hello prawo dowolnego serwera Wyświetla hello menu kontekstowego dla tego serwera.

![Połączenia nie powiodło się](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Obciążenia serwera mapy
Kliknięcie przycisku **obciążenia serwera mapy** przejście tooa nowej mapy z wybranego serwera hello jako nową maszynę fokus hello.

### <a name="show-self-links"></a>Pokaż linki do samego siebie
Kliknięcie przycisku **Pokaż Self-Links** węzła serwera hello ponownie rysuje wraz ze wszystkimi linki do samego siebie, które są połączeń TCP, które rozpoczęcia i zakończenia procesów w ramach powitania serwera. Jeśli linki do samego siebie są wyświetlane, hello zmiany polecenia menu za**Ukryj Self-Links**, dzięki czemu można je wyłączyć.

## <a name="computer-summary"></a>Podsumowanie komputera
Witaj **podsumowanie maszyny** okienko zawiera przegląd systemu operacyjnego serwera, liczby zależności i danych z innych rozwiązań pakietu Operations Management Suite. Dane te obejmują metryki wydajności, bilety usług technicznej śledzenia zmian, zabezpieczeń i aktualizacje.

![Okienko Podsumowanie maszyny](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Właściwości komputera i procesu
Po przejściu mapy mapy usług, możesz wybrać maszyn i procesy dodatkowy kontekst toogain dotyczące ich właściwości. Maszyny zawierają informacje dotyczące DNS nazwy, adresów IPv4, procesora CPU i pamięci, pojemności, typu maszyny Wirtualnej, systemu operacyjnego i wersji, ostatniego ponownego rozruchu czas i identyfikatory hello ich agentów Operations Management Suite i mapy usługi.

![W okienku właściwości maszyny](media/oms-service-map/machine-properties.png)

Szczegóły procesu można zbierać z metadanych systemu operacyjnego dotyczące uruchamiania procesów, w tym nazwę procesu, opis procesu, nazwę użytkownika i domeny (w systemie Windows), nazwę firmy, nazwa produktu, wersja produktu, katalog roboczy, wiersza polecenia i procesu Godzina rozpoczęcia.

![W okienku właściwości procesu](media/oms-service-map/process-properties.png)

Witaj **podsumowanie procesu** okienko udostępnia dodatkowe informacje o łączności hello procesu, takie jak jego powiązanych portów, połączeń przychodzących i wychodzących i nie powiodło się połączenia.

![Okienko Podsumowanie procesu](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Integracji programu Operations Management Suite alertów
Mapy usług integruje się z alertami tooshow uruchamiany Operations Management Suite alerty dla wybranego serwera hello w zakresie czasu hello wybrane. powitania serwera Wyświetla ikonę, jeśli są aktualne alerty i hello **alerty maszyny** w okienku wyświetlana lista alertów hello.

![W okienku alertów maszyny](media/oms-service-map/machine-alerts.png)

tooenable mapy usługi toodisplay powiązanych alertów, Utwórz regułę alertu dla określonego komputera. toocreate odpowiednie alerty:
- Dołącz toogroup klauzuli komputera (na przykład **komputera interwał 1 minuta**).
- Wybierz tooalert w oparciu metryki pomiaru.

![Konfiguracja alertów](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Integracji programu Operations Management Suite dziennika zdarzeń
Mapy usług integruje się z tooshow wyszukiwania dziennika liczbę wszystkie zdarzenia dziennika dostępne dla wybranego serwera hello podczas hello wybrany zakres czasu. Można kliknąć każdy wiersz na liście hello tooLog toojump liczby zdarzeń wyszukiwania i zobacz hello osobny dziennik zdarzeń.

![Okienko dziennika zdarzeń maszyny](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Integracji programu Operations Management Suite działu
Mapa usług integracji z hello łącznika zarządzania usługi IT odbywa się automatycznie, gdy oba rozwiązania są włączone i skonfigurowane w obszarze roboczym usługi Operations Management Suite. Witaj integracji mapy usługi etykietą "Działu". Aby uzyskać więcej informacji, zobacz [centralnie zarządzać zarządzanie usługami IT — elementów roboczych za pomocą łącznika zarządzania usługi IT](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Witaj **działu maszyny** okienko Wyświetla listę wszystkich zdarzeń zarządzania usługami INFORMATYCZNYMI dla wybranego serwera hello w zakresie czasu hello wybrane. powitania serwera Wyświetla ikonę, jeśli bieżący elementów i wyświetlane okienku maszyny działu hello.

![Okienko działu maszyny](media/oms-service-map/service-desk.png)

Kliknij element hello tooopen w rozwiązaniu Zarządzanie usługami IT — połączonych **elementu roboczego widoku**.

Kliknij przycisk Szczegóły hello tooview elementu hello wyszukiwania dziennika **Pokaż dziennik wyszukiwania**.


## <a name="operations-management-suite-change-tracking-integration"></a>Integracja śledzenia zmian pakiet zarządzania Operations
Mapa usług integracji z śledzenia zmian odbywa się automatycznie, gdy oba rozwiązania są włączone i skonfigurowane w obszarze roboczym usługi Operations Management Suite.

Witaj **śledzenia zmian maszyny** okienku są wyświetlane wszystkie zmiany z najnowszych hello najpierw, wraz z toodrill łącza, dół tooLog wyszukiwania, aby uzyskać dodatkowe szczegóły.

![Okienko śledzenia zmian maszyny](media/oms-service-map/change-tracking.png)

Witaj poniższy obraz jest szczegółowy widok zdarzenie Zmianakonfiguracji, które można napotkać po wybraniu **Pokaż w analizy dzienników**.

![Zmianakonfiguracji zdarzeń](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Integracji programu Operations Management Suite wydajności
Witaj **wydajność maszyny** okienko przedstawia metryki wydajności standardowe hello wybranego serwera. Witaj metryki obejmują wykorzystania Procesora, wykorzystanie pamięci, sieci bajtów wysłanych i odebranych i listę najważniejszych procesów hello sieci bajtów wysłanych i odebranych. tooget hello sieci dane dotyczące wydajności, należy również włączono hello rozwiązania podczas transmisji danych 2.0 w Operations Management Suite.

![Okienko wyników maszyny](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Integracji programu Operations Management Suite zabezpieczeń
Mapy usług integracji z zabezpieczeniami i inspekcji odbywa się automatycznie, gdy oba rozwiązania są włączone i skonfigurowane w obszarze roboczym usługi Operations Management Suite.

Witaj **zabezpieczeń maszyny** w okienku zostaną wyświetlone dane z hello rozwiązania Operations Management Suite zabezpieczeń i inspekcji dla hello wybranego serwera. Okienko Hello zawiera podsumowanie oczekujących bezpieczeństwo serwera hello podczas hello wybrany zakres czasu. Kliknięcie dowolnej ćwiczeń problemy zabezpieczeń hello w dół do wyszukiwania dziennika, aby uzyskać szczegółowe informacje o nich.

![Okienko zabezpieczeń komputera](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Integracji programu Operations Management Suite aktualizacje
Mapa usług integracji z zarządzania aktualizacjami odbywa się automatycznie, gdy oba rozwiązania są włączone i skonfigurowane w obszarze roboczym usługi Operations Management Suite.

Witaj **Machine aktualizacje** okienku są wyświetlane dane z hello rozwiązania zarządzania programu Operations Management Suite aktualizacji dla wybranego serwera hello. Okienko Hello zawiera podsumowanie dowolnych brakujących aktualizacji dla serwera hello podczas hello wybrany zakres czasu.

![Okienko śledzenia zmian maszyny](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Dane spisu komputera i procesu mapy usługi są dostępne dla [wyszukiwania](../log-analytics/log-analytics-log-searches.md) w analizy dzienników. Można zastosować tego tooscenarios danych, która zawiera planowania migracji, analizy pojemności, odnajdywania i rozwiązywanie problemów z wydajnością na żądanie.

Jeden rekord jest generowany na godzinę dla każdego komputera unikatowy i procesu, ponadto toohello rekordów, które są generowane, gdy proces lub komputer uruchamia lub jest na dodawanej tooService mapy. Te rekordy mają właściwości hello w hello następujące tabele. Witaj pól i wartości w zdarzeniach ServiceMapComputer_CL hello mapy toofields hello zasobu maszyny w hello interfejs API Menedżera zasobów Azure ServiceMap. Witaj pól i wartości w zdarzeniach ServiceMapProcess_CL hello mapować toohello pola hello procesu zasobu w hello interfejs API Menedżera zasobów Azure ServiceMap. pole ResourceName_s Hello zgodne pola Nazwa hello hello odpowiadający jej zasób usługi Resource Manager. 

>[!NOTE]
>Wzrostem funkcje mapy usługi te pola są toochange podmiotu.

Nie ma właściwości wewnętrznie generowane służy tooidentify procesy unikatowy i komputerami:

- Komputer: Użyj ResourceId lub ResourceName_s toouniquely zidentyfikować komputer w obszarem roboczym usługi Operations Management Suite.
- Proces: Toouniquely ResourceId Użyj Zidentyfikuj proces roboczy usługi Operations Management Suite. ResourceName_s jest unikatowy w ramach kontekstu hello hello maszyny, na których hello proces działa (MachineResourceName_s) 

Ponieważ wiele rekordów może istnieć dla określonego procesu i komputera w określonym okresie, zapytania mogą zwracać więcej niż jeden rekord dla hello tym samym komputerze lub proces. tooinclude hello tylko ostatniego rekordu, Dodaj "| Zapytanie toohello deduplikacji ResourceId".

### <a name="servicemapcomputercl-records"></a>Rejestruje ServiceMapComputer_CL
Rekordy z typem *ServiceMapComputer_CL* dane spisu dla serwerów z agentami mapy usługi. Te rekordy zawierają właściwości hello hello w poniższej tabeli:

| Właściwość | Opis |
|:--|:--|
| Typ | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| Identyfikator zasobu | unikalny identyfikator maszyny w obszarze roboczym hello Hello |
| ResourceName_s | unikalny identyfikator maszyny w obszarze roboczym hello Hello |
| ComputerName_s | komputer Hello FQDN |
| Ipv4Addresses_s | Lista adresów IPv4 powitania serwera |
| Ipv6Addresses_s | Lista adresów IPv6 powitania serwera |
| DnsNames_s | Tablicę nazw DNS |
| OperatingSystemFamily_s | Systemu Windows lub Linux |
| OperatingSystemFullName_s | Pełna nazwa systemu operacyjnego hello Hello  |
| Bitness_s | Liczba bitów Hello hello maszyny (32-bitowy lub 64-bitowe)  |
| PhysicalMemory_d | Witaj fizycznej pamięci w MB |
| Cpus_d | Witaj liczba procesorów CPU |
| CpuSpeed_d | Witaj szybkość Procesora w MHz|
| VirtualizationState_s | *Nieznany*, *fizycznych*, *wirtualnego*, *funkcji hypervisor* |
| VirtualMachineType_s | *funkcji Hyper-v*, *vmware*i tak dalej |
| VirtualMachineNativeMachineId_g | Witaj identyfikator VM przypisany przez jego funkcji hypervisor |
| VirtualMachineName_s | Nazwa Hello hello maszyny Wirtualnej |
| BootTime_t | Witaj rozruchu |



### <a name="servicemapprocesscl-type-records"></a>Rejestruje typ ServiceMapProcess_CL
Rekordy z typem *ServiceMapProcess_CL* mają dane spisu dla procesów połączenia TCP na serwerach z agentami mapy usługi. Te rekordy zawierają właściwości hello hello w poniższej tabeli:

| Właściwość | Opis |
|:--|:--|
| Typ | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| Identyfikator zasobu | Unikatowy identyfikator procesu, w obszarze roboczym hello Hello |
| ResourceName_s | Witaj Unikatowy identyfikator procesu maszynie hello, na którym jest uruchomiony|
| MachineResourceName_s | Nazwa zasobu Hello hello maszyny |
| ExecutableName_s | Nazwa pliku wykonywalnego procesu hello Hello |
| StartTime_t | czas rozpoczęcia puli procesów Hello |
| FirstPid_d | pierwszy identyfikator PID Hello w puli procesów hello |
| Description_s | Opis procesu Hello |
| CompanyName_s | Nazwa Hello hello firmy |
| InternalName_s | Wewnętrzna nazwa Hello |
| ProductName_s | Nazwa Hello hello produktu |
| ProductVersion_s | Wersja produktu Hello |
| FileVersion_s | Wersja pliku Hello |
| CommandLine_s | Witaj wiersza polecenia |
| ExecutablePath _s | toohello Hello ścieżki pliku wykonywalnego |
| WorkingDirectory_s | katalog roboczy Hello |
| Nazwa użytkownika | konta Hello, w których hello jest wykonywany proces |
| UserDomain | Hello domeny, w których hello jest wykonywany proces |


## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników

### <a name="list-all-known-machines"></a>Wyświetl listę wszystkich maszyn znane
Typ = ServiceMapComputer_CL | Funkcja deduplikacji ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Pojemność pamięci fizycznej hello listy wszystkich zarządzanych komputerów.
Typ = ServiceMapComputer_CL | Wybierz PhysicalMemory_d, ComputerName_s | ResourceId deduplikacji

### <a name="list-computer-name-dns-ip-and-os"></a>Nazwa komputera listy, DNS, adresu IP i systemu operacyjnego.
Typ = ServiceMapComputer_CL | Wybierz ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s | Funkcja deduplikacji ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Znajdź wszystkie procesy z "sql" w wierszu polecenia hello
Typ = ServiceMapProcess_CL CommandLine_s = \*sql\* | deduplikacji ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Znajdź maszyny (najnowszych rekord) według nazwy zasobu
Typ = "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" ServiceMapComputer_CL | Funkcja deduplikacji ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Znajdź maszyny (najnowszych rekord) za pomocą adresu IP
Typ = "10.229.243.232" ServiceMapComputer_CL | Funkcja deduplikacji ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Wyświetl listę wszystkich procesów znanych na określonym komputerze
Typ ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b =" | Funkcja deduplikacji ResourceId

### <a name="list-all-computers-running-sql"></a>Lista wszystkich komputerów z programem SQL
Typ w ResourceName_s ServiceMapComputer_CL = {typu = ServiceMapProcess_CL \*sql\* | Różne MachineResourceName_s} | Funkcja deduplikacji ResourceId | Różne ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>Wyświetla listę wszystkich wersji produktu unikatowy curl w mojej centrum danych
Typ = ServiceMapProcess_CL ExecutableName_s = curl | Różne ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Tworzenie grupy komputerów wszystkich komputerów z systemem CentOS
Typ = ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Różne ComputerName_s


## <a name="rest-api"></a>Interfejs API REST
Wszystkie hello serwera, procesów i zależności w mapie usługi są dostępne dane za pośrednictwem hello [interfejsu API REST mapy usługi](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>dane diagnostyczne i użycia
Firma Microsoft automatycznie zbiera dane użycia i wydajności przez korzystanie z hello usługi mapy usługi. Firma Microsoft używa tego tooprovide danych i poprawy hello jakości, bezpieczeństwa i integralności hello usługi mapy usługi. tooprovide dokładne i skuteczne funkcje do rozwiązywania problemów, hello danych zawiera informacje o konfiguracji hello oprogramowania, takie jak systemu operacyjnego i wersji, adres IP, nazwę DNS i nazwę stacji roboczej. Firma Microsoft gromadzi nazwisk, adresów ani innych informacji kontaktowych.

Aby uzyskać więcej informacji na temat zbierania i użycia danych, zobacz hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [dziennika wyszukiwania](../log-analytics/log-analytics-log-searches.md) danych tooretrieve analizy dzienników, które są zbierane przez usługę mapy.


## <a name="troubleshooting"></a>Rozwiązywanie problemów
Zobacz hello [Rozwiązywanie problemów z sekcji dokumentu Konfigurowanie mapy usługi hello](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Opinia
Masz opinię, abyśmy o mapy usługi lub tej dokumentacji?  Można znaleźć w naszych [strony User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), gdzie można sugeruje funkcje lub głosowania zapasową istniejących sugestie.
