---
title: "aaaRunbook dane wyjściowe i komunikaty w automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toocreate i pobierania danych wyjściowych i błędów komunikaty z elementów runbook automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Element Runbook danych wyjściowych i komunikatów w usłudze Automatyzacja Azure
Większość elementów runbook automatyzacji Azure będzie miał jakiegoś typu danych wyjściowych, takich jak użytkownik toohello komunikat błędu lub obiekt złożony przeznaczony toobe używane przez inny przepływ pracy. Środowisko Windows PowerShell udostępnia [wiele strumieni](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend dane wyjściowe skryptu lub przepływ pracy. Automatyzacja Azure działa z każdym z tych strumieni inaczej, a należy stosować najlepsze rozwiązania dotyczące toouse każdego podczas tworzenia elementu runbook.

Witaj Poniższa tabela zawiera krótki opis każdego strumienia hello i jego zachowanie w portalu zarządzania Azure hello zarówno podczas uruchamiania opublikowanego elementu runbook, jak i podczas [testowania elementu runbook](automation-testing-runbook.md). W kolejnych sekcjach znajdują się dodatkowe informacje na temat każdego strumienia.

| Strumień | Opis | Opublikowano | Testowanie |
|:--- |:--- |:--- |:--- |
| Dane wyjściowe |Obiekty, które mają toobe używane przez inne elementy runbook. |Zapisane toohello historii zadań. |Wyświetlane w okienku danych wyjściowych testu hello. |
| Ostrzeżenie |Komunikat ostrzegawczy przeznaczony dla użytkownika hello. |Zapisane toohello historii zadań. |Wyświetlane w okienku danych wyjściowych testu hello. |
| Błąd |Komunikat o błędzie przeznaczony dla użytkowników hello. W przeciwieństwie do wyjątku hello runbook odtwarzanie jest kontynuowane komunikat o błędzie domyślnie. |Zapisane toohello historii zadań. |Wyświetlane w okienku danych wyjściowych testu hello. |
| Pełne |Komunikaty z informacjami ogólne lub debugowania. |Zapisane historii toojob tylko jeśli dla elementu runbook hello jest włączone rejestrowanie pełne. |Wyświetlane w okienku danych wyjściowych testu hello tylko wtedy, gdy $VerbosePreference ustawiono tooContinue w elemencie runbook hello. |
| Postęp |Rejestruje przed i po każdym działaniu w elemencie runbook hello są generowane automatycznie. Element runbook Hello nie powinny podejmować toocreate swoich własnych rekordów postępu, ponieważ są one przeznaczone dla użytkownika interaktywnego. |Zapisane historii toojob tylko, jeśli dla elementu runbook hello jest włączone rejestrowanie postępu. |Nie są wyświetlane w okienku danych wyjściowych testu hello. |
| Debugowanie |Komunikaty przeznaczone dla użytkownika interaktywnego. Nie można używać w elementach runbook. |Nie można zapisać historii toojob. |Nie można zapisać tooTest okienku danych wyjściowych. |

## <a name="output-stream"></a>Strumień wyjściowy
strumień wyjściowy Hello jest przeznaczony dla danych wyjściowych obiektów utworzonych przy użyciu skryptu lub przepływu pracy po uruchomieniu poprawnie. W automatyzacji Azure ten strumień jest używany głównie dla obiektów, które mają toobe używane przez [nadrzędne elementy runbook, które wywołań bieżącego elementu runbook hello](automation-child-runbooks.md). Gdy możesz [wywołać wbudowanego elementu runbook](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) z nadrzędnego elementu runbook, zwraca dane z nadrzędnego toohello strumienia wyjściowego hello. Hello wyjściowego strumienia toocommunicate informacje ogólne wstecz toohello użytkownika należy używać tylko, jeśli wiadomo, że hello runbook nigdy nie zostanie wywołana przez inny element runbook. Najlepszym rozwiązaniem, jednak należy zwykle użyć hello [strumień pełny](#Verbose) toocommunicate ogólne informacje toohello użytkownika.

Można zapisywać danych toohello wyjściowego strumienia przy użyciu [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) lub umieszczając obiekt hello w osobnym wierszu w elemencie runbook hello.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Dane wyjściowe funkcji
Podczas pisania toohello strumienia wyjściowego w funkcji, który znajduje się w elemencie runbook, dane wyjściowe hello są przekazywane wstecz toohello elementu runbook. Jeśli hello runbook przypisuje tej zmiennej tooa danych wyjściowych, następnie są one zapisywane toohello strumienia wyjściowego. Zapisywanie tooany innych strumieni w funkcji hello zapisze toohello odpowiedniego strumienia hello elementu runbook.

Należy wziąć pod uwagę hello następującego przykładowego elementu runbook.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


Witaj strumień wyjściowy dla zadania elementu runbook hello mogą być następujące:

    Output inside of function
    Output outside of function

Witaj strumień pełny dla zadania elementu runbook hello mogą być następujące:

    Verbose outside of function
    Verbose inside of function

Po opublikowaniu elementu runbook hello i przed rozpoczęciem pracy należy również włączyć pełne rejestrowanie, w ustawieniach runbook hello w kolejności tooget hello pełne strumieni wyjściowych.

### <a name="declaring-output-data-type"></a>Deklaracyjny typ danych wyjściowych
Przepływ pracy można określić hello typ danych wyjściowych za pomocą hello [atrybutu OutputType](http://technet.microsoft.com/library/hh847785.aspx). Ten atrybut nie ma znaczenia w czasie wykonywania, ale zapewnia Autor elementów runbook toohello wskazanie w czasie projektowania danych wyjściowych hello oczekiwano elementu hello runbook. W miarę hello narzędzi dla elementów runbook tooevolve, znaczenie hello deklarowanie typów danych wyjściowych w czasie projektowania będzie zyskiwać na znaczeniu. W związku z tym jest najlepszym rozwiązaniem tooinclude tej deklaracji w żadnych tworzonym elemencie runbook.

W tym miejscu znajduje się lista przykładowe typy danych wyjściowych:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Witaj następujący przykładowy element runbook generuje obiekt ciągu i zawiera deklarację typu jego danych wyjściowych. Jeśli element runbook generuje tablicę pewnego typu, następnie należy także określić typ hello jako tablica min. tooan hello typu.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare typ danych wyjściowych w elementach runbook Grapical lub graficzny przepływ pracy programu PowerShell, można wybrać hello **wejściowa i wyjściowa** opcji menu i wprowadź nazwę hello hello output typu.  Zalecane jest użycie toomake Nazwa klasy .NET hello pełne go łatwo zidentyfikować podczas odwoływania się do nadrzędnego elementu runbook.  Dzięki temu wszystkie właściwości hello magistrali danych toohello tej klasy w elemencie runbook hello a zapewnia dużą elastyczność w przypadku, gdy ich użycie jako logikę warunkową, rejestrowania i odwołuje się do wartości dla innych działań w elemencie runbook hello.<br> ![Opcja Runbook dane wejściowe i wyjściowe](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

W hello poniższy przykład firma Microsoft ma dwa toodemonstrate graficznych elementów runbook tej funkcji.  Jeśli stosujemy modelu moduły runbook hello będziemy mieć jeden element runbook, który służy jako hello *uwierzytelniania szablonem* Zarządzanie uwierzytelniania za pomocą platformy Azure przy użyciu hello konto Uruchom jako.  Nasze drugiego elementu runbook, które zwykle przeprowadziłby hello core logiki tooautomate danego scenariusza, w tym przypadku będzie tooexecute hello *uwierzytelniania szablonem* i wyświetlić hello wyniki tooyour **testu** okienku danych wyjściowych.  W normalnych okolicznościach trzeba ten element runbook czymś przed wyjściowego hello korzystanie z usług zasobów z hello podrzędnego elementu runbook.    

Poniżej przedstawiono podstawowe logiki hello hello **AuthenticateTo Azure** elementu runbook.<br> ![Przykład szablonem uwierzytelniania](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Zawiera typ danych wyjściowych hello *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, który zwróci właściwości profilu hello uwierzytelniania.<br> ![Przykład typ danych wyjściowych elementu Runbook](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Gdy ten element runbook jest bardzo proste do przodu, istnieje jeden toocall elementu konfiguracji się tutaj.  Ostatnie działanie Hello jest wykonywany hello **Write-Output** polecenia cmdlet, jak i zapisów hello profilu danych tooa $_ zmiennej przy użyciu wyrażenie programu PowerShell dla hello **Inputobject** parametr, który jest wymagany dla tej polecenia cmdlet.  

Witaj drugiego elementu runbook w tym przykładzie, o nazwie *ChildOutputType testu*, po prostu mamy dwóch działań.<br> ![Przykład podrzędnych Output typ elementu Runbook](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

Pierwsze działanie Hello wywołuje hello **AuthenticateTo Azure** działanie elementu runbook i hello drugi działa hello **Write-Verbose** polecenia cmdlet z hello **źródła danych** z  **Dane wyjściowe działania** , a wartość hello **ścieżkę pola** jest **Context.Subscription.SubscriptionName**, który jest określenie dane wyjściowe kontekstu hello hello  **AuthenticateTo Azure** elementu runbook.<br> ![Write-Verbose polecenia cmdlet parametr źródła danych](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

dane wyjściowe Hello jest nazwą hello hello subskrypcji.<br> ![Wyniki Runbook ChildOutputType testu](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Jeden notatkę dotyczącą zachowania hello hello formantu o typie danych wyjściowych.  Podczas wpisywania tekstu, wartość w polu Typ danych wyjściowych hello na powitania danych wejściowych i wyjściowych bloku właściwości, mieć tooclick poza kontrolą powitania po wpisaniu, aby Twoje toobe wpis rozpoznany przez formant hello.  

## <a name="message-streams"></a>Strumienie komunikatów
W przeciwieństwie do strumienia wyjściowego hello strumieni komunikatów są zamierzone toocommunicate informacji toohello użytkownika. Istnieje wiele strumieni komunikatów dla różnych typów informacji, a każdy różni się w automatyzacji Azure.

### <a name="warning-and-error-streams"></a>Strumienie ostrzeżeń i błędów
strumienie ostrzeżeń i błędów Hello są zamierzone toolog problemów, które występują w elemencie runbook. Są one zapisywane w historii zadań toohello, gdy element runbook jest wykonywane i znajdują się w hello okienku danych wyjściowych testu w portalu zarządzania Azure hello podczas testowania elementu runbook. Domyślnie hello runbook kontynuuje wykonywanie po ostrzeżeniu lub błędzie. Możesz określić danego elementu runbook hello ma zostać zawieszony w przypadku ostrzeżenia lub błędu przez ustawienie [zmiennej preferencji](#PreferenceVariables) w elemencie runbook hello przed utworzeniem wiadomość hello. Na przykład toocause toosuspend elementu runbook, w przypadku wystąpienia błędu jak wyjątek, ustaw **$ErrorActionPreference** tooStop.

Utwórz wiadomość ostrzeżenia lub błędu przy użyciu hello [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) lub [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) polecenia cmdlet. Działania mogą także zapisywać toothese strumieni.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Strumień pełny
strumień komunikatów pełnych Hello jest ogólne informacje o działaniu elementu runbook hello. Ponieważ hello [strumienia debugowania](#Debug) jest niedostępny w elemencie runbook, komunikaty pełne należy używać dla informacji debugowania. Domyślnie komunikaty pełne z opublikowanych elementów runbook nie będą przechowywane w historii zadań hello. toostore komunikaty pełne, skonfiguruj opublikowane elementy runbook tooLog rekordów pełnych na karcie Konfigurowanie hello elementu runbook hello w hello portalu zarządzania Azure. W większości przypadków Zachowaj ustawienie domyślne hello bez rejestrowania rekordów pełnych dla elementu runbook ze względu na wydajność. Włącz ten tootroubleshoot tylko opcja lub debugowania elementu runbook.

Gdy [testowania elementu runbook](automation-testing-runbook.md), komunikaty pełne nie są wyświetlane, nawet jeśli hello runbook jest skonfigurowany toolog rekordów pełnych. toodisplay komunikaty pełne podczas [testowania elementu runbook](automation-testing-runbook.md), należy ustawić tooContinue zmiennej hello $VerbosePreference. Z tego zestawu zmiennej komunikaty pełne pojawi się w hello okienku danych wyjściowych testu z hello portalu Azure.

Utwórz komunikat trybu informacji pełnej przy użyciu hello [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) polecenia cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Strumień debugowania
strumień debugowania Hello jest przeznaczony dla użytkownika interaktywnego i nie należy używać w elementach runbook.

## <a name="progress-records"></a>Rekordy postępu
Jeśli skonfigurujesz postępu toolog runbook rejestruje (na karcie Konfiguracja hello hello runbook w portalu Azure hello), a następnie rekord zostanie zapisany toohello historii zadań przed i po każdym uruchomieniem działania. W większości przypadków Zachowaj ustawienie domyślne hello nie rejestrowania rekordów postępu dla elementu runbook w kolejności toomaximize wydajności. Włącz ten tootroubleshoot tylko opcja lub debugowania elementu runbook. Podczas testowania elementu runbook, komunikaty o postępie nie są wyświetlane, nawet jeśli hello runbook jest skonfigurowany toolog rekordów postępu.

Witaj [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) polecenia cmdlet jest nieprawidłowy w elemencie runbook, ponieważ ta wartość jest przeznaczona do użycia z użytkownika interaktywnego.

## <a name="preference-variables"></a>Zmienne preferencji
Program Windows PowerShell korzysta [zmienne preferencji](http://technet.microsoft.com/library/hh847796.aspx) toodetermine jak toodifferent toodata wysyłane toorespond danych wyjściowych strumieni. Te zmienne można ustawić w toocontrol elementu runbook, sposób odpowiadania przez niego toodata przesyłane do różnych strumieni.

Witaj Poniższa tabela zawiera listę zmiennych preferencji hello, których można użyć w elementach runbook oraz ich prawidłowe i domyślne wartości. Należy pamiętać, że ta tabela zawiera tylko wartości hello, które są prawidłowe w elemencie runbook. Dodatkowe wartości są prawidłowe dla zmiennych preferencji hello, gdy jest używany w programie Windows PowerShell poza usługi Automatyzacja Azure.

| Zmienna | Wartość domyślna | Prawidłowe wartości |
|:--- |:--- |:--- |
| WarningPreference |Kontynuuj |Stop<br>Kontynuuj<br>SilentlyContinue |
| ErrorActionPreference |Kontynuuj |Stop<br>Kontynuuj<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Kontynuuj<br>SilentlyContinue |

Witaj w poniższej tabeli wymieniono hello zachowanie hello wartości zmiennych preferencji, które są prawidłowe w elementach runbook.

| Wartość | Zachowanie |
|:--- |:--- |
| Kontynuuj |Rejestruje wiadomość hello i kontynuuje wykonywanie elementu runbook hello. |
| SilentlyContinue |Kontynuuje wykonywanie elementu runbook hello bez rejestrowania wiadomości powitania. To ustawienie działa hello wiadomość hello ignorowania. |
| Stop |Rejestruje wiadomość hello i wstrzymuje hello elementu runbook. |

## <a name="retrieving-runbook-output-and-messages"></a>Pobieranie elementu runbook dane wyjściowe i komunikaty
### <a name="azure-portal"></a>Azure Portal
Witaj szczegóły zadania elementu runbook można wyświetlić w hello portalu Azure hello na karcie zadania elementu runbook. Witaj Podsumowanie zadania hello wyświetli hello parametry wejściowe i hello [strumienia wyjściowego](#Output) dodanie toogeneral informacje o hello zadania i wszelkie wyjątki, jeśli takie były. Witaj historii zawiera komunikaty ze hello [strumienia wyjściowego](#Output) i [strumienie ostrzeżeń i błędów](#WarningError) w toohello dodanie [strumień pełny](#Verbose) i [postępu Rejestruje](#Progress) Jeśli hello runbook jest skonfigurowany toolog pełne i rekordy postępu.

### <a name="windows-powershell"></a>Windows PowerShell
W programie Windows PowerShell można pobrać dane wyjściowe i komunikaty z elementu runbook za pomocą hello [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) polecenia cmdlet. To polecenie cmdlet wymaga hello identyfikator hello zadania i ma parametr o nazwie strumienia, w którym określić które tooreturn strumienia. Możesz określić wszelkie tooreturn wszystkich strumieni zadania hello.

Poniższy przykład Hello uruchamia przykładowego elementu runbook, a następnie czeka na jego toocomplete. Po zakończeniu jego strumień wyjściowy jest zbierany z zadania hello.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Tworzenie graficznych
Dla graficznych elementów runbook dodatkowe rejestrowanie jest dostępne w formie hello śledzenia poziom aktywności.  Istnieją dwa poziomy śledzenia: Basic i szczegółowe.  W śledzenia, mogą zobaczyć hello start, a czas zakończenia każde działanie w hello runbook oraz informacje dotyczące ponownych prób działań tooany, takie jak liczba prób i godzina rozpoczęcia działania hello.  W szczegółowego śledzenia, należy uzyskać śledzenia plus danych wejściowych i danych wyjściowych dla każdego działania.  Należy pamiętać, że obecnie hello śledzenia rekordów są zapisywane przy użyciu strumień pełny hello, więc musisz włączyć pełne rejestrowanie, gdy włączone śledzenie.  Dla graficznych elementów runbook z włączonym śledzeniem nie istnieje potrzeba toolog rekordów postępu, ponieważ służy śledzenia hello hello tych samych celów i więcej informacji.

![Zadanie tworzenia graficznego strumieni widoku](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Z hello powyżej zrzut ekranu widać, gdy jest włączone pełne rejestrowanie i śledzenia dla graficznych elementów runbook, znacznie więcej informacji o dostępnych w środowisku produkcyjnym hello, wyświetlić strumieni zadania.  Te dodatkowe informacje mogą być niezbędne podczas rozwiązywania problemów w środowisku produkcyjnym z elementu runbook, a w związku z tym należy włączać jedynie go do tego celu, a nie jako rozwiązaniem ogólne.    
rejestruje śledzenia Hello może być szczególnie wiele.  Z graficznym elementem runbook śledzenia, należy uzyskać dwa rekordy toofour na działanie w zależności od tego, czy skonfigurowano śledzenie podstawowy lub szczegółowy.  Jeśli nie potrzebujesz tego postępu hello tootrack informacji elementu runbook do rozwiązywania problemów, można tookeep, śledzenie jest wyłączone.

**tooenable poziom aktywności śledzenia, wykonaj następujące kroki hello.**

1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Polecenie hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.
3. W bloku elementów Runbook hello kliknij tooselect graficznego elementu runbook z listy elementów runbook.
4. W bloku ustawienia hello hello wybrany element runbook, kliknij **rejestrowania i śledzenia**.
5. Na powitania kliknij przycisk rejestrowania i śledzenia bloku, w obszarze rejestrowania rekordów pełnych **na** tooenable pełnego rejestrowania i śledzenia udner poziom aktywności zmienić poziom śledzenia hello zbyt**podstawowe** lub **szczegółowy**  na podstawie poziomu hello śledzenia wymagane.<br>
   
   ![Graficzny tworzenia rejestrowania i śledzenia bloku](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Analiza dzienników programu Microsoft Operations Management Suite (OMS)
Automatyzacja może wysyłać runbook zadania stanu i zadania strumienie tooyour programu Microsoft Operations Management Suite (OMS) obszar roboczy analizy dzienników.  Za pomocą analizy dzienników można,

* Uzyskiwanie wglądu w zadaniach automatyzacji 
* Wyzwalacz poczty e-mail lub alertu oparte na stan zadania elementu runbook (np. nie powiodło się lub wstrzymane) 
* Zapis zaawansowanych zapytań na strumienie zadania 
* Korelowanie zadań na konta automatyzacji 
* Wizualizuj historię zadania wraz z upływem czasu    

Aby uzyskać więcej informacji dotyczących sposobu integracji tooconfigure z toocollect analizy dzienników skorelowania i korzystania z danych zadania, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Następne kroki
* więcej informacji o wykonanie elementu runbook, w jaki sposób toomonitor zadań i inne szczegółowe informacje techniczne, zobacz toolearn [śledzić zadania elementu runbook](automation-runbook-execution.md)
* toounderstand toodesign i użyj podrzędnych elementów runbook, zobacz temat [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md)

