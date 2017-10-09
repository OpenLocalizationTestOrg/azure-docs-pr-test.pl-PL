---
title: "aaaAgent kondycji rozwiązania OMS | Dokumentacja firmy Microsoft"
description: "W tym artykule jest zamierzone toohelp zrozumieć, jak toouse toomonitor tego rozwiązania hello kondycji agentów raportowania bezpośrednio tooOMS lub System Center Operations Manager."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>Rozwiązanie Agent Health w usłudze OMS
rozwiązanie agenta kondycji Hello w OMS pomaga zrozumieć, dla wszystkich agentów hello raportowania bezpośrednio toohello obszarem roboczym pakietu OMS lub tooOMS podłączone grupy zarządzania programu System Center Operations Manager, które odpowiadać i przesyłanie danych operacyjnych.  Użytkownik może także śledzić wartości liczby agentów są wdrażane, gdzie są rozproszone geograficznie i wykonywać inne zapytania toomaintain pogłębianie wiedzy na temat dystrybucji hello agentów wdrożonych w Azure, innych środowiskach w chmurze lub lokalnie.    

## <a name="prerequisites"></a>Wymagania wstępne
Przed przystąpieniem do wdrażania tego rozwiązania, upewnij się, ma obecnie obsługiwana [agentów systemu Windows](../log-analytics/log-analytics-windows-agents.md) raportowania toohello obszarem roboczym pakietu OMS lub reporting tooan [grupy zarządzania programu Operations Manager](../log-analytics/log-analytics-om-agents.md) zintegrowane z sieci Obszar roboczy OMS.    

## <a name="solution-components"></a>Składniki rozwiązania
To rozwiązanie obejmuje hello następujące zasoby, które są dodawane tooyour obszaru roboczego i agentów podłączonego bezpośrednio lub Operations Manager podłączonej grupy zarządzania.

### <a name="management-packs"></a>Pakiety administracyjne
Jeśli grupa zarządzania programu System Center Operations Manager jest połączonych tooan obszarem roboczym pakietu OMS, hello następujące pakiety administracyjne są zainstalowane w programie Operations Manager.  Te pakiety administracyjne są również instalowane na bezpośrednio połączonych komputerach z systemem Windows po dodaniu tego rozwiązania. Nie ma nic tooconfigure lub zarządzać za pomocą tych pakietów administracyjnych.

* Microsoft System Center Advisor HealthAssessment Direct Channel Intelligence Pack  (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor HealthAssessment Server Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Aby uzyskać więcej informacji dotyczących sposobu aktualizowania rozwiązania pakietów administracyjnych, zobacz [tooLog połączenie programu Operations Manager Analytics](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Konfiguracja
Dodaj tooyour rozwiązania hello kondycji agenta z obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [dodać rozwiązania](../log-analytics/log-analytics-add-solutions.md). Nie są wymagane żadne dalsze czynności konfiguracyjne.


## <a name="data-collection"></a>Zbieranie danych
### <a name="supported-agents"></a>Obsługiwani agenci
Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie.

| Połączone źródło | Obsługiwane | Opis |
| --- | --- | --- |
| Agenci dla systemu Windows | Tak | Zdarzenia pulsu są zbierane z bezpośrednich agentów systemu Windows.|
| Grupa zarządzania programu System Center Operations Manager | Tak | Pulsu zdarzenia są zbierane z agentów grupy zarządzania toohello raportowania co 60 sekund i przesyłane dalej tooLog Analytics. Połączenie bezpośrednie z tooLog agentów programu Operations Manager Analytics nie jest wymagane. Dane zdarzeń pulsu jest przekazywany z hello zarządzania grupy toohello analizy dzienników repozytorium.|

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello
Po dodaniu hello rozwiązania tooyour obszarem roboczym pakietu OMS hello **agenta kondycji** kafelka zostanie dodany tooyour OMS z pulpitu nawigacyjnego. Kafelek ten pokazuje hello łączna liczba agentów i hello liczby agentów nie odpowiada w hello ostatnich 24 godzin.<br><br> ![Kafelek rozwiązania Agent Health na pulpicie nawigacyjnym](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Polecenie hello **agenta kondycji** hello tooopen kafelka **agenta kondycji** pulpitu nawigacyjnego.  pulpit nawigacyjny Hello zawiera kolumny hello w hello w poniższej tabeli. Każda kolumna wymieniono top zdarzenia dziesięć hello według liczby spełniających kryteria kolumny hello określenia zakresu czasu. Możesz uruchomić wyszukiwanie dziennik zawiera listę całego hello wybierając **zobaczyć wszystkie** u dołu prawo hello każdej kolumny lub przez kliknięcie nagłówka kolumny hello.

| Kolumna | Opis |
|--------|-------------|
| Liczba agentów w miarę upływu czasu | Trend liczby agentów w okresie siedmiu dni dla agentów systemu Linux i Windows.|
| Liczba nieodpowiadających agentów | Lista agentów, które nie zostały wysłane pulsu w hello ostatnich 24 godzin.|
| Rozkład według typu systemu operacyjnego | Rozkład liczby agentów systemu Windows i Linux w Twoim środowisku.|
| Rozkład według wersji agenta | Partycja hello innego agenta wersji zainstalowanej w środowisku oraz liczbę każdej z nich.|
| Rozkład według kategorii agenta | Partycja hello różnych kategorii agenci, którzy wysyłają pulsu zdarzeń: bezpośrednie agentów, agenci programu Operations Manager lub powitania serwera zarządzania programu Operations Manager.|
| Rozkład według grupy zarządzania | Partycja hello różnych grup zarządzania programu SCOM w danym środowisku.|
| Lokalizacja geograficzna agentów | Partycja hello różnych krajów, gdzie masz agentów i łączna liczba hello liczby agentów, które zostały zainstalowane w każdym kraju.|
| Liczba zainstalowanych bram | Witaj liczbę serwerów, które mają hello zainstalowano bramę OMS i listę tych serwerów.|

![Przykład pulpitu nawigacyjnego rozwiązania Agent Health](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
rozwiązanie Hello tworzy jeden typ rekordu w repozytorium OMS hello.  

### <a name="heartbeat-records"></a>Rekordy Heartbeat
Tworzony jest rekord o typie **Heartbeat**.  Te rekordy mają właściwości hello w hello w poniższej tabeli.  

| Właściwość | Opis |
| --- | --- |
| Typ | *Heartbeat*|
| Kategoria | Wartością jest *Direct Agent*, *SCOM Agent* lub *SCOM Management Server*.|
| Computer | Nazwa komputera.|
| OSType | System operacyjny Windows lub Linux.|
| OSMajorVersion | Wersja główna systemu operacyjnego.|
| OSMinorVersion | Wersja pomocnicza systemu operacyjnego.|
| Wersja | Wersja agenta pakietu OMS lub agenta programu Operations Manager.|
| SCAgentChannel | Wartością jest *Direct* i/lub *SCManagementServer*.|
| IsGatewayInstalled | Jeśli zainstalowana jest brama usługi OMS, wartością jest *true*; w przeciwnym razem wartością jest *false*.|
| ComputerIP | Adres IP komputera hello.|
| RemoteIPCountry | Lokalizacja geograficzna, w której wdrożony jest komputer.|
| ManagementGroupName | Nazwa grupy zarządzania programu Operations Manager.|
| SourceComputerId | Unikatowy identyfikator komputera.|
| RemoteIPLongitude | Długość geograficzna lokalizacji geograficznej komputera.|
| RemoteIPLatitude | Szerokość geograficzna lokalizacji geograficznej komputera.|

Każdy agent raportowania serwer zarządzania programu Operations Manager tooan wyśle dwóch pulsów i wartość właściwości SCAgentChannel będzie zawierać jednocześnie **bezpośredniego** i **SCManagementServer** w zależności od tego, co Źródło danych analizy dziennika i rozwiązania, jakie włączono w ramach subskrypcji pakietu OMS. Jeżeli pamiętasz, dane z rozwiązań są wysyłane bezpośrednio z programu Operations Manager management server toohello OMS usługi sieci web, lub z powodu hello ilości danych zbieranych na agencie hello są wysyłane bezpośrednio z usługi sieci web tooOMS agenta hello. Dla zdarzeń pulsu, które mają wartość hello **SCManagementServer**, hello wartość ComputerIP jest hello adres IP serwera zarządzania hello, ponieważ dane hello faktycznie są przekazywane przez nią.  Pulsów, w którym SCAgentChannel ustawiono zbyt**bezpośredniego**, jest publiczny adres IP hello hello agenta.  

## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników
Witaj poniższej tabeli przedstawiono przykładowy dziennik wyszukuje rekordy zebrane przez to rozwiązanie.

| Zapytanie | Opis |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Łączna liczba agentów |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Liczba agentów nie odpowiada w hello ostatnich 24 godzinach |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Liczba agentów nie odpowiada w hello ostatnich 15 minut |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Komputery online (w ostatnich 24 godzinach hello) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Całkowita liczba agentów w tryb Offline w ostatnich 30 minut (hello ostatnich 24 godzin) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Pobierz trend liczby agentów w miarę upływu czasu według wartości OSType|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Rozkład według typu systemu operacyjnego |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Rozkład według wersji agenta |
| Type=Heartbeat&#124;measure count() by Category |Rozkład według kategorii agenta |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Rozkład według grupy zarządzania |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Lokalizacja geograficzna agentów |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Liczba zainstalowanych bram usługi OMS |


>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](../log-analytics/log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.
>
>| Zapytanie | Opis |
|:---|:---|
| Heartbeat &#124; distinct Computer |Łączna liczba agentów |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Liczba agentów nie odpowiada w hello ostatnich 24 godzinach |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Liczba agentów nie odpowiada w hello ostatnich 15 minut |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Komputery online (w ostatnich 24 godzinach hello) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Całkowita liczba agentów w tryb Offline w ostatnich 30 minut (hello ostatnich 24 godzin) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Pobierz trend liczby agentów w miarę upływu czasu według wartości OSType|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Rozkład według typu systemu operacyjnego |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Rozkład według wersji agenta |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Rozkład według kategorii agenta |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Rozkład według grupy zarządzania |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Lokalizacja geograficzna agentów |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Liczba zainstalowanych bram usługi OMS |

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej na temat [alertów w usłudze Log Analytics](../log-analytics/log-analytics-alerts.md), aby poznać szczegóły generowania alertów z usługi Log Analytics.
