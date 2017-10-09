---
title: "aaaAzure pakiet IoT połączone fabryki omówienie | Dokumentacja firmy Microsoft"
description: "Opis hello pakiet IoT Azure połączone fabryki wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Rozpoczynanie pracy z hello połączone fabryki wstępnie skonfigurowane rozwiązanie

Pakiet Azure IoT [wstępnie rozwiązań] [ lnk-preconfigured-solutions] łączenie wielu Azure IoT usług toodeliver end-to-end rozwiązania, które implementuje typowych scenariuszy biznesowych IoT. Witaj *połączonych fabryki* wstępnie skonfigurowane rozwiązanie łączy monitorów tooand przemysłowych urządzeń. Możesz użyć hello rozwiązania tooanalyze hello strumienia danych z urządzenia i wydajności operacyjnej toodrive i rentowność.

W tym samouczku przedstawiono sposób tooprovision hello połączenia fabryki wstępnie skonfigurowane rozwiązanie. On również przeprowadzi Cię przez hello podstawowych funkcji hello wstępnie skonfigurowane rozwiązanie. Dostępne wiele z tych funkcji z rozwiązania hello *pulpitu nawigacyjnego* która wdraża jako część rozwiązania hello wstępnie skonfigurowane:

![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania połączonej fabryki][img-cf-home]

toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.

> [!NOTE]
> Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].
> 
> 

## <a name="provision-hello-solution"></a>Zainicjuj obsługę hello rozwiązania

1. Zaloguj się przy użyciu poświadczeń konta Azure tooazureiotsuite.com, a następnie kliknij przycisk "**+**" toocreate rozwiązania.
2. Kliknij przycisk **wybierz** na powitania **połączonych fabryki** kafelka.
3. W polu **Nazwa rozwiązania** wprowadź nazwę wstępnie skonfigurowanego rozwiązania dla połączonej fabryki.
4. Wybierz hello **subskrypcji** i **Region** toouse tooprovision hello rozwiązanie.
5. Kliknij przycisk **Utwórz rozwiązanie** hello toobegin w procesie inicjowania obsługi. Ten proces zwykle trwa kilka minut toorun.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>Podczas oczekiwania na powitania inicjowania obsługi administracyjnej toocomplete procesu

1. Kliknij Kafelek hello rozwiązania z **inicjowania obsługi administracyjnej** stanu.
2. Powiadomienie hello **inicjowania obsługi administracyjnej stanów** podczas wdrażania usług platformy Azure w ramach subskrypcji platformy Azure.
3. Po ukończeniu inicjowania obsługi administracyjnej hello zmiany stanu zbyt**gotowe**.
4. Kliknij przycisk hello kafelka toosee hello szczegóły rozwiązania w okienku po prawej stronie powitania.

> [!NOTE]
> Jeśli wystąpią problemy dotyczące wdrażania rozwiązania hello wstępnie skonfigurowane, przejrzyj [uprawnienia w witrynie azureiotsuite.com hello] [ lnk-permissions] i hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md). Jeśli hello problemy będą się powtarzać, Utwórz biletu usługi na powitania [portal][lnk-portal].

Czy istnieją szczegółowe informacje można oczekiwać toosee, które nie są wyświetlane dla rozwiązania? Prześlij nam swoje propozycje dotyczące funkcji, korzystając ze strony [User Voice](https://feedback.azure.com/forums/321918-azure-iot) (Opinie użytkowników).

## <a name="scenario-overview"></a>Omówienie scenariusza

Podczas wdrażania hello połączone fabryki wstępnie skonfigurowane rozwiązanie, jest on wstępnie wypełnione zasobów umożliwiających toostep za pośrednictwem typowy scenariusz przemysłowych. W tym scenariuszu kilka fabryki połączony raport rozwiązania toohello hello danych wartości wymagane toocompute ogólnej wydajności sprzętu (OEE) oraz kluczowych wskaźników wydajności (KPI). Hello następnych sekcjach opisano sposób do:

* Monitorowanie fabryki, linii produkcyjnych, ogólnej wydajności stacji i wartości kluczowych wskaźników wydajności.
* Analizowanie danych telemetrycznych hello wygenerowane z tych urządzeń przy użyciu usługi Azure czas serii Insights
* Działania dotyczące problemów toofix alertów

Kluczowy element w tym scenariuszu jest, że te akcje można wykonać zdalnie z poziomu pulpitu nawigacyjnego hello rozwiązania. Nie trzeba urządzeń toohello fizyczny dostęp.

## <a name="view-hello-solution-dashboard"></a>Pulpit nawigacyjny rozwiązania hello widoku

pulpit nawigacyjny rozwiązania Hello umożliwia toomanage hello wdrożyć rozwiązanie. Jest to hierarchiczna reprezentacja globalnej konfiguracji fabryki. Można na przykład wyświetlić ogólną wydajność sprzętu oraz kluczowe wskaźniki wydajności, opublikować nowe węzły na potrzeby telemetrii i reagować na alerty.

1. Po ukończeniu inicjowania obsługi administracyjnej hello i wskazuje hello Kafelek wstępnie skonfigurowane rozwiązanie **gotowe**, wybierz **uruchamianie** tooopen portalem rozwiązania połączonych fabryki na nowej karcie.

    ![Uruchamianie hello wstępnie skonfigurowane rozwiązanie][img-launch-solution]

1. Domyślnie hello rozwiązanie portalu pokazuje hello *pulpitu nawigacyjnego*. obszary tooother toonavigate hello portalu, użyj hello menu na powitania po lewej stronie powitania strony.

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania połączonej fabryki][cf-img-menu]

pulpit nawigacyjny Hello Wyświetla hello następujących informacji:

* A **listy fabryki** panelu, pokazujący stan hello, lokalizacji i bieżącej konfiguracji produkcji hello rozwiązania. Przy pierwszym uruchomieniu rozwiązania hello, istnieje wiele urządzeń symulowane. Symulacja wiersza produkcyjnym Hello składa się z trzech rzeczywistych OPC UA serwerom na linii produkcyjnej symulowane zadań i udostępnianie danych. Aby uzyskać więcej informacji na temat OPC UA Zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).
* A **mapy** czy lokalizacji hello Wyświetla wszystkie urządzenia podłączone toohello rozwiązania. rozwiązanie Hello można użyć informacji tooplot interfejsu API map Bing hello na mapie hello. Jeśli subskrypcja obejmuje interfejs API usługi Mapy Bing w wersji Enterprise, ta funkcja jest używana automatycznie. Jeśli nie, zobacz hello [— często zadawane pytania] [ lnk-faq] toolearn jak toomake hello dynamicznie mapy.
* Panel **Alerty**, na którym są wyświetlane alerty generowane, gdy wartość telemetrii lub ogólnej wydajności sprzętu bądź kluczowego wskaźnika wydajności przekroczy określony próg.
* **Ogólnej wydajności sprzętu** panelu, które pokazuje hello OEE wartości dla całego przedsiębiorstwa hello lub hello fabryki/produkcji wiersza/stacji można jest wyświetlana. Ta wartość jest agregowana poziomu hello stacji widoku toohello przedsiębiorstwa. Rysunek OEE Hello i jej elementów składowych można analizować dalej.
* **Kluczowe wskaźniki wydajności** panelu, który wyświetla hello liczbę jednostek wyprodukowanych i energii używane przez hello całego przedsiębiorstwa lub wiersza fabryki/produkcyjnego hello stacji można jest wyświetlana. Wartości te są agregowane z poziomu stacji widoku toohello przedsiębiorstwa.

## <a name="view-factories"></a>Wyświetlanie fabryk

Witaj *fabryki* panelu pokazuje hello lokalizację geograficzną wszystkich fabryki hello w hello rozwiązania, stanu i bieżącej konfiguracji produkcji. Z listy lokalizacje hello można przejść toohello innych poziomów w hierarchii rozwiązania hello. Wiersze Hello liście hello są hiperłącza, które łącze Szczegóły hello produkcji wiersze w tej lokalizacji. Następnie jest możliwe toodrill do hello szczegóły wiersza produkcyjnym i w dół widok poziomu toohello stacji. Można także zastosować dla listy toohello filtrów.

![Fabryki we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-factories] 

1. Witaj **panelu fabryki** pokazuje hello listy fabryki dla tego rozwiązania.

2. Lista fabryki Hello początkowo zawiera sześć fabryki utworzone przez hello w procesie inicjowania obsługi. Można dodać dodatkowych urządzeń fizycznych i symulowane toohello rozwiązania.

3. Szczegóły hello tooview fabryki, kliknij wiersz hello hello fabryki liście.

4. tooview hello szczegóły wiersza produkcyjnym, kliknij wiersz hello hello na liście.

5. tooview hello opublikowane węzłów OPC UA stacji na linii produkcyjnej hello, kliknij wiersz hello liście hello.

6. Szczegóły tooview w określonym węźle w stacji hello, kliknij wiersz hello hello na liście. Ta akcja spowoduje uruchomienie hello kontekstu panel z wizualizacji Insights serii czasu. Kliknij te wykresy toodo dalszej analizy w środowisku explorer Insights serii czasu hello.

## <a name="view-map"></a>Wyświetlanie mapy

Jeśli subskrypcja obejmuje toohello dostępu do interfejsu API map Bing, hello *fabryki* Mapa pokazuje hello lokalizacji geograficznej i stan fabryk hello w hello rozwiązania. toodrill hello lokalizacji uzyskać szczegółowe informacje, kliknij przycisk Lokalizacje hello wyświetlone na mapie hello.

![Mapa we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-map]

## <a name="view-alerts"></a>Wyświetlanie alertów

Witaj **alertu** panelu przedstawia alerty generowane ze względu tooa podać wartość lub obliczoną wartość OEE/KPI przekroczeniu skonfigurowanego progu. Panel ten przedstawia alerty na każdym poziomie hierarchii hello, w widoku globalnego toohello hello stacji widoku poziomu. alerty Hello zawierają opis alertu hello, datę, czas, lokalizacji i liczby wystąpień. Aby uzyskać wgląd w dane toohello, który spowodował alert hello przy użyciu hello czasu Insights serii danych. Hello Insights serii czas, który wizualizacji danych w hello alerty, jeśli to możliwe. Jeśli jesteś administratorem, można wykonać akcje domyślne hello alertów, takie jak:

* Witaj Zamknij alert.
* Wiadomości powitania alertu.

Opcjonalnie możesz wykonać bardziej złożone akcje. Na przykład dla hello wykorzystania OPC UA węzła hello zestawu możesz:

* Wyświetlenie dodatkowych informacji na stronie internetowej w nowym oknie przeglądarki.
* Ograniczenia hello Przyczyna alertu hello przez wywołanie metody OPC UA hello urządzenia.
* Pomiń hello dostępność hello domyślne akcje.

    ![Alerty we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alerts]

> [!NOTE]
> Te alerty są generowane przez zasady, które są określone w pliku konfiguracji w hello wstępnie skonfigurowane rozwiązanie. Te reguły mogą generować alerty, gdy hello OEE lub wartości wskaźnika KPI lub wartości węzła UA OPC są powyżej ich skonfigurowany próg.

1. Witaj **panelu alerty** pokazuje hello alertów wygenerowanych w tym rozwiązaniu.

2. tooview hello szczegóły alertu, kliknij alert hello hello alerty panelu.

3. toofurther analizować dane alertów hello, kliknij wykres hello hello alertu panelu tooopen hello czasu serii Insights explorer środowiska.

4. tooaddress hello alertu, kilka akcje są dostępne w panelu alertu hello. Wybierz odpowiednią opcję powitania dla Ciebie, a następnie kliknij przycisk hello wykonania akcji przycisku polecenia.

## <a name="view-overall-equipment-efficiency"></a>Wyświetlanie ogólnej wydajności sprzętu

Stawki OEE hello wydajności proces produkcji hello przy użyciu klucza parametry operacyjne dotyczące produkcji. OEE jest branżowy standard miary obliczane przez pomnożenie hello dostępności szybkości, współczynnik wydajności i jakości szybkość: OEE = dostępności x jakości wydajności x.

![Ogólna wydajność sprzętu we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-oee]

1. tooview OEE dla dowolnego poziomu w hierarchii hello Przejdź toohello określony widok, które są wymagane. Witaj OEE w tym widoku są wyświetlane w panelu hello wraz z każdego z elementów hello, wchodzące w skład hello OEE procent.

2. toofurther analizowanie hello OEE na dowolnym poziomie hello hierarchii danych, kliknij przycisk hello OEE, dostępności, wydajności i jakości procent. Kontekst pojawia się okno z informacjami dotyczącymi serii czasu zasilanego wizualizacje, które zawiera dane ze hello w ciągu ostatniej godziny, ostatnich 24 godzinach i ostatnich 7 dni.

    ![Wizualizacje usługi TSI we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-tsi-visualization]

3. toofurther analizować dane alertów hello, kliknij wykres hello w panelu alertu hello. Ta akcja powoduje otwarcie hello czasu serii Insights explorer środowiska.

    ![Eksplorator usługi TSI we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Wyświetlanie kluczowych wskaźników wydajności

Witaj rozwiązanie zapewnia dwie kluczowe wskaźniki wydajności, *jednostek na godzinę* i *zużycia energii w kWh*.

![Kluczowy wskaźnik wydajności we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-kpi]

1. jednostki tooview na godzinę lub energii użytej do dowolnego poziomu hierarchii hello Przejdź toohello określony widok, które są wymagane. jednostki Hello na godzinę i energii używane wyświetlania hello panelu.

2. jednostki tooanalyze na godzinę lub energii użytej do dowolnego poziomu hierarchii hello co więcej, kliknij przycisk miernika hello w hello **kluczowych wskaźników wydajności** panelu. Pojawia się, że okno kontekstu z wizualizacjami Insights serii czasu zasilane umożliwiając tooview danych z hello ostatniej godziny hello w ostatnich 24 godzinach i w ciągu ostatnich 7 dni.

## <a name="scenario-review"></a>Przegląd scenariusza

W tym scenariuszu można monitorować fabryki OEE i wskaźników KPI wartości, na pulpicie nawigacyjnym hello. Następnie użyto tooprovide Insights serii czasu więcej informacji toohelp Przejdź dalej do hello dane telemetryczne dla toohelp OEE i wskaźników KPI z wykrywania anomalii. Problemy tooview alertu panelu hello również używać razem z fabryki i użyto hello Akcje dostępne tooyou tooresolve hello alertu.

## <a name="other-features"></a>Pozostałe funkcje

Hello w następujących sekcjach opisano niektóre dodatkowe funkcje, które nie zostały opisane w poprzednim scenariuszu hello hello połączone fabryki rozwiązania.

## <a name="apply-filters"></a>Stosowanie filtrów

1. Kliknij przycisk hello **cudzysłów ostrokątny** toodisplay listę dostępnych filtrów w panelu lokalizacje fabryki hello lub hello alerty panelu.

2. panel Filtry Hello jest wyświetlany dla Ciebie. 

    ![Filtry we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alert-filter]

3. Wybierz filtr hello, która jest wymagana. Możliwe jest również możliwe tootype niezależnych do pól filtr hello.

4. Filtr Hello jest następnie stosowany dla Ciebie. Stan filtru Hello jest także pokazany na pulpicie nawigacyjnym hello za pośrednictwem lejka, która wyświetla w hello fabryk i alerty tabel.

    ![Filtry we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Filtra aktywnego nie ma wpływu na powitania wyświetlane wartości OEE i kluczowego wskaźnika wydajności, tylko filtry hello wyświetlanie zawartości.

5. tooclear filtra, kliknij lejka hello i kliknij filtr w panelu kontekstu filtr hello. Witaj tekst **wszystkie** jest wyświetlana w hello fabryk i alerty tabel.

## <a name="browse-an-opc-ua-server"></a>Przeglądanie serwera OPC UA

Podczas wdrażania hello wstępnie skonfigurowane rozwiązanie automatycznie udostępnić symulowane serwerów OPC UA, które można przeglądać za pomocą przeglądarki rozwiązania hello. Są to *symulowane serwery OPC UA*. Serwery symulowane ułatwiają dla Ciebie tooexperiment z rozwiązaniem hello wstępnie bez hello potrzeby toodeploy prawdziwe, fizycznych serwerów. Tooconnect rzeczywiste rozwiązania toohello OPC UA serwera, zobacz hello [łączenie rozwiązania fabryki wstępnie toohello podłączone urządzenie OPC UA] [ lnk-connect-cf] samouczka.

1. Kliknij hello **ikona fabryki** na pasku nawigacyjnym hello pulpitu nawigacyjnego.

    ![Przeglądarka serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-browser]

2. Wybierz jeden z serwerów hello hello wstępnie skonfigurowanej listy. Ta lista zawiera serwery hello, które są wdrażane dla Ciebie w hello wstępnie skonfigurowane rozwiązanie.

    ![Wybieranie serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-choice]

3. Kliknij przycisk **Połącz**. Zostanie wyświetlone okno dialogowe zabezpieczeń. Na symulacyjnych hello jest bezpieczne tooclick **Kontynuuj**

4. tooexpand dowolny z węzłów hello powitania serwera drzewa, kliknij go. Węzły, które publikują dane telemetryczne, mają obok swoich nazw znaczniki.

    ![Drzewo serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-tree]

5. Kliknij prawym przyciskiem myszy element tooread, zapisu, publikować lub wywołać tego węzła. tooyou dostępne akcje Hello są zależne od swoje uprawnienia i atrybuty hello hello węzła. Hello odczytać toodisplays opcji panelu kontekstu pokazujący wartość hello hello określonego węzła. Witaj zapisu opcja wyświetla panel kontekstu, gdzie można wprowadzić nową wartość. Opcja wywołania Hello wyświetlany jest węzeł wprowadzane parametry hello hello wywołania.

## <a name="publish-a-node"></a>Publikowanie węzła

Po przejściu *symulowane serwera OPC UA*, można także toopublish nowe węzły. Można analizować dane telemetryczne hello z tych węzłów w rozwiązaniu hello. Te *symulowane serwerów OPC UA* był łatwo tooexperiment z rozwiązaniem hello wstępnie bez wdrażania rzeczywistego urządzenia fizycznego.

1. Przeglądaj tooa węzła w hello OPC UA serwera przeglądarki drzewa, że chcesz toopublish.

2. Kliknij prawym przyciskiem myszy węzeł hello.

3. Wybierz polecenie **Publikuj**.

    ![Publikowanie węzła przez połączoną fabrykę][cf-img-publish-node]

4. Pojawia się okno kontekstu informuje, że hello publikowania zakończyła się pomyślnie. węzeł Hello jest wyświetlany w widoku poziomu stacji hello znacznik wyboru obok siebie.

    ![Pomyślne publikowanie we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-publish-success]

## <a name="command-and-control"></a>Sterowanie i kontrola

Fabryka połączonych Hello umożliwia poleceń i kontroli urządzeń branży bezpośrednio z chmury hello. Możesz użyć tej funkcji tooalerts toorespond, który jest generowany przez urządzenie hello. Na przykład może wysyłać polecenia toohello urządzenia ze hello chmury. Można znaleźć hello dostępnych poleceń w hello **StationCommands** węzła w hello OPC UA serwerów przeglądarki drzewa. W tym scenariuszu możesz otworzyć zawór wersji wykorzystania na stacji zestawu hello wiersza produkcyjnym we Wrocławiu. Funkcje polecenia i kontroli toouse hello, musisz być w hello **administratora** rolę hello wstępnie wdrażania rozwiązania.

1. Przeglądaj toohello **StationCommands** węzła w hello OPC UA serwera przeglądarki drzewa.

2. Wybierz polecenie hello, że chcesz użycia.

3. Kliknij prawym przyciskiem myszy węzeł hello.

4. Wybierz polecenie **Wywołaj**.

    ![Polecenie wywoływania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-command]

5. Panel kontekstu pojawia się informacją, którego metoda zamierzasz toocall i dotyczy żadnych szczegółów parametru.

6. Wybierz polecenie **Wywołaj**.

    ![Kontekst wywołania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-context]

7. panel kontekstu Hello jest zaktualizowane tooinform że hello wywołania metody, które zakończyło się pomyślnie. Możesz sprawdzić hello wywołanie zakończyło się pomyślnie, odczytując wartości hello hello wykorzystania węzła, który zaktualizowany w wyniku wywołania hello.

    ![Powodzenie wywołania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Tle hello

Podczas wdrażania wstępnie skonfigurowanych rozwiązań procesu wdrażania hello tworzy wiele zasobów w hello subskrypcji platformy Azure, które wybrano. Te zasoby można wyświetlić w hello Azure [portal][lnk-portal]. Utworzenie procesu wdrażania Hello **grupy zasobów** o nazwie na podstawie nazwy hello wybierz wstępnie skonfigurowanego rozwiązania:

![Wstępnie skonfigurowane rozwiązanie w hello portalu Azure][img-cf-portal]

Można wyświetlać ustawienia hello każdego zasobu, wybierając ją z listy hello zasobów w grupie zasobów hello.

Można również wyświetlić kod źródłowy hello hello wstępnie skonfigurowane rozwiązanie. Hello połączonych fabryki wstępnie skonfigurowane rozwiązanie kod źródłowy jest w hello [azure iot — połączony fabryka] [ lnk-cfgithub] repozytorium GitHub:

Gdy wszystko będzie gotowe, możesz usunąć hello wstępnie skonfigurowane rozwiązanie z subskrypcją platformy Azure na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji. Ta witryna umożliwia delete tooeasily hello wszystkie zasoby, które zostały udostępnione po utworzeniu hello wstępnie skonfigurowane rozwiązanie.

> [!NOTE]
> tooensure Usuń wszystkie powiązane toohello wstępnie skonfigurowane rozwiązanie, usuń go na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji. Nie należy usuwać hello grupy zasobów w portalu hello.

## <a name="next-steps"></a>Następne kroki

Teraz, po wdrożeniu rozwiązania pracy wstępnie skonfigurowane, można nadal wprowadzenie pakiet IoT odczytując hello następujące artykuły:

* [Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][lnk-rm-walkthrough]
* [Łączenie rozwiązania połączonych fabryki wstępnie toohello urządzenia][lnk-connect-cf]
* [Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md