---
title: "aaaGet pracę z wstępnie rozwiązania | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka toolearn jak toodeploy pakiet IoT Azure wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Rozpoczynanie pracy z rozwiązaniami hello wstępnie

Pakiet Azure IoT [wstępnie rozwiązań] [ lnk-preconfigured-solutions] łączenie wielu Azure IoT usług toodeliver end-to-end rozwiązania, które implementuje typowych scenariuszy biznesowych IoT. Witaj *monitorowania zdalnego* wstępnie skonfigurowane rozwiązanie łączy monitorów tooand urządzenia. Można użyć hello rozwiązania tooanalyze hello strumienia danych z urządzeniami i wyników biznesowych tooimprove poprzez procesy automatycznie odpowiadać toothat strumienia danych.

W tym samouczku przedstawiono sposób monitorowania zdalnego hello tooprovision wstępnie skonfigurowane rozwiązanie. On również przeprowadzi Cię przez hello podstawowych funkcji hello wstępnie skonfigurowane rozwiązanie. Dostępne wiele z tych funkcji z rozwiązania hello *pulpitu nawigacyjnego* która wdraża jako część rozwiązania hello wstępnie skonfigurowane:

![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-dashboard]

toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.

> [!NOTE]
> Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Omówienie scenariusza

Podczas wdrażania hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, jest wypełniana wstępnie zasobów umożliwiających toostep za pośrednictwem zdalnego typowym scenariuszem monitorowania. W tym scenariuszu kilka urządzeń podłączonych toohello rozwiązania są raportowania temperatury nieoczekiwane wartości. Hello następnych sekcjach opisano sposób do:

* Identyfikowanie urządzeń hello wysyłania temperatury nieoczekiwane wartości.
* Skonfiguruj te urządzenia toosend bardziej szczegółowe dane telemetryczne.
* Rozwiąż hello problem przez aktualizację oprogramowania układowego hello na tych urządzeniach.
* Upewnij się, że Twoje działanie zostało rozwiązane hello problem.

Kluczowy element w tym scenariuszu jest, że te akcje można wykonać zdalnie z poziomu pulpitu nawigacyjnego hello rozwiązania. Nie trzeba urządzeń toohello fizyczny dostęp.

## <a name="view-hello-solution-dashboard"></a>Pulpit nawigacyjny rozwiązania hello widoku

pulpit nawigacyjny rozwiązania Hello umożliwia toomanage hello wdrożyć rozwiązanie. Można na przykład wyświetlać dane telemetryczne, dodawać urządzenia i konfigurować reguły.

1. Po ukończeniu inicjowania obsługi administracyjnej hello i wskazuje hello Kafelek wstępnie skonfigurowane rozwiązanie **gotowe**, wybierz **uruchamianie** tooopen zdalnego monitorowania rozwiązania portalem na nowej karcie.

    ![Uruchamianie hello wstępnie skonfigurowane rozwiązanie][img-launch-solution]

1. Domyślnie hello rozwiązanie portalu pokazuje hello *pulpitu nawigacyjnego*. Można przejść obszarów tooother hello rozwiązanie portalu przy użyciu hello menu na powitania po lewej stronie powitania strony.

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-menu]

pulpit nawigacyjny Hello Wyświetla hello następujących informacji:

* Mapy zawiera hello lokalizację każdego urządzenia połączone toohello rozwiązania. Przy pierwszym uruchomieniu rozwiązania hello, istnieją 25 urządzeń symulowane. Witaj symulowanego urządzenia są zaimplementowane jako zadań Webjob Azure, a rozwiązania hello używa informacji tooplot interfejsu API map Bing hello na mapie hello. Zobacz hello [— często zadawane pytania] [ lnk-faq] toolearn jak toomake hello dynamicznie mapy.
* Panel **Historia telemetrii**, na którym są wyświetlane niemal w czasie rzeczywistym dane telemetryczne dotyczące wilgotności i temperatury pochodzące z wybranego urządzenia oraz dane zagregowane, takie jak wilgotność maksymalna, minimalna i średnia.
* Panel **Historia alarmów**, na którym są wyświetlane ostatnie zdarzenia alarmów generowane w przypadku przekroczenia progu przez wartość telemetryczną. W przykładach toohello dodanie utworzone przez hello wstępnie skonfigurowane rozwiązanie można zdefiniować własne alarmy.
* Panel **Zadania**, na którym są wyświetlane informacje o zaplanowanych zadaniach. Własne zadania można zaplanować na stronie **Zadania zarządzania**.

## <a name="view-alarms"></a>Wyświetlanie alarmów

panel Historia alarm Hello pokazuje wyższe niż wartości oczekiwanej telemetrii raportowania pięciu urządzeń.

![Historia TODO Alarm hello pulpit nawigacyjny rozwiązania][img-alarms]

> [!NOTE]
> Alarmy te są generowane przez regułę, która znajduje się w hello wstępnie skonfigurowane rozwiązanie. Ta reguła generuje alert, gdy wartość temperatury hello wysyłanych przez urządzenia przekracza 60. Można zdefiniować własne reguły oraz akcje, wybierając [reguły](#add-a-rule) i [akcje](#add-an-action) w menu po lewej stronie powitania.

## <a name="view-devices"></a>Wyświetlanie urządzeń

Witaj *urządzeń* lista zawiera wszystkie urządzenia hello zarejestrowane w rozwiązaniu hello. Z listy urządzeń hello można wyświetlać i edytować metadane urządzenia Dodaj lub usuń urządzeń i wywołania metod na urządzeniach. Można filtrować i sortować listę hello urządzeń na liście urządzeń hello. Można również dostosować kolumn hello hello listę urządzeń.

1. Wybierz **urządzeń** listę urządzeń hello tooshow dla tego rozwiązania.

   ![Widok listy urządzeń hello hello rozwiązanie portalu][img-devicelist]

1. Lista urządzeń Hello pokazuje początkowo 25 urządzeń symulowane utworzonych przez hello w procesie inicjowania obsługi. Można dodać dodatkowych urządzeń fizycznych i symulowane toohello rozwiązania.

1. Szczegóły hello tooview urządzenia, wybierz urządzenie na liście urządzeń hello.

   ![Wyświetl szczegóły urządzenia hello w portalu rozwiązania hello][img-devicedetails]

Witaj **szczegóły urządzenia** panelu zawiera sześć sekcje:

* Kolekcja łączy włączyć możesz toocustomize hello ikonę urządzenia, wyłączyć urządzenie hello, Dodaj regułę, wywoływanie metody lub wysyłać polecenia. Porównanie poleceń (komunikatów wysyłanych z urządzenia do chmury) i metod (metod bezpośrednich) znajduje się w temacie [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].
* Witaj **dwie urządzenia - tagi** sekcja umożliwia wartości tagów tooedit hello urządzenia. Można wyświetlić wartości tagów w hello listę urządzeń i używać listę urządzeń hello toofilter wartości tagu.
* Witaj **dwie urządzenia - żądanego właściwości** sekcja umożliwia tooset właściwości wartości toobe wysyłane toohello urządzenia.
* Hello **dwie urządzenia - zgłosił właściwości** sekcji przedstawiono wysyłane z urządzenia hello wartości właściwości.
* Witaj **właściwości urządzenia** sekcja zawiera informacje z rejestru tożsamości hello, takie jak urządzenie hello klucze identyfikator i uwierzytelniania.
* Witaj **ostatnich zadań** sekcja zawiera informacje dotyczące zadań, które ostatnio ustawione tego urządzenia.

## <a name="filter-hello-device-list"></a>Lista urządzeń hello filtru

Można użyć tylko te urządzenia, które wysyłają wartości temperatury nieoczekiwany toodisplay filtru. Hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie obejmuje hello **złej kondycji urządzeń** urządzenia tooshow o wartości średnia temperatura przekracza 60 filtrować. Możesz również [utworzyć własne filtry](#add-a-filter).

1. Wybierz **Otwórz zapisany filtr** toodisplay listę dostępnych filtrów. Następnie wybierz pozycję **złej kondycji urządzeń** tooapply hello filtru:

    ![Wyświetl listę hello filtry][img-unhealthy-filter]

1. Lista urządzeń Hello zawiera obecnie tylko urządzenia z wartością średnią temperaturę większa niż 60.

    ![Lista filtrowane urządzeń hello widok przedstawiający złej kondycji urządzenia][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Aktualizowanie żądanych właściwości

Na tym etapie zidentyfikowano zestaw urządzeń, które mogą wymagać naprawy. Jednak zdecydujesz, że częstotliwość danych hello 15 sekund jest niewystarczająca dla wyczyść diagnozy problemu hello. Zmiana hello telemetrii częstotliwość toofive sekund tooprovide z więcej toobetter punktów danych zdiagnozowaniu problemu hello. Ta konfiguracja zmiany tooyour urządzeń zdalnych można wypchnąć hello rozwiązanie portalu. Istnieje możliwość zmiany hello raz, ocenić wpływ hello i działa na powitania wyniki.

Wykonaj te kroki toorun zadanie, które zmienia hello **TelemetryInterval** wymaganą właściwość hello wpływ na urządzenia. Gdy urządzenia hello otrzymują hello nowe **TelemetryInterval** wartość właściwości, zmień ich telemetrii toosend konfiguracji co pięć sekund zamiast co 15 sekund:

1. Gdy hello listę złej kondycji urządzeń są wyświetlane na liście urządzeń hello, wybierz **harmonogramu zadań**, następnie **Edytuj dwie urządzenia**.

1. Wywołanie zadania hello **interwał telemetrii zmiany**.

1. Zmień wartość hello hello **żądanej właściwości** nazwa **żądany. Config.TelemetryInterval** toofive sekund.

1. Wybierz pozycję **Zaplanuj**.

    ![Zmień hello TelemetryInterval właściwości toofive sekund][img-change-interval]

1. Możesz monitorować postęp hello zadania hello na powitania **zadań zarządzania** w portalu hello na stronie.

> [!NOTE]
> Toochange wartość żądanej właściwości dla poszczególnych urządzeń, należy użyć hello **odpowiednie właściwości** części hello **szczegóły urządzenia** panelu zamiast uruchamiania zadania.

To zadanie ustawia wartość hello hello **TelemetryInterval** wymaganą właściwość w Witaj dwie urządzenia dla wszystkich hello urządzenia wybrane przez filtr hello. urządzenia Hello pobierania tej wartości ze Witaj dwie urządzenia i zaktualizować ich zachowanie. Gdy urządzenie pobiera i przetwarza żądaną właściwość z dwie urządzenia, ustawia hello odpowiadającej podanej wartości właściwości.

## <a name="invoke-methods"></a>Wywoływanie metod

Podczas wykonywania zadania hello zauważysz hello lista urządzeń zła czy te urządzenia mają stary (mniej niż w wersji 1.6) oprogramowania układowego wersji.

![Wersja oprogramowania układowego hello złej kondycji urządzeń zgłoszonych hello widoku][img-old-firmware]

Ta wersja oprogramowania układowego może być hello głównej przyczyny nieoczekiwanego hello temperatury wartości, ponieważ wiadomo, że inne dobrej kondycji urządzenia były ostatnio zaktualizowano tooversion 2.0. Można użyć wbudowanych hello **starego oprogramowanie układowe urządzeń** filtrować tooidentify wszystkie urządzenia z stare wersje oprogramowania układowego. Z portalu hello można zdalnie zaktualizować wszystkie urządzenia hello nadal działa stare wersje oprogramowania układowego:

1. Wybierz **Otwórz zapisany filtr** toodisplay listę dostępnych filtrów. Następnie wybierz pozycję **starego oprogramowanie układowe urządzeń** tooapply hello filtru:

    ![Wyświetl listę hello filtry][img-old-filter]

1. Lista urządzeń Hello zawiera obecnie tylko urządzenia z stare wersje oprogramowania układowego. Ta lista zawiera pięć urządzeń hello identyfikowane przez hello **złej kondycji urządzeń** filtru oraz trzy dodatkowe urządzenia:

    ![Lista filtrowane urządzeń hello widok przedstawiający starego urządzeń][img-filtered-old-list]

1. Wybierz pozycję **Harmonogram zadań**, a następnie pozycję **Wywołaj metodę**.

1. Ustaw **Nazwa zadania** za**tooversion aktualizacji oprogramowania układowego 2.0**.

1. Wybierz **InitiateFirmwareUpdate** jako hello **metody**.

1. Zestaw hello **FwPackageUri** parametru zbyt**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Wybierz pozycję **Zaplanuj**. domyślne Hello jest teraz dla hello toorun zadania.

    ![Utwórz zadanie tooupdate hello oprogramowanie układowe hello wybrane urządzeń][img-method-update]

> [!NOTE]
> Tooinvoke metody na poszczególne urządzenia, wybierz opcję **metody** w hello **szczegóły urządzenia** panelu zamiast uruchamiania zadania.

To zadanie wywołuje hello **InitiateFirmwareUpdate** metoda bezpośrednia na wszystkich urządzeniach hello wybrane przez filtr hello. Urządzenia reagowanie tooIoT koncentratora i inicjuje proces aktualizacji oprogramowania układowego hello asynchronicznie. urządzenia Hello Podaj informacjami o stanie procesu aktualizacji oprogramowania układowego hello za pomocą wartości właściwości zgłoszone, jak pokazano w powitania po zrzuty ekranu. Wybierz hello **Odśwież** ikona tooupdate hello informacji hello list urządzeń i zadania:

![Listy zadań przedstawiający uruchamianie listy aktualizacji oprogramowania układowego hello][img-update-1]
![listę urządzeń przedstawiający stan aktualizacji oprogramowania układowego][img-update-2]
![listy przedstawiający hello oprogramowania układowego aktualizacji listy zadań ukończone][img-update-3]

> [!NOTE]
> W środowisku produkcyjnym można zaplanować zadania toorun w oknie obsługi wyznaczonych.

## <a name="scenario-review"></a>Przegląd scenariusza

W tym scenariuszu zidentyfikowanego potencjalny problem z niektórych urządzeń zdalnego przy użyciu historii alarm hello na powitania pulpitu nawigacyjnego i filtru. Następnie używane hello filtru i tooremotely zadania skonfigurować hello urządzeń tooprovide więcej informacji o toohelp zdiagnozować problem hello. Na koniec użyto filtr i zadania konserwacji tooschedule na urządzeniach hello, których to dotyczy. Jeśli zwróci toohello pulpitu nawigacyjnego, można sprawdzić, czy nie ma już wszystkie alarmy przesyłanych z urządzeń w rozwiązaniu. Można użyć filtru tooverify, że oprogramowanie układowe hello jest aktualny na wszystkich urządzeniach hello rozwiązania, oraz czy nie ma więcej złej kondycji urządzeń:

![Filtr przedstawiający, że wszystkie urządzenia mają aktualne oprogramowanie układowe][img-updated]

![Filtr przedstawiający, że wszystkie urządzenia są w dobrej kondycji][img-healthy]

## <a name="other-features"></a>Pozostałe funkcje

Witaj poniższych sekcjach opisano niektóre dodatkowe funkcje hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, które nie zostały opisane w ramach hello poprzednim scenariuszu.

### <a name="customize-columns"></a>Dostosowywanie kolumn

Można dostosować hello informacje wyświetlane na liście urządzeń hello, wybierając **Edytor kolumn**. Istnieje możliwość dodawania i usuwania kolumn, w których są wyświetlane zgłaszane wartości właściwości i tagów. Można również zmieniać kolejność kolumn i ich nazwy:

   ![Lista urządzeń hello zakres przechowywania Edytor kolumny][img-columneditor]

### <a name="customize-hello-device-icon"></a>Dostosowywanie hello ikonę urządzenia

Można dostosować wyświetlane na liście urządzeń hello z hello ikonę urządzenia hello **szczegóły urządzenia** panelu w następujący sposób:

1. Wybierz hello tooopen ikonę ołówka hello **obraz edycji** panelu dla urządzenia:

   ![Otwieranie edytora obrazu dla urządzenia][img-startimageedit]

1. Przekaż nowy obraz lub użyć jednego z istniejących obrazów hello a następnie wybierz pozycję **zapisać**:

   ![Edytowanie edytora obrazu dla urządzenia][img-imageedit]

1. Witaj obrazu teraz wyświetlany w hello **ikona** kolumny hello urządzenia.

> [!NOTE]
> Obraz powitania jest przechowywany w magazynie obiektów blob. Tag w dwie urządzenia hello zawiera obraz toohello łącze w magazynie obiektów blob.

### <a name="add-a-device"></a>Dodawanie urządzenia

Podczas wdrażania rozwiązania hello wstępnie zainicjować obsługę automatycznie 25 urządzeń próbki widoczne w hello listę urządzeń. Są to *symulowane urządzenia* uruchamiane w zadaniu WebJob Azure. Symulowane urządzeń ułatwiają dla Ciebie tooexperiment z rozwiązaniem hello wstępnie bez hello potrzeby toodeploy prawdziwe, fizycznych urządzeń. Tooconnect rozwiązania toohello rzeczywistego urządzenia, zobacz hello [połączyć Twoje toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie] [ lnk-connect-rm] samouczka.

Witaj poniższej procedurze pokazano, jak tooadd rozwiązania toohello symulowane urządzenie:

1. Przejdź wstecz toohello listę urządzeń.

1. Wybierz urządzenie, tooadd **+ Dodaj urządzenie** hello dole po lewej stronie ekranu.

   ![Dodaj urządzenie toohello wstępnie skonfigurowane rozwiązanie][img-adddevice]

1. Wybierz **Dodaj nowy** na powitania **symulowane urządzenie** kafelka.

   ![Określanie szczegółów nowego urządzenia na pulpicie nawigacyjnym][img-addnew]

   W toocreating dodanie nowych symulowane urządzenie, można także dodać urządzenia fizycznego po wybraniu toocreate **urządzenia niestandardowe**. toolearn więcej informacji na temat połączenia urządzeń fizycznych toohello rozwiązania, zobacz [połączyć toohello Twojego urządzenia zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, pakiet IoT][lnk-connect-rm].

1. Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia** i wprowadź unikatowy identyfikator urządzenia, np. **moje_urzadzenie_01**.

1. Wybierz pozycję **Utwórz**.

   ![Zapisywanie nowego urządzenia][img-definedevice]

1. W kroku 3 w artykule **dodać symulowane urządzenie**, wybierz **gotowe** tooreturn toohello urządzenia listy.

1. Możesz wyświetlić urządzenia **systemem** hello listy urządzeń.

    ![Wyświetlanie nowego urządzenia na liście urządzeń][img-runningnew]

1. Można również wyświetlić dane telemetryczne z nowego urządzenia na pulpicie nawigacyjnym hello symulowane hello:

    ![Wyświetlanie telemetrii z nowego urządzenia][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Wyłączanie i usuwanie urządzenia

Można wyłączyć urządzenie, a następnie je usunąć:

![Wyłączanie i usuwanie urządzenia][img-disable]

### <a name="add-a-rule"></a>Dodawanie reguły

Brak reguł dla nowego urządzenia hello zostały dodane. W tej sekcji możesz dodać regułę, która uruchamia alarm, gdy temperatury hello zgłoszone przez hello nowe, że urządzenia przekracza 47 stopni. Przed rozpoczęciem należy zauważyć, że Pokazuje historię telemetrii hello hello nowe urządzenie na pulpicie nawigacyjnym hello temperatury urządzenia hello nigdy nie przekracza 45 stopni.

1. Przejdź wstecz toohello listę urządzeń.

1. tooadd reguły hello urządzenia, wybierz nowe urządzenie hello **listy urządzeń**, a następnie wybierz pozycję **Dodaj regułę**.

1. Utworzyć regułę, która używa **temperatury** jako hello pola danych i używa **AlarmTemp** jako hello dane wyjściowe, gdy hello temperatura przekracza 47 stopni:

    ![Dodawanie reguły urządzenia][img-adddevicerule]

1. Wybierz zmiany, toosave **Zapisz i Wyświetl reguły**.

1. Wybierz **polecenia** w okienku szczegółów urządzenia hello na powitania nowe urządzenie.

    ![Dodawanie reguły urządzenia][img-adddevicerule2]

1. Wybierz **ChangeSetPointTemp** z listy poleceń hello i zestaw **SetPointTemp** too45. Następnie wybierz pozycję **Wyślij polecenie**:

    ![Dodawanie reguły urządzenia][img-adddevicerule3]

1. Przejdź wstecz toohello pulpitu nawigacyjnego. Po pewnym czasie, pojawi się nowy wpis w hello **historii Alarm** okienku, gdy temperatury hello zgłoszone przez nowe urządzenie przekracza próg stopnia 47 hello:

    ![Dodawanie reguły urządzenia][img-adddevicerule4]

1. Możesz sprawdzić i edytować wszystkie reguły na powitania **reguły** strony pulpitu nawigacyjnego hello:

    ![Wyświetlanie listy reguł urządzenia][img-rules]

1. Możesz sprawdzić i edytować wszystkie akcje hello, które można podjąć w regule tooa odpowiedzi na powitania **akcje** strony pulpitu nawigacyjnego hello:

    ![Wyświetlanie listy akcji urządzenia][img-actions]

> [!NOTE]
> Jest możliwe toodefine akcje, które można wysyłać wiadomości e-mail lub SMS w odpowiedzi tooa reguły lub zintegrować z systemu z biznesowych, za pośrednictwem [aplikacji logiki][lnk-logic-apps]. Aby uzyskać więcej informacji, zobacz hello [tooyour połączyć aplikację logiki Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-logicapptutorial].

### <a name="manage-filters"></a>Zarządzanie filtrami

Na liście urządzeń hello można utworzyć, Zapisz i ponownie załaduj filtry toodisplay niestandardową listą Centrum tooyour podłączonych urządzeń. toocreate filtru:

1. Wybierz ikonę filtra edycji hello powyżej hello listę urządzeń:

    ![Otwórz hello edytora filtru][img-editfiltericon]

1. W hello **edytora filtru**, Dodaj hello pola, operatory i listę urządzeń hello toofilter wartości. Wiele toorefine klauzule można dodać filtru. Wybierz **filtru** tooapply hello filtru:

    ![Tworzenie filtru][img-filtereditor]

1. W tym przykładzie listy hello są filtrowane według producenta i numer modelu:

    ![Filtrowana lista][img-filterelist]

1. toosave filtru o nazwie niestandardowe, wybierz hello **Zapisz jako** ikona:

    ![Zapisywanie filtru][img-savefilter]

1. tooreapply filtr zostały zapisane wcześniej, wybierz hello **Otwórz zapisany filtr** ikona:

    ![Otwieranie filtru][img-openfilter]

Filtry można tworzyć na postawie identyfikatora urządzenia, stanu urządzenia, żądanych właściwości, zgłaszanych właściwości i tagów. Dodać własne urządzenie tooa znaczniki niestandardowe w hello **tagi** sekcji hello **szczegóły urządzenia** panelu lub uruchomić tagi tooupdate zadania na wielu urządzeniach.

> [!NOTE]
> W hello **edytora filtru**, można użyć hello **Widok zaawansowanego** tekst zapytania hello tooedit bezpośrednio.

### <a name="commands"></a>Polecenia

Z hello **szczegóły urządzenia** panelu, możesz wysłać polecenia toohello urządzenia. Po pierwszym uruchomieniu urządzenia, wysyła się, że informacje o hello polecenia obsługuje toohello rozwiązania. Omówienie hello różnice między poleceń i metody, zobacz [opcje chmury do urządzenia Azure IoT Hub][lnk-c2d-guidance].

1. Wybierz **polecenia** w hello **szczegóły urządzenia** panelu dla wybranego urządzenia hello:

   ![Polecenia urządzenia na pulpicie nawigacyjnym][img-devicecommands]

1. Wybierz **PingDevice** z hello listę poleceń.

1. Wybierz pozycję **Wyślij polecenie**.

1. Stan hello hello polecenia w historii poleceń hello jest widoczny.

   ![Stan polecenia na pulpicie nawigacyjnym][img-pingcommand]

rozwiązanie Hello śledzi stan hello każdego polecenia wysyłane. Początkowo wynik hello jest **oczekujące**. Gdy urządzenie hello zgłasza, że uruchomione polecenie hello, zbyt zestaw wyników hello**Powodzenie**.

## <a name="behind-hello-scenes"></a>Tle hello

Podczas wdrażania wstępnie skonfigurowanych rozwiązań procesu wdrażania hello tworzy wiele zasobów w hello subskrypcji platformy Azure, które wybrano. Te zasoby można wyświetlić w hello Azure [portal][lnk-portal]. Utworzenie procesu wdrażania Hello **grupy zasobów** o nazwie na podstawie nazwy hello wybierz wstępnie skonfigurowanego rozwiązania:

![Wstępnie skonfigurowane rozwiązanie w hello portalu Azure][img-portal]

Można wyświetlać ustawienia hello każdego zasobu, wybierając ją z listy hello zasobów w grupie zasobów hello.

Można również wyświetlić kod źródłowy hello hello wstępnie skonfigurowane rozwiązanie. Hello zdalnej kontroli kodu źródłowego wstępnie skonfigurowane rozwiązanie jest w hello [azure iot — zdalnego monitorowania] [ lnk-rmgithub] repozytorium GitHub:

* Witaj **DeviceAdministration** folder zawiera kod źródłowy hello hello pulpitu nawigacyjnego.
* Witaj **symulatora** folder zawiera kod źródłowy hello hello symulowane urządzenie.
* Witaj **EventProcessor** folder zawiera kod źródłowy hello hello zaplecza procesu, który obsługuje hello przychodzących danych telemetrycznych.

Gdy wszystko będzie gotowe, możesz usunąć hello wstępnie skonfigurowane rozwiązanie z subskrypcją platformy Azure na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji. Ta witryna umożliwia delete tooeasily hello wszystkie zasoby, które zostały udostępnione po utworzeniu hello wstępnie skonfigurowane rozwiązanie.

> [!NOTE]
> tooensure Usuń wszystkie powiązane toohello wstępnie skonfigurowane rozwiązanie, usuń go na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji i nie usuwaj hello grupy zasobów w portalu hello.

## <a name="next-steps"></a>Następne kroki

Teraz, po wdrożeniu rozwiązania pracy wstępnie skonfigurowane, można nadal wprowadzenie pakiet IoT odczytując hello następujące artykuły:

* [Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego][lnk-rm-walkthrough]
* [Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-connect-rm]
* [Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md