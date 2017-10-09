---
title: "rozwiązanie do zarządzania w OMS aaaUpdate | Dokumentacja firmy Microsoft"
description: "W tym artykule jest zamierzone toohelp zrozumieć, jak toouse toomanage tego rozwiązania aktualizacji dla komputerów z systemem Windows i Linux."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>Rozwiązanie do zarządzania aktualizacjami w usłudze OMS

![Symbol Zarządzanie aktualizacjami](./media/oms-solution-update-management/update-management-symbol.png)

Hello rozwiązania zarządzania aktualizacjami w OMS pozwala aktualizacje zabezpieczeń systemu operacyjnego toomanage wdrożona na platformie Azure, komputery z systemem Windows i Linux lokalnych środowiskach lub innych dostawców chmury.  Można szybko ocenić stan hello dostępne aktualizacje na wszystkich komputerach agenta i zarządzać nimi hello proces instalowania aktualizacji wymaganych dla serwerów.


## <a name="solution-overview"></a>Omówienie rozwiązania
Komputery zarządzane przez OMS użyć następujących hello do wykonania ocena i aktualizacja wdrożenia:

* Agent usługi OMS dla systemu Windows lub Linux
* Platforma PowerShell Desired State Configuration (DSC) dla systemu Linux
* Hybrydowy proces roboczy elementu runbook usługi Automation
* Usługa Microsoft Update lub Windows Server Update Services dla komputerów z systemem Windows

następujące diagramy Hello pokazuje połączony widok koncepcyjny przepływu danych i zachowanie hello sposób rozwiązania hello ocenia i stosuje tooall aktualizacje zabezpieczeń systemu Windows Server i komputery z systemem Linux w obszarze roboczym.    

#### <a name="windows-server"></a>Windows Server
![Przepływ procesu zarządzania aktualizacjami dla systemu Windows Server](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Przepływ procesu zarządzania aktualizacjami dla systemu Linux](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Po komputera hello wykonuje skanowanie zgodności aktualizacji, agent pakietu OMS hello przekazuje informacje hello w tooOMS zbiorczego. Na komputerze okno skanowania zgodności hello jest domyślnie wykonywane co 12 godzin.  Ponadto harmonogram skanowania w poszukiwaniu toohello, hello skanowanie pod kątem zgodności aktualizacji jest inicjowana w ciągu 15 minut, jeśli hello Microsoft Monitoring Agent (MMA) jest tooupdate uruchomić ją ponownie, poprzedni instalacji i po zainstalowaniu aktualizacji.  Z komputera z systemem Linux domyślnie skanowania zgodności hello jest wykonywane co 3 godziny, a skanowanie zgodności jest inicjowane w ciągu 15 minut, jeśli hello MMA agent jest ponownie uruchamiany.  

Witaj informacje o zgodności jest następnie przetwarzany i podsumowane w pulpitach nawigacyjnych hello uwzględnione w rozwiązaniu hello lub wyszukiwanie przy użyciu zdefiniowanych przez użytkownika lub pre-zdefiniowanych przez zapytania.  Hello rozwiązania raporty hello jak aktualny komputer opiera się na jakie źródła są skonfigurowane toosynchronize z.  Jeśli komputer z systemem Windows hello jest tooWSUS tooreport skonfigurowany, w zależności od tego, kiedy usługi WSUS ostatniej synchronizacji z usługą Microsoft Update, wyniki hello mogą się różnić od pokazuje Microsoft Updates.  Witaj takie same dla komputerów z systemem Linux, które są skonfigurowane tooreport tooa lokalnego repozytorium i publicznego repozytorium.   

Można wdrożyć i zainstalować aktualizacje oprogramowania na komputerach, które wymagają aktualizacji hello przez utworzenie zaplanowanego wdrożenia.  Aktualizacje sklasyfikowane jako *opcjonalnie* nie znajdują się w zakresie wdrażania w przypadku komputerów z systemem Windows hello tylko wymaganych aktualizacji.  Witaj zaplanowane wdrożenie definiuje komputerów docelowych otrzymają hello odpowiednie aktualizacje, albo jawne określenie komputera, lub wybierając [grupy komputerów](../log-analytics/log-analytics-computer-groups.md) które jest oparte na dziennik wyszukiwania z określonego zestawu komputery.  Również określić tooapprove harmonogram i wyznaczyć pewien czas, kiedy aktualizacje są dozwolone toobe instalowane w ramach.  Aktualizacje są instalowane przez elementy runbook w usłudze Azure Automation.  Nie można wyświetlić tych elementów runbook i nie wymagają one żadnej konfiguracji.  Podczas wdrażania aktualizacji, tworzy harmonogram uruchamia element główny aktualizacji na powitania określenia czasu na komputerach hello uwzględnione.  Ten główny element runbook uruchamia podrzędny element runbook na każdym agencie, który przeprowadza instalację wymaganych aktualizacji.       

Na powitania daty i godziny w hello wdrożenia aktualizacji komputerów docelowych hello wykonuje wdrożenia hello równolegle.  Skanowanie jest pierwszym aktualizacje hello tooverify wykonywane są nadal wymagane i instaluje je.  Koniecznie toonote dla komputerów klienckich WSUS, jeśli hello aktualizacje nie zostały zatwierdzone w programie WSUS, wdrażanie aktualizacji hello zakończą się niepowodzeniem.  wyniki Hello hello stosowane aktualizacje są przekazywane toobe tooOMS przetwarzane i podsumowano w pulpitach nawigacyjnych hello lub hello wyszukiwanie hello zdarzenia.     

## <a name="prerequisites"></a>Wymagania wstępne
* rozwiązanie Hello obsługuje zostanie wykonana oceny aktualizacji dla systemu Windows Server 2008 lub nowszy, a następnie zaktualizuj wdrożenia dla systemu Windows Server 2008 R2 z dodatkiem SP1 lub nowszy.  Opcje instalacji Server Core i Nano Server nie są obsługiwane.

    > [!NOTE]
    > Obsługa wdrażania aktualizacji tooWindows Server 2008 R2 z dodatkiem SP1 wymaga programu .NET Framework 4.5 i WMF 5.0 lub nowszej.
    >  
* Systemy operacyjne klienta systemu Windows nie są obsługiwane.  
* Agentów systemu Windows musi być skonfigurowany toocommunicate z serwerem z systemem Windows Server Update Services (WSUS) lub mają dostęp tooMicrosoft aktualizacji.  

    > [!NOTE]
    > Hello Windows agent nie można zarządzać jednocześnie przez program System Center Configuration Manager.  
    >
* CentOS 6 (x86/x64) i 7 (x64)  
* Red Hat Enterprise 6 (x86/x64) i 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) i 12 (x64)  
* Ubuntu 12.04 LTS i nowsze x86/x64   
    > [!NOTE]  
    > aktualizacje tooavoid stosowane poza oknem konserwacji na Ubuntu, ponownie skonfiguruj aktualizacje automatyczne toodisable nienadzorowanego uaktualnienia pakietu. Aby uzyskać informacje na temat tooconfigure tego, zobacz [temat aktualizacji automatycznych w hello Ubuntu Server — przewodnik](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Agentów systemu Linux, musi mieć repozytorium aktualizacji tooan dostępu.  

    > [!NOTE]
    > Agent pakietu OMS dla systemu Linux skonfigurowane obszary robocze OMS toomultiple tooreport nie jest obsługiwany w tym rozwiązaniu.  
    >

Aby uzyskać dodatkowe informacje na temat sposobu tooinstall hello Agent pakietu OMS dla systemu Linux i pobrać najnowszą wersję hello, można znaleźć za[Operations Management Suite agenta dla systemu Linux](https://github.com/microsoft/oms-agent-for-linux).  Informacji dotyczących sposobu tooinstall hello OMS agenta dla systemu Windows, temacie [Operations Management Suite agenta dla systemu Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Uprawnienia
W kolejności toocreate wdrożeń aktualizacji, należy toobe przyznane roli współautora hello konta automatyzacji i obszaru roboczego analizy dzienników.  

## <a name="solution-components"></a>Składniki rozwiązania
To rozwiązanie obejmuje hello następujące zasoby, które zostały dodane konto automatyzacji tooyour i agentów podłączonego bezpośrednio lub Operations Manager podłączonej grupy zarządzania.

### <a name="management-packs"></a>Pakiety administracyjne
Jeśli grupa zarządzania programu System Center Operations Manager jest połączonych tooan obszarem roboczym pakietu OMS, hello następujące pakiety administracyjne są zainstalowane w programie Operations Manager.  Te pakiety administracyjne są również instalowane na bezpośrednio połączonych komputerach z systemem Windows po dodaniu tego rozwiązania. Nie ma nic tooconfigure lub zarządzać za pomocą tych pakietów administracyjnych.

* Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* Pakiet administracyjny wdrożenia aktualizacji

Aby uzyskać więcej informacji dotyczących sposobu aktualizowania rozwiązania pakietów administracyjnych, zobacz [tooLog połączenie programu Operations Manager Analytics](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Grupy hybrydowych procesów roboczych
Po włączeniu tego rozwiązania, komputer z systemem Windows bezpośrednio połączony tooyour obszarem roboczym pakietu OMS jest automatycznie skonfigurowany jako hybrydowy proces roboczy elementu Runbook toosupport hello elementy runbook zawarte w tym rozwiązaniu.  Dla każdego komputera z systemem Windows są zarządzane przez rozwiązanie hello będzie wyświetlane w bloku grup roboczych Runbook hybrydowego hello konta automatyzacji hello następującą konwencją hello *Hostname FQDN_GUID*.  Te grupy nie mogą być celami dla elementów runbook na Twoim koncie, w przeciwnym razie działanie tych elementów zakończy się niepowodzeniem. Te grupy są wyłącznie zamierzonego toosupport hello rozwiązanie do zarządzania.   

Można jednak dodać hello systemu Windows komputerów tooa hybrydowy proces roboczy elementu Runbook grupę w Twojej toosupport konta automatyzacji elementu runbook usługi Automatyzacja, tak długo, jak używasz hello tego samego konta dla rozwiązania hello i członkostwa w grupie hybrydowy proces roboczy elementu Runbook.  Ta funkcja została dodana tooversion 7.2.12024.0 hello hybrydowy proces roboczy elementu Runbook.  

## <a name="configuration"></a>Konfiguracja
Wykonaj następujące kroki tooadd hello zarządzania aktualizacjami rozwiązania tooyour obszarem roboczym pakietu OMS hello i upewnij się, że agenci są raportowania. Obszar roboczy tooyour już połączoną agentów systemu Windows są automatycznie dodawane bez konieczności dodatkowej konfiguracji.

Można wdrożyć rozwiązanie hello przy użyciu hello następujące metody:

* Z portalu Azure Marketplace w hello portalu Azure, wybierając oferty usługi Automatyzacja i kontrola hello lub rozwiązania do zarządzania aktualizacjami
* Z hello OMS galerii rozwiązań w obszarze roboczym pakietu OMS

Jeśli masz już konto automatyzacji i obszarem roboczym pakietu OMS połączone w hello tej samej grupie zasobów i region, wybierając Automatyzacja i kontrola będzie Sprawdź konfigurację i instaluj hello rozwiązania i tylko ją skonfigurować w obu usług.  Wybieranie rozwiązania do zarządzania aktualizacji hello z portalu Azure Marketplace dostarcza hello takie samo zachowanie.  Jeśli nie masz albo usługi wdrożone w ramach subskrypcji, wykonaj kroki hello w hello **Utwórz nowe rozwiązanie** bloku i potwierdzenie tooinstall hello innych wstępnie zaznaczona zalecane rozwiązania.  Opcjonalnie można dodać tooyour rozwiązania zarządzania aktualizacjami hello obszarem roboczym pakietu OMS hello kroki opisane w [rozwiązań dodać OMS](../log-analytics/log-analytics-add-solutions.md) z hello galerii rozwiązań.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>Potwierdź OMS agentów i tooOMS podłączone grupy zarządzania programu Operations Manager

tooconfirm bezpośrednio połączony Agent pakietu OMS dla systemu Linux i Windows komunikują się z usługą OMS, po kilku minutach można uruchomić powitania po wyszukiwania dziennika:

* Linux — `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows — `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

Na komputerze z systemem Windows możesz przejrzeć następujące tooverify agenta łączność z usługą OMS hello:

1.  Otwórz program Microsoft Monitoring Agent w Panelu sterowania, a na powitania **Analiza dzienników Azure (OMS)** pozycję hello agenta wyświetla komunikat z informacją: **hello Microsoft Monitoring Agent została pomyślnie nawiązano połączenie toohello firmy Microsoft Usługa Operations Management Suite**.   
2.  Otwórz dziennik zdarzeń systemu Windows hello, przejdź zbyt**aplikacji i usług Menedżera Logs\Operations** i poszukaj zdarzeń identyfikator 3000 i 5002 ze źródła łącznika usługi.  Te zdarzenia wskazują hello komputer został zarejestrowany za pomocą hello obszarem roboczym pakietu OMS i odbiera konfiguracji.  

Jeśli hello agent nie jest możliwe toocommunicate z hello usługę i jest skonfigurowany toocommunicate z hello internet za pośrednictwem zapory lub serwera proxy, potwierdź hello zapory lub serwera proxy jest prawidłowo skonfigurowane, przeglądając [sieci Konfiguracja agenta Windows](../log-analytics/log-analytics-windows-agents.md#network) lub [konfigurację sieci dla agenta systemu Linux](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Jeśli systemy Linux są toocommunicate skonfigurowany za pomocą serwera proxy lub bramy OMS i dołączania tego rozwiązania, zaktualizuj hello *proxy.conf* uprawnienia toogrant hello omiuser grupy uprawnienie do odczytu w pliku hello przez wykonywanie hello następującego polecenia:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Po przeprowadzeniu oceny nowo dodani agenci systemu Linux będą mieć stan **Zaktualizowane**.  Ten proces może zająć godziny too6.

tooconfirm programu Operations Manager grupy zarządzania komunikuje się z usługą OMS, zobacz [zweryfikować integracji programu Operations Manager z usługą OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Zbieranie danych
### <a name="supported-agents"></a>Obsługiwani agenci
Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie.

| Połączone źródło | Obsługiwane | Opis |
| --- | --- | --- |
| Agenci dla systemu Windows |Tak |rozwiązanie Hello zbiera informacje o aktualizacjach systemu z agentów systemu Windows i inicjuje instalacji wymaganych aktualizacji. |
| Agenci dla systemu Linux |Tak |rozwiązanie Hello zbiera informacje o aktualizacjach systemu z agentów systemów Linux i inicjuje instalacji wymaganych aktualizacji na obsługiwanych dystrybucjach. |
| Grupa zarządzania programu Operations Manager |Tak |rozwiązanie Hello zbiera informacje o aktualizacji systemu przez agentów w dołączonej grupy zarządzania.<br>Połączenie bezpośrednie z tooLog agenta programu Operations Manager hello Analytics nie jest wymagane. Dane są przesyłane z hello zarządzania grupy toohello OMS repozytorium. |
| Konto magazynu Azure |Nie |Magazyn Azure nie zawiera informacji o aktualizacjach systemu. |

### <a name="collection-frequency"></a>Częstotliwość zbierania
Skanowanie każdego zarządzanego komputera z systemem Windows odbywa się dwa razy dziennie. Co 15 minut hello interfejsu API systemu Windows jest wywoływana tooquery dla hello ostatniej aktualizacji czasu toodetermine Jeśli stan został zmieniony, a jeśli tak jest inicjowane skanowania zgodności.  Skanowanie każdego zarządzanego komputera z systemem Linux odbywa się co 3 godziny.

Go może potrwać od 30 minut się too6 godzin hello pulpitu nawigacyjnego toodisplay zaktualizowane dane z zarządzanych komputerów.   

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello
Po dodaniu obszar roboczy OMS tooyour rozwiązania zarządzania aktualizacjami hello hello **zarządzania aktualizacjami** kafelka zostanie dodany tooyour OMS z pulpitu nawigacyjnego. Ten Kafelek Wyświetla graficzną reprezentację hello liczby komputerów i liczba w danym środowisku i ich zgodności aktualizacji.<br><br>
![Kafelek podsumowujący zarządzanie aktualizacjami](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Wyświetlanie ocen aktualizacji
Polecenie hello **zarządzania aktualizacjami** hello tooopen kafelka **zarządzania aktualizacjami** pulpitu nawigacyjnego.<br><br> ![Pulpit nawigacyjny podsumowujący zarządzanie aktualizacjami](./media/oms-solution-update-management/update-management-dashboard.png)<br>

Ten pulpit nawigacyjny zawiera szczegółowy podział stanu aktualizacji według typu systemu operacyjnego i klasyfikacji aktualizacji — krytyczna, bezpieczeństwa lub inna (taka jak aktualizacja definicji). powoduje Hello każdego kafelka na tym pulpicie nawigacyjnym odzwierciedlać tylko te aktualizacje, które zostały zatwierdzone do wdrożenia, która jest oparta na podstawie źródło synchronizacji komputerów hello.   Witaj **wdrożenia aktualizacji** kafelka w przypadku wybrania, przekieruje Cię toohello strony wdrożenia aktualizacji, którym można wyświetlać harmonogramy, wdrożenia aktualnie uruchomione, jest wdrażanie ukończone lub Planowanie nowego wdrożenia.  

Można uruchomić wszystkie rekordy przez kliknięcie kafelka określonego hello lub toorun zapytania określonej kategorii i wstępnie zdefiniowane kryteria wyszukiwania dziennika, wybierz jedną z dostępnych w ramach hello listy hello **typowych kwerend aktualizacji** kolumny.    

## <a name="installing-updates"></a>Instalowanie aktualizacji
Po aktualizacji zostały ocenione wszystkie hello systemu Linux i komputerów z systemem Windows w obszarze roboczym, można posiadasz wymagane aktualizacje zainstalowane przez utworzenie *wdrożenia aktualizacji*.  Wdrożenie aktualizacji to zaplanowana instalacja wymaganych aktualizacji na co najmniej jednym komputerze.  Określ hello Data i godzina wdrożenia hello dodatkowo tooa komputer lub grupę komputerów, które powinny znajdować się w zakresie hello wdrożenia.  toolearn więcej informacji na temat grup komputerów, zobacz [grup komputerów w analizy dzienników](../log-analytics/log-analytics-computer-groups.md).  Po dołączeniu grup komputerów w danym wdrożeniu aktualizacji memnbership grupy jest oceniane tylko raz w hello godzina utworzenia harmonogramu.  Grupy tooa kolejne zmiany nie są widoczne.  toowork wokół, Usuń wdrożenie aktualizacji hello zaplanowane i utwórz ją ponownie.

> [!NOTE]
> Maszyny wirtualne systemu Windows wdrożone z hello Azure Marketplace domyślnie są ustawione tooreceive automatyczne aktualizacje z usługi Windows Update.  To zachowanie nie zmienia się po dodaniu tego rozwiązania lub obszar roboczy tooyour maszyn wirtualnych systemu Windows.  Jeśli to zrobisz, nie jest aktywnie zarządzanych aktualizacje dotyczące tego rozwiązania, hello domyślne zachowanie (automatyczne stosowanie aktualizacji) będą stosowane.  

Dla maszyn wirtualnych utworzonych z hello na żądanie Red Hat Enterprise Linux (RHEL) dostępnych obrazów w portalu Azure Marketplace, są one hello zarejestrowanych tooaccess [Red Hat aktualizacji infrastruktury (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) wdrożona na platformie Azure.  Inne dystrybucji systemu Linux, musi zostać zaktualizowany z repozytorium pliku online dystrybucjach powitania po ich obsługiwane metody.  

### <a name="viewing-update-deployments"></a>Wyświetlanie wdrożeń aktualizacji
Kliknij przycisk hello **wdrożenia aktualizacji** kafelka tooview hello lista istniejące wdrożenia aktualizacji.  Są one pogrupowane według stanu — **Zaplanowano**, **Uruchomiono** i **Ukończono**.<br><br> ![Strona harmonogramu wdrożenia aktualizacji](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

w hello w poniższej tabeli opisano Hello wyświetlania właściwości dla każdego wdrożenia aktualizacji.

| Właściwość | Opis |
| --- | --- |
| Nazwa |Nazwa hello wdrożenia aktualizacji. |
| Harmonogram |Typ harmonogramu.  Dostępne opcje to *Jednorazowo*, *Co tydzień* i *Co miesiąc*. |
| Godzina rozpoczęcia |Data i godzina, które hello wdrożenia aktualizacji jest zaplanowane toostart. |
| Czas trwania |Liczba minut hello wdrożenia aktualizacji jest dozwolone toorun.  Jeśli wszystkie aktualizacje nie są zainstalowane w ramach tego czasu trwania, a następnie hello pozostałych aktualizacji musi czekać hello dalej wdrożenia aktualizacji. |
| Serwery |Liczba komputerów objętych hello wdrożenia aktualizacji.  |
| Stan |Bieżący stan hello wdrożenia aktualizacji.<br><br>Możliwe wartości:<br>- Nie uruchomiono<br>- Uruchomiono<br>- Ukończono |

Zaznacz ukończonego wdrożenia aktualizacji tooview hello szczegółów ekran zawierającej kolumny hello w hello w poniższej tabeli.  Te kolumny nie będzie wypełniana w przypadku hello wdrażanie aktualizacji nie został jeszcze uruchomiony.<br><br> ![Przegląd wyników wdrożenia aktualizacji](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Kolumna | Opis |
| --- | --- |
| **Widok komputerów** | |
| Komputery z systemem Windows |Wyświetla liczbę hello w hello wdrożenia aktualizacji według stanu komputerów z systemem Windows.  Polecenie toorun stanu wyszukiwania dziennika, zwracając się, że wszystkie aktualizowania rekordów o stanie dla hello wdrożenia aktualizacji. |
| Komputery z systemem Linux |Wyświetla liczbę hello komputery z systemem Linux w hello wdrożenia aktualizacji według stanu.  Polecenie toorun stanu wyszukiwania dziennika, zwracając się, że wszystkie aktualizowania rekordów o stanie dla hello wdrożenia aktualizacji. |
| Stan instalacji komputera |Wyświetla listę komputerów hello objętego hello wdrażania aktualizacji i procent hello aktualizacji, których pomyślnie zainstalowano. Kliknij jeden z hello toorun wpisów dziennika wyszukiwania zwracanie wszystkich aktualizacji krytycznych i brak. |
| **Widok aktualizacji** | |
| Aktualizacje systemu Windows |Zawiera listę aktualizacji systemu Windows objętych hello wdrażania aktualizacji i ich stan instalacji dla każdej aktualizacji.  Wybierz wyszukiwanie dziennika przekazywania wszystkich aktualizowania rekordów dla tej konkretnej aktualizacji lub kliknij toorun stan hello wyszukiwania dziennika zwracanie wszystkich aktualizacji rejestruje wdrożenia hello toorun aktualizacji. |
| Aktualizacje systemu Linux |Wyświetla listę Linux aktualizacje zawarte w hello wdrażania aktualizacji i ich stan instalacji dla każdej aktualizacji.  Wybierz wyszukiwanie dziennika przekazywania wszystkich aktualizowania rekordów dla tej konkretnej aktualizacji lub kliknij toorun stan hello wyszukiwania dziennika zwracanie wszystkich aktualizacji rejestruje wdrożenia hello toorun aktualizacji. |

### <a name="creating-an-update-deployment"></a>Tworzenie wdrożenia aktualizacji
Utwórz nowe wdrożenie aktualizacji, klikając hello **Dodaj** u góry hello hello tooopen ekranie powitania **nowe wdrożenie aktualizacji** strony.  Należy podać wartości dla właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
| --- | --- |
| Nazwa |Wdrażanie aktualizacji hello tooidentify unikatową nazwę. |
| Strefa czasowa |Strefa czasowa toouse hello czas rozpoczęcia. |
| Typ harmonogramu | Typ harmonogramu.  Dostępne opcje to *Jednorazowo*, *Co tydzień* i *Co miesiąc*.  
| Godzina rozpoczęcia |Data i godzina toostart hello wdrożenia aktualizacji. **Uwaga:** hello najwcześniej wdrożenia można uruchomić jest 30 minutach od bieżącego czasu, jeśli potrzebujesz toodeploy natychmiast. |
| Czas trwania |Liczba minut hello wdrożenia aktualizacji jest dozwolone toorun.  Jeśli wszystkie aktualizacje nie są zainstalowane w ramach tego czasu trwania, a następnie hello pozostałych aktualizacji musi czekać hello dalej wdrożenia aktualizacji. |
| Komputery |Nazwy komputerów lub tooinclude grup komputerów i obiektów docelowych w hello wdrożenia aktualizacji.  Wybierz jeden lub więcej wpisów z listy rozwijanej hello. |

<br><br> ![Strona nowego wdrożenia aktualizacji](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Przedział czasu
Domyślnie hello zakres danych hello przeanalizowane w hello rozwiązania do zarządzania aktualizacji jest z wszystkich podłączonych grup zarządzania wygenerowaniem hello ostatni 1 dzień.

Wybierz zakres czasu hello toochange danych hello **na podstawie danych** u góry hello hello pulpitu nawigacyjnego. Możesz wybrać rekordy utworzone lub zaktualizowane w ramach hello ostatnich 7 dni, 1 dzień lub 6 godzin. Możesz też wybrać opcję **Niestandardowy** i określić niestandardowy zakres dat.

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Witaj rozwiązania do zarządzania aktualizacjami tworzy dwa typy rekordów w repozytorium OMS hello.

### <a name="update-records"></a>Rekordy Update (Aktualizacja)
Rekord o typie **Update** (Aktualizacja) jest tworzony dla każdej aktualizacji, która jest zainstalowana lub wymagana na poszczególnych komputerach. Aktualizacja rekordów mają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
| --- | --- |
| Typ |*Aktualizacja* |
| SourceSystem |Źródło Hello zatwierdzonych instalacji aktualizacji hello.<br>Możliwe wartości:<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Linux Servers (serwery systemu Linux pobrane z menedżerów pakietów) |
| Approved (Zatwierdzono) |Określa, czy aktualizacja hello zostało zatwierdzone do instalacji.<br> W przypadku serwerów z systemem Linux jest to obecnie opcjonalne, ponieważ poprawki nie są zarządzane przez usługę OMS. |
| Klasyfikacja dla systemu Windows |Klasyfikacja aktualizacji hello.<br>Możliwe wartości:<br>- Applications (Aplikacje)<br>- Critical Updates (Aktualizacje krytyczne)<br>- Definition Updates (Aktualizacje definicji)<br>- Feature Packs (Pakiety funkcji)<br>- Security Updates (Aktualizacje zabezpieczeń)<br>- Service Packs (Dodatki Service Pack)<br>- Update Rollups (Pakiety zbiorcze aktualizacji)<br>- Updates (Aktualizacje) |
| Klasyfikacja dla systemu Linux |Cassification hello aktualizacji.<br>Możliwe wartości:<br>- Critical Updates (Aktualizacje krytyczne)<br>- Security Updates (Aktualizacje zabezpieczeń)<br>- Other Updates (Inne aktualizacje) |
| Computer (Komputer) |Nazwa komputera hello. |
| InstallTimeAvailable |Określa, czy hello czas instalacji jest dostępny z innych agentów zainstalowanych hello sam aktualizacji. |
| InstallTimePredictionSeconds |Szacowany czas instalacji, w sekundach, w oparciu o innych agentów zainstalowanych hello tej samej aktualizacji. |
| KBID |Identyfikator artykułu hello KB, który opisuje hello aktualizacji. |
| ManagementGroupName |Nazwa grupy zarządzania hello agentów programu SCOM.  W przypadku innych agentów jest to AOI-<workspace ID>. |
| MSRCBulletinID |Identyfikator biuletynu Microsoft hello opisujące hello aktualizacji. |
| MSRCSeverity |Ważność hello biuletynu zabezpieczeń.<br>Możliwe wartości:<br>- Critical (Krytyczny)<br>- Important (Ważny)<br>- Moderate (Średni) |
| Optional (Opcjonalność) |Określa, czy aktualizacja hello jest opcjonalne. |
| Product (Produkt) |Nazwa aktualizacji hello hello jest.  Kliknij przycisk **widoku** tooopen hello artykułu w przeglądarce. |
| PackageSeverity |ważność Hello hello luki w zabezpieczeniach naprawiane przez tę aktualizację, zgodnie z raportem hello Linux distro dostawców. |
| PublishDate |Data i godzina hello aktualizacja została zainstalowana. |
| RebootBehavior |Określa, czy aktualizacji hello wymusza ponowne uruchomienie komputera.<br>Możliwe wartości:<br>- canrequestreboot (może wymagać ponownego uruchomienia)<br>- neverreboots (nigdy nie uruchamia ponownie) |
| RevisionNumber |Numer poprawki hello aktualizacji. |
| SourceComputerId |Identyfikator GUID toouniquely identyfikacji hello komputera. |
| TimeGenerated |Data i godzina hello rekordu ostatniej aktualizacji. |
| Tytuł |Tytuł hello aktualizacji. |
| UpdateID |Identyfikator GUID toouniquely zidentyfikować hello aktualizacji. |
| UpdateState |Określa, czy aktualizacja hello jest zainstalowana na tym komputerze.<br>Możliwe wartości:<br>-Zainstalowany — aktualizacja hello jest zainstalowany na tym komputerze.<br>-Potrzeb — hello aktualizacji nie jest zainstalowany i jest wymagane na tym komputerze. |

Po wykonaniu wyszukiwania dziennika zwraca rekordów z typem **aktualizacji** można wybrać hello **aktualizacje** widoku, który zawiera zestaw kafelków podsumowania aktualizacji hello zwrócona przez wyszukiwanie hello. Można kliknąć pozycji hello w hello **Brak i stosowane aktualizacje** i **aktualizacji wymaganych i opcjonalnych** Kafelki tooscope hello widoku toothat zestaw aktualizacji. Wybierz hello **listy** lub **tabeli** wyświetlić tooreturn hello poszczególne rekordy.<br>

![Widok aktualizacji wyszukiwania w dzienniku z aktualizacją typu rekord](./media/oms-solution-update-management/update-la-view-updates.png)  

W hello **tabeli** widoku, możesz kliknąć hello **KBID** dla żadnych rekordów tooopen przeglądarki z artykułem hello KB. Dzięki temu tooquickly należy przeczytać o szczegóły hello hello dana aktualizacja.<br>

![Widok tabeli wyszukiwania w dzienniku z kafelkami aktualizacji typu rekord](./media/oms-solution-update-management/update-la-view-table.png)

W hello **listy** widok, kliknij hello **widoku** łącze dalej toohello KBID tooopen hello KB artykułu.<br>

![Widok listy wyszukiwania w dzienniki z kafelkami aktualizacji typu rekord](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>Rekordy UpdateSummary
Rekord **UpdateSummary** jest tworzony dla każdego komputera agenta systemu Windows. Ten rekord jest aktualizowana każdorazowo hello komputer zostaje przeprowadzone skanowanie aktualizacji. **UpdateSummary** rekordów mają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
| --- | --- |
| Typ |UpdateSummary |
| SourceSystem |OpsManager |
| Computer (Komputer) |Nazwa komputera hello. |
| CriticalUpdatesMissing |Liczba na komputerze hello brakuje aktualizacji krytycznych. |
| ManagementGroupName |Nazwa grupy zarządzania hello agentów programu SCOM. W przypadku innych agentów jest to AOI-<workspace ID>. |
| NETRuntimeVersion |Wersja środowiska uruchomieniowego .NET hello zainstalowany na komputerze hello. |
| OldestMissingSecurityUpdateBucket |Zasobnik toocategorize hello czas od momentu opublikowania hello najstarsze brakujących aktualizacji zabezpieczeń na tym komputerze.<br>Możliwe wartości:<br>- OIder (Starsze)<br>- 180 days ago (180 dni temu)<br>- 150 days ago (150 dni temu)<br>- 120 days ago (120 dni temu)<br>- 90 days ago (90 dni temu)<br>- 60 days ago (60 dni temu)<br>- 30 days ago (30 dni temu)<br>- Recent (Najnowsze) |
| OldestMissingSecurityUpdateInDays |Liczba dni od momentu opublikowania hello najstarsze brakujących aktualizacji zabezpieczeń na tym komputerze. |
| OsVersion |Wersja systemu operacyjnego hello zainstalowanego na komputerze hello. |
| OtherUpdatesMissing |Liczba innych aktualizacji na komputerze hello brakuje. |
| SecurityUpdatesMissing |Liczba aktualizacji zabezpieczeń na komputerze hello brakuje. |
| SourceComputerId |Identyfikator GUID toouniquely identyfikacji hello komputera. |
| TimeGenerated |Data i godzina hello rekordu ostatniej aktualizacji. |
| TotalUpdatesMissing |Całkowita liczba aktualizacji na komputerze hello brakuje. |
| WindowsUpdateAgentVersion |Numer wersji hello usługi Windows Update agent na komputerze hello. |
| WindowsUpdateSetting |Ustawienie jak hello komputer instaluje ważne aktualizacje.<br>Możliwe wartości:<br>- Disabled (Wyłączono)<br>- Notify before installation (Powiadom przed rozpoczęciem instalacji)<br>- Scheduled installation (Instalacja zaplanowana) |
| WSUSServer |Adres URL programu WSUS na serwerze, jeśli komputer hello jest skonfigurowany toouse jeden. |

## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników
Witaj w poniższej tabeli zawiera przykładowy dziennik wyszukuje rekordów aktualizacji zebrane przez to rozwiązanie.

| Zapytanie | Opis |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Serwery z systemem Windows wymagające aktualizacji |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Serwery z systemem Linux wymagające aktualizacji | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Wszystkie komputery z brakującymi aktualizacjami |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Brakujące aktualizacje dla konkretnego komputera (zastąp wartość własną nazwą komputera)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Wszystkie komputery z brakującymi aktualizacjami krytycznymi i zabezpieczeń | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Aktualizacje krytyczne lub zabezpieczeń wymagane przez komputery, na których aktualizacje są stosowane ręcznie |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |Zdarzenia błędu dotyczące komputerów, na których brakuje wymaganych aktualizacji krytycznych lub zabezpieczeń |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Wszystkie komputery z brakującymi pakietami zbiorczymi aktualizacji | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Różne brakujące aktualizacje na wszystkich komputerach | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Serwer z systemem Windows z aktualizacjami, które nie powiodły się podczas przebiegu aktualizacji | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Serwer z systemem Linux z aktualizacjami, które nie powiodły się podczas przebiegu aktualizacji | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |Korzystanie przez komputer z usług WSUS | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Konfiguracja automatycznej aktualizacji | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Komputery z wyłączoną automatyczną aktualizacją | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Listy wszystkich maszyn Linux hello, w których jest dostępna aktualizacja pakietu | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Listy wszystkich maszyn hello Linux, które dostępna aktualizacja pakietu, który usterki krytyczne lub zabezpieczeń | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |Lista wszystkich pakietów, które mają dostępną aktualizację | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |Lista wszystkich pakietów, dla których jest dostępna aktualizacja o znaczeniu krytycznym lub dotycząca luki w zabezpieczeniach | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Lista wdrożeń aktualizacji, które zmodyfikowały komputery | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Komputery, które zostały zaktualizowane w ramach tego przebiegu aktualizacji (zastąp wartość nazwą własnego wdrożenia aktualizacji) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Listę wszystkich komputerów "Ubuntu" hello z dostępna aktualizacja | 

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Ta sekcja zawiera informacje toohelp Rozwiązywanie problemów z hello rozwiązania do zarządzania aktualizacji.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Jak mogę rozwiązywać problemy przy dołączaniu?
Jeśli wystąpią problemy podczas próby rozwiązania hello tooonboard lub maszyny wirtualnej, sprawdź hello **aplikacji i usług Menedżera Logs\Operations** dziennika zdarzeń dla zdarzenia ze zdarzenia 4502 identyfikator i zdarzenia komunikat zawierający **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Witaj w poniższej tabeli wyróżniono określone komunikaty o błędach i możliwe rozwiązanie dla każdego.  

| Komunikat | Przyczyna | Rozwiązanie |   
|----------|----------|----------|  
| Nie można tooRegister komputera w celu zarządzania poprawki<br>rejestracja nie powiodła się z powodu wyjątku<br>System.InvalidOperationException: {"Message": "Maszyna jest już<br>zarejestrowany tooa innego konta. "} | Komputer jest już obszar roboczy tooanother został załadowany do zarządzania aktualizacjami | Przeprowadzić czyszczenie starego artefaktów przez [usuwanie grupa hello hybrydowych elementu runbook](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Jest zbyt zarejestrować komputera w celu zarządzania poprawki<br>rejestracja nie powiodła się z powodu wyjątku<br>System.Net.Http.HttpRequestException: Wystąpił błąd podczas wysyłania żądania hello. ---><br>System.Net.WebException: połączenie podstawowe hello<br>zostało zamknięte: Wystąpił nieoczekiwany błąd<br>przy odbiorze. ---> System.ComponentModel.Win32Exception:<br>Nie można komunikować powitania klienta i serwera<br>ponieważ nie mają wspólnego algorytmu | Serwer proxy/brama/zapora blokuje komunikację | [Przejrzyj wymagania dotyczące sieci](../automation/automation-offering-get-started.md#network-planning)|  
| Nie można tooRegister komputera w celu zarządzania poprawki<br>rejestracja nie powiodła się z powodu wyjątku<br>Newtonsoft.Json.JsonReaderException: Błąd podczas analizowania wartości nieskończoności dodatniej. | Serwer proxy/brama/zapora blokuje komunikację | [Przejrzyj wymagania dotyczące sieci](../automation/automation-offering-get-started.md#network-planning)| 
| Witaj certyfikat przedstawiony przez usługę hello <wsid>. oms.opinsights.azure.com<br>nie został wystawiony przez urząd certyfikacji<br>używany na potrzeby usług firmy Microsoft. Skontaktuj się z<br>toosee administrator sieci, jeśli korzystają z serwera proxy przechwytującego<br>komunikację TLS/SSL. |Serwer proxy/brama/zapora blokuje komunikację | [Przejrzyj wymagania dotyczące sieci](../automation/automation-offering-get-started.md#network-planning)|  
| Nie można tooRegister komputera w celu zarządzania poprawki<br>rejestracja nie powiodła się z powodu wyjątku<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Nie można toocreate certyfikatu z podpisem własnym. ---><br>System.UnauthorizedAccessException: Odmowa dostępu. | Niepowodzenie generowania certyfikatu z podpisem własnym | Sprawdź, czy konto systemowe ma<br>toofolder dostęp do odczytu:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Jak rozwiązywać problemy z wdrożeniami aktualizacji?
Można wyświetlić wyniki hello elementu runbook hello odpowiedzialnych za wdrażanie aktualizacji hello dołączonych do wdrożenia aktualizacji hello zaplanowane z hello bloku zadania konta automatyzacji, która jest połączona z obszarem roboczym pakietu OMS hello obsługi tego rozwiązania.  Witaj runbook **MicrosoftOMSComputer poprawki** jest podrzędnego elementu runbook, którego celem jest określony zarządzany komputer i przeglądanie strumień pełny hello przedstawia szczegółowe informacje dotyczące tego wdrożenia.  Hello danych wyjściowych będzie wyświetlane, którego wymagane aktualizacje są stosowane, Pobierz stan, stan instalacji oraz dodatkowe szczegółowe informacje.<br><br> ![Stan zadania wdrożenia aktualizacji](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Aby uzyskać więcej informacji, zobacz [Automation runbook output and messages](../automation/automation-runbook-output-and-messages.md) (Dane wyjściowe i komunikaty elementu runbook usługi Automation).   

## <a name="next-steps"></a>Następne kroki
* Użyj dziennika wyszukiwania w [analizy dzienników](../log-analytics/log-analytics-log-searches.md) tooview szczegółowe dane aktualizacji.
* [Tworzenie własnych pulpitów nawigacyjnych](../log-analytics/log-analytics-dashboards.md) przedstawiających zgodność aktualizacji na zarządzanych komputerach.
* [Tworzenie alertów](../log-analytics/log-analytics-alerts.md) po wykryciu braku aktualizacji krytycznych na komputerach lub komputera z wyłączonymi aktualizacjami automatycznymi.  
