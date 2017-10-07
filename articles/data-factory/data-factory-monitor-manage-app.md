---
title: "aaaMonitor i zarządzanie nimi w potokach danych - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello monitorowanie i zarządzanie toomonitor aplikacji i zarządzanie fabryki danych Azure i potoki."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Monitorowanie i zarządzanie nimi potoki fabryki danych Azure przy użyciu aplikacji hello monitorowanie i zarządzanie
> [!div class="op_single_selector"]
> * [Przy użyciu portalu Azure/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Przy użyciu monitorowania i zarządzania aplikacjami](data-factory-monitor-manage-app.md)
>
>

W tym artykule opisano, jak toouse hello toomonitor aplikacji zarządzania i monitorowania, zarządzania i debugowania potoki z fabryki danych. Zawiera także informacje o jak toocreate alerty tooget powiadomienie dotyczące niepowodzeń. Użytkownik może rozpocząć korzystanie z aplikacji hello przez oglądaniu powitania po wideo:

> [!NOTE]
> Witaj interfejsu użytkownika pokazano hello wideo może nie pasować informacje wyświetlane w portalu hello. Jest nieco starszy, przy zachowaniu pojęcia hello tego samego. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Uruchamianie aplikacji hello monitorowanie i zarządzanie
hello toolaunch monitora i aplikacji do zarządzania, kliknij przycisk hello **Monitor & Zarządzaj** Kafelek na powitania **fabryki danych** bloku fabryką danych.

![Monitorowanie kafelka na stronie głównej hello fabryki danych](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Powinna zostać wyświetlona aplikacja monitorowanie i zarządzanie hello otworzyć w osobnym oknie.  

![Aplikacja do monitorowania i zarządzania](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyczyść hello **zablokować pliki cookie innych firm, a dane lokacji** pole wyboru--lub Zachowaj ono zaznaczone, utworzyć wyjątek **login.microsoftonline.com** , a następnie spróbuj ponownie tooopen hello aplikacji.


Na liście działanie Windows hello w środkowym okienku hello zobaczysz okno działania przy każdym uruchomieniu działania. Na przykład jeśli hello toorun działania zaplanowane co godzinę przez pięć godzin, zobacz pięć okien działania skojarzonych z wycinków danych pięć. Jeśli nie widzisz działania windows hello liście u dołu hello hello następujące:
 
- Aktualizacja hello **godzina rozpoczęcia** i **czas zakończenia** filtrów w hello top toomatch hello start i end razy potoku sieci, a następnie kliknij hello **Zastosuj** przycisku.  
- Lista działań Windows Hello nie zostanie automatycznie odświeżony. Kliknij przycisk hello **Odśwież** przycisk na powitania narzędzi hello **okien działania** listy.  

Jeśli nie masz tootest aplikacji fabryki danych te kroki, hello samouczek: [kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych przy użyciu fabryki danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Zrozumienie aplikacji hello monitorowanie i zarządzanie
Dostępne są trzy karty po lewej stronie powitania: **Eksploratora zasobów**, **widoków monitorowania**, i **alerty**. Witaj pierwszej karcie (**Eksploratora zasobów**) jest domyślnie zaznaczona.

### <a name="resource-explorer"></a>Eksplorator zasobów
Znajdują się hello w następujących tematach:

* Witaj Eksploratora zasobów **widok drzewa** w okienku po lewej stronie powitania.
* Witaj **widoku diagramu** u góry hello w środkowym okienku hello.
* Witaj **okien działania** listy u dołu hello w środkowym okienku hello.
* Witaj **właściwości**, **działania okna Eksploratora**, i **skryptu** karty w okienku po prawej stronie powitania.

W Eksploratorze zasobów zobacz temat wszystkie zasoby (potoki, zestawy danych połączonych usług) w fabryce danych hello w widoku drzewa. Po wybraniu obiektu, w Eksploratorze zasobów:

* Witaj skojarzone jednostki zostanie wyróżniona w widoku diagramu hello fabryki danych.
* [Skojarzone działanie windows](data-factory-scheduling-and-execution.md) zostały wyróżnione na liście działanie Windows hello u dołu hello.  
* właściwości Hello hello wybranego obiektu są wyświetlane w oknie właściwości hello w okienku po prawej stronie powitania.
* Hello definicji JSON wybranego obiektu hello jest wyświetlany, jeśli ma to zastosowanie. Na przykład: połączonej usługi, zestawu danych lub potoku.

![Eksplorator zasobów](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Zobacz hello [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu, aby uzyskać szczegółowe informacje o pojęciach dotyczących działania systemu windows.

### <a name="diagram-view"></a>Widok diagramu
Hello widoku diagramu fabryki danych zapewnia jeden z toomonitor szkła i zarządzanie fabryki danych i jego zasoby. Po wybraniu podmiot fabryki danych (dataset/potoku) w widoku diagramu hello:

* w widoku drzewa hello wybrano jednostki fabryki danych Hello.
* Witaj skojarzone działanie, które systemu windows są wyróżnione na liście działanie Windows hello.
* właściwości Hello hello wybranego obiektu są wyświetlane w oknie właściwości hello.

Po włączeniu potoku hello (nie jest w stanie wstrzymania) jest wyświetlany zielony linią:

![Potok uruchomiona](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Można wstrzymać, wznowić lub zakończenie potoku, wybierając ją w widoku diagramu hello i za pomocą przycisków hello na pasku poleceń hello.

![Wstrzymanie/wznowienie na pasku poleceń hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Istnieją trzy przyciski paska poleceń dla potoku hello w hello widoku diagramu. Możesz użyć hello drugiego przycisku toopause hello potoku. Wstrzymywanie nie zakończyć hello aktualnie uruchomione działania i umożliwia ich kontynuować toocompletion. przycisk trzeci Hello potoku hello wstrzymuje i kończy istniejące wykonywanych działań. pierwszy przycisk Hello wznawia hello potoku. Wstrzymanie planowaną zmienia kolor hello hello potoku. Na przykład wstrzymanie potoku wygląda powitania po obrazu: 

![Wstrzymane potoku](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Można wybrać wiele potoki dwóch lub więcej używając hello klawisz Ctrl. Potoki wielu hello polecenia paska przycisków toopause/wznawiania można użyć w czasie.

Użytkownik może również kliknąć prawym przyciskiem myszy potoku i wybrania opcji toosuspend, Wznów lub zakończenie potoku. 

![Menu kontekstowe dla potoku](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Kliknij przycisk hello **Otwórz potoku** opcję toosee wszystkie działania hello w potoku hello. 

![Menu Otwórz potok](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

W widoku potoku hello otwarty można zobaczyć wszystkie działania w potoku hello. W tym przykładzie jest tylko jedno działanie: działanie kopiowania. 

![Otwarty potoku](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo kopii toohello poprzedni widok, kliknij przycisk Nazwa fabryki danych hello hello nawigacją menu u góry hello.

W widoku potoku hello po wybraniu wyjściowy zestaw danych lub gdy mysz przesuwa się nad hello wyjściowy zestaw danych, zobaczysz okno podręczne działania Windows hello dla tego zestawu danych.

![Okno podręczne działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Można kliknąć szczegóły toosee okna działania dla niego hello **właściwości** okna w okienku po prawej stronie powitania.

![Działanie właściwości okna](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

W okienku po prawej stronie powitania, Przełącz toohello **działania okna Eksploratora** karcie toosee więcej szczegółów.

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Zobacz też **rozpoznać zmienne** dla każdego próba uruchomienia działania w hello **prób** sekcji.

![Zmienne rozwiązany](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Przełącz toohello **skryptu** karcie toosee hello JSON skryptu definicji hello wybranego obiektu.   

![Karta skryptu](./media/data-factory-monitor-manage-app/ScriptTab.png)

Można wyświetlić okien działania w trzech miejscach:

* Witaj okien działania wyskakujących w hello widoku diagramu (w środkowym okienku).
* Działanie okno Eksploratora Hello w okienku po prawej stronie powitania.
* Lista działania systemu Windows Hello w hello dolnym okienku.

W oknie podręcznym działania Windows hello i działania okna Eksploratora toohello można przewijać w poprzednim tygodniu i hello hello następnym tygodniu za pomocą strzałki w lewo i w prawo.

![Strzałki prawej/lewej strony okna Eksploratora działania](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

U dołu hello hello widoku diagramu, zobacz tych przycisków: powiększanie, zmniejszanie, tooFit powiększenia powiększenie 100%, Zablokuj układ. Witaj **układu blokady** przycisk zapobiega przypadkowemu przenoszeniu tabel i potoków hello widoku diagramu. Jest on domyślnie. Można ją wyłączyć i przenosić jednostek hello diagramu. Wyłączenie opcji, można użyć hello ostatniego przycisk tooautomatically pozycji tabele i potoki. Można również powiększanie lub pomniejszanie za pomocą kółka myszy hello.

![Diagram przedstawiający polecenia powiększenia widoku](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Lista działania systemu Windows
Lista okien działania Hello u dołu hello w środkowym okienku hello Wyświetla wszystkie działania windows hello zestawu danych, wybranym hello Eksploratora zasobów lub hello widoku diagramu. Domyślnie lista hello jest w kolejności malejącej, co oznacza, że widoczny hello najnowsze okno działania u góry hello.

![Lista działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Ta lista nie odświeżane automatycznie, więc go odświeżyć. Użyj przycisku Odśwież hello na powitania toomanually narzędzi.  

Działanie systemu windows może działać w jednym z hello następujące stany:

<table>
<tr>
    <th align="left">Stan</th><th align="left">Podstan</th><th align="left">Opis</th>
</tr>
<tr>
    <td rowspan="8">Oczekiwanie</td><td>ScheduleTime</td><td>czas Hello nie pochodzą dla hello działania okna toorun.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>zależności strumienia wychodzącego Hello nie są gotowe.</td>
</tr>
<tr>
<td>ComputeResources</td><td>zasoby obliczeniowe Hello nie są dostępne.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Wszystkie wystąpienia działania hello są zajęte uruchamianiem innych okien działania.</td>
</tr>
<tr>
<td>ActivityResume</td><td>działanie Hello jest wstrzymane i nie można uruchomić okien działania hello, dopóki nie zostanie wznowione.</td>
</tr>
<tr>
<td>Spróbuj ponownie</td><td>ponawiane Hello wykonania działania.</td>
</tr>
<tr>
<td>Walidacja</td><td>Weryfikacja jeszcze się nie rozpoczął.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Sprawdzanie poprawności jest ponowione toobe oczekiwania.</td>
</tr>
<tr>
<tr>
<td rowspan="2">W toku</td><td>Sprawdzanie poprawności</td><td>Trwa sprawdzanie poprawności.</td>
</tr>
<td>-</td>
<td>Okno działania Hello jest przetwarzana.</td>
</tr>
<tr>
<td rowspan="4">Nie powiodło się</td><td>Upłynął limit czasu</td><td>Witaj działania wykonywanie trwało dłużej niż jest dozwolonych przez działanie hello.</td>
</tr>
<tr>
<td>Anulowane</td><td>Okno działania Hello zostało anulowane przez akcję użytkownika.</td>
</tr>
<tr>
<td>Walidacja</td><td>Weryfikacja nie powiodła się.</td>
</tr>
<tr>
<td>-</td><td>Okno działania Hello nie toobe wygenerowany lub sprawdzić jego poprawności.</td>
</tr>
<td>Gotowe</td><td>-</td><td>Okno działania Hello jest gotowy do użycia.</td>
</tr>
<tr>
<td>Pominięto</td><td>-</td><td>Okno działania Hello nie został przetworzony.</td>
</tr>
<tr>
<td>Brak</td><td>-</td><td>Okno działania używane tooexist inny stan, ale został zresetowany.</td>
</tr>
</table>


Po kliknięciu okno działania na liście hello Zobacz szczegółowe informacje o nim w hello **Eksploratora Windows działania** lub hello **właściwości** okno na powitania prawo.

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Odśwież działania systemu windows
Szczegóły Hello nie są automatycznie odświeżane, należy więc hello odświeżania (przycisk hello drugi) na pasku toomanually odświeżania hello działania systemu windows lista poleceń hello.  

### <a name="properties-window"></a>Okno właściwości
Okno właściwości Hello znajduje się w okienku prawej hello hello zarządzania i monitorowania aplikacji.

![Okno właściwości](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Wyświetla właściwości elementu hello, wybranym hello Eksploratora zasobów (widok drzewa), widok diagramu lub listę okien działania.

### <a name="activity-window-explorer"></a>Działanie okno Eksploratora
Witaj **działania okna Eksploratora** okno jest w okienku prawej hello hello zarządzania i monitorowania aplikacji. Wyświetla szczegółowe informacje o okno działania hello wybranego w oknie podręcznym działania Windows hello lub listy działania Windows hello.

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Okno działania tooanother można przełączać, klikając go w widoku kalendarza hello u góry hello. Można również użyć przycisk strzałki w lewo/Strzałka w prawo hello okien działania top toosee hello z hello poprzedniego tygodnia lub hello następnym tygodniu.

Można użyć przycisków paska narzędzi hello hello dolnym okienku toorerun hello działania okno lub odświeżyć szczegóły hello w okienku hello.

### <a name="script"></a>Skrypt
Można użyć hello **skryptu** kartę tooview hello definicji JSON hello wybrane jednostek fabryki danych (połączonej usługi, zestawu danych lub potoku).

![Karta skryptu](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Używanie widoków systemu
Witaj zarządzania i monitorowania aplikacji zawiera widoki wbudowanych systemu (**ostatnie okien działania**, **nie powiodło się okien działania**, **okien działania w toku**) który Zezwalaj tooview windows ostatnie/nie powiodło się/w trakcie działania z fabryki danych.

Przełącz toohello **widoków monitorowania** karcie po lewej stronie powitania, klikając go.

![Karta widoków monitorowania](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Obecnie istnieją trzy widoki systemowe, które są obsługiwane. Wybierz opcję toosee ostatnie działanie systemu windows, okien działania nie powiodło się lub okien działania w toku na liście działanie Windows hello (u dołu hello hello w środkowym okienku).

Po wybraniu hello **ostatnie okien działania** opcji, zobacz wszystkie ostatnie okien działania w porządku malejącym hello **ostatniej próby czasu**.

Można użyć hello **nie powiodło się okien działania** wyświetlanie okien działania toosee nie powiodło się na liście hello. Wybierz przedział nieudana czynność w hello szczegółów toosee listy informacji na ten temat w hello **właściwości** okna lub hello **działania okna Eksploratora**. Możesz również pobrać wszystkie dzienniki dla okna działanie nie powiodło się.

## <a name="sort-and-filter-activity-windows"></a>Sortuj i Filtruj działania systemu windows
Zmiana hello **godzina rozpoczęcia** i **czas zakończenia** ustawienia w poleceniu hello paska toofilter działania w systemie windows. Po zmianie hello godzinę rozpoczęcia i zakończenia, kliknij hello przycisku Dalej toohello zakończenia czasu toorefresh hello okien działania listę.

![Czas rozpoczęcia i zakończenia](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Obecnie wszystkie godziny są w formacie UTC w aplikacji hello zarządzania i monitorowania.
>
>

W hello **listę okien działania**, kliknij nazwę hello kolumny (na przykład: stanu).

![Działanie systemu Windows lista kolumn menu](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Można wykonać następujące hello:

* Sortowanie w kolejności rosnącej.
* Sortowanie w kolejności malejącej.
* Filtruj według jednego lub więcej wartości (gotowe, oczekiwania itd.).

Po określeniu filtru w kolumnie jest wyświetlany przycisk filtru hello włączone dla tej kolumny, co oznacza, że hello wartości w kolumnie hello są filtrowane wartości.

![Filtrować według kolumny z listy działania Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Można użyć tych samych wyskakującego okienka filtrów tooclear hello. tooclear wszystkie filtry dla listy działania Windows hello, kliknij przycisk Wyczyść filtr hello na powitania paska poleceń.

![Wyczyść wszystkie filtry dla listy działania Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Akcje usługi partia zadań
### <a name="rerun-selected-activity-windows"></a>Uruchom ponownie wybrane działanie systemu windows
Wybierz przedział działania, kliknij hello strzałka na powitania pierwszy przycisk paska poleceń w dół i wybierz **Uruchom ponownie** / **ponownie z powyżej w potoku**. Po wybraniu hello **ponownie z powyżej w potoku** opcji zwracające on również wszystkich okien działania nadrzędnego.
    ![Ponownie uruchom okno działania](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Można również wybrać wiele okien działania liście hello i uruchom je ponownie na powitania tym samym czasie. Może być toofilter okien działania na podstawie stanu hello (na przykład: ****)--i uruchom ponownie po usunięciu hello problem, który powoduje hello działania windows toofail okien działania hello nie powiodło się. Zobacz hello następujących sekcji, aby uzyskać więcej informacji dotyczących filtrowania działania windows hello na liście.  

### <a name="pauseresume-multiple-pipelines"></a>Wstrzymanie/wznowienie wielu potoki
Można multiselect potoki dwóch lub więcej używając hello klawisz Ctrl. Korzystając z przycisków paska poleceń hello (które są wyróżnione na powitania czerwony prostokąt powitania po obrazu) toopause/wznowienia ich.

![Wstrzymanie/wznowienie na pasku poleceń hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Tworzenie alertów
Witaj **alerty** strony pozwala na tworzenie alertów i wyświetlanie/edytowanie/usuwanie istniejące alerty. Użytkownik może również Włącz/Wyłącz alert. toosee hello strony alertów, kliknij przycisk hello **alerty** kartę.

![Karta alerty](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate alertu
1. Kliknij przycisk **dodać Alert** tooadd alertu. Zobacz hello **szczegóły** strony.

    ![Utwórz alerty — strona szczegółów](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Określ hello **nazwa** i **opis** hello alert, a następnie kliknij przycisk **dalej**. Powinny pojawić się hello **filtry** strony.

    ![Utwórz alerty — filtry strony](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Wybierz hello **zdarzeń**, **stan**, i **podstanu** (opcjonalnie), które mają toocreate usługi fabryka danych alertów dla i kliknij przycisk **dalej**. Powinny pojawić się hello **adresatów** strony.

    ![Utwórz alerty — strona adresatów](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Wybierz hello **poczty E-mail Administratorzy subskrypcji** opcji lub wprowadź **e-mail administratora dodatkowe**i kliknij przycisk **Zakończ**. Powinien zostać wyświetlony alert hello hello na liście.

    ![Lista alertów](./media/data-factory-monitor-manage-app/AlertsList.png)

Na liście alertów hello użyj przycisków hello, które są skojarzone z hello alertu tooedit/delete/Włącz/Wyłącz alert.

### <a name="eventstatussubstatus"></a>Podstan zdarzeń/stanu
Witaj Poniższa tabela zawiera listę hello dostępnych zdarzeń oraz Stany (i podstany).

| Nazwa zdarzenia | Stan | Podstan |
| --- | --- | --- |
| Działanie Uruchom wprowadzenie |Rozpoczęto |Uruchamianie |
| Działanie Uruchom Zakończono |Powodzenie |Powodzenie |
| Działanie Uruchom Zakończono |Nie powiodło się |Alokacja zasobów nie powiodło się<br/><br/>Wykonanie nie powiodło się<br/><br/>Upłynął limit czasu<br/><br/>Sprawdzanie poprawności nie powiodło się<br/><br/>porzucone |
| Rozpoczęto tworzenie klastra HDI na żądanie |Rozpoczęto |-|
| Pomyślnie utworzono klaster HDI na żądanie |Powodzenie |-|
| Usunąć klaster HDI na żądanie |Powodzenie |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, usunąć lub wyłączyć alertu

Użyj powitania po tooedit przycisków (wyróżnionych kolorem czerwonym), usuń lub Wyłącz alert.

![Przyciski alertów](./media/data-factory-monitor-manage-app/AlertButtons.png)
