---
title: "aaaNetwork monitora wydajności rozwiązania Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Monitor wydajności sieci w Azure Log Analytics pomaga monitorować wydajność hello Twojej sieci w pobliżu real jednorazowej toodetect i zlokalizuj wąskich gardeł wydajności sieci."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Monitor wydajności rozwiązania analizy dzienników sieci

![Symbol monitora wydajności sieci](./media/log-analytics-network-performance-monitor/npm-symbol.png)

W tym dokumencie opisano, jak tooset w górę i użyj hello monitora wydajności sieci rozwiązania analizy dzienników, która pomaga monitorować wydajność hello Twojej sieci w pobliżu real jednorazowej toodetect i zlokalizuj wąskich gardeł wydajności sieci. Z hello rozwiązania monitora wydajności sieci można monitorować utraty hello i opóźnienia między dwiema sieciami podsieci lub serwerów. Monitor wydajności sieci wykrywa problemy z siecią jak blackholing ruchu, błędy routingu i że metod monitorowania sieci z konwencjonalnej nie są możliwe toodetect problemów. Monitor wydajności sieci generuje alerty i powiadamia, gdy naruszenia progu dla połączenia sieciowego. Tych progów mogą być automatycznie rozpoznawane przez hello system, lub można je skonfigurować toouse niestandardowych reguł alertów. Monitor wydajności sieci zapewnia szybkie wykrycie problemów z wydajnością sieci i lokalizuje źródła hello hello problem tooa konkretnym segmencie sieci lub urządzenia.

Można wykrywać problemy z siecią z pulpitu nawigacyjnego rozwiązania hello, który zawiera podsumowanie informacji o tym ostatnie zdarzenia kondycji sieci, łączy sieciowych w złej kondycji i łączy podsieci, stoją utraty pakietów wysokiej i opóźnienie sieci. Użytkownik może przechodzenia do sieci łącze tooview hello bieżący stan kondycji łączy podsieci, a także łącza między węzłami. Można również wyświetlić hello trendów historycznych utraty i opóźnienie sieci hello, podsieci i poziomu węzła do węzła. Można wykrywać przejściowe problemy z siecią przez wyświetlanie trendów historycznych wykresów do utraty pakietów i opóźnienia i Znajdź wąskich gardeł sieci w formie mapy topologii. wykres interaktywny topologii Hello pozwala tras sieciowych przeskoku przeskoku hello toovisualize, aby ustalić hello źródłem problemu hello. Na przykład innych rozwiązań, można użyć wyszukiwania dziennika dla różnych analytics wymagania toocreate niestandardowych raportów na podstawie hello danych zebranych przez Monitor wydajności sieci.

rozwiązanie Hello używa transakcji syntetycznych jako podstawowy mechanizm toodetect sieci błędów. Tak można go używać bez względu na urządzenie sieciowe określonego dostawcy lub modelu. Działa ona za pośrednictwem lokalnego, w chmurze (IaaS) i środowisk hybrydowych. rozwiązanie Hello automatycznie odnajduje hello topologii sieci i różne trasy w sieci.

Typowej sieci monitorowania produktów fokus na powitania monitorowania sieci kondycji urządzenia (routery, przełączniki itd.), ale nie zapewniają wgląd w hello rzeczywista jakość połączenie sieciowe między dwoma punktami, które w Monitorze wydajności sieci.

### <a name="using-hello-solution-standalone"></a>Przy użyciu hello rozwiązania autonomiczne
Jakość hello toomonitor połączeń sieciowych między ich krytycznych obciążeń należy sieci, centrów danych lub Lokacje, możesz za pomocą hello monitora wydajności sieci rozwiązania samodzielnie toomonitor kondycji łączności między:

* wiele centrów danych lub office witryn, które są połączone za pomocą sieci publicznych lub prywatnych
* krytycznych obciążeń, które są uruchomione aplikacje biznesowe
* usługi w chmurze publicznej, takich jak Microsoft Azure lub usługi Amazon Web Services (AWS) i lokalnej sieci, jeśli masz IaaS (VM) dostępne i masz bram skonfigurowane tooallow komunikacji między lokalnymi sieciami i sieciach w chmurze
* Sieci platformy Azure i lokalnego używania Express Route

### <a name="using-hello-solution-with-other-networking-tools"></a>Za pomocą rozwiązania hello przy użyciu innych narzędzi sieci
Jeśli chcesz toomonitor aplikacji biznesowych, służy hello rozwiązania monitora wydajności sieci jako narzędzia pomocnika rozwiązania tooother sieci. Wolnej sieci może prowadzić tooslow aplikacji i Monitor wydajności sieci może ułatwić badać problemy wydajności aplikacji, które są spowodowane przez problemy z siecią podstawowej. Ponieważ hello rozwiązanie nie wymaga żadnych urządzeń toonetwork dostępu, administrator aplikacji hello nie wymaga toorely sieci informacji tooprovide zespołu o jak hello sieci wpływa na aplikacje.

Ponadto jeśli już inwestycji w inne narzędzia do monitorowania sieci, następnie hello rozwiązania można uzupełnić te narzędzia ponieważ najbardziej tradycyjnych rozwiązań monitorowania sieci nie zapewniają wgląd w sieci end-to-end metryki wydajności, takich jak utraty i opóźnienia.  Hello rozwiązania monitora wydajności sieci może pomóc wypełnienia tego odstępu.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Instalowanie i konfigurowanie agentów hello rozwiązania
Użyj hello podstawowych procesów tooinstall agentów na [tooLog komputerów Windows połączyć Analytics](log-analytics-windows-agents.md) i [tooLog połączenie programu Operations Manager Analytics](log-analytics-om-agents.md).

> [!NOTE]
> Będzie konieczne tooinstall co najmniej 2 agentów w kolejności toohave toodiscover wystarczającej ilości danych i monitorowania zasobów sieciowych. W przeciwnym razie wartość hello rozwiązania pozostanie w stanie konfigurowanie do momentu zainstalowania i skonfigurowania dodatkowych czynników.
>
>

### <a name="where-tooinstall-hello-agents"></a>Gdzie tooinstall hello agentów
Przed zainstalowaniem agentów należy rozważyć hello topologii sieci i które części hello sieciowych można toomonitor. Zaleca się zainstalowanie więcej niż jednego agenta dla każdej podsieci, które mają toomonitor. Innymi słowy dla każdej podsieci, które mają toomonitor wybierz co najmniej dwa serwery lub maszyn wirtualnych i zainstalować agenta hello na nich.

Jeśli nie wiesz o hello topologii sieci, należy zainstalować agentów hello na serwerach z krytycznych obciążeń w miejscu wydajność sieci hello toomonitor. Na przykład można Śledź tookeep połączenie sieciowe między serwerem sieci Web i serwer z programem SQL Server. W tym przykładzie należy zainstalować agenta na obu serwerach.

Agenci monitorują łączność sieciową (linki) między hostami — nie hostów hello samodzielnie. Tak, toomonitor połączenia sieciowego, należy zainstalować agentów na obu punktów końcowych tego łącza.

### <a name="configure-agents"></a>Konfigurowanie agentów

Jeśli planujesz protokołu ICMP hello toouse dla transakcji syntetycznych, należy hello tooenable następujące reguły zapory dla niezawodnego przy użyciu protokołu ICMP:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Jeśli planujesz hello toouse protokołu TCP potrzebne porty zapory tooopen dla tooensure tych komputerów, który może komunikować się agentów. Należy toodownload, a następnie uruchom hello [skrypt programu PowerShell EnableRules.ps1](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) bez żadnych parametrów w oknie programu PowerShell z uprawnieniami administracyjnymi.

Witaj skrypt tworzy kluczy rejestru wymaganych przez hello monitora wydajności sieci i tworzy połączeń TCP toocreate agentów tooallow reguł zapory systemu Windows ze sobą. klucze rejestru Hello utworzony przez skrypt hello również określić, czy toolog hello debugowania hello ścieżkę hello plików dzienników i dzienniki. Definiuje również port TCP agenta hello używany do komunikacji. wartości Hello tych kluczy są automatycznie ustawiane przez skrypt hello, dlatego nie należy ręcznie zmienić te klucze.

port Hello domyślnie otwierany jest 8084. Można użyć portu niestandardowego, podając parametr hello `portNumber` toohello skryptu. Jednak hello tego samego portu należy używać na wszystkich komputerach hello gdzie hello skrypt jest uruchamiany.

> [!NOTE]
> Hello EnableRules.ps1 skrypt umożliwia skonfigurowanie reguł zapory systemu Windows tylko na komputerze hello gdzie hello skrypt jest uruchamiany. Jeśli masz zapory sieciowej, należy upewnić się, że umożliwia ruch kierowany do hello port TCP używany przez Monitor wydajności sieci.
>
>

## <a name="configuring-hello-solution"></a>Konfigurowanie rozwiązania hello
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

1. Hello rozwiązania monitora wydajności sieci uzyskuje dane z komputerów z systemem Windows Server 2008 SP 1 lub nowszym lub Windows 7 z dodatkiem SP1 lub nowszy, które są takie same hello wymagania hello Microsoft Monitoring Agent (MMA). Agenci programu NPM można również uruchomić na pulpicie/klienckie systemy operacyjne Windows (Windows 10, Windows 8.1, Windows 8 i Windows 7).
    >[!NOTE]
    >Witaj agentów dla systemów operacyjnych Windows server obsługuje zarówno TCP, jak i protokołu ICMP jako hello protokoły dla transakcji syntetycznych. Klienckie systemy operacyjne Windows hello agentów obsługuje jednak tylko ICMP jako protokół powitania dla transakcji syntetycznych.

2. Dodaj obszar roboczy tooyour rozwiązania monitora wydajności sieci hello z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).  
   ![Symbol monitora wydajności sieci](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. W portalu OMS hello, zostanie wyświetlony nowy Kafelek zatytułowany **monitora wydajności sieci** z wiadomość hello *rozwiązanie wymaga dodatkowej konfiguracji*. Będziesz potrzebować tooconfigure hello rozwiązania tooadd sieci na podstawie podsieci i węzły, które zostały wykryte przez agentów. Kliknij przycisk **monitora wydajności sieci** toostart Konfigurowanie hello domyślnej sieci.  
   ![rozwiązanie wymaga dodatkowej konfiguracji](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Konfigurowanie rozwiązania hello z domyślnej sieci
Na stronie konfiguracji hello, zobaczysz jednej sieci o nazwie **domyślne**. Jeśli jeszcze nie zdefiniowano żadnych sieci, wszystkie podsieci automatycznie odnalezione hello są umieszczane w hello domyślnej sieci.

Gdy utworzysz sieci, możesz dodać tooit podsieci i podsieci jest usuwane z hello domyślnej sieci. Jeśli usuniesz sieci, wszystkie jego podsieci automatycznie są zwracane toohello domyślnej sieci.

Innymi słowy sieć domyślne hello jest hello kontener dla wszystkich podsieci hello, które nie znajdują się w dowolnej sieci zdefiniowanej przez użytkownika. Nie można edytować ani usunąć hello domyślnej sieci. Zawsze pozostaje w systemie hello. Jednak można utworzyć dowolną liczbę sieci odpowiednio do potrzeb.

W większości przypadków hello podsieci w organizacji będzie można uporządkować w więcej niż jedną sieć i należy utworzyć jeden lub więcej sieci toologically grupy podsieci.

### <a name="create-new-networks"></a>Tworzenie nowych sieci
Sieć w Monitorze wydajności w sieci jest kontenerem dla podsieci. Z dowolnej nazwy i Dodaj sieci toohello podsieci można utworzyć sieci. Na przykład można utworzyć sieci o nazwie *Building1* , a następnie dodać podsieci lub można utworzyć sieci o nazwie *DMZ* , a następnie dodaj wszystkie podsieci należących toodemilitarized strefy toothis sieci.

#### <a name="toocreate-a-new-network"></a>toocreate nowej sieci
1. Kliknij przycisk **sieci Dodaj** , a następnie wpisz hello sieci nazwę i opis.
2. Wybierz co najmniej jednej podsieci, a następnie kliknij przycisk **Dodaj**.
3. Kliknij przycisk **zapisać** toosave hello konfiguracji.  
   ![Dodawanie sieci](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Poczekaj, aż agregacja danych
Po zapisaniu hello konfiguracji po raz pierwszy, rozpoczyna się rozwiązania hello pobierania sieci pakietów utraty i opóźnienia między węzłami hello, jeżeli agenci są zainstalowani. Ten proces może trochę potrwać, czasami 30 minut. W tym stanie hello monitora wydajności sieci kafelka na stronie Przegląd hello wyświetla komunikat z informacją *agregacja danych w procesie*.

![agregacja danych w toku](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Po przekazaniu danych hello zobaczysz hello przedstawiający Kafelek aktualizacji Monitora wydajności sieci danych.

![Kafelek monitora wydajności sieci](./media/log-analytics-network-performance-monitor/npm-tile.png)

Kliknij pozycję pulpit nawigacyjny hello kafelka tooview hello monitora wydajności sieci.

![Pulpit nawigacyjny sieci monitora wydajności](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Edytuj ustawienia monitorowania dla podsieci
Wszystkie podsieci, gdy co najmniej jeden agent został zainstalowany są wyświetlane na powitania **podsieci** karcie na stronie konfiguracji hello.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable lub Wyłącz monitorowanie dla określonej podsieci
1. Toohello dalej hello zaznacz lub usuń zaznaczenie pola **podsieci Identyfikatora** , a następnie upewnij się, że **na użytek monitorowania** jest wybrane lub wyczyszczone, gdzie to właściwe. Można zaznaczyć lub wyczyścić wielu podsieci. Po wyłączeniu podsieciami, które nie są monitorowane, jak agenci hello zostanie zaktualizowany toostop polecenie ping innych agentów.
2. Wybierz węzły hello mają toomonitor dla określonej podsieci, wybierając je z listy hello i przeniesienie podsieć hello hello wymagane węzłów między listami hello zawierającego węzły niemonitorowane i monitorowane.
   Możesz dodać niestandardowe **opis** toohello podsieci, jeśli chcesz.
3. Kliknij przycisk **zapisać** toosave hello konfiguracji.  
   ![Edytuj podsieci](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Wybierz toomonitor węzłów
Wszystkie węzły hello, które zainstalowano na nich agenta są wymienione w hello **węzłów** kartę.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable lub Wyłącz monitorowanie dla węzłów
1. Wybierz lub wyczyść hello węzły mają toomonitor, lub zatrzymać monitorowanie.
2. Kliknij przycisk **na użytek monitorowania**, lub wyczyść, zależnie od potrzeb.
3. Kliknij pozycję **Zapisz**.  
   ![Aby włączyć monitorowanie węzła](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>Ustaw reguły monitorowania
Monitor wydajności sieci generuje kondycji zdarzenia dotyczące hello łączności między dwa węzły lub łączy podsieci lub sieci, gdy naruszenia progu. Tych progów mogą być automatycznie rozpoznawane przez hello system, lub można je skonfigurować niestandardowe reguły alertów.

Witaj *domyślną regułę* jest tworzony przez hello system i tworzy zdarzenie kondycji, w przypadku naruszenia hello rozpoznawane przez system próg łączy utraty lub opóźnienia między jakiejkolwiek parze sieci lub podsieć. Można wybrać toodisable hello domyślną regułę i utworzyć niestandardowe reguły monitorowania

#### <a name="toocreate-custom-monitoring-rules"></a>toocreate niestandardowe reguły monitorowania
1. Kliknij przycisk **Dodaj regułę** w hello **Monitor** i wprowadzić hello nazwa i opis reguły.
2. Wybierz pary hello sieci lub podsieć toomonitor łącza z list hello.
3. Najpierw wybierz z listy rozwijanej sieć hello hello sieci, w których hello znajduje się pierwszy podsieć/s zainteresowania, a następnie wybierz hello podsieć/s z listy rozwijanej hello odpowiednich podsieci.
   Wybierz **wszystkie podsieci** Jeśli chcesz toomonitor hello wszystkich podsieci w połączenia sieciowego. Podobnie wybierz hello innych podsieci/s zainteresowań. I kliknięcie **dodać wyjątek** tooexclude monitorowanie dla konkretnego podsieć łączy się z zaznaczenia hello wprowadzone.
4. Wybór między ICMP i TCP protokołów wykonania transakcji syntetycznych.
5. Jeśli nie chcesz toocreate zdarzenia kondycji dla wybranych elementów hello, wyczyść **Włącz monitorowanie kondycji w łączach hello objęte regułą**.
6. Wybierz warunki monitorowania.
   Można ustawić progami niestandardowymi kondycji zdarzenie generacji, wpisując wartości progowe. Zawsze, gdy wartość hello warunku hello wykraczają poza jego próg dla pary wybranego sieć/podsieć hello, jest generowane zdarzenie kondycji.
7. Kliknij przycisk **zapisać** toosave hello konfiguracji.  
   ![Utwórz regułę niestandardową monitorowania](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Po zapisaniu reguły monitorowania tej reguły można zintegrować z zarządzania alertami, klikając **Tworzenie alertów**. Automatycznie tworzona jest reguła alertu z zapytania wyszukiwania hello i innych wymaganych parametrów wypełniane automatycznie. Przy użyciu reguły alertu, możesz otrzymywać pocztą e-mail alertów, oprócz toohello istniejących alertów w ramach programu NPM. Alerty można również uruchomić czynności zaradczych z elementami runbook i ich można zintegrować z istniejącymi rozwiązaniami zarządzania usługi za pomocą elementów webhook. Możesz kliknąć **Zarządzanie Alert** ustawienia alertu hello tooedit.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Wybierz prawa ICMP protocol hello lub TCP

Monitor wydajności sieci (NPM) używa metryki wydajności transakcji syntetycznych toocalculate sieci podobnie jak pakiet opóźnienia utratą i łącza. toounderstand to lepiej, należy wziąć pod uwagę NPM agenta połączonych tooone koniec połączenia sieciowego. Ten NPM agent wysyła sondowania pakietów tooa drugi NPM agenta tooanother połączonych koniec hello sieci. Witaj drugi odpowiedzi agenta z pakietów odpowiedzi. Ten proces jest powtarzany kilka razy. Mierząc liczba hello odpowiedzi i czas trwania tooreceive odpowiedź, hello pierwszego NPM agenta ocenia czas oczekiwania linku oraz operacjach porzucania pakietów.

Hello format, rozmiar i kolejność tych pakietów jest określana przez protokół hello, który można wybrać podczas tworzenia reguł monitorowania. Na podstawie protokołu pakietów hello, hello pośredniczące urządzenia sieciowe (routery, przełączniki itd.) może różnie te pakiety. W rezultacie wybranego protokołu wpływ na dokładność hello hello wyników. I wybór protokołu określa, czy wszystkie wymagane ręczne wykonanie czynności należy wykonać po wdrożeniu rozwiązania NPM hello.

NPM oferuje hello wybór między protokołów ICMP i TCP wykonania transakcji syntetycznych.
Jeśli wybierzesz protokołu ICMP, podczas tworzenia reguły transakcji syntetycznych, agenci NPM hello używają ECHA ICMP wiadomości toocalculate hello sieci opóźnienia i utratę pakietów. ECHA protokołu ICMP hello używa sama komunikatu to znaczy wysyłane przez narzędzie Ping z konwencjonalnej hello. Użycie jako hello protokołu TCP, NPM agenci wysyłają pakietu TCP SYN za pośrednictwem sieci hello. Następuje uzgadniania TCP ukończenia, a następnie usuwając hello połączenia przy użyciu RST pakietów.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Punkty tooconsider przed wybraniem hello protokołu
Należy wziąć pod uwagę hello przed wybraniem toouse protokołu w związku z informacjami:

##### <a name="discovering-multiple-network-routes"></a>Odnajdywanie wiele tras z sieci
Protokół TCP jest dokładniejsze podczas rozpoznawania wiele tras i wymaga mniejszej liczby agentów w każdej podsieci. Na przykład jeden lub dwaj agenci za pomocą protokołu TCP umożliwia odnalezienie wszystkich nadmiarowe ścieżki między podsieciami. Należy jednak kilka agentów przy użyciu protokołu ICMP tooachieve podobne wyniki. Za pomocą protokołu ICMP, jeśli masz *N* liczba tras między dwiema podsieciami, potrzebujesz więcej niż 5*N* agentów w podsieci źródłowe lub docelowe.

##### <a name="accuracy-of-results"></a>Dokładność wyników
Routery i przełączniki zwykle tooassign tooICMP ECHO pakietów porównaniu tooTCP pakietami o niższym priorytecie. W niektórych sytuacjach silnie ładowane urządzeń sieciowych, hello dane uzyskiwane przez protokół TCP dokładniejsze odzwierciedla utraty hello i opóźnienia wystąpił przez aplikacje. Dzieje się tak, ponieważ większość ruchu aplikacji hello przepływa za pośrednictwem protokołu TCP. W takich przypadkach ICMP zawiera mniej dokładne tooTCP wyniki porównywane.

##### <a name="firewall-configuration"></a>Konfiguracja zapory
Protokół TCP wymaga, że port docelowy tooa wysyłania pakietów TCP. Witaj domyślny port używany przez agentów NPM jest 8084, jednak można go zmienić po skonfigurowaniu agentów. Należy tak, czy z zapory sieciowe lub reguły NSG (na platformie Azure) są zezwala na ruch na porcie hello tooensure. Należy również toomake się, że skonfigurowano zaporą lokalne powitania na komputerach hello, jeżeli agenci są zainstalowani tooallow ruchu na tym porcie.

Używając reguł zapory tooconfigure skrypty programu PowerShell na komputerach z systemem Windows, muszą tooconfigure Zapora sieciowa ręcznie.

Z kolei w protokołu ICMP przy użyciu portu nie będzie działać. W większości przypadków enterprise ruch protokołu ICMP jest dozwolone przy użyciu narzędzia Diagnostyka sieci toouse chcesz hello narzędzie Ping tooallow zapór hello. Tak Jeśli jeden komputer z innej można wywołać, następnie służy protokołu ICMP hello bez konieczności zapór tooconfigure ręcznie.

> [!NOTE]
> W przypadku, gdy nie masz pewności, jakie toouse protokołu, wybierz toostart ICMP z. Jeśli nie są zadowalające hello wyniki, zawsze można przełączać tooTCP później.


#### <a name="how-tooswitch-hello-protocol"></a>Jak tooswitch hello protokołu

W przypadku wybrania toouse ICMP podczas wdrażania tooTCP można przełączać w dowolnym momencie poprzez edycję hello domyślna reguła monitorowania.

##### <a name="tooedit-hello-default-monitoring-rule"></a>Reguła monitorowania tooedit hello domyślnej
1.  Przejdź za**wydajność sieci** > **Monitor** > **Konfiguruj** > **Monitor** a następnie kliknij przycisk **domyślną regułę**.
2.  Przewiń toohello **protokołu** sekcji, a następnie wybierz protokół hello, które mają toouse.
3.  Kliknij przycisk **zapisać** tooapply hello ustawienie.

Nawet wtedy, gdy reguła domyślna hello jest przy użyciu określonego protokołu, możesz utworzyć nowe reguły z innego protokołu. Nawet tworzenia różnych zasad gdzie niektórych reguł hello używać protokołu ICMP, a inny używa protokołu TCP.




## <a name="data-collection-details"></a>Szczegóły danych kolekcji
Monitor wydajności sieci używa TCP SYN SYNACK potwierdzenie uzgadnianie pakietów, gdy TCP jest wybrane i odpowiedzi ECHA ICMP ECHA protokołu ICMP, gdy ICMP jest wybrany jako hello toocollect utraty i opóźnienia informacji o protokole. Traceroute jest również używane tooget informacji dotyczących topologii.

Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla monitora wydajności sieci.

| Platformy | Bezpośrednie agenta | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |Komunikaty ECHA ICMP/uzgodnienia TCP co 5 sekund danych wysyłane co 3 minuty |

rozwiązanie Hello używa transakcji syntetycznych tooassess hello kondycji hello sieci. Agenci OMS zainstalowany w punkcie różnych pakietów TCP exchange sieci hello lub echa protokołu ICMP (w zależności od protokołu hello wybrany do monitorowania) ze sobą. W procesie hello agentów Dowiedz się hello obustronne czasu i pakietów utraty, ile. Okresowo każdy agent wykonuje także trasy śledzenia tooother toofind agentów wszystkie hello różne trasy w sieci hello, które należy sprawdzić. Agenci hello przy użyciu tych danych, można wywnioskować hello opóźnienia sieci i rysunki utraty pakietów. testy Hello są powtarzane co pięć sekund i dane są agregowane dla trzy minuty przez agentów hello przed przekazaniem go toohello usługi analizy dzienników.

> [!NOTE]
> Mimo że agentów komunikują się ze sobą często, nie generują one dużą ilość ruchu sieciowego podczas przeprowadzania testów hello. Agenci polegać tylko na TCP SYN SYNACK potwierdzenie uzgadnianie pakietów toodetermine hello utraty i opóźnienia — żadne dane, które są wymieniane pakietów. W trakcie tego procesu agentów komunikują się ze sobą tylko w razie potrzeby i topologii komunikacyjnej agenta hello jest zoptymalizowany tooreduce ruchu sieciowego.
>
>

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello
W tej sekcji opisano wszystkie funkcje pulpitu nawigacyjnego hello i w jaki sposób toouse je.

### <a name="solution-overview-tile"></a>Kafelka przeglądu rozwiązania
Po włączeniu hello rozwiązania monitora wydajności sieci hello kafelka rozwiązania na stronie Przegląd OMS hello zapewnia szybki przegląd kondycji sieci hello. Wyświetla wykres przedstawiający hello liczba łączy podsieci w dobrej kondycji i złej kondycji. Po kliknięciu kafelka hello otwiera hello pulpit nawigacyjny rozwiązania.

![Kafelek monitora wydajności sieci](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Pulpit nawigacyjny rozwiązania monitora wydajności sieci
Witaj **podsumowania sieci** blok zawiera podsumowanie informacji o sieciach hello wraz z ich rozmiar względny. Następuje to Kafelki przedstawiający łączna liczba łączy sieciowych, łącza podsieci i ścieżki w systemie hello (ścieżka składa się z adresów IP hello dwa hosty z agentami i wszystkich przeskokach hello między nimi).

Witaj **zdarzenia kondycji sieci górnej** bloku zawiera listę najnowszych zdarzeń, kondycji i alertów w systemie hello i czas hello ponieważ hello zdarzeń była aktywna. Zdarzenie kondycji lub alert jest generowany utraty pakietów hello lub opóźnienia sieci lub podsieć łącza przekracza próg.

Witaj **łączy sieciowych w złej kondycji górnej** bloku pokazuje listę łączy sieciowych w złej kondycji. Są to hello łączy sieciowych, który ma co najmniej jednego zdarzenia kondycji niekorzystny ich w chwili hello.

Hello **łączy podsieci Top najbardziej utraty** i **łączy podsieci z opóźnieniem najbardziej** bloków Wyświetl łączy podsieci top hello przez utraty pakietów i odpowiednio góry łączy podsieci opóźnienie. Duże opóźnienie lub niektóre ilości utraty pakietów mogą znajdować się na niektórych łączy sieciowych. Takie łącza są wyświetlane na listach dziesięć top hello, ale nie jest oznaczony jako niepoprawny.

Witaj **typowych kwerend** blok zawiera zestaw zapytania wyszukiwania, które pobierają sieci nieprzetworzone dane monitorowania bezpośrednio. Te zapytania można użyć jako punktu wyjścia do tworzenia zapytań niestandardowych raportowania.

![Pulpit nawigacyjny sieci monitora wydajności](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Przechodzenie do szczegółów dla głębokości
Możesz kliknąć różnych łączy na powitania rozwiązania pulpitu nawigacyjnego toodrill rozwijanej głębiej do żadnych obszarów zainteresowań. Na przykład gdy zostanie wyświetlony alert lub łączy sieciowych w złej kondycji, są wyświetlane na pulpicie nawigacyjnym hello, kliknięcie go tooinvestigate dodatkowe. Strona tooa, która zawiera listę wszystkich łączy podsieci hello hello określonej sieci łącza spowoduje przekierowanie. Będziesz w stanie toosee hello utraty, opóźnienia i kondycji stanu każdego łącza podsieci i szybko dowiedzieć łączy podsieci, które są przyczyną problemu hello. Następnie możesz kliknąć **wyświetlanie łączy węzłów** toosee wszystkich łączy węzłów hello podsieci zła hello łącza. Następnie możesz wyświetlić poszczególnych łączy węzła do węzła i łącza hello węzłów w złej kondycji.

Możesz kliknąć **widoku topologii** tooview hello przeskoku przeskoku topologii hello tras między węzłami hello źródłowym i docelowym. Witaj zła tras lub przeskoków są zaznaczone na czerwono, aby można szybko zidentyfikować hello problem tooa konkretnego fragmentu hello sieci.

![Przechodzenie do szczegółów danych](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Rejestrator stanu sieci

Każdy widok wyświetla migawkę kondycji Twojej sieci w określonym punkcie w czasie. Domyślnie wyświetlany jest stan ostatniej hello. pasek Hello u góry strony hello hello pokazuje hello punktu w czasie, dla którego jest wyświetlany stan hello. Można wybrać toogo w czasu i Wyświetl migawki hello kondycji Twojej sieci, klikając pasek hello na **akcje**. Można również wybrać tooenable lub wyłączyć automatyczne odświeżanie dla dowolnej strony, podczas wyświetlania hello najnowszy stan.

![Stan sieci](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Trend wykresów
Na każdym poziomie, że przechodzenie do szczegółów, zostanie wyświetlony trend hello utraty i czas oczekiwania dla połączenia sieciowego. Wykresy trendu są również dostępne dla łączy podsieci i węzła. Hello interwał hello tooplot wykresu można zmienić za pomocą formantów czasu hello u góry hello hello wykresu.

Wykresy trendu Pokaż historycznych perspektywy hello wydajność połączenia sieciowego. Niektóre problemy z siecią są charakter przejściowy i będzie toocatch twardych tylko na podstawie bieżącego stanu sieci hello hello. Jest to spowodowane problemy można szybko surface i zniknąć przed każdy powiadomienia tylko tooreappear w późniejszym momencie. Takie przejściowych problemów również może być trudne dla administratorów aplikacji, ponieważ te problemy wraz ze wzrostem niewyjaśniony czas odpowiedzi aplikacji, nawet jeśli wszystkie składniki aplikacji wyświetlane toorun sprawnie często powierzchni.

Tego rodzaju problemy mogą łatwo wykryć, analizując wykresu trendu, w której problem hello będą wyświetlane jako nagłym kolekcji utratę pakiet lub opóźnienia sieci.

![wykresu trendu](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>mapy topologii przeskoku przeskoku
Przedstawia Monitor wydajności hello topologii przeskoku przeskoku tras między dwa węzły na mapie interakcyjne topologii w sieci. Mapy topologii hello można wyświetlić, wybierając węzeł łącze, a następnie klikając polecenie **widoku topologii**. Ponadto można wyświetlić mapy topologii hello, klikając **ścieżki** kafelka na pulpicie nawigacyjnym hello. Po kliknięciu **ścieżki** na pulpicie nawigacyjnym hello, będziesz mieć tooselect hello węzły źródłowe i docelowe z hello panelu po lewej stronie, a następnie kliknij przycisk **wykreślenia** tooplot hello tras między hello dwa węzły.

mapy topologii Hello Wyświetla jak wiele tras należą do zakresu od hello dwa węzły i jakie ścieżek hello danych potrwać pakietów. Wąskich gardeł wydajności sieci są oznaczone na czerwono na powitania mapy topologii. Analizując red kolorowe elementy na mapie topologii hello można znaleźć połączenia sieciowego uszkodzony lub uszkodzenia urządzenia sieciowego.

Po kliknięciu węzła lub kursor nad nim hello mapy topologii, zobaczysz hello właściwości węzła hello, takie jak adres IP i nazwy FQDN. Kliknij przycisk toosee przeskoku, jest adres IP. Możesz toofilter określonej trasy przy użyciu filtrów hello w okienku akcji zwijanej hello. I hello topologii sieci można również uprościć, ukrywając hello przeskoków za pomocą suwaka hello w okienku akcji hello. Możesz powiększania lub poza mapy topologii hello za pomocą kółka myszy.

Należy zauważyć, tej topologii hello pokazano hello mapy topologii warstwy 3 i nie zawiera warstwy 2 urządzenia i połączeń.

![mapy topologii przeskoku przeskoku](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Lokalizacja usterek
Monitor wydajności sieci jest wąskich gardeł sieci hello stanie toofind bez połączenia toohello urządzeń sieciowych. Na podstawie hello danych zebranych z hello sieci i stosując zaawansowane algorytmy na wykresie sieci hello, Monitor wydajności sieci sprawia, że prawdopodobieństwa szacowania hello części sieci, które są najbardziej prawdopodobną hello źródłem problemu hello.

Ta metoda jest wąskich gardeł sieci hello toodetermine przydatne, gdy toohops dostępu nie jest dostępna, ponieważ nie wymaga żadnych toobe dane zbierane z hello urządzeń sieciowych, takich jak routery i przełączniki. Jest to przydatne także wtedy, gdy hello przeskoków między dwoma węzłami nie znajdują się w sieci kontrolę administracyjną. Na przykład przeskoków hello może być routery usługodawców internetowych.

### <a name="log-analytics-search"></a>Wyszukaj analizy dzienników
Wszystkie dane, które jest dostępne graficznie za pośrednictwem hello pulpit nawigacyjny z Monitora wydajności sieci i przechodzenia strony jest również dostępna natywnie w wyszukiwaniu analizy dzienników. Można zbadać hello danych przy użyciu języka zapytań wyszukiwania hello i twórz raporty niestandardowe eksportując hello tooExcel danych lub usługi Power BI. Witaj **typowych kwerend** bloku na pulpicie nawigacyjnym hello ma niektóre przydatne zapytań, które służy jako punkt początkowy dla tworzenia własnych kwerendy i raporty hello.

![zapytania wyszukiwania](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Znajdź hello główną przyczynę alertu health
Teraz, gdy zostały przedstawione monitora wydajności sieci, Przyjrzyjmy się proste badanie przyczynę hello kondycji zdarzenie.

1. Na stronie Przegląd hello, otrzymasz szybkiej migawki o kondycji hello sieci obserwując hello **monitora wydajności sieci** kafelka. Należy zauważyć, że poza podsieci hello 6 łączy monitorowane, jest w złej kondycji 2. Gwarantuje to dochodzenia. Kliknij pozycję pulpit nawigacyjny hello kafelka tooview hello rozwiązania.  
   ![Kafelek monitora wydajności sieci](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. W poniższym obrazie przykład Witaj można zauważyć, że istnieje zdarzenie kondycji połączenia sieciowego, który jest nieprawidłowy. Zdecyduj, problem hello tooinvestigate i kliknij przycisk hello **DMZ2 DMZ1** toofind łącze sieci poza głównym hello hello problemu.  
   ![przykład łączy sieciowych w złej kondycji](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. Strona przechodzenia Hello zawiera wszystkich łączy podsieci hello w **DMZ2 DMZ1** połączenia sieciowego. Można zauważyć, że dla obu hello łączy podsieci, opóźnienia hello przekroczyło próg hello tworzenia połączenia sieciowego hello złej kondycji. Można również sprawdzić hello trendów opóźnienia zarówno hello łączy podsieci. Można użyć czas hello formant wyboru w toofocus wykres hello na powitania wymagany zakres czasu. Widać hello porę dnia hello, gdy czas oczekiwania został osiągnięty Szczyt. Dzienniki hello tego problemu hello tooinvestigate okresu czasu można będzie później wyszukiwać. Kliknij przycisk **wyświetlanie łączy węzłów** toodrill rozwijanej dalej.  
   ![przykład łączy podsieci w złej kondycji](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Podobne toohello poprzedniej strony, strony przechodzenia hello hello łącza określonej podsieci wyświetlane w jego łączy węzłów składników. Można wykonywać działania podobne tutaj tak samo jak w poprzednim kroku hello. Kliknij przycisk **widoku topologii** topologii hello tooview między węzłami hello 2.  
   ![przykład łączy węzłów w złej kondycji](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Wszystkie ścieżki hello między węzłami hello 2 wybrane na wykresie hello mapy topologii. Można zwizualizować topologii przeskoku przeskoku hello tras między dwa węzły na powitania mapy topologii. Umożliwia danych istnieje jak wiele tras między dwoma węzłami hello i jakie ścieżek hello pakiety danych są tworzone. Wąskich gardeł wydajności sieci są oznaczone kolorem czerwonym. Analizując red kolorowe elementy na mapie topologii hello można znaleźć połączenia sieciowego uszkodzony lub uszkodzenia urządzenia sieciowego.  
   ![przykład widoku topologii złej kondycji](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. utraty Hello, opóźnienia i hello liczbę przeskoków w poszczególnych ścieżek, które mogą być przeglądane na powitania **akcji** okienka. Użyj hello pasek przewijania tooview hello szczegóły tych ścieżek w złej kondycji.  Użyj hello filtry tooselect hello ścieżki z przeskoku zła hello hello topologii hello tylko wybrany ścieżki są kreślone. Możesz użyć toozoom kółka myszy lub wyjścia hello mapy topologii.

   Witaj poniżej obrazu wyraźnie widać hello przyczynę hello problem obszarów toohello określonej sekcji sieci hello analizując hello ścieżki i przeskoków kolorem czerwonym. Kliknięcie w węźle mapy topologii hello ujawnia hello właściwości węzła hello, w tym hello nazwy FQDN i adresów IP. Kliknięcie skoku zawiera adres IP hello hello przeskoku.  
   ![Zła topologia — przykład szczegóły ścieżki](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Przekazywanie opinii

- **UserVoice** — możesz zamieścić pomysłów dla monitora wydajności sieci funkcji, że chcesz, abyśmy toowork na. Można znaleźć w naszych [strony UserVoice](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Dołącz do naszych kohorty** — NAS interesuje zawsze o nowych klientów, Dołącz do naszych kohorty. Jako część możesz uzyskać wczesny dostęp toonew funkcje i pomóc nam w ulepszaniu monitora wydajności sieci. Jeśli interesuje Cię dołączenie, wypełnienie wychodzący to [szybkie ankiety](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Następne kroki
* [Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowe rekordów danych wydajności sieci.
