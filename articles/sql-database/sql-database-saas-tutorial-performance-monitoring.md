---
title: "wydajność aaaMonitor wiele baz danych Azure SQL w wielodostępnych aplikacji SaaS | Dokumentacja firmy Microsoft"
description: "Monitorowanie i zarządzanie nimi wydajności baz danych i pul aplikacji SaaS Wingtip bazy danych SQL Azure hello"
keywords: "samouczek usługi sql database"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Monitorowanie wydajności aplikacji Wingtip SaaS hello

W tym samouczku są przedstawione kilka kluczowych scenariuszy zarządzania używana w aplikacji SaaS. Za pomocą działania toosimulate generator obciążenia dla wszystkich baz danych dzierżawy, hello wbudowaną funkcję monitorowania i alertów funkcje bazy danych SQL i pule elastyczne przedstawiono.

aplikacji Wingtip SaaS Hello wykorzystuje model danych pojedynczej dzierżawy, gdzie każda właściwość (dzierżawcy) ma własne bazy danych. Jak wiele aplikacji SaaS hello zakładano wzorzec obciążenia dzierżawy to nieprzewidywalne i sporadyczne. Innymi słowy, sprzedaż biletów może nastąpić w dowolnej chwili. tootake zaletą tego wzorca użycia typowych bazy danych, dzierżawy, baz danych są wdrażane na elastyczne pule baz danych. Pule elastyczne zoptymalizować hello kosztów rozwiązania udostępniania zasobów przez wiele baz danych. W przypadku tego typu wzorzec jest ważne toomonitor bazy danych i puli zasobów użycia tooensure, który ładuje rozsądnych jest równoważone między pule. Należy również tooensure, że odpowiednie zasoby pojedynczych baz danych, i że pule nie są naciśnięcie klawisza ich [eDTU](sql-database-what-is-a-dtu.md) limity. W tym samouczku opisuje sposoby toomonitor i zarządzanie nimi baz danych i pul, jak i tootake akcję naprawczą w odpowiedzi toovariations obciążenia pracą.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Symulowanie użycia baz danych dzierżawy hello uruchamiając generator podana obciążenia
> * Monitor hello dzierżawy baz danych, ponieważ one odpowiadać toohello wzrost obciążenia
> * Skalowanie w górę hello elastycznej puli w odpowiedzi toohello zwiększona bazy danych obciążenia
> * Obsługi administracyjnej drugiego działania bazy danych saldo tooload puli elastycznej


toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toosaas-performance-management-patterns"></a>Wprowadzenie tooSaaS wydajności zarządzania wzorce

Zarządzanie wydajnością bazy danych składa się z kompilowania i analizowanie danych dotyczących wydajności, a następnie reaguje toothis danych przez dostosowanie wartości parametrów toomaintain akceptowalny czas odpowiedzi aplikacji. Podczas obsługi wielu dzierżawców, elastyczne pule baz danych są tooprovide ekonomiczny sposób zasobów i zarządzanie nimi dla grupy baz danych z nieprzewidywalnych obciążeń. Przy pewnych wzorcach obciążenia korzyści mogą się pojawić przy zarządzaniu w puli zaledwie dwoma bazami danych S3.

![nośnik](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Pule i baz danych hello w pulach, powinny być monitorowane tooensure, które pozostają w dopuszczalnych zakresach wydajności. Dostosuj hello puli konfiguracji toomeet hello potrzeb obciążenia agregacji hello wszystkich baz danych, zapewnienie odpowiedniej dla hello jednostek Edtu puli hello ogólną obciążenia. Dostosuj hello na bazę danych min i -database maksymalną liczbę jednostek eDTU wartości tooappropriate wartości dla wymagań określonej aplikacji.

### <a name="performance-management-strategies"></a>Strategie zarządzania wydajnością

* tooavoid o toomanually monitorować wydajność, najbardziej skutecznych jest zbyt**ustawić alerty, które są wyzwalane w razie baz danych lub pul Zabłąkana poza normalne zakresy**.
* Witaj toorespond tooshort termin wahań poziom wydajności agregacji hello puli, **poziom eDTU puli można skalować w górę lub w dół**. W przypadku tego wahań na podstawie regularnych lub przewidywalną **skalowania puli hello może być zaplanowane toooccur automatycznie**. Na przykład skalowanie w dół może nastąpić, kiedy przewidywane jest niskie obciążenie — w nocy lub podczas weekendów.
* toorespond toolonger termin wahań lub zmiany w liczbie baz danych, hello **pojedynczych baz danych można przenieść do innej puli**.
* wzrost termin tooshort toorespond *poszczególnych* obciążenie bazy danych **pojedynczych baz danych można znaleźć poza puli i przypisane poziom wydajności poszczególnych**. Po to za sobą zmniejszenie obciążenia hello, hello bazy danych może być zwracany toohello puli. Jeśli jest to znane z wyprzedzeniem, baz danych można przenieść pre-emptively się, że baza danych hello tooensure ma zawsze zasobów hello i tooavoid wpływu na innych baz danych w puli hello. Jeśli to wymaganie jest przewidywalne, takie jak miejsce, w których występują łazienkowych sprzedaży biletów dla popularnych zdarzenia, a następnie to zachowanie zarządzania można zintegrować aplikacji hello.

Witaj [portalu Azure](https://portal.azure.com) zawiera wbudowane monitorowanie i alerty na najwięcej zasobów. W usłudze SQL Database funkcje monitorowania i zgłaszania alertów są dostępne na poziomie baz danych i pul. Ten wbudowany, monitorowanie i alerty jest określonych zasobów, dlatego jest wygodne toouse dla małej liczby zasobów, ale nie jest wygodną podczas pracy z wielu zasobów.

W scenariuszach dużych którym pracujesz z wielu reources [analizy dzienników (OMS)](sql-database-saas-tutorial-log-analytics.md) mogą być używane. Jest to oddzielne usługa Azure, która udostępnia analityka w porównaniu z emitowany dzienniki diagnostyczne i dane telemetryczne zebrane w obszarze roboczym analizy dzienników. Analizy dzienników można zbierać dane telemetryczne z wielu usług i być tooquery używane i Ustaw alerty.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Pobieranie kodu źródłowego aplikacji Wingtip hello i skryptów

Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Aprowizacja dodatkowych dzierżaw

Pule mogą być ekonomicznego z dwóch S3 baz danych, hello więcej baz danych znajdujących się w hello puli hello bardziej ekonomiczne rozwiązanie staje się hello uśrednianie efekt. Aby dobrze zrozumieć działanie monitorowania wydajności i zarządzania nią w dużej skali, w tym samouczku zalecamy wdrożenie co najmniej 20 baz danych.

Jeśli już alokacji partii dzierżaw w samouczku wcześniejsze pominąć toohello [Symulacja użycie na wszystkich baz danych dzierżawy](#simulate-usage-on-all-tenant-databases) sekcji.

1. Otwórz... \\Modułów uczenia\\zarządzania i monitorowania wydajności\\*PerformanceMonitoringAndManagement.ps1 pokaz* w hello *PowerShell ISE*. Nie zamykaj tego skryptu, gdyż w ramach tego samouczka będzie konieczne uruchomienie kilku scenariuszy.
1. Ustaw zmienną **$DemoScenario** = **1**, **Provision a batch of tenants** (Aprowizacja partii dzierżaw)
1. Naciśnij klawisz **F5** toorun hello skryptu.

skrypt Hello wdroży 17 dzierżaw w mniej niż pięć minut.

Witaj *TenantBatch nowy* skrypt używa zestawu połączonych lub zagnieżdżone [Menedżera zasobów](../azure-resource-manager/index.md) szablonów, które tworzenia partii dzierżawcy, która domyślnie kopiuje hello bazy danych **basetenantdb** na powitania katalogu serwera toocreate hello nowych dzierżawy baz danych, następnie rejestruje je w katalogu hello i na koniec inicjuje ich typu hello dzierżawy nazwę i miejsce. Jest to zgodne z sposób hello aplikacji hello przepisy nowej dzierżawy. Wszelkie zmiany wprowadzone za*basetenantdb* są stosowane tooany nowi dzierżawcy elastycznie później. Zobacz hello [samouczek Zarządzanie schematami](sql-database-saas-tutorial-schema-management.md) toosee jak zmiany schematu toomake zbyt*istniejących* dzierżawy baz danych (łącznie hello *basetenantdb* bazy danych).

## <a name="simulate-usage-on-all-tenant-databases"></a>Symulowanie użycia we wszystkich baz danych dzierżaw

Witaj *PerformanceMonitoringAndManagement.ps1 pokaz* skryptów jest pod warunkiem że symuluje pracą dzierżawy w przypadku wszystkich baz danych. obciążenia Hello jest generowana z użyciem jednego ze scenariuszy dostępnych obciążenia hello:

| Demonstracja | Scenariusz |
|:--|:--|
| 2 | Generowanie obciążenia o normalnym natężeniu (ok. 40 jednostek DTU) |
| 3 | Generowanie obciążenia z dłuższymi i częstszymi skokami wartości dla każdej bazy danych|
| 4 | Generowanie obciążenia o wyższych skokach wartości DTU dla każdej bazy danych (ok. 80 jednostek DTU)|
| 5 | Generowanie normalnego obciążenia oraz wysokiego obciążenia dla jednej dzierżawy (ok. 95 jednostek DTU)|
| 6 | Generowanie niezrównoważonego obciążenia dla wielu pul|

generator obciążenia Hello stosuje *syntetycznych* obciążenia procesora CPU — tylko do tooevery dzierżawcy w bazie danych. Hello generator uruchamia zadanie dla każdego dzierżawcy bazy danych, która wywołuje procedurę przechowywaną okresowo generujący hello obciążenia. poziomy obciążenia Hello (w jednostkach Edtu), czas trwania i interwały są różne dla wszystkich baz danych, symulując dzierżawy nieprzewidywalne działanie.

1. Otwórz... \\Modułów uczenia\\zarządzania i monitorowania wydajności\\*PerformanceMonitoringAndManagement.ps1 pokaz* w hello *PowerShell ISE*. Nie zamykaj tego skryptu, gdyż w ramach tego samouczka będzie konieczne uruchomienie kilku scenariuszy.
1. Ustaw **$DemoScenario** = **2**, *Generuj normalnym natężeniu obciążenia*.
1. Naciśnij klawisz **F5** tooapply tooall obciążenia dzierżawcy baz danych.

Wingtip jest to aplikacja SaaS i hello rzeczywiste obciążenie aplikacji SaaS jest zazwyczaj sporadyczne i nieprzewidywalny. toosimulate to tworzy generator obciążenia hello losowego obciążenia dystrybuowana do wszystkich dzierżawców. Kilka minut są wymagane dla hello tooemerge wzorzec obciążenia, więc Uruchom generator obciążenia hello 3 – 5 minut przed podjęciem próby wykonania toomonitor obciążenia hello hello następujące sekcje.

> [!IMPORTANT]
> generator obciążenia Hello jest uruchomiona jako serię zadań w lokalnej sesji programu PowerShell. Zachowaj hello *PerformanceMonitoringAndManagement.ps1 pokaz* Otwórz kartę! Jeśli zamknąć kartę hello lub zawiesić komputera, zatrzymuje hello generator obciążenia. generator obciążenia Hello pozostaje w *wywoływania zadania* stanu, w którym generuje obciążenie nowi dzierżawcy, które są udostępniane po rozpoczęciu hello generator. Użyj *Ctrl-C* toostop wywoływania nowe zadania i zakończenia hello skryptu. generator obciążenia Hello będzie toorun, ale tylko na istniejących dzierżawców.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Monitorowanie użycia zasobów przy użyciu hello portalu Azure

użycie zasobów hello toomonitor, że załadowane wyniki z hello są stosowane, otwórz hello portalu toohello puli zawierającej hello dzierżawcy z bazy danych:

1. Otwórz hello [portalu Azure](https://portal.azure.com) i Przeglądaj toohello *tenants1 -&lt;użytkownika&gt;*  serwera.
1. Przewiń w dół, zlokalizuj elastyczne pule i kliknij pozycję **Pool1**. Ta pula zawiera wszystkie hello dzierżawy bazy danych utworzono dotychczas.

Obserwować hello **monitorowania puli elastycznej** i **elastycznej bazy danych monitorowania** wykresów.

Witaj puli użycie zasobów jest hello użycie agregacji bazy danych dla wszystkich baz danych w puli hello. Wykres bazy danych Hello pokazuje hello pięć najnowszych baz danych:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Ponieważ istnieją dodatkowych baz danych w puli hello poza hello pięciu top, wykorzystania puli hello zawiera działanie, które nie zostanie uwzględniony w hello top pięć baz danych wykresu. Aby uzyskać więcej informacji, kliknij przycisk **wykorzystania zasobów bazy danych**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Ustawianie alertów wydajności na powitania puli

Ustawić alert puli hello, które wyzwala na \>75% wykorzystania w następujący sposób:

1. Otwórz *Pool1* (na powitania *tenants1 -\<użytkownika\>*  serwera) w hello [portalu Azure](https://portal.azure.com).
1. Kliknij pozycję **Reguły alertów**, a następnie kliknij przycisk **+ Dodaj alert**:

   ![dodawanie alertu](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Podaj nazwę, taką jak **Wysoki poziom jednostek DTU**,
1. Ustaw hello następujące wartości:
   * **Metryka = Procent eDTU**
   * **Warunek = większa niż**.
   * **Próg = 75**.
   * **Okres = za pośrednictwem hello ostatnich 30 minut**.
1. Dodaj toohello adres e-mail *email(s) dodatkowe administratora* polu i kliknij przycisk **OK**.

   ![ustawianie alertu](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Skalowanie mocno obciążonej puli w górę

Jeśli poziom agregacji obciążenia hello zwiększa się w punkcie toohello puli maxes limit puli hello i osiągnie użycie w jednostkach eDTU 100%, wydajność jedna baza danych ma wpływ i potencjalnie spowalniając czas odpowiedzi na zapytania dla wszystkich baz danych w puli hello.

**Krótka termin**, należy wziąć pod uwagę skalowaniu hello puli tooprovide dodatkowe zasoby lub usuwanie baz danych z puli hello (przenoszenia ich pule tooother lub poza hello puli tooa autonomicznej usługi warstwy).

**Dłuższym okresie**, należy wziąć pod uwagę optymalizacji zapytań lub indeksu użycia tooimprove bazy danych wydajności. W zależności od hello aplikacji czułości tooperformance problemy z jego najlepszych praktyk tooscale puli się przed jego użycie w jednostkach eDTU 100%. Użyj toowarn alertu należy wcześniej.

Można symulować puli zajęty przez zwiększania obciążenia hello utworzonego przez hello generator. Powoduje hello tooburst baz danych częściej i hello dłużej, zwiększa obciążenie agregacji w puli hello bez zmiany wymagań hello hello pojedynczych baz danych. Skalowanie w górę puli hello łatwo odbywa się w portalu hello lub z programu PowerShell. Tego ćwiczenia używa hello portalu.

1. Ustaw *$DemoScenario* = **3**, _obciążenia Generuj z dłużej i częstsze seria na bazę danych_ tooincrease intensywność hello hello agregacji obciążenie Pula Hello bez zmiany obciążenia szczytowego hello wymagane przez każdą bazę danych.
1. Naciśnij klawisz **F5** tooapply tooall obciążenia dzierżawcy baz danych.

1. Przejdź za**Pool1** w hello portalu Azure.

Monitor hello zwiększone użycie w jednostkach eDTU puli na wykresie górny hello. Zajmuje kilka minut, aż hello nowe wyższe obciążenie tookick, ale powinny pojawić szybko rozpocząć toohit maksymalnego wykorzystania puli hello, a jako obciążenia hello steadies do hello nowy wzorzec, szybko overloads hello puli.

1. tooscale się puli powitania kliknij **Konfigurowanie puli** u góry hello hello **Pool1** strony.
1. Dostosuj hello **eDTU puli** ustawienie zbyt**100**. Zmiana liczby jednostek eDTU puli hello nie ustawień hello na bazę danych (co jest nadal 50 eDTU max na bazę danych). Można wyświetlić ustawienia na bazę danych hello na powitania po prawej stronie powitania **Konfigurowanie puli** strony.
1. Kliknij przycisk **zapisać** toosubmit hello żądania tooscale hello puli.

Wróć za**Pool1** > **omówienie** hello tooview monitorowania wykresy. Monitorowanie efektu hello zapewnienia puli hello więcej zasobów (chociaż z kilku baz danych i losowego obciążenia nie zawsze jest łatwe toosee ostatecznie dopóki nie zostanie uruchomione przez pewien czas). Podczas poszukujesz opatrzone wykresy hello pamiętać niż 100% na powitania górny teraz wykresu reprezentuje 100 jednostek Edtu, na powitania niższe wykresu 100% jest nadal jako hello 50 jednostek Edtu na bazę danych max jest nadal Edtu 50.

Bazy danych nadal online i w pełni dostępne w trakcie procesu hello. W hello moment ostatniego każda baza danych jest gotowy toobe włączyć hello nowych jednostek eDTU puli, wszystkie aktywne połączenia są uszkodzone. Kod aplikacji zawsze powinna być zapisana połączeń tooretry porzucony i nawiąże toohello hello skalowanych puli bazy danych.

## <a name="load-balance-between-pools"></a>Równoważenie obciążenia między zestawami

Jako alternatywne tooscaling zapasowej puli hello. Utwórz pulę drugi i przenoszenia baz danych do niego toobalance hello obciążenia między Witaj dwie pule. toodo hello nowej puli muszą być utworzone na tym samym serwerze co hello hello najpierw..

1. W hello [portalu Azure](https://portal.azure.com), otwórz hello **tenants1 -&lt;użytkownika&gt;**  serwera.
1. Kliknij przycisk **+ nowej puli** toocreate puli na powitania bieżącego serwera.
1. Na powitania **elastycznej puli baz danych** szablonu:

    1. Ustaw **nazwa** za*Pool2*.
    1. Pozostaw hello cenowym jako **puli standardowej**.
    1. Kliknij przycisk **Konfiguruj pulę**,
    1. Ustaw **eDTU puli** za*50 eDTU*.
    1. Kliknij przycisk **dodać bazy danych** toosee listy baz danych na serwerze hello, w którym można dodać zbyt*Pool2*.
    1. Wybierz wszystkie toomove 10 bazach danych tych toohello nowej puli, a następnie kliknij przycisk **wybierz**. Jeśli działała generator obciążenia hello, usługa hello już wie, że profilu wydajności wymaga puli większy niż rozmiar 50 eDTU domyślne hello i zaleca się, począwszy od 100 ustawienia liczby jednostek eDTU.

    ![Zalecenia](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. W tym samouczku, pozostaw domyślne hello Edtu 50, a następnie kliknij przycisk **wybierz** ponownie.
    1. Wybierz **OK** toocreate hello nowej puli i toomove hello wybrane baz danych do niego.

Tworzenie puli hello i przenoszenie baz danych hello zajmuje kilka minut. Jak przenoszeniu baz danych pozostają online i jest całkowicie dostępny do hello ostatnio moment, w którym wszystkie otwarte połączenia są zamykane. Tak długo, jak długo mają niektóre logika ponowień, klienci będą następnie łączyć bazy danych toohello w nowej puli hello.

Przeglądaj zbyt**Pool2** (na powitania *tenants1* serwera) tooopen hello puli i monitorować jego wydajność. Jeśli nie widzisz, poczekaj, aż Inicjowanie obsługi administracyjnej nowych toocomplete puli hello.

Pojawi się że użycie zasobów na *Pool1* spadła oraz że *Pool2* podobnie jest załadowane.

## <a name="manage-performance-of-a-single-database"></a>Zarządzanie wydajności pojedynczej bazy danych

Jeśli długoterminowa wysokie obciążenie, w zależności od konfiguracji puli hello, napotyka pojedynczej bazy danych w puli może często toodominate hello zasobów w puli hello i mieć wpływ na inne bazy danych. Działanie hello jest prawdopodobnie toocontinue przez pewien czas, hello bazy danych można tymczasowo przeniesiony poza hello puli. Dzięki temu hello bazy danych toohave hello dodatkowe zasoby musi i izoluje go z hello innych baz danych.

Tego ćwiczenia symuluje efekt hello Hall porozumieniu firmy Contoso, u których występują znaczne obciążenie biletów Przejdź w sprzedaży dla popularnych uzgodnieniu.

1. Otwórz hello... \\ *PerformanceMonitoringAndManagement.ps1 pokaz* skryptu.
1. Ustaw wartość zmiennej **$DemoScenario = 5, Generate a normal load plus a high load on a single tenant (approx. 95 DTU)** (Generowanie normalnego obciążenia oraz wysokiego obciążenia dla jednej dzierżawy (ok. 95 jednostek DTU)).
1. Ustaw wartość zmiennej **$SingleTenantDatabaseName = contosoconcerthall**
1. Wykonywanie za pomocą skryptu hello **F5**.


1. W hello [portalu Azure](https://portal.azure.com) Otwórz **Pool1**.
1. Sprawdź hello **monitorowania puli elastycznej** wykresu i poszukaj hello zwiększone użycie w jednostkach eDTU puli. Po minucie lub dwóch większych obciążeń hello powinien rozpocząć tookick w i powinny zostać wyświetlone trafienia w puli hello 100% wykorzystania.
1. Sprawdź hello **elastycznej bazy danych monitorowania** wyświetlania, który pokazuje hello najnowszych baz danych w hello ostatniej godziny. Witaj *contosoconcerthall* bazy danych wkrótce powinny się wyświetlać jako jedną z hello pięć najnowszych baz danych.
1. **Kliknij pozycję Monitorowanie elastycznej bazy danych hello** **wykresu** i otwiera hello **wykorzystania zasobów bazy danych** strony, których można monitorować żadnej z hello baz danych. W ten sposób można odizolować hello wyświetlanej hello *contosoconcerthall* bazy danych.
1. Z listy hello baz danych, kliknij przycisk **contosoconcerthall**.
1. Kliknij przycisk **warstwy cenowej (skala Dtu)** tooopen hello **skonfigurować wydajności** strony, w którym można ustawić poziomu wydajności autonomiczne hello bazy danych.
1. Polecenie hello **standardowe** karcie Opcje skali hello tooopen w warstwie standardowa hello.
1. Slajd hello **jednostek dtu w warstwie suwaka** tooright tooselect **100** Dtu. Uwaga odpowiada cel usługi toohello, **S3**.
1. Kliknij przycisk **Zastosuj** toomove hello bazy danych z puli hello i zapewnić ich *standardowa S3* bazy danych.
1. Po zakończeniu skalowanie jest Ukończ, monitor hello wprowadzone w bazie danych contosoconcerthall hello i Pool1 na powitania elastycznej bloków puli i bazy danych.

Po zaspokojenie hello wysokie obciążenie bazy danych contosoconcerthall hello należy niezwłocznie powraca tooreduce puli toohello kosztów. Jeśli nie jest jasne podczas którego nastąpi można ustawić alert w bazie danych hello który zostanie wyzwolone w momencie jego użycie jednostek DTU spadnie poniżej hello na bazę danych max na powitania puli. Przenoszenie bazy danych do puli opisano w ćwiczeniu 5.

## <a name="other-performance-management-patterns"></a>Inne wzorce zarządzania wydajnością

**Skalowanie uprzedzające** w według powyższego ćwiczenia hello, gdzie zostały przedstawione w sposób tooscale izolowanej bazy danych, możesz wiedziały toolook bazy danych, które dla. Jeśli zarządzanie hello Hall porozumieniu Contoso poinformowała Wingtips hello zbliżającym się sprzedaży biletów, hello bazy danych może zostały usunięte z puli hello pre-emptively. W przeciwnym razie go prawdopodobnie wymagałoby alert w puli hello lub hello toospot bazy danych została co dzieje. Nie ma toolearn na ten temat z hello innych dzierżaw w hello puli strona skarżąca obniżeniem wydajności. A jeśli dzierżawy hello można przewidzieć, jak długo będą potrzebne dodatkowe zasoby Konfigurowanie usługi Automatyzacja Azure runbook toomove hello bazy danych z puli hello i następnie z powrotem w zdefiniowanym harmonogramem.

**Skalowanie samoobsługi dzierżawy** ponieważ skalowanie jest łatwo wywoływana za pośrednictwem interfejsu API zarządzania hello zadania, można łatwo wbudowanie możliwości hello tooscale dzierżawcy z bazy danych w aplikacji uwzględniającym dzierżawy i użyć funkcji usługi SaaS. Na przykład zezwolić dzierżaw self-administer skalowanie w górę i w dół, prawdopodobnie połączone bezpośrednio rozliczeń tootheir!

**Skalowanie puli w górę i w dół wzorce użycia toomatch harmonogramu**

W przypadku, gdy użycie agregacji dzierżawy następuje wzorców użycia przewidywalne, można tooscale usługi Automatyzacja Azure puli górę i w dół zgodnie z harmonogramem. Na przykład pulę można skalować w dół po godzinie 18:00 i ponownie w górę przed godziną 6:00 w dni robocze, jeśli wiadomo, że pomiędzy tymi godzinami występuje spadek wymagań dotyczących zasobów.



## <a name="next-steps"></a>Następne kroki

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Symulowanie użycia baz danych dzierżawy hello uruchamiając generator podana obciążenia
> * Monitor hello dzierżawy baz danych, ponieważ one odpowiadać toohello wzrost obciążenia
> * Skalowanie w górę hello elastycznej puli w odpowiedzi toohello zwiększona bazy danych obciążenia
> * Obsługi administracyjnej drugiego puli elastycznej tooload saldo hello działania bazy danych

[Samouczek przywracania pojedynczej dzierżawy](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Dodatkowe zasoby

* Dodatkowe [samouczki, które zależą od hello wdrażanie aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Pule elastyczne SQL](sql-database-elastic-pool.md)
* [Azure Automation](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) — samouczek konfigurowania usługi Log Analytics i korzystania z niej
