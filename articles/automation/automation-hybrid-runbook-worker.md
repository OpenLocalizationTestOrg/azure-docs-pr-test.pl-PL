---
title: aaaAzure automatyzacji hybrydowymi elementami roboczymi Runbook | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera informacje o instalowaniu i używaniu hybrydowy proces roboczy elementu Runbook, która jest funkcją automatyzacji Azure, która pozwala toorun elementów runbook na maszynach w lokalnym centrum danych lub dostawcy usług w chmurze."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Automatyzację zasobów w centrum danych lub w chmurze chronionej za pomocą hybrydowy proces roboczy elementu Runbook
Elementy Runbook automatyzacji Azure nie może uzyskać dostępu zasobów w innych chmur lub w środowisku lokalnym, ponieważ są uruchamiane w hello chmury Azure.  Hello funkcji hybrydowego procesu roboczego elementu Runbook usługi Automatyzacja Azure pozwala toorun elementy runbook bezpośrednio na komputerze hello hostującego rolę hello, względem zasobów w toomanage środowiska hello tych zasobów lokalnych. Elementy Runbook są przechowywane i zarządzane w automatyzacji Azure i następnie dostarczyć tooone lub więcej wyznaczonych komputerów.  

Ta funkcja jest zaprezentowana w powitania po obrazu:<br>  

![Omówienie procesu roboczego elementu Runbook hybrydowego](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Informacje techniczne hello aspekty roli i wdrażania hybrydowego procesu roboczego elementu Runbook, zobacz [Przegląd architektury automatyzacji](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Hybrydowego procesu roboczego elementu Runbook grup
Każdy hybrydowy proces roboczy elementu Runbook jest członkiem grupy hybrydowego procesu roboczego elementu Runbook, którą określono podczas instalacji agenta hello.  Grupy mogą obejmować jednego agenta, ale można zainstalować wielu agentów w grupie wysokiej dostępności.

Po uruchomieniu elementu runbook na hybrydowy proces roboczy elementu Runbook zostanie określona grupa hello jest uruchamiany na.  Hello członkami grupy hello ustalić, który proces roboczy usług hello żądania.  Nie można określić określonego procesu roboczego.

## <a name="relationship-tooservice-management-automation"></a>Relacja tooService Management Automation
[Usługa zarządzania Strukturę automatyzacja](https://technet.microsoft.com/library/dn469260.aspx) pozwala toorun hello tego samego elementów runbook, które są obsługiwane przez usługi Automatyzacja Azure w centrum danych lokalnych. SMA zwykle jest wdrażany wraz z dodatkiem Service Pack systemu Windows Azure, zgodnie z interfejsem graficznym do zarządzania SMA zawiera pakietu Windows Azure Pack. W przeciwieństwie do automatyzacji Azure SMA wymaga instalacji lokalnej, zawierająca hello toohost serwerów sieci web interfejsu API, runbook toocontain bazy danych i konfiguracji SMA i zadania elementów runbook tooexecute procesy robocze elementu Runbook. Automatyzacja Azure udostępnia te usługi w chmurze hello i wymaga tylko toomaintain hello hybrydowych procesów roboczych elementu Runbook w środowisku lokalnym.

W przypadku istniejącego użytkownika SMA można przenosić z toobe automatyzacji elementów runbook tooAzure używane z hybrydowy proces roboczy elementu Runbook bez zmian, przy założeniu, że działają one własnych tooresources uwierzytelniania, zgodnie z opisem w [uruchamiania elementów runbook na element Runbook hybrydowego Proces roboczy](automation-hrw-run-runbooks.md).  Elementy Runbook działają w kontekście hello hello konta usługi na serwerze worker hello będące uwierzytelniania hello elementów runbook SMA.

Możesz użyć hello następujące kryteria toodetermine, czy usługi Automatyzacja Azure z hybrydowy proces roboczy elementu Runbook lub Service Management Automation jest bardziej odpowiednie dla wymagań.

* SMA wymaga instalacji lokalnej jego podstawowych składników, które są połączone tooWindows pakietu Azure Pack, jeśli wymagany jest interfejs zarządzania w trybie graficznym. Wyższe koszty utrzymania niż Automatyzacja Azure, w którym agent został zainstalowany na lokalnym programów runbook Worker musi tylko są potrzeby więcej zasobów lokalnych. agenci Hello są zarządzane przez usługi Operations Management Suite, dalsze zmniejszenie kosztów obsługi.
* Usługi Automatyzacja Azure w chmurze hello są przechowywane jego elementy runbook, a następnie dostarcza ich lokalne tooon hybrydowymi elementami roboczymi Runbook. Zasady zabezpieczeń nie zezwalają na to zachowanie, należy użyć SMA.
* SMA jest dołączony do programu System Center; i dlatego wymaga licencji programu System Center 2012 R2. Automatyzacja Azure jest oparta na modelu warstwowych subskrypcji.
* Automatyzacja Azure udostępnia zaawansowane funkcje, takie jak graficznych elementów runbook, które nie są dostępne w programie SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Instalowanie hello procesu roboczego elementu Runbook hybrydowego systemu Windows 

tooinstall i skonfiguruj hybrydowych Windows Runbook Worker, istnieją dwie metody.  Witaj zalecana metoda jest przy użyciu automatyzacji toocompletely elementu runbook automatyzacji procesu hello wymagane tooconfigure komputerem z systemem Windows.  Druga metoda Hello jest zgodnie z procedurą krok po kroku instalacji toomanually i skonfigurować rolę hello.  

> [!NOTE]
> toomanage hello konfiguracji serwerów pomocniczych hello roli hybrydowy proces roboczy elementu Runbook z konfiguracji żądanego stanu (DSC), należy tooadd ich jako węzły DSC.  Aby uzyskać więcej informacji na temat dołączania ich do zarządzania za pomocą usługi Konfiguracja DSC, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md).           
><br>
>Po włączeniu hello [rozwiązania do zarządzania aktualizacjami](../operations-management-suite/oms-solution-update-management.md), komputer z systemem Windows podłączony tooyour obszarem roboczym pakietu OMS zostanie automatycznie skonfigurowany jako elementy runbook hybrydowy proces roboczy elementu Runbook toosupport zawartych w tym rozwiązaniu.  Jednak nie jest zarejestrowany z wszystkich grup hybrydowy proces roboczy już zdefiniowane na Twoim koncie automatyzacji.  Hello komputera można dodać grupy hybrydowego procesu roboczego elementu Runbook tooa w Twojej toosupport konta automatyzacji elementu runbook usługi Automatyzacja tak długo, jak używasz hello tego samego konta dla rozwiązania hello i członkostwa w grupie hybrydowy proces roboczy elementu Runbook.  Ta funkcja została dodana tooversion 7.2.12024.0 hello hybrydowy proces roboczy elementu Runbook.  

Hello Przejrzyj następujące informacje dotyczące hello [wymagania sprzętowe i programowe](automation-offering-get-started.md#hybrid-runbook-worker) i [informacji do przygotowania sieci](automation-offering-get-started.md#network-planning) przed rozpoczęciem wdrażania hybrydowego procesu roboczego elementu Runbook.  Po pomyślnym wdrożeniu runbook worker, przejrzyj [uruchamiania elementów runbook na hybrydowy proces roboczy elementu Runbook](automation-hrw-run-runbooks.md) toolearn jak tooconfigure Twojego tooautomate elementów runbook przetwarza w lokalnym centrum danych lub w innym środowisku chmury.  
 
### <a name="automated-deployment"></a>Wdrożenie zautomatyzowane

Wykonaj następujące hello kroki tooautomate hello instalację i konfigurację roli procesu roboczego hybrydowego Windows hello.  

1. Pobierz hello *OnPremiseHybridWorker.ps1 nowy* skryptu z hello [galerii programu PowerShell](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) bezpośrednio z rolą hybrydowy proces roboczy elementu Runbook hello komputera hello lub z innego komputera w sieci środowisko i skopiować go toohello procesu roboczego.  

    Witaj *OnPremiseHybridWorker.ps1 nowy* skrypt wymaga następujących parametrów podczas wykonywania hello:

  * *AutomationAccountName* (wymagane) - hello nazwa konta automatyzacji.  
  * *ResourceGroupName* (wymagane) - hello nazwę grupy zasobów hello skojarzonych z Twoim kontem automatyzacji.  
  * *HybridGroupName* (wymagane) - hello nazwę grupy hybrydowego procesu roboczego elementu Runbook, określony jako element docelowy dla elementów runbook hello obsługi tego scenariusza. 
  *  *Identyfikator subskrypcji* (wymagane) — Witaj identyfikator subskrypcji platformy Azure, do których należy konto automatyzacji.
  *  *WorkspaceName* (opcjonalnie) — Witaj OMS nazwa obszaru roboczego.  Jeśli nie masz obszar roboczy OMS, hello skrypt tworzy i konfiguruje jeden.  

     > [!NOTE]
     > Obecnie są hello tylko regiony automatyzacji obsługiwane w przypadku integracji z usługą OMS - **południowo-wschodnia Australia**, **wschodnie stany USA 2**, **Azja południowo-wschodnia**, i **zachodnie Europa**.  Jeśli Twoje konto usługi Automatyzacja nie jest w jednym z tych regionów, hello skrypt tworzy obszarem roboczym pakietu OMS, ale go ostrzega, że jej nie może połączyć je razem.
     > 
2. Na komputerze, należy uruchomić **programu Windows PowerShell** z hello **Start** ekranu w trybie administratora.  
3. Z hello powłoka wiersza polecenia programu PowerShell Przejdź toohello folder, który zawiera skrypt hello pobrane i wykonaj go zmiana hello wartości parametrów *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, i *- WorkspaceName*.

     > [!NOTE] 
     > Po wykonaniu hello script są tooauthenticate zostanie wyświetlony monit o systemie Azure.  Możesz **musi** Zaloguj się przy użyciu konta należącego do roli Administratorzy subskrypcji hello i współadministratorem subskrypcji hello.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. Jesteś tooinstall zostanie wyświetlony monit o tooagree **NuGet** i zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń platformy Azure.<br><br> ![Wykonanie skryptu OnPremiseHybridWorker nowy](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Po zakończeniu skryptu hello bloku hybrydowego procesu roboczego grupy hello wyświetli hello nową grupę i liczby elementów członkowskich lub jeśli istniejącą grupę, jest zwiększany hello liczby elementów członkowskich.  Grupy hello można wybrać z listy hello na powitania **hybrydowego procesu roboczego grupy** bloku i wybierz hello **hybrydowych procesów roboczych** kafelka.  Na powitania **hybrydowych procesów roboczych** bloku, zobacz każdego członka grupy hello na liście.  

### <a name="manual-deployment"></a>Ręczne wdrażanie 
Raz wykonać hello pierwsze dwa kroki dla danego środowiska automatyzacji, a następnie powtórz hello pozostałe kroki na każdym komputerze pracownika.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Utwórz obszar roboczy usługi Operations Management Suite
Jeśli nie masz już obszar roboczy usługi Operations Management Suite, następnie utwórz ją przy użyciu instrukcji w [Zarządzanie obszaru roboczego](../log-analytics/log-analytics-manage-access.md). Istniejący obszar roboczy można użyć, jeśli już istnieje.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Dodaj tooOperations rozwiązania Automatyzacja obszarem roboczym Management Suite
Rozwiązania Dodaj funkcje tooOperations Management Suite.  Witaj rozwiązanie do automatyzacji dodaje funkcje na tym obsługę hybrydowy proces roboczy elementu Runbook usługi Automatyzacja Azure.  Po dodaniu obszar roboczy tooyour rozwiązania hello automatycznie wypycha procesu roboczego składniki toohello agenta komputera instalującym hello następnego kroku.

Postępuj zgodnie z instrukcjami hello w [tooadd rozwiązania za pomocą galerii rozwiązań hello](../log-analytics/log-analytics-add-solutions.md) tooadd hello **automatyzacji** obszar roboczy usługi Operations Management Suite tooyour rozwiązania.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Zainstaluj hello Microsoft Monitoring Agent
Hello Microsoft Monitoring Agent łączy się z komputerami tooOperations Management Suite.  Po zainstalowaniu agenta hello na komputerze lokalnym i podłącz go tooyour obszaru roboczego, będzie automatycznie pobierał hello składniki wymagane do hybrydowy proces roboczy elementu Runbook.

Postępuj zgodnie z instrukcjami hello w [tooLog komputerów Windows połączyć Analytics](../log-analytics/log-analytics-windows-agents.md) tooinstall hello agenta na powitania na komputerze lokalnym.  Można Powtórz ten proces dla wielu komputerów tooadd wielu pracowników tooyour środowiska.

Gdy hello agent pomyślnie nawiązało połączenie tooOperations Management Suite, będzie wymieniony na powitania **połączonych źródeł** kartę hello Operations Management Suite **ustawienia** okienka.  Możesz zweryfikować tego agenta hello poprawnie pobrała rozwiązania Automatyzacja powitania po folder o nazwie **AzureAutomationFiles** w C:\Program Files\Microsoft Monitoring Agent\Agent.  wersję hello tooconfirm hello hybrydowy proces roboczy elementu Runbook, można przejść hello Agent\Agent\AzureAutomation\ monitorowania i Uwaga tooC:\Program Files\Microsoft \\ *wersji* podfolderu.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Zainstalowania środowiska elementu runbook hello i połączyć tooAzure automatyzacji
Podczas dodawania agenta tooOperations Management Suite hello rozwiązania Automatyzacja umieszcza dół hello **HybridRegistration** moduł programu PowerShell, który zawiera hello **Add-HybridRunbookWorker** polecenia cmdlet.  Użyj tego polecenia cmdlet tooinstall hello runbook środowiska na komputerze hello i zarejestrowanie go za pomocą usługi Automatyzacja Azure.

Otwórz sesję programu PowerShell w trybie administratora i uruchom następujące polecenia tooimport hello modułu hello.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Następnie uruchom hello **Add-HybridRunbookWorker** polecenia cmdlet przy użyciu hello następującej składni:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Możesz uzyskać hello informacji wymaganych dla tego polecenia cmdlet z hello **zarządzanie kluczami** bloku w hello portalu Azure.  Otwórz ten blok, wybierając hello **klucze** opcję hello **ustawienia** bloku na Twoim koncie automatyzacji.

![Omówienie procesu roboczego elementu Runbook hybrydowego](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** jest nazwą hello hello grupy hybrydowych procesów roboczych elementu Runbook. Jeśli ta grupa już istnieje na koncie automatyzacji hello, bieżący komputer hello jest dodawany tooit.  Jeśli go jeszcze nie istnieje, następnie jest dodawany.
* **Punkt końcowy** jest hello **adres URL** w hello **zarządzanie kluczami** bloku.
* **Token** jest hello **podstawowy klucz dostępu** w hello **zarządzanie kluczami** bloku.  

Użyj hello **-Verbose** przełącznik z **Add-HybridRunbookWorker** tooreceive szczegółowe informacje na temat instalacji hello.

#### <a name="5-install-powershell-modules"></a>5. Zainstaluj moduły programu PowerShell
Elementy Runbook można użyć dowolnego hello działań i poleceń cmdlet zdefiniowane w modułach hello zainstalowanej w środowisku usługi Automatyzacja Azure.  Te moduły nie są automatycznie wdrożone tooon lokalnych komputerów, więc należy ją zainstalować ręcznie.  wyjątek Hello jest hello Azure moduł, który jest instalowany domyślnie, zapewniając toocmdlets dostęp do wszystkich usług platformy Azure i działań automatyzacji Azure.

Ponieważ hello podstawowym celem hello funkcji hybrydowego procesu roboczego elementu Runbook jest toomanage zasobów lokalnych, prawdopodobnie wymagana tooinstall hello modułów, które obsługują te zasoby.  Można odwoływać się za[instalowanie modułów](http://msdn.microsoft.com/library/dd878350.aspx) informacje na temat instalowania modułów programu Windows PowerShell.  Moduły, które są zainstalowane musi znajdować się w lokalizacji odwołuje PSModulePath zmiennej środowiskowej, dzięki czemu są automatycznie importowane przez hello hybrydowy proces roboczy.  Aby uzyskać więcej informacji, zobacz [hello Modyfikowanie ścieżki instalacji PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Usuwanie hybrydowy proces roboczy elementu Runbook 
Co najmniej jeden hybrydowymi elementami roboczymi Runbook można usunąć z grupy lub usunąć grupę hello, w zależności od wymagań.  tooremove hybrydowy proces roboczy elementu Runbook z komputera lokalnego, wykonaj hello następujące kroki.

1. W hello portalu Azure Przejdź tooyour konta automatyzacji.  
2. Z hello **ustawienia** bloku, wybierz opcję **klucze** i zanotuj wartości pola hello **adres URL** i **podstawowy klucz dostępu**.  Te informacje są niezbędne dla hello następnego kroku.
3. Otwórz sesję programu PowerShell w trybie administratora i uruchom następujące hello command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Użyj hello **-Verbose** przełączać szczegółowy dziennik hello proces usuwania.

> [!NOTE]
> Nie powoduje usunięcia hello Microsoft Monitoring Agent z komputera hello, tylko funkcje hello i konfiguracji hello roli hybrydowy proces roboczy elementu Runbook.  

## <a name="remove-hybrid-worker-groups"></a>Usuń grupy hybrydowego procesu roboczego
tooremove grupy, należy najpierw tooremove hello hybrydowy proces roboczy elementu Runbook z każdego komputera, który jest członkiem grupy hello przy użyciu hello procedury przedstawionej wcześniej, a następnie wykonaj następujące kroki tooremove hello grupy hello.  

1. Otwórz konto automatyzacji hello w hello portalu Azure.
2. Wybierz hello **hybrydowego procesu roboczego grupy** kafelka w hello **hybrydowego procesu roboczego grupy** bloku, wybierz hello grupy toodelete.  Po wybraniu hello określonej grupy, hello **grupy hybrydowych procesów roboczych** bloku właściwości jest wyświetlany.<br> ![Blok grupy hybrydowych procesów roboczych elementu Runbook](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. W bloku właściwości hello hello wybraną grupę, kliknij **usunąć**.  Pojawi się pytaniem, czy użytkownik tooconfirm tę akcję, wybierz opcję **tak** , gdy chcesz tooproceed.<br> ![Okno dialogowe potwierdzenia usunięcia grupy](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Ten proces może potrwać kilka sekund toocomplete i można śledzić postęp w obszarze **powiadomienia** hello menu.  

## <a name="troubleshooting"></a>Rozwiązywanie problemów 
Hello hybrydowy proces roboczy elementu Runbook jest zależna od hello toocommunicate Microsoft Monitoring Agent z procesem roboczym hello automatyzacji konta tooregister, odbierania zadań i stan raportu. W przypadku niepowodzenia rejestracji pracownika hello poniżej przedstawiono niektóre możliwe przyczyny błędu hello:  

1. Hello hybrydowy proces roboczy jest związany z serwera proxy lub zapory.  
    Sprawdź, czy komputer hello ma wychodzący dostęp too*.azure-automation.net na porcie 443.  

2. Witaj komputera hello hybrydowy proces roboczy jest uruchomiona na ma mniejszą niż minimalne wymagania dotyczące sprzętu hello [wymagania](automation-offering-get-started.md#hybrid-runbook-worker).  
    Komputery z systemem hello hybrydowy proces roboczy elementu Runbook powinna spełniać hello minimalne wymagania sprzętowe przed oznaczeniem go toohost tej funkcji. W przeciwnym razie w zależności od wykorzystania zasobów hello innych procesów w tle i rywalizacji spowodowane przez elementy runbook podczas wykonywania, hello komputera będzie stają się nadmiernie wykorzystywany i spowodować opóźnienia zadania elementu runbook i przekroczeń limitu czasu.
   Upewnij się, komputer hello wyznaczonych funkcji hybrydowego procesu roboczego elementu Runbook hello toorun spełnia hello minimalne wymagania sprzętowe.  Jeśli tak, monitorować toodetermine wykorzystanie procesora CPU i pamięci korelacja hello wydajności procesów hybrydowy proces roboczy elementu Runbook i systemu Windows.  Jeśli brak pamięci lub dużego wykorzystania procesora CPU, może to wskazywać tooupgrade potrzeby hello lub dodać dodatkowych procesorów lub zwiększenie pamięci tooaddress hello zasobu "wąskie gardło" i usunąć błąd hello. Można również wybrać zasób różnych obliczeń obsługiwanych hello minimalne wymagania i skalowane, gdy wymaganego obciążenia wskazywać wzrost jest konieczne.
    
3. Witaj usługi Microsoft Monitoring Agent nie jest uruchomiona.  
    Jeśli nie jest uruchomiona usługa Microsoft Monitoring Agent Windows hello, zapobiega to hello hybrydowy proces roboczy elementu Runbook komunikację z usługi Automatyzacja Azure.  Sprawdź hello agent jest uruchomiony, wprowadzając następujące polecenie w programie PowerShell hello: `get-service healthservice`.  Jeśli hello usługa zostanie zatrzymana, wprowadź następujące polecenia programu PowerShell toostart hello usługi hello: `start-service healthservice`.  

4. W hello **aplikacji i usług Menedżera Logs\Operations** dziennika zdarzeń, zobacz zdarzenia 4502 i zawierający EventMessage **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**z powitania po opis: *hello certyfikat przedstawiony przez usługę hello <wsid>. oms.opinsights.azure.com nie został wystawiony przez urząd certyfikacji używany dla usług firmy Microsoft. Jeśli korzystają z serwera proxy przechwytującego komunikację TLS/SSL, skontaktuj się z toosee administratora sieci. Witaj artykuł KB3126513 zawiera dodatkowe informacje dotyczące rozwiązywania problemów, które występują problemy dotyczące połączenia.*
    Może to być spowodowane przez użytkownika serwera proxy lub sieć zapory blockking komunikacji tooMicrosoft Azure.  Sprawdź, czy komputer hello ma wychodzący dostęp too*.azure-automation.net na porty 443.

Dzienniki są przechowywane lokalnie na każdym hybrydowy proces roboczy na C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Można sprawdzić, czy istnieją ostrzeżenia lub zdarzenia błędów zapisane toohello **aplikacji i usług Logs\Microsoft-SMA\Operations** i **aplikacji i usług Menedżera Logs\Operations** dziennika zdarzeń Wskazuje z łącznością lub innego problemu dołączania hello roli tooAzure automatyzacji lub problem podczas wykonywania normalnych operacji.  

## <a name="next-steps"></a>Następne kroki
Przegląd [uruchamiania elementów runbook na hybrydowy proces roboczy elementu Runbook](automation-hrw-run-runbooks.md) toolearn jak tooconfigure Twojego tooautomate elementów runbook przetwarza w lokalnym centrum danych lub w innym środowisku chmury.
