---
title: aaaGraphical tworzenia automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Tworzenie graficznych pozwala toocreate elementów runbook usługi Automatyzacja Azure bez Praca z kodem. Ten artykuł zawiera wprowadzenie toographical tworzenia i wszystkie szczegóły hello wymagane toostart tworzenia graficznego elementu runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Graficzny tworzenia w programie usługi Automatyzacja Azure
## <a name="introduction"></a>Wprowadzenie
Tworzenie graficznych umożliwia toocreate elementów runbook automatyzacji Azure bez złożoności hello hello podstawowy kod programu Windows PowerShell lub przepływ pracy programu PowerShell. Dodaj działania toohello kanwy z biblioteki poleceń cmdlet i elementy runbook, je połączyć ze sobą i skonfiguruj tooform przepływ pracy.  Jeśli kiedykolwiek mający doświadczenie z programu System Center Orchestrator lub automatyzacji zarządzania usługi (SMA), to powinno wyglądać tooyou znane.   

Ten artykuł zawiera toographical wprowadzenie do tworzenia i hello koncepcje potrzebne tooget uruchomiona podczas tworzenia graficznego elementu runbook.

## <a name="graphical-runbooks"></a>Graficznych elementów runbook
Wszystkie elementy runbook w automatyzacji Azure są przepływów pracy programu Windows PowerShell.  Graficzne i przepływ pracy programu PowerShell graficznego elementów runbook do generowania kodu programu PowerShell jest uruchamiany przez pracowników automatyzacji hello, ale nie jest możliwe tooview go lub go bezpośrednio modyfikować.  Graficzny element runbook może być przekonwertowany tooa runbook graficzny przepływ pracy programu PowerShell i na odwrót, ale ich nie może być przekonwertowany tooa tekstowa elementu runbook. Nie można zaimportować tekstową istniejącego elementu runbook do edytora graficznego hello.  

## <a name="overview-of-graphical-editor"></a>Omówienie edytora graficznego usługi
Można otworzyć edytora graficznego usługi hello w portalu Azure hello przez utworzenie lub edycję graficznego elementu runbook.

![Graficzny obszaru roboczego](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Witaj poniższych sekcjach opisano hello formantów w oknie edytora graficznego usługi hello.

### <a name="canvas"></a>Kanwy
Hello kanwy jest, gdzie projektowania elementu runbook.  Dodaj działania z węzłów hello w hello biblioteki kontroli toohello runbook i łączenia ich z logiką hello toodefine łącza hello elementu runbook.

Formanty hello można użyć u dołu hello toozoom kanwy hello i wylogowanie.

![Graficzny obszaru roboczego](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Formant biblioteki
Hello formant biblioteki jest, gdzie wybierz [działania](#activities) tooadd tooyour runbook.  Należy je dodać kanwy toohello podłączenia ich tooother działania.  Zawiera cztery sekcje opisane w poniższej tabeli hello.

| Sekcja | Opis |
|:--- |:--- |
| Polecenia cmdlet |Zawiera wszystkie polecenia cmdlet hello, które mogą być używane w elemencie runbook.  Polecenia cmdlet są zorganizowane według modułu.  Wszystkie moduły hello, które zostały zainstalowane na Twoim koncie automatyzacji będą dostępne. |
| Elementy Runbook |Zawiera elementy runbook hello na Twoim koncie automatyzacji. Te elementy runbook mogą być dodawane toobe kanwy toohello używany jako podrzędne elementy runbook. Wyświetlane są tylko elementów runbook hello same podstawowe typu jako hello runbook edytowany; Graficzne elementy runbook tylko opartych na środowisku PowerShell w elementach runbook są pokazane, gdy przepływ pracy programu PowerShell graficznego elementów runbook są wyświetlane tylko przepływ pracy opartych na środowisku PowerShell elementów runbook. |
| Elementy zawartości |Obejmuje hello [zasoby automatyzacji](http://msdn.microsoft.com/library/dn939988.aspx) na koncie automatyzacji, który może być używana w elemencie runbook.  Podczas dodawania elementu runbook tooa zasobów, spowoduje to dodanie działania przepływu pracy, który pobiera hello wybranych zasobów.  W przypadku hello zasobów zmiennej można wybrać czy tooadd tooget działania hello hello zmiennej lub ustaw zmienną. |
| Sterowanie elementem Runbook |Obejmuje działania kontroli elementu runbook, które mogą być używane w bieżącym elemencie runbook. A *Rozgałęzienie* przyjmuje wielu danych wejściowych i czeka, aż wszystkie została ukończona przed kontynuowanie hello przepływu pracy. A *kod* jeden lub więcej wierszy kodu programu PowerShell lub przepływ pracy programu PowerShell, w zależności od typu graficznym elementem runbook hello odbywa się działanie.  To działanie można użyć niestandardowego kodu lub funkcje, które są trudne tooachieve z innymi działaniami. |

### <a name="configuration-control"></a>Kontrola konfiguracji
Hello Kontrola konfiguracji jest, gdzie podać szczegóły dla obiekt na kanwie hello. właściwości Hello dostępne w tym formancie zależy od typu hello wybranego obiektu.  Po wybraniu opcji w hello konfiguracji kontroli, zostanie otwarty dodatkowe bloki w kolejności tooprovide dodatkowe informacje.

### <a name="test-control"></a>Formant testu
Hello kontroli testu nie jest wyświetlany po pierwszym uruchomieniu hello edytora graficznego. Po otwarciu możesz interaktywnie [test graficznym elementem runbook](#graphical-runbook-procedures).  

## <a name="graphical-runbook-procedures"></a>Procedury graficznym elementem runbook
### <a name="exporting-and-importing-a-graphical-runbook"></a>Eksportowanie i importowanie graficznego elementu runbook
Można wyeksportować tylko hello opublikowanej wersji graficznego elementu runbook.  Jeśli hello elementu runbook nie został opublikowany, następnie hello **eksportu opublikowane** przycisk zostanie wyłączone.  Po kliknięciu hello **eksportu opublikowane** przycisku, hello element runbook jest pobrany tooyour komputera lokalnego.  Nazwa Hello hello pliku odpowiada nazwie hello hello runbook za pomocą *graphrunbook* rozszerzenia.

![Eksportuj opublikowanych](media/automation-graphical-authoring-intro/runbook-export.png)

Możesz zaimportować plik elementu runbook graficzny lub graficzny przepływ pracy programu PowerShell, wybierając hello **zaimportować** podczas dodawania elementu runbook.   Po wybraniu hello pliku tooimport można zachować hello sam **nazwa** lub podaj nową.  po jego ocenia pliku hello wybranego i jeśli próba tooselect innego typu, która jest niepoprawna, komunikat zostanie wyświetlone, biorąc pod uwagę, istnieje ryzyko potencjalnych konfliktów i podczas konwersji, mogą wystąpić Hello pola typu element Runbook zostanie wyświetlona hello typu element runbook błędy składniowe.  

![Importowanie elementu runbook](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Testowanie graficznego elementu runbook
Możesz przetestować hello wersję roboczą elementu runbook w portalu Azure hello podczas opuszczania hello opublikowane wersji elementu runbook hello bez zmian lub można przetestować nowy element runbook, zanim został opublikowany. Dzięki temu, że tooverify możesz który hello element runbook działa poprawnie przed zastąpieniem opublikowanej wersji hello. Podczas testowania elementu runbook hello wersja robocza elementu runbook jest wykonywane, i wykonywane są wszystkie akcje, które wykonuje. Historia zadań nie zostało utworzone, ale dane wyjściowe są wyświetlane w okienku danych wyjściowych testu hello. 

Otwórz hello kontroli testu dla elementu runbook, otwierając hello runbook do edycji, a następnie kliknij polecenie hello **okienku testu** przycisku.

![Przycisk Test okienko](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

dla parametrów wejściowych i hello runbook można uruchomić, klikając hello Hello kontroli testu wyświetli monit o **Start** przycisku.

![Przyciski sterowania testu](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Publikowanie graficznego elementu runbook
Każdy element runbook automatyzacji Azure ma wersję roboczą i opublikowaną wersję. Tylko wersję opublikowaną hello jest dostępne toobe uruchomić i tylko wersję roboczą hello można edytowane. Witaj wersję opublikowaną nie mają wpływu wersję roboczą toohello żadnych zmian. Gdy wersję roboczą hello jest dostępne gotowe toobe, należy ją opublikować, która zastępuje hello wersję opublikowaną wersję roboczą hello.

Możesz opublikować graficznego elementu runbook, otwierając hello runbook do edycji, a następnie klikając hello **publikowania** przycisku.

![Przycisk Opublikuj](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Element runbook nie został opublikowany, ma stan **nowy**.  Po opublikowaniu ma stan **opublikowano**.  Po zmodyfikowaniu runbook powitania po opublikowaniu i wersje roboczą i opublikowaną hello są różne, hello runbook ma stan **w edycji**.

![Stany elementu Runbook](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

Masz również hello opcja toorevert toohello opublikowaną wersję elementu runbook.  Optymalizacji zgłasza wszystkie zmiany wprowadzone od elementu runbook hello ostatniej publikacji i zastępuje hello wersję roboczą elementu hello runbook hello opublikowanej wersji.

![Przywróć toopublished przycisku](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>Działania
Działania są blokami konstrukcyjnymi hello elementu runbook.  Działanie może być polecenia cmdlet programu PowerShell, podrzędnego elementu runbook lub działania przepływu pracy.  Dodaj element runbook toohello działanie prawym przyciskiem myszy klikając w hello formant biblioteki i wybierając **dodać toocanvas**.  Można następnie kliknij i przeciągnij go w dowolnym miejscu na powitania kanwy, że chcesz tooplace działania hello.  Witaj lokalizacji hello aktywności hello na kanwie hello nie mają wpływ hello działania elementu runbook hello w dowolny sposób.  Możesz układu elementu runbook jednak znaleźć najodpowiedniejszy toovisualize jej działania. 

![Dodaj toocanvas](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Wybierz działanie hello na powitania kanwy tooconfigure jego właściwości i parametrów w bloku konfiguracji hello.  Możesz zmienić hello **etykiety** z toosomething działania hello, będący tooyou opisowy.  nadal trwa Hello oryginalnego polecenia cmdlet, po prostu zmieniasz jego nazwę wyświetlaną, która będzie używana w hello edytora graficznego.  Etykieta Hello muszą być unikatowe w hello elementu runbook. 

### <a name="parameter-sets"></a>Zestawy parametrów
Zestaw parametrów definiuje parametry obowiązkowe i opcjonalne hello, które będzie akceptować wartości dla określonego polecenia cmdlet.  Wszystkie polecenia cmdlet zawierać co najmniej jeden zestaw parametrów, a niektóre wiele.  Jeśli polecenie cmdlet ma wiele zestawów parametrów, następnie należy wybrać która z nich będzie używać, aby można było skonfigurować parametrów.  Hello parametrów, które można skonfigurować będzie zależeć od zestaw parametrów hello wybranego przez użytkownika.  Możesz zmienić zestaw parametrów hello używany w działaniu, wybierając **ustawić parametr** i wybierając inny zestaw.  W takim przypadku wszystkie wartości parametrów, które skonfigurowano zostaną utracone.

Poniższy przykład hello polecenia cmdlet Get-AzureRmVM hello ma trzy zestawów parametrów.  Nie można skonfigurować wartości parametrów, dopiero po wybraniu hello zestawów parametrów.  Witaj ListVirtualMachineInResourceGroupParamSet zestaw parametrów jest dla zwracania wszystkich maszyn wirtualnych w grupie zasobów i ma jeden parametr opcjonalny.  Witaj GetVirtualMachineInResourceGroupParamSet służy do określania hello maszyny wirtualnej mają tooreturn i ma dwa obowiązkowe i jeden parametr opcjonalny.

![Zestaw parametrów](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Wartości parametrów
Określ wartość dla parametru, wybierz toodetermine źródła danych, jak można określić wartość hello.  Witaj źródeł danych, które są dostępne dla określonego parametru będzie zależeć od hello prawidłowe wartości tego parametru.  Na przykład wartość Null nie będzie dostępna opcja dla parametru, który nie zezwala na wartości null.

| Źródło danych | Opis |
|:--- |:--- |
| Stała wartość |Wpisz wartość dla parametru hello.  To jest dostępna tylko dla hello następujące typy danych: Int32, Int64, String, Boolean, DateTime, przełącznika. |
| Dane wyjściowe działania |Dane wyjściowe z poprzedzającą hello bieżące działanie w przepływie pracy hello działania.  Zostaną wyświetlone wszystkie prawidłowe działania.  Wybierz tylko hello działania toouse dane wyjściowe dla wartości parametru hello.  Jeśli działanie hello generuje obiekt o wiele właściwości, można wpisać w polu Nazwa hello właściwości hello po wybraniu hello działania. |
| Dane wejściowe elementu Runbook |Wybierz parametr wejściowy elementu runbook jako parametru działania toohello wejściowego. |
| Zasób zmiennej |Wybierz zmiennej automatyzacji jako dane wejściowe. |
| Zasób poświadczeń |Wybierz poświadczenie automatyzacji jako dane wejściowe. |
| Zasób certyfikatu |Wybierz certyfikat usługi Automatyzacja jako dane wejściowe. |
| Zasób połączenia |Wybierz połączenie automatyzacji jako dane wejściowe. |
| Wyrażenie programu PowerShell |Określ prosty [wyrażenie programu PowerShell](#powershell-expressions).  przed wynik działania i hello hello używany dla wartości parametru hello zostanie obliczone wyrażenie Hello.  Można użyć zmiennych toorefer toohello dane wyjściowe działania lub parametr wejściowy elementu runbook. |
| Nieskonfigurowane |Czyści żadnej wartości, który został wcześniej skonfigurowany. |

#### <a name="optional-additional-parameters"></a>Dodatkowe parametry opcjonalne
Wszystkie polecenia cmdlet będzie mieć hello opcja tooprovide dodatkowe parametry.  Są to typowe parametry programu PowerShell lub inne parametry niestandardowe.  Jest wyświetlane pole tekstowe, w którym można podać parametry, używając składni programu PowerShell.  Na przykład toouse hello **pełne** wspólnego parametru należy określić **"-Verbose: $True"**.

### <a name="retry-activity"></a>Ponów próbę wykonania działania
**Sposób ponawiania próby** umożliwia toobe działania uruchamiać wielokrotnie, dopóki nie zostanie spełniony określony warunek, podobnie jak pętli.  Tej funkcji można używać działań, które należy uruchamiać wielokrotnie, są podatne na błąd i może wymagają więcej niż jeden prób w przypadku powodzenia lub testowanie informacji wyjściowych hello hello działania dla prawidłowych danych.    

Po włączeniu retry działania można ustawić opóźnienie i warunek.  Opóźnienie Hello jest hello czas (w sekundach lub minutach) tego elementu runbook hello czeka przed jej uruchomieniem hello działania.  Jeśli opóźnienie nie zostanie określony, działanie hello zostanie uruchomione ponownie natychmiast po jej zakończeniu. 

![Opóźnienie ponownych prób działań](media/automation-graphical-authoring-intro/retry-delay.png)

warunek ponawiania Hello jest wyrażenie programu PowerShell, które jest oceniane po każdym działaniu hello czasu.  Jeśli wyrażenie hello rozpoznaje tooTrue, następnie hello działanie jest uruchomione ponownie.  Jeśli wyrażenie hello rozpoznaje tooFalse hello działania nie uruchomi ponownie, a hello runbook przenosi na toohello następnego działania. 

![Opóźnienie ponownych prób działań](media/automation-graphical-authoring-intro/retry-condition.png)

Hello ponawiania warunku można użyć zmiennej o nazwie $RetryData zapewniająca dostęp tooinformation o ponownych prób działań hello.  Ta zmienna ma właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| NumberOfAttempts |Liczba przypadków systemem hello działania. |
| Dane wyjściowe |Dane wyjściowe z hello ostatniego uruchomienia działania hello. |
| TotalDuration |Przekroczono czasu, jaki upłynął od uruchomienia działania hello hello po raz pierwszy. |
| StartedAt |Czas w działaniu hello format czasu UTC najpierw została uruchomiona. |

Poniżej przedstawiono przykłady działania ponawiania próby warunki.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Po skonfigurowaniu warunek ponów próbę wykonania działania hello obejmuje dwa tooremind wizualnych użytkownik.  Jeden są prezentowane w działaniu hello i hello innych jest przeglądając konfiguracji hello hello działania.

![Wskaźniki Visual ponów próbę wykonania działania](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>Sterowanie przepływem pracy skryptu
Kontroli kodu jest specjalnym działaniu, które akceptuje skrypt programu PowerShell lub przepływ pracy programu PowerShell w zależności od typu hello graficzny element runbook zostanie utworzony w kolejności tooprovide funkcje, które w przeciwnym razie jest dostępna.  Nie można zaakceptować parametrów, ale może użyć zmiennych dla działania danych wyjściowych i runbook parametrów wejściowych.  Żadnych danych wyjściowych hello działania są dodawane magistrali danych toohello Jeśli go nie ma żadnego wychodzących łącza, w którym Zapisz go w jest dodano dane wyjściowe toohello hello elementu runbook.

Na przykład hello następujący kod wykonuje obliczenia daty przy użyciu zmiennej wejściowe elementu runbook o nazwie $NumberOfDays.  Wysyła następnie obliczeniowej godzina jako używane przez kolejne działania w elemencie runbook hello toobe danych wyjściowych.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Łącza i przepływu pracy
A **łącze** w graficznym elementem runbook łączy dwa działania.  Jest on wyświetlany na kanwie hello jako strzałka z działania docelowego toohello hello źródła działania.  działania Hello działać w kierunku hello strzałki powitania od działania docelowego hello uruchamianie po zakończeniu działania źródłowego hello.  

### <a name="create-a-link"></a>Utwórz łącze
Utwórz łącze między dwa działania przez wybranie działania źródłowego hello i kliknięcie okręgu hello u dołu hello hello kształtu.  Przeciągnij działanie docelowe toohello strzałkę hello i wersji.

![Utwórz łącze](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Wybierz hello link tooconfigure jej właściwości w bloku konfiguracji hello.  Obejmuje to hello typu łącza, które jest opisane w poniższej tabeli hello.

| Typ łącza | Opis |
|:--- |:--- |
| Potok |działanie docelowe Hello jest uruchamiana raz dla każdego obiektu danych wyjściowych z działania źródłowego hello.  działanie docelowe Hello nie zostanie uruchomiony, jeśli działania źródłowego hello powoduje żadnych danych wyjściowych.  Dane wyjściowe z działania źródłowego hello jest dostępna jako obiekt. |
| Sekwencja |działanie docelowe Hello jest wykonywane tylko raz.  Odbiera tablicę obiektów z działania źródłowego hello.  Dane wyjściowe z działania źródłowego hello jest dostępna jako tablica obiektów. |

### <a name="starting-activity"></a>Działanie początkowe
Graficznego elementu runbook rozpoczyna się od żadnych działań, które nie mają łączy przychodzących.  Jest to często tylko jedno działanie, które będą działać jako hello uruchomienie działania elementu runbook hello.  Jeśli wielu działań nie ma łącze przychodzących, hello runbook zostanie uruchomiony uruchamiając równolegle.  Go zostanie następnie wykonaj toorun łącza hello innych działań każdego zakończeniu.

### <a name="conditions"></a>Warunki
Po określeniu warunku łącza, działanie docelowe hello tylko jest uruchamiane, gdy warunek hello rozpoznaje tootrue.  Zwykle użyjesz zmiennej $ActivityOutput w warunku tooretrieve hello dane wyjściowe z działania źródłowego hello.  

Link potoku należy określić warunek dla pojedynczego obiektu i warunku hello jest obliczane dla każdego obiektu danych wyjściowych przez działania źródłowego hello.  działanie docelowe Hello jest następnie uruchom dla każdego obiektu, który spełnia warunek hello.  Na przykład z działania źródłowego z Get AzureRmVm, hello składni mogłyby zostać użyte do tooretrieve łącza warunkowe potoku tylko maszyn wirtualnych w hello grupy zasobów o nazwie *grupa1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Łącza sekwencji hello jest tylko obliczoną warunku raz od zawierający wszystkie obiekty dane wyjściowe działania źródłowego hello, zwracany jest tablicą.  W związku z tym łącze sekwencji nie może służyć do filtrowania jak łącze potoku, ale po prostu określić, czy hello następne działanie jest uruchamiane. Na przykład mieć hello następującego zestawu działań w naszym runbook uruchamianie maszyny Wirtualnej.<br> ![Łączy warunkowych sekwencja](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Istnieją trzy inną sekwencję łącza, które sprawdzania wartości zostały podane parametry wejściowe elementu runbook tootwo reprezentujący nazwę maszyny Wirtualnej i nazwę grupy zasobów w toodetermine kolejności, czyli hello odpowiednią akcję tootake — uruchamianie jednej maszyny Wirtualnej, uruchomienie wszystkich maszyn wirtualnych w hello Grupa zasobów, lub wszystkich maszyn wirtualnych w ramach subskrypcji.  Hello sekwencji łącza między Connect tooAzure i Get jednej maszyny Wirtualnej w tym miejscu jest hello logiki warunek:

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Używając łączy warunkowych, hello danych dostępnych z hello źródła działania tooother działań w oddziale będą filtrowane przez hello warunku.  Jeśli działanie jest hello źródła toomultiple łącza, tekst hello dane, które tooactivities dostępne w każdej gałęzi jest uzależniony od hello warunku łącza hello łączenie toothat gałęzi.

Na przykład Witaj **Start AzureRmVm** działania w elemencie runbook hello poniżej uruchamiania wszystkich maszyn wirtualnych.  Składa się z dwóch łączy warunkowych.  pierwszy łączy warunkowych HELLO korzysta z wyrażenia hello *$ActivityOutput ["AzureRmVM Start"]. IsSuccessStatusCode - eq $true* toofilter, jeśli działanie Start AzureRmVm hello ukończone pomyślnie.  Witaj drugi używa wyrażenia hello *$ActivityOutput ["AzureRmVM Start"]. IsSuccessStatusCode - ne $true* toofilter Jeśli hello AzureRmVm rozpoczęcia działania maszyny wirtualnej hello toostart nie powiodła się.  

![Przykład łączy warunkowych](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Czynność hello pierwszy link i używa dane wyjściowe działania hello Get-AzureVM tylko otrzyma hello maszyn wirtualnych, które zostały uruchomione na powitania uruchomienia Get AzureVM.  Wszystkie działania hello drugi link pobierze tylko maszyn wirtualnych hello hello, które zostały przerwane na powitania uruchomienia Get AzureVM.  Wszystkie działania łącze trzeci hello otrzyma wszystkich maszyn wirtualnych niezależnie od ich uruchomiona.

### <a name="junctions"></a>Skrzyżowania
Połączenie jest specjalnym działaniu, które będzie czekać do momentu zostały ukończone wszystkie gałęzie przychodzących.  Dzięki temu można toorun wielu działań równolegle i upewnij się, zostały ukończone wszystkie zmiany przed kontynuowaniem.

Natomiast Rozgałęzienie może mieć dowolną liczbę linki przychodzące, nie więcej niż jeden z tych linków można potoku.  nie jest ograniczona liczba Hello łączy przychodzących sekwencji.  Może być toocreate hello połączenia z wielu łączy przychodzących potoku i Zapisz hello elementu runbook, ale zakończy się niepowodzeniem podczas uruchamiania.

w poniższym przykładzie Hello jest częścią elementu runbook, która rozpoczyna się zestaw maszyn wirtualnych podczas pobierania jednocześnie toobe poprawki stosowane toothose maszyny.  Połączenie jest używane tooensure czy oba procesy zostały zakończone przed kontynuowaniem hello elementu runbook.

![Rozgałęzienie](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Cykle
Cykl jest podczas działania docelowego łączy się ponownie tooits źródła działania lub tooanother działania ostatecznie połączone ponownie tooits źródła.  Cykle obecnie nie są dozwolone w tworzenia graficznego.  Jeśli element runbook ma cykl, zapisze właściwie, ale spowoduje wystąpienie błędu podczas uruchamiania.

![Cykl](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Udostępnianie danych między działaniami
Wszystkie dane, które są danymi wyjściowymi działania łącza wychodzących napisano toohello *magistrali danych* hello elementu runbook.  Wszystkie działania w elemencie runbook hello można użyć danych na wartości parametrów toopopulate magistrali danych hello lub obejmują w kodzie skryptu.  Działanie ma dostęp do danych wyjściowych hello wszelkie poprzednie działanie w przepływie pracy hello.     

Sposób zapisywania danych hello toohello magistrali danych zależy od typu hello łącza na powitania działania.  Aby uzyskać **potoku**, dane hello jest wyświetlany jako obiekty wielokrotności.  Aby uzyskać **sekwencji** połączyć, hello dane są dane wyjściowe w formie tablicy.  Jeśli istnieje tylko jedna wartość, będą dane wyjściowe jako tablica pojedynczy element.

Można uzyskać dostępu do danych na powitania magistrali danych przy użyciu jednej z dwóch metod.  Najpierw używa **dane wyjściowe działania** źródła danych toopopulate parametr innego działania.  Jeśli dane wyjściowe hello jest obiektem, można określić jedną właściwość.

![Dane wyjściowe działania](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

Można również pobierać dane wyjściowe działania w hello **wyrażenie programu PowerShell** źródła danych lub **skrypt przepływu pracy** działania ze zmienną ActivityOutput.  Jeśli dane wyjściowe hello jest obiektem, można określić jedną właściwość.  Zmienne ActivityOutput Użyj hello składni.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Punkty kontrolne
Można ustawić [punktów kontrolnych](automation-powershell-workflow.md#checkpoints) w elemencie runbook graficzny przepływ pracy programu PowerShell, wybierając *runbook punktu kontrolnego* na żadnych działań.  Powoduje to toobe punktu kontrolnego, ustawić po hello działanie jest uruchomione.

![Punkt kontrolny](media/automation-graphical-authoring-intro/set-checkpoint.png)

Punkty kontrolne są włączyć tylko w elementach runbook graficzny przepływ pracy programu PowerShell, nie jest dostępna w graficznych elementów runbook.  Jeśli element runbook hello używa poleceń cmdlet systemu Azure, należy wykonać czynność użyciu o AzureRMAccount Dodaj w przypadku hello runbook został wstrzymany i ponownie uruchamia z tego punktu kontrolnego na inny proces roboczy. 

## <a name="authenticating-tooazure-resources"></a>Uwierzytelnianie tooAzure zasobów
Elementy Runbook automatyzacji Azure, które zarządzania zasobami Azure wymaga tooAzure uwierzytelniania.  Witaj [konta Uruchom jako](automation-offering-get-started.md#creating-an-automation-account) hello domyślne metody tooaccess zasobów usługi Azure Resource Manager w ramach subskrypcji z elementu runbook usługi Automatyzacja jest (również określonego tooas nazwy głównej usługi).  Ta funkcjonalność tooa graficznym elementem runbook można dodać, dodając hello **AzureRunAsConnection** trwałego połączenia, który używa hello PowerShell [Get AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) polecenia cmdlet i [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) kanwy toohello polecenia cmdlet. Jest to zilustrowane w hello poniższy przykład.<br>![Uruchom jako działania uwierzytelniania](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Hello aktywność uzyskać Uruchom jako połączenia (tj. Get-AutomationConnection), jest skonfigurowany z wartości stałej źródła danych o nazwie AzureRunAsConnection.<br>![Konfiguracja połączenia Uruchom jako](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
Hello następne działanie Add-AzureRmAccount dodaje hello uwierzytelnić konta Uruchom jako do użycia w elemencie runbook hello.<br>
![Dodaj AzureRmAccount zestaw parametrów](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Dla parametrów hello **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, i **TENANTID** toospecify hello nazwa właściwości hello hello pola ścieżka będzie potrzebny ponieważ działanie Hello generuje obiekt o wiele właściwości.  W przeciwnym razie podczas wykonywania elementu runbook hello, nie będzie tooauthenticate próby.  Jest to, co jest potrzebne w minimalnej tooauthenticate, element runbook z hello konto Uruchom jako.

toomaintain zapewnienia zgodności dla subskrybentów, którzy utworzyli automatyzacji konta przy użyciu [konta usługi Azure AD](automation-create-aduser-account.md) toomanage wdrażania klasycznego Azure lub dla zasobów usługi Azure Resource Manager hello tooauthenticate — metoda to polecenie cmdlet Add-AzureAccount hello z [zasób poświadczeń](automation-credentials.md) reprezentujący użytkownika usługi Active Directory z toohello dostępu do konta platformy Azure.

Ten funkcji tooa graficzny element runbook można dodać, dodając kanwie toohello zasobów poświadczeń, następuje działanie Add-AzureAccount.  Dodaj-AzureAccount używa hello działania poświadczeń dla jej danych wejściowych.  Jest to zilustrowane w hello poniższy przykład.

![Działania uwierzytelniania](media/automation-graphical-authoring-intro/authentication-activities.png)

Masz tooauthenticate na początku hello hello runbook i po każdym punktu kontrolnego.  Oznacza to, dodawanie działanie dodania Add-AzureAccount po żadnego działania Checkpoint-Workflow. Nie ma potrzeby dodawania poświadczeń działania, ponieważ może użyć hello takie same 

![Dane wyjściowe działania](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Element Runbook wejściowe i wyjściowe
### <a name="runbook-input"></a>Dane wejściowe elementu Runbook
Element runbook może wymagać dane wejściowe, albo z danych użytkownika, po rozpoczęciu hello runbook za pomocą portalu Azure hello lub z innego elementu runbook, jeśli bieżący hello jest używany jako element podrzędny.
Na przykład jeśli element runbook, który tworzy maszynę wirtualną, konieczne może tooprovide informacje, takie jak nazwa hello hello maszyny wirtualnej i innych właściwości każdym uruchomieniu hello elementu runbook.  

Akceptuje dane wejściowe dla elementu runbook przez zdefiniowanie jednego lub więcej parametrów wejściowych.  Podaj wartości tych parametrów, każdy element runbook hello czas uruchomienia.  Po uruchomieniu elementu runbook z hello portalu Azure, zostanie wyświetlony monit tooprovide wartości hello hello runbook parametrów wejściowych.

Parametry wejściowe elementu runbook można uzyskać, klikając hello **dane wejściowe i wyjściowe** przycisk na pasku narzędzi elementu runbook hello.  

![Element Runbook wyjścia](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Spowoduje to otwarcie hello **wejściowa i wyjściowa** kontrolki, w którym można edytować istniejące parametr wejściowy lub Utwórz nowy, klikając **dodać dane wejściowe**. 

![Dodawanie danych wejściowych](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Każdy parametr wejściowy jest zdefiniowana przez właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Nazwa |Unikatowa nazwa Hello hello parametru.  To może zawierać tylko znaków alfanumerycznych i nie może zawierać spacji. |
| Opis |Opcjonalny opis hello parametru wejściowego. |
| Typ |Oczekiwano wartości parametru hello typu danych.  Hello portalu Azure zapewni odpowiednią kontrolkę dla hello — typ danych dla każdego parametru monitując o dane wejściowe. |
| Obowiązkowy |Określa, czy należy podać wartość parametru hello.  Nie można uruchomić elementu runbook Hello, jeśli nie zostanie określona wartość dla każdego obowiązkowy parametr, który nie ma zdefiniowanej wartości domyślnej. |
| Wartość domyślna |Określa, jakie korzyści jest używane dla parametru hello, jeśli nie podano.  To może być wartością Null lub określoną wartość. |

### <a name="runbook-output"></a>Wynik uruchomienia elementu Runbook
Dane utworzone przez działalności, która nie ma wychodzących łącza zostanie dodany toohello [danych wyjściowych elementu hello runbook](http://msdn.microsoft.com/library/azure/dn879148.aspx).  dane wyjściowe Hello są zapisane na powitania zadanie elementu runbook i jest dostępne tooa nadrzędny element runbook, gdy element runbook hello jest używany jako element podrzędny.  

## <a name="powershell-expressions"></a>Wyrażenia programu PowerShell
Jedną z zalet hello tworzenia graficznego oferuje Ci hello możliwości toobuild elementu runbook przy minimalnej znajomości programu PowerShell.  Obecnie, trzeba tooknow bitowej programu PowerShell, chociaż w celu wypełnienia pewnych [wartości parametrów](#activities) i ustawienia [połączonych warunków](#links-and-workflow).  W tej sekcji przedstawiono krótkie wprowadzenie wyrażenia tooPowerShell dla tych użytkowników, którzy mogą nie być zapoznać się z nim.  Szczegółowe informacje dotyczące programu PowerShell są dostępne pod adresem [skryptów programu Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). 

### <a name="powershell-expression-data-source"></a>Źródło danych wyrażenie programu PowerShell
Wyrażenie programu PowerShell można użyć jako źródła toopopulate hello wartości danych [parametru działania](#activities) z wynikami hello niektórych kodu programu PowerShell.  Może to być pojedynczy wiersz kodu, który wykonuje niektórych funkcji prostego lub wiele wierszy, które wykonują niektóre złożonej logiki.  Wszystkie dane wyjściowe polecenia, który nie jest przypisany tooa zmienna jest wartość parametru toohello danych wyjściowych. 

Na przykład hello następujące polecenie spowoduje output hello bieżącą datę. 

    Get-Date

Witaj następujących poleceń kompilacji ciąg z hello bieżącą datę i przypisz je tooa zmiennej.  zawartość Hello zmiennej hello są następnie wysyłane dane wyjściowe toohello 

    $string = "hello current date is " + (Get-Date)
    $string

Witaj następujące polecenia oceń hello bieżącą datę i zwraca ciąg wskazujący czy hello bieżącego dnia jest weekendowe lub dzień tygodnia. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Dane wyjściowe działania
dane wyjściowe hello toouse z wcześniejszego działania w elemencie runbook hello, użyj zmiennej hello $ActivityOutput hello składni.

    $ActivityOutput['Activity Label'].PropertyName

Na przykład może mieć działania o właściwości, która wymaga hello nazwę maszyny wirtualnej w takim przypadku można użyć powitania po wyrażeniu.

    $ActivityOutput['Get-AzureVm'].Name

Jeśli zwróci właściwości hello wymagany obiekt maszyny wirtualnej hello zamiast tylko właściwości, a następnie możesz hello hello cały obiekt przy użyciu składni.

    $ActivityOutput['Get-AzureVm']

Umożliwia także hello dane wyjściowe działania w wyrażeniu bardziej złożonych, takie jak następujące hello, który łączy toohello nazwę maszyny wirtualnej.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Warunki
Użyj [operatory porównania](https://technet.microsoft.com/library/hh847759.aspx) toocompare wartości lub określić, jeśli wartość jest zgodna z określonym wzorcem.  Porównanie zwraca wartość $true lub $false.

Na przykład hello następującego warunku Określa, czy hello maszyny wirtualnej z działania o nazwie *Get-AzureVM* jest obecnie *zatrzymana*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

Hello następujące warunku sprawdza, czy hello tej samej maszyny wirtualnej jest w stanie żadnych innych niż *zatrzymana*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

Można połączyć wiele warunków za pomocą [operatora logicznego](https://technet.microsoft.com/library/hh847789.aspx) takich jak **- i** lub **- lub**.  Na przykład następujące hello warunku sprawdza, czy hello tej samej maszyny wirtualnej w poprzednim przykładzie hello jest w stanie *zatrzymana* lub *zatrzymywanie*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Obiektach HashTable
[Obiektach HashTable](http://technet.microsoft.com/library/hh847780.aspx) są pary nazwa/wartość, które są przydatne w przypadku zwracanie zestawu wartości.  Właściwości dla niektórych działań może oczekiwać hashtable zamiast prostą wartością.  Może również zostać wyświetlony hashtable określonego tooas słownika. 

Można utworzyć obiektu hashtable z hello składni.  Tablica skrótów może zawierać dowolną liczbę wpisów, ale każda jest definiowana za pomocą nazwy i wartości.

    @{ <name> = <value>; [<name> = <value> ] ...}

Na przykład hello poniższe wyrażenie tworzy toobe hashtable, używany w źródle danych hello parametru działania, szacowany hashtable z wartościami wyszukiwaniem w Internecie.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

Witaj poniższym przykładzie użyto wyjściowymi działania o nazwie *uzyskać połączenia w usłudze Twitter* toopopulate obiektu hashtable.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Następne kroki
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md) 
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)
* Zobacz tooknow więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)
* toounderstand przy użyciu tooauthenticate hello konta Uruchom jako automatyzacji, zobacz [skonfigurować Azure konta Uruchom jako](automation-sec-configure-azure-runas-account.md)

