---
title: aaaMigrating z tooAzure Orchestrator automatyzacji | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak pakiety toomigrate elementów runbook i integracja z programu System Center Orchestrator tooAzure automatyzacji."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Migrowanie z programu Orchestrator tooAzure automatyzacji (Beta)
Elementy Runbook w [programu System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) są oparte na działań z pakietów integracyjnych, które zostały napisane specjalnie dla programu Orchestrator, gdy elementy runbook automatyzacji Azure są oparte na programie Windows PowerShell.  [Graficznych elementów runbook](automation-runbook-types.md#graphical-runbooks) automatyzacji Azure mają podobne elementy runbook tooOrchestrator wygląd z ich działania polecenia cmdlet programu PowerShell, podrzędnych elementów runbook i zasoby.

Witaj [System Center Orchestrator Migration Toolkit](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) zawiera narzędzia tooassist w konwertowania elementów runbook programu Orchestrator tooAzure automatyzacji.  Ponadto runbook hello tooconverting samodzielnie, należy przekonwertować hello Pakiety integracyjne z działaniami hello, że elementy runbook hello Użyj toointegration modułów za pomocą poleceń cmdlet programu Windows PowerShell.  

Poniżej znajduje się hello podstawowy proces podczas konwertowania Orchestrator tooAzure elementy runbook automatyzacji.  Każda z tych czynności jest szczegółowo opisane w poniższych sekcjach hello.

1. Pobierz hello [System Center Orchestrator Migration Toolkit](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) zawierający narzędzia hello i moduły omówione w tym artykule.
2. Importuj [modułu działań standardowych](#standard-activities-module) w automatyzacji Azure.  W tym przekonwertowanego wersje standardowych działań programu Orchestrator, które mogą być używane przez elementy runbook przekonwertowany.
3. Importuj [moduły integracji programu System Center Orchestrator](#system-center-orchestrator-integration-modules) w automatyzacji Azure dla tych pakietów integracyjnych, używany przez elementy runbook dostępnym dla programu System Center.
4. Konwertuj niestandardowe i inne pakiety integracyjne za pomocą hello [Integration Pack konwertera](#integration-pack-converter) i zaimportować do usługi Automatyzacja Azure.
5. Konwertuj elementy runbook programu Orchestrator przy użyciu hello [konwertera Runbook](#runbook-converter) i zainstalować automatyzacji Azure.
6. Ręcznie utworzyć wymagane zasoby programu Orchestrator w usłudze Automatyzacja Azure, ponieważ hello konwertera elementu Runbook nie konwertuje tych zasobów.
7. Skonfiguruj [hybrydowy proces roboczy elementu Runbook](#hybrid-runbook-worker) w elementach runbook toorun przekonwertowane centrum danych lokalnych będą uzyskiwać dostęp do zasobów lokalnych.

## <a name="service-management-automation"></a>Service Management Automation
[Automatyzacja zarządzania usługami](http://technet.microsoft.com/library/dn469260.aspx) (SMA) są przechowywane i uruchamia elementy runbook w centrum danych lokalnych jak Orchestrator i używa hello tego samego moduły integracji jako automatyzacji Azure. Witaj [konwertera Runbook](#runbook-converter) konwertuje elementy runbook programu Orchestrator elementów runbook toographical mimo że nie są obsługiwane w programie SMA.  Można nadal zainstalować hello [standardowy moduł działania](#standard-activities-module) i [moduły integracji programu System Center Orchestrator](#system-center-orchestrator-integration-modules) do programu SMA, ale należy ręcznie [przepisywania elementy runbook](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>Hybrydowy proces roboczy elementu Runbook
Elementy Runbook w programie Orchestrator są przechowywane na serwerze bazy danych i uruchamiać na serwerach runbook, zarówno w centrum danych lokalnych.  Elementy Runbook automatyzacji Azure są przechowywane w hello chmury Azure i można uruchomić w centrum danych lokalnych za pomocą [hybrydowy proces roboczy elementu Runbook](automation-hybrid-runbook-worker.md).  Jest to, jak zwykle będzie uruchamiane elementy runbook skonwertowane z programu Orchestrator, ponieważ są one zaprojektowane toorun na serwerach lokalnych.

## <a name="integration-pack-converter"></a>Konwerter pakietu integracyjnego
Witaj Integration Pack konwertera konwertuje pakietów integracyjnych, które zostały utworzone przy użyciu hello [Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) modułów toointegration oparte na programie Windows PowerShell, który można zaimportować do usługi Automatyzacja Azure lub Automatyzacja zarządzania usługami.  

Po uruchomieniu hello Integration Pack konwertera są prezentowane za pomocą kreatora, co umożliwi tooselect integracji pliku pakietu (oip).  Kreator Hello, a następnie wyświetla hello działania zawarte w tym pakiecie integracyjnym i umożliwia tooselect, które zostaną poddane migracji.  Po zakończeniu pracy Kreatora hello tworzy zawierającego odpowiednie polecenie cmdlet dla każdego działania hello w pakiecie integracyjnym oryginalnego hello modułu integracji.

### <a name="parameters"></a>Parametry
Właściwości działania w pakiecie integracyjnym hello są przekonwertowanego tooparameters hello odpowiedniego polecenia cmdlet w module integracji hello.  Polecenia cmdlet programu Windows PowerShell ma zestaw [wspólne parametry](http://technet.microsoft.com/library/hh847884.aspx) które mogą być używane wszystkie polecenia cmdlet.  Na przykład hello - Verbose parametr powoduje, że polecenia cmdlet toooutput szczegółowe informacje na temat jej działania.  Polecenie cmdlet nie może być parametrem hello takie same nazwy co parametr wspólnej.  Jeśli działanie ma właściwości o hello takie same nazwy co parametr wspólnej, hello Kreator wyświetli monit o możesz tooprovide inną nazwę dla parametru hello.

### <a name="monitor-activities"></a>Działań monitorowania
Elementy runbook w programie Orchestrator rozpoczyna się od monitorowania [monitorowania aktywności](http://technet.microsoft.com/library/hh403827.aspx) i uruchamiaj stale toobe oczekiwania wywołana przez konkretnego zdarzenia.  Usługi Automatyzacja Azure nie obsługuje elementów runbook monitora, więc żadnych działań monitorowania w pakiecie integracyjnym hello nie zostanie przekonwertowany.  Zamiast tego polecenia cmdlet symbol zastępczy jest tworzony w hello modułu integracji dla działania monitorowania hello.  To polecenie cmdlet nie ma żadnych funkcji, ale pozwala toobe zainstalowane przekonwertowany element runbook, który korzysta z niego.  Ten element runbook nie będą mogli toorun automatyzacji Azure, ale można ją zainstalować, aby można go zmodyfikować.

### <a name="integration-packs-that-cannot-be-converted"></a>Pakiety integracyjne, których nie można przekonwertować
Nie można przekonwertować pakietów integracyjnych, które nie zostały utworzone z OIT z hello Integration Pack konwertera. Brak niektórych pakietów integracyjnych firmy Microsoft, nie można przekonwertować z tego narzędzia.  Zostały przekonwertowane wersje te pakiety integracyjne [dostępne do pobrania](#system-center-orchestrator-integration-modules) , dzięki czemu mogą być instalowane w automatyzacji Azure lub Service Management Automation.

## <a name="standard-activities-module"></a>Działania standardowe modułu
Orchestrator zawiera zestaw [działań standardowych](http://technet.microsoft.com/library/hh403832.aspx) które nie są uwzględnione w pakiecie integracyjnym, ale są używane przez wiele elementów runbook.  Witaj standardowych działań jest integracja moduł, który zawiera równoważne polecenia cmdlet dla każdego z tych działań.  Przed zaimportowaniem przekonwertowanego elementów runbook, który użyć standardowego działania, należy zainstalować ten moduł integracji automatyzacji Azure.

Ponadto toosupporting przekonwertować elementów runbook, polecenia cmdlet hello w module działań standardowych hello może być używany przez kogoś zapoznać się z Orchestrator toobuild nowych elementów runbook automatyzacji Azure.  Gdy funkcje hello wszystkich działań standardowych hello można wykonywać za pomocą polecenia cmdlet, mogą one działają inaczej.  Witaj polecenia cmdlet w hello przekonwertować standardowych działań, które moduł będzie działać hello takie same jak ich odpowiednich działań i użycia tych samych parametrach hello.  Może to ułatwić hello istniejących Orchestrator runbook autora w ich tooAzure przejścia elementu runbook usługi Automatyzacja.

## <a name="system-center-orchestrator-integration-modules"></a>Moduły integracji programu System Center Orchestrator
Firma Microsoft udostępnia [Pakiety integracyjne](http://technet.microsoft.com/library/hh295851.aspx) do tworzenia składników programu System Center tooautomate elementów runbook i innych produktów.  Niektóre z tych pakietów integracyjnych obecnie są oparte na OIT, ale obecnie nie może być przekonwertowany toointegration modułów z powodu znanych problemów.  [Moduły integracji programu System Center Orchestrator](https://www.microsoft.com/download/details.aspx?id=49555) obejmuje przekonwertowanego wersje tych pakietów integracyjnych, które mogą być importowane do automatyzacji Azure i automatyzacja zarządzania usługami.  

W wersji RTM hello tego narzędzia zaktualizowane wersje pakietów integracyjnych hello oparte na OIT, który może zostać przekonwertowany z powitalne Integration Pack konwertera zostaną opublikowane.  Wskazówki dotyczące będzie również podać tooassist konwertowania elementów runbook przy użyciu działań z pakietów integracyjnych hello nie jest oparty na OIT.

## <a name="runbook-converter"></a>Konwerter elementu Runbook
Witaj konwertera Runbook konwertuje elementy runbook programu Orchestrator do [graficznych elementów runbook](automation-runbook-types.md#graphical-runbooks) który można zaimportować do usługi Automatyzacja Azure.  

Konwerter elementu Runbook jest zaimplementowany jako moduł programu PowerShell za pomocą polecenia cmdlet, o nazwie **ConvertFrom SCORunbook** wykonująca hello konwersji.  Po zainstalowaniu narzędzia hello utworzy sesję programu PowerShell tooa skrótu, który ładuje hello polecenia cmdlet.   

Poniżej jest hello podstawowy proces tooconvert elementu runbook programu Orchestrator i zaimportuj go do usługi Automatyzacja Azure.  Witaj poniższe sekcje zawierają dodatkowe szczegóły za pomocą narzędzia hello i Praca z przekonwertowanego elementów runbook.

1. Eksportuj co najmniej jeden element runbook z programu Orchestrator.
2. Uzyskaj moduły integracji dla wszystkich działań w hello elementu runbook.
3. Konwertuj elementy runbook programu Orchestrator hello hello eksportowanego pliku.
4. Przejrzyj informacje w dziennikach toovalidate hello konwersji i toodetermine wszelkie wymagane działania ręcznego.
5. Zaimportuj przekonwertowany elementów runbook do automatyzacji Azure.
6. Utwórz wszystkie wymagane zasoby w automatyzacji Azure.
7. Edytuj hello runbook w automatyzacji Azure toomodify wszelkie wymagane działania.

### <a name="using-runbook-converter"></a>Za pomocą konwertera elementu Runbook
Witaj składnię **ConvertFrom SCORunbook** wygląda następująco:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - export toohello ścieżki pliku zawierającego tooconvert elementów runbook hello.
* Moduł — rozdzielana przecinkami lista zawierająca działania w elementach runbook hello moduły integracji.
* OutputFolder - ścieżka toohello folderu toocreate przekonwertować graficznych elementów runbook.

następujące przykładowe polecenie konwertuje hello elementów runbook w pliku eksportu o nazwie Hello **MyRunbooks.ois_export**.  Te elementy runbook za pomocą hello usługi Active Directory i pakiety integracyjne programu Data Protection Manager.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Pliki dziennika
Witaj konwertera elementu Runbook utworzy następujące pliki dziennika w hello hello tej samej lokalizacji co hello przekonwertować elementu runbook.  Jeśli istnieją już pliki hello, następnie zostaną one zastąpione informacjami uzyskanymi z ostatnich konwersji hello.

| Plik | Zawartość |
|:--- |:--- |
| Konwerter Runbook - Progress.log |Szczegółowy opis kroków konwersji hello, w tym informacje o każdym działaniu pomyślnie przekonwertowany i ostrzeżenie dla każdego działania nie został przekonwertowany. |
| Konwerter Runbook - Summary.log |Podsumowanie hello ostatni konwersji, w tym wszelkie ostrzeżenia i wykonaj zadań wymagających tooperform, takich jak tworzenie wymagane dla elementu runbook hello przekonwertować zmiennej. |

### <a name="exporting-runbooks-from-orchestrator"></a>Eksportowanie elementów runbook z programu Orchestrator
Hello konwertera Runbook współpracuje z pliku eksportu programu Orchestrator, który zawiera jeden lub więcej elementów runbook.  W pliku eksportu hello utworzy odpowiedni element runbook usługi Automatyzacja Azure dla każdego elementu runbook programu Orchestrator.  

tooexport elementu runbook z programu Orchestrator, kliknij prawym przyciskiem myszy nazwę hello hello runbook w programie Runbook Designer i wybierz **wyeksportować**.  tooexport wszystkich elementów runbook w folderze, kliknij prawym przyciskiem myszy nazwę hello hello i wybierz polecenie **wyeksportować**.

### <a name="runbook-activities"></a>Działania elementu Runbook
Witaj konwertera Runbook konwertuje każde działanie w hello odpowiadające mu działanie tooa Orchestrator runbook automatyzacji Azure.  Dla tych działań, których nie można przekonwertować aktywności symbol zastępczy jest tworzony w hello runbook za pomocą tekst ostrzeżenia.  Po zaimportowaniu hello przekonwertować elementu runbook do automatyzacji Azure, musisz zastąpić żadnego z tych działań prawidłowy działania, wykonujące hello wymagane funkcje.

Wszystkie działania programu Orchestrator w hello [standardowy moduł działania](#standard-activities-module) zostanie przekonwertowany.  Brak niektórych standardowych działań programu Orchestrator, które nie znajdują się w tym module jednak i nie są konwertowane.  Na przykład **wysyłania zdarzenia platformy** nie zawiera usługi Automatyzacja Azure odpowiednika ponieważ zdarzeń hello jest tooOrchestrator określone.

[Monitorowanie działań](https://technet.microsoft.com/library/hh403827.aspx) nie są konwertowane, ponieważ nie nie równoważne toothem automatyzacji Azure.  Witaj wyjątków są monitor działania w [konwertować Pakiety integracyjne](#integration-pack-converter) który będą przekonwertowane toohello symbolu zastępczego działania.

Wszystkie działania z [przekonwertować pakiet integracyjny](#integration-pack-converter) zostaną przekonwertowane, jeśli możesz zapewnić modułu integracji toohello ścieżka hello hello **modułów** parametru.  Pakiety integracyjne programu System Center, można użyć hello [moduły integracji programu System Center Orchestrator](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Zasoby programu orchestrator
Hello konwertera Runbook konwertuje tylko elementy runbook, a nie inne zasoby programu Orchestrator liczników, zmiennych lub połączeń.  Liczniki są nieobsługiwane w automatyzacji Azure.  Połączenia i zmienne są obsługiwane, ale należy je utworzyć ręcznie.  pliki dziennika Hello będzie poinformować hello element runbook wymaga tych zasobów i określenie odpowiednich zasobów muszą toocreate automatyzacji Azure dla hello poprawnie przekonwertować toooperate elementu runbook.

Na przykład element runbook może użyć zmiennej toopopulate określoną wartość w działaniu.  Witaj przekonwertowany element runbook zostanie przekonwertować aktywności hello i określ zasób zmiennej automatyzacji Azure z hello takie same nazwy co zmienna Orchestrator hello.  Będą to wymienione w hello **Runbook konwertera - Summary.log** pliku, który jest tworzony po konwersji hello.  Konieczne będzie toomanually utworzyć ten zasób zmiennej automatyzacji Azure przed użyciem hello elementu runbook.

### <a name="input-parameters"></a>Parametry wejściowe
Elementy Runbook w programie Orchestrator akceptują parametrów wejściowych z hello **inicjalizowania danych** działania.  Jeśli runbook hello konwertowanej obejmuje to działanie, a następnie [parametru wejściowego](automation-graphical-authoring-intro.md#runbook-input-and-output) w hello Azure automatyzacji elementu runbook jest tworzona dla każdego parametru w działaniu hello.  A [kontroli przepływu pracy skryptu](automation-graphical-authoring-intro.md#activities) działania jest tworzony w hello przekonwertować runbook, który pobiera i zwraca każdego parametru.  Żadnych działań w elemencie runbook hello korzystających z parametrem wejściowym można znaleźć toohello wyjście z tego działania.

Przyczyna Hello, że ta strategia jest używana jest funkcja hello dublowany toobest w hello Orchestrator runbook.  Działania w nowych graficznych elementów runbook powinien odwoływać się bezpośrednio tooinput parametrów przy użyciu źródła danych wejściowych elementu Runbook.

### <a name="invoke-runbook-activity"></a>Działania wywołania elementu Runbook
Elementy Runbook w programie Orchestrator zaczynać się inne elementy runbook hello **Wywołaj element Runbook** działania. Jeśli konwertowany runbook hello obejmuje tego działania i hello **czekać na ukończenie** opcja jest ustawiona, a następnie działania elementu runbook jest tworzony dla niego w elemencie runbook hello przekonwertowany.  Jeśli hello **czekać na ukończenie** opcja nie jest ustawiona, a następnie tworzony jest działanie skryptu przepływu pracy, który używa **Start AzureAutomationRunbook** toostart hello runbook.  Po zaimportowaniu hello przekonwertować elementu runbook do automatyzacji Azure należy zmodyfikować informacje hello określony w działaniu hello tego działania.

## <a name="related-articles"></a>Pokrewne artykuły:
* [System Center 2012 — Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Automatyzacja zarządzania usługami](https://technet.microsoft.com/library/dn469260.aspx)
* [Hybrydowy proces roboczy elementu Runbook](automation-hybrid-runbook-worker.md)
* [Działania standardowe programu orchestrator](http://technet.microsoft.com/library/hh403832.aspx)
* [Pobierz System Center Orchestrator Migration Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
