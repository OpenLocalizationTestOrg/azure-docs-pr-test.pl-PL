---
title: "aaaAlert rozwiązania do zarządzania w Operations Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Hello rozwiązania zarządzania alertami Log Analytics pomaga analizować wszystkie alerty hello w danym środowisku.  Dodanie alertów tooconsolidating wygenerowaniem OMS go importuje alerty z połączonych grup zarządzania programu System Center Operations Manager do analizy dzienników."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Alert rozwiązania do zarządzania w Operations Management Suite (OMS)

![Ikona zarządzania alertu](media/log-analytics-solution-alert-management/icon.png)

Witaj rozwiązania zarządzania alertami pomaga analizować wszystkie alerty hello w repozytorium analizy dzienników.  Te alerty mogą pochodzić z różnych źródeł, łącznie z tych źródeł [utworzone przez analizy dzienników](log-analytics-alerts.md) lub [zaimportowane z Nagios lub Zabbix](log-analytics-linux-agents.md).  Witaj rozwiązania również importuje alerty z dowolnej [podłączone grupy zarządzania programu System Center Operations Manager](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Wymagania wstępne
rozwiązanie Hello współpracuje z żadnych rekordów w repozytorium analizy dzienników hello z typem **alertu**, dlatego należy wykonać, niezależnie od konfiguracji jest wymagana toocollect tych rekordów.

- W przypadku alertów analizy dzienników [tworzyć reguły alertów](log-analytics-alerts.md) toocreate alertów rejestruje bezpośrednio w repozytorium hello.
- W przypadku alertów Nagios i Zabbix [skonfigurować te serwery](log-analytics-linux-agents.md) toosend alerty tooLog Analytics.
- W przypadku alertów programu System Center Operations Manager [połączyć z obszaru roboczego analizy dzienników programu Operations Manager management grupy tooyour](log-analytics-om-agents.md).  Wszystkie alerty utworzone w programie System Center Operations Manager są importowane do analizy dzienników.  

## <a name="configuration"></a>Konfiguracja
Dodaj tooyour rozwiązania zarządzania alertami hello obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [dodać rozwiązania](log-analytics-add-solutions.md).  Nie są wymagane żadne dalsze czynności konfiguracyjne.

## <a name="management-packs"></a>Pakiety administracyjne
Jeśli grupa zarządzania programu System Center Operations Manager jest połączonych tooyour obszarem roboczym pakietu OMS, hello następujące pakiety administracyjne są zainstalowane w programie System Center Operations Manager podczas dodawania tego rozwiązania.  Brak konfiguracji lub konserwacji hello pakiety administracyjne wymagane.  

* Zarządzania alertami programu Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Aby uzyskać więcej informacji dotyczących sposobu aktualizowania rozwiązania pakietów administracyjnych, zobacz [tooLog połączenie programu Operations Manager Analytics](log-analytics-om-agents.md).

## <a name="data-collection"></a>Zbieranie danych
### <a name="agents"></a>Agenci
Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie.

| Połączone źródło | Pomoc techniczna | Opis |
|:--- |:--- |:--- |
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Nie |Bezpośrednie agentów systemu Windows nie generują alerty.  Można tworzyć alerty analizy dziennika zdarzeń i zebrać danych wydajności z systemu Windows agentów. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie |Bezpośrednie agentów systemu Linux nie generują alerty.  Dziennik analizy alerty mogą być tworzone z zdarzenia i dane wydajności zebrane z agentów systemu Linux.  Nagios i Zabbix alerty są zbierane z tych serwerów, które wymagają hello agenta systemu Linux. |
| [Grupa zarządzania programu System Center Operations Manager](log-analytics-om-agents.md) |Tak |Alerty, które są generowane na agenty programu Operations Manager są dostarczane toohello grupy zarządzania, a następnie przesłane dalej tooLog Analytics.<br><br>Połączenie bezpośrednie z tooLog agentów programu Operations Manager Analytics nie jest wymagane. Dane alertów jest przekazywany z hello zarządzania grupy toohello analizy dzienników repozytorium. |


### <a name="collection-frequency"></a>Częstotliwość zbierania
- Rekordy alertu są toohello dostępne rozwiązania, jak są przechowywane w repozytorium hello.
- Alert dane są wysyłane z hello programu Operations Manager management grupy tooLog Analytics co trzy minuty.  

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello
Po dodaniu obszar roboczy OMS tooyour rozwiązania zarządzania alertami hello hello **zarządzania alertami** kafelka dodaniu tooyour OMS z pulpitu nawigacyjnego.  Ten Kafelek Wyświetla graficzną reprezentację hello liczby aktywnych alertów, które zostały wygenerowane w ramach hello ostatnich 24 godzinach i liczba.  Nie można zmienić tego zakresu czasu.

![Alert kafelka zarządzania](media/log-analytics-solution-alert-management/tile.png)

Polecenie hello **zarządzania alertami** hello tooopen kafelka **zarządzania alertami** pulpitu nawigacyjnego.  pulpit nawigacyjny Hello zawiera kolumny hello w hello w poniższej tabeli.  Każda kolumna zawiera hello top 10 alertów przez dopasowanie liczby kolumny kryteria hello określenia zakresu zakresu i czasu.  Możesz uruchomić wyszukiwanie dziennika, które zawiera listę całego hello klikając **zobaczyć wszystkie** u dołu hello hello kolumny lub przez kliknięcie nagłówka kolumny hello.

| Kolumna | Opis |
|:--- |:--- |
| Alerty krytyczne |Wszystkie alerty o ważności krytyczna pogrupowane według nazwę alertu.  Kliknij nazwę alertu toorun wyszukiwanie dziennika zwracanie wszystkich rekordów dla tego alertu. |
| Alerty ostrzegawcze |Wszystkie alerty o ważności ostrzeżenie pogrupowane według nazwę alertu.  Kliknij nazwę alertu toorun wyszukiwanie dziennika zwracanie wszystkich rekordów dla tego alertu. |
| Alerty aktywne SCOM |Wszystkie alerty zebranych z programu Operations Manager przez każdy stan inny niż *zamknięte* pogrupowane według źródła tego alertu wygenerowanego hello. |
| Wszystkie aktywne alerty |Wszystkie alerty o wszelkich ważność pogrupowane według nazwę alertu. Tylko innych niż obejmuje alertów programu Operations Manager z jakimkolwiek stanem stanów *zamknięte*. |

Jeśli przewiń w prawo toohello hello pulpit nawigacyjny zawiera kilka typowych zapytań, które można kliknąć tooperform [wyszukiwania dziennika](log-analytics-log-searches.md) dla danych alertów.

![Pulpit nawigacyjny zarządzania alertu](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Witaj rozwiązania zarządzania alertami analizuje żadnych rekordów z typem **alertu**.  Alerty utworzone przez analizy dzienników lub zbierane z Nagios lub Zabbix nie są bezpośrednio zbierane przez rozwiązanie hello.

rozwiązanie Hello zaimportować alerty z programu System Center Operations Manager i tworzy odpowiedni rekord dla każdego typu **alertu** i SourceSystem z **OpsManager**.  Te rekordy zawierają właściwości hello hello w poniższej tabeli:  

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Alert* |
| SourceSystem |*OpsManager* |
| AlertContext |Szczegóły elementu danych hello, który spowodował hello toobe alertów wygenerowanych w formacie XML. |
| AlertDescription |Szczegółowy opis hello alertu. |
| Identyfikatorem alertu |Identyfikator GUID hello alertu. |
| AlertName |Nazwa alertu hello. |
| AlertPriority |Poziom priorytetu hello alertu. |
| AlertSeverity |Poziom ważności alertu hello. |
| Stan alertu |Najnowszy stan rozwiązania alertu hello. |
| LastModifiedBy |Nazwa użytkownika hello, który ostatniej modyfikacji alertu hello. |
| ManagementGroupName |Nazwa grupy zarządzania hello gdzie hello alert został wygenerowany. |
| RepeatCount |Liczba hello sam alert został wygenerowany dla hello sam monitorowany obiekt od rozwiązywany. |
| ResolvedBy |Nazwa użytkownika hello, który hello alertu. Pusta, jeśli hello alert nie zostały rozpoznane. |
| SourceDisplayName |Wyświetlana nazwa hello obiekt, który wygenerował hello alert monitorowania. |
| SourceFullName |Pełna nazwa hello obiekt, który wygenerował hello alert monitorowania. |
| TicketId |Identyfikator biletu hello alert, jeśli środowisko programu System Center Operations Manager hello jest zintegrowany z proces przypisywania biletów dla alertów.  Identyfikator pusty biletu nie jest przypisany. |
| TimeGenerated |Data i godzina hello alert został utworzony. |
| TimeLastModified |Data i godzina hello alert został ostatnio zmieniony. |
| TimeRaised |Data i godzina hello alert został wygenerowany. |
| TimeResolved |Data i godzina hello alert został rozwiązany. Pusta, jeśli hello alert nie zostały rozpoznane. |

## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników
Witaj poniższej tabeli przedstawiono przykładowy dziennik wyszukuje rekordy alertów zebranych przez to rozwiązanie: 

| Zapytanie | Opis |
|:--- |:--- |
| Typ alertu SourceSystem = = OpsManager AlertSeverity = błąd TimeRaised > teraz 24 godzin |Alerty krytyczne zgłoszone podczas hello w ciągu ostatnich 24 godzin |
| Typ alertu AlertSeverity = = ostrzeżenie TimeRaised > teraz 24 godzin |Alerty ostrzegawcze zgłoszone podczas hello w ciągu ostatnich 24 godzin |
| Typ alertu SourceSystem = = OpsManager stan alertu! = TimeRaised zamkniętego > teraz 24 godzin &#124; Miara count() jako liczba wg SourceDisplayName |Źródła z aktywnymi alertami zgłoszonymi w hello ostatnich 24 godzin |
| Typ alertu SourceSystem = = OpsManager AlertSeverity = błąd TimeRaised > teraz - 24-GODZINNY stan alertu! = zamknięty |Alerty krytyczne zgłoszone podczas hello w ciągu ostatnich 24 godzin, które są nadal aktywne |
| Typ alertu SourceSystem = OpsManager TimeRaised = > teraz - 24-GODZINNY stan alertu = zamknięte |Alerty zgłoszone w hello ostatnich 24 godzin, które teraz są zamknięte |
| Typ alertu SourceSystem = OpsManager TimeRaised = > teraz - 1 dzień &#124; Miara count() jako liczba wg AlertSeverity |Alerty zgłoszone w ciągu ostatniej doby pogrupowane według ważności hello |
| Typ alertu SourceSystem = OpsManager TimeRaised = > teraz - 1 dzień &#124; Sortowanie RepeatCount desc |Alerty zgłoszone w ciągu ostatniej doby posortowane według wartości liczby powtórzeń hello |


>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello poprzedzających zapytania zmieniłby toohello następujące:
>
>| Zapytanie | Opis |
|:---|:---|
| Alert &#124; gdzie SourceSystem == "OpsManager" i AlertSeverity == "error" i TimeRaised > ago(24h) |Alerty krytyczne zgłoszone podczas hello w ciągu ostatnich 24 godzin |
| Alert &#124; gdzie AlertSeverity == "ostrzeżenie" i TimeRaised > ago(24h) |Alerty ostrzegawcze zgłoszone podczas hello w ciągu ostatnich 24 godzin |
| Alert &#124; gdzie SourceSystem == "OpsManager" i stan alertu! = "Zamknięte" i TimeRaised > ago(24h) &#124; Podsumuj Count = count() przez SourceDisplayName |Źródła z aktywnymi alertami zgłoszonymi w hello ostatnich 24 godzin |
| Alert &#124; gdzie SourceSystem == "OpsManager" i AlertSeverity == "error" i TimeRaised > ago(24h) i stan alertu! = "Zamknięte" |Alerty krytyczne zgłoszone podczas hello w ciągu ostatnich 24 godzin, które są nadal aktywne |
| Alert &#124; gdzie SourceSystem == "OpsManager" i TimeRaised > ago(24h) i stan alertu == "Zamknięte" |Alerty zgłoszone w hello ostatnich 24 godzin, które teraz są zamknięte |
| Alert &#124; gdzie SourceSystem == "OpsManager" i TimeRaised > ago(1d) &#124; Podsumuj Count = count() przez AlertSeverity |Alerty zgłoszone w ciągu ostatniej doby pogrupowane według ważności hello |
| Alert &#124; gdzie SourceSystem == "OpsManager" i TimeRaised > ago(1d) &#124; Sortuj według RepeatCount desc |Alerty zgłoszone w ciągu ostatniej doby posortowane według wartości liczby powtórzeń hello |


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat [alertów w usłudze Log Analytics](log-analytics-alerts.md), aby poznać szczegóły generowania alertów z usługi Log Analytics.
