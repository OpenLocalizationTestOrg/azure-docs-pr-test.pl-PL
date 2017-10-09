---
title: "aaaTroubleshooting usługi Automatyzacja Azure typowych problemów | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje toohelp Rozwiązywanie problemów i Rozwiąż typowe błędy usługi Automatyzacja Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "Błąd automatyzacji, rozwiązywania problemów, problem"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Rozwiązywanie typowych problemów w usłudze Automatyzacja Azure 
Ten artykuł zawiera pomoc w rozwiązywaniu typowych błędów mogą wystąpić w automatyzacji Azure, a także sugeruje możliwe rozwiązania tooresolve je.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Błędy uwierzytelniania podczas pracy z elementami runbook usługi Automatyzacja Azure
### <a name="scenario-sign-in-tooazure-account-failed"></a>Scenariusz: Konto logowania tooAzure nie powiodło się
**Błąd:** hello błąd "Unknown_user_type: Nieznany typ użytkownika" jest wyświetlany podczas pracy z poleceniami cmdlet Add-AzureAccount lub Login-AzureRmAccount hello.

**Przyczyną błędu hello:** ten błąd występuje, jeśli nazwa zasobu poświadczeń hello jest nieprawidłowa lub jeśli hello nazwy użytkownika i hasło użyte zasób poświadczenia usługi Automatyzacja hello toosetup nie są prawidłowe.

**Porady dotyczące rozwiązywania problemów:** w kolejności toodetermine, co jest nieprawidłowe, podjąć hello następujące kroki:  

1. Upewnij się, że nie masz żadnych znaków specjalnych, w tym hello  **@**  w hello automatyzacji zasobów Nazwa poświadczenia używasz tooconnect tooAzure.  
2. Sprawdź można hello nazwy użytkownika i hasła, które są przechowywane w hello poświadczenia usługi Automatyzacja Azure w Edytorze lokalnych PowerShell ISE. Można to zrobić, uruchamiając następujące polecenia cmdlet programu PowerShell ISE hello hello:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Jeśli uwierzytelnianie nie powiedzie się lokalnie, oznacza to, że nie skonfigurowano poświadczeń usługi Azure Active Directory poprawnie. Odwołuje się zbyt[uwierzytelniania przy użyciu usługi Azure Active Directory tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) blogu post tooget hello Azure Active Directory konta są nieprawidłowo skonfigurowane.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Scenariusz: Nie można toofind hello subskrypcji platformy Azure
**Błąd:** błąd powitania "hello subskrypcji o nazwie ``<subscription name>`` nie można odnaleźć" podczas pracy z poleceniami cmdlet wybierz AzureSubscription lub Select-AzureRmSubscription hello.

**Przyczyną błędu hello:** ten błąd występuje, jeśli nazwa subskrypcji hello jest nieprawidłowa lub hello Azure Active Directory użytkownika, który próbuje Szczegóły subskrypcji hello tooget nie jest skonfigurowany jako administrator subskrypcji hello.

**Porady dotyczące rozwiązywania problemów:** w kolejności toodetermine jeśli zostały prawidłowo uwierzytelnione tooAzure i ma subskrypcję toohello dostęp próbujesz tooselect, wykonać hello następujące kroki:  

1. Upewnij się, że uruchamiasz hello **Add-AzureAccount** przed uruchomieniem hello **AzureSubscription wybierz** polecenia cmdlet.  
2. Jeśli ten komunikat o błędzie, należy zmodyfikować kod, dodając hello **Get-AzureSubscription** polecenie cmdlet hello **Add-AzureAccount** polecenia cmdlet, a następnie wykonaj hello kodu.  Teraz Sprawdź, czy dane wyjściowe hello Get AzureSubscription zawiera szczegółowe informacje dotyczące Twojej subskrypcji.  

   * Jeśli nie widać żadnych szczegółów subskrypcji w danych wyjściowych hello, oznacza to, hello subskrypcji nie jest jeszcze zainicjowana.  
   * Jeśli widzisz hello Szczegóły subskrypcji w danych wyjściowych hello, upewnij się, czy za pomocą hello subskrypcji poprawna nazwa lub identyfikator hello **AzureSubscription wybierz** polecenia cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Scenariusz: Uwierzytelnianie tooAzure nie powiodło się, ponieważ jest włączone uwierzytelnianie wieloskładnikowe
**Błąd:** hello wystąpi błąd "Add-AzureAccount: AADSTS50079: rejestracji silnego uwierzytelniania (dowód do góry) jest wymagana" podczas uwierzytelniania tooAzure z Azure nazwę użytkownika i hasło.

**Przyczyną błędu hello:** wprowadzić uwierzytelnianie wieloskładnikowe na koncie Azure, nie można użyć tooAzure tooauthenticate użytkownika usługi Azure Active Directory.  Zamiast tego należy toouse certyfikatu lub tooAzure tooauthenticate główną usługi.

**Porady dotyczące rozwiązywania problemów:** toouse certyfikatu z hello poleceń cmdlet do zarządzania usługi Azure, zobacz zbyt[tworzeniem i dodawaniem toomanage certyfikatu Azure usługi.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse nazwy głównej usługi za pomocą poleceń cmdlet usługi Azure Resource Manager, można znaleźć zbyt[Tworzenie usługi głównej, przy użyciu portalu Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md) i [uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Typowe błędy podczas pracy z elementami runbook
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Scenariusz: rozpoczęcia zadania elementu runbook hello podjęto trzy razy, ale nie toostart w każdym
**Błąd:** element runbook nie powiodło się z powodu błędu hello "" hello zadania została zainstalowana trzy razy, ale nie powiodło się."

**Przyczyną błędu hello:** przyczyną tego błędu może być hello z następujących powodów:  

1. Limit pamięci.  Udokumentowanych limity ilość pamięci przydzielona tooa piaskownicy [ograniczenia usługi automatyzacja](../azure-subscription-service-limits.md#automation-limits) tak zadania może się nie powieść go, gdy używa ponad 400 MB pamięci. 

2. Niezgodny moduł.  Taka sytuacja może wystąpić, jeśli moduł zależności nie są prawidłowe, a jeśli nie są one, element runbook zwykle zwróci błąd "Nie można odnaleźć polecenia" lub "Nie można powiązać parametr" wiadomości. 

**Porady dotyczące rozwiązywania problemów:** żadnego z następujących rozwiązań hello będzie naprawić hello:  

* Sugerowane metody toowork przed upływem limitu pamięci hello są toosplit hello obciążenia między wieloma elementami runbook, przetwarza jak najwięcej danych w pamięci, nie toowrite niepotrzebne dane wyjściowe elementy runbook lub należy wziąć pod uwagę liczbę punktów kontrolnych zapisu do programu PowerShell elementy runbook przepływu pracy.  

* Należy tooupdate Azure moduły, wykonując kroki hello [jak tooupdate programu Azure PowerShell modułów w automatyzacji Azure](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Scenariusz: Element Runbook nie powiodło się z powodu obiektu po deserializacji
**Błąd:** element runbook nie powiodło się z powodu błędu hello "nie można powiązać parametr ``<ParameterName>``. Nie można przekonwertować hello ``<ParameterType>`` wartości typu Deserialized ``<ParameterType>`` tootype ``<ParameterType>``".

**Przyczyną błędu hello:** Jeśli element runbook przepływu pracy programu PowerShell, przechowuje złożonych obiektów w formacie zdeserializowany, w kolejności toopersist swój stan elementu runbook Jeśli hello przepływ pracy zostanie zawieszony.  

**Porady dotyczące rozwiązywania problemów:**  
Wszelkie hello następujące trzy rozwiązania będzie rozwiązanie tego problemu:

1. Jeśli użytkownik są przekazanie w potoku obiektów złożony z jednego tooanother polecenia cmdlet, otoczenie tych poleceń cmdlet w bloku skryptu InlineScript.  
2. Przekazać hello nazw ani wartości potrzebnych z hello obiekt złożony zamiast przekazywanie hello całego obiektu.  
3. Użyj elementu runbook programu PowerShell zamiast element runbook przepływu pracy programu PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Scenariusz: Zadanie elementu Runbook nie powiodło się, ponieważ przekroczono przydział przydzielone hello
**Błąd:** zadania elementu runbook nie powiedzie się z powodu błędu powitania "hello osiągnięto limit przydziału dla hello miesięczne łącznego czasu wykonywania zadania dla tej subskrypcji".

**Przyczyną błędu hello:** ten błąd występuje, gdy hello wykonywania zadań przekracza hello 500-minutowy wolnego limitu przydziału dla Twojego konta. Ten przydział dotyczy rodzaje tooall zadania wykonywania zadań, takich jak testowanie zadania uruchamiania zadania z portalu hello, wykonywanie zadania za pomocą elementów webhook i planowania tooexecute zadania przy użyciu albo hello portalu Azure lub w centrum danych. więcej informacji o cenach dla automatyzacji Zobacz toolearn [cennik automatyzacji](https://azure.microsoft.com/pricing/details/automation/).

**Porady dotyczące rozwiązywania problemów:** Jeśli chcesz toouse ponad 500 minut przetwarzania miesięcznie należy toochange subskrypcji z warstwy podstawowej toohello warstwę bezpłatna hello. Możesz uaktualnić warstwy Basic toohello przez pobieranie hello następujące kroki:  

1. Zaloguj się tooyour subskrypcji platformy Azure  
2. Wybierz konto Automatyzacja hello, które chcesz tooupgrade  
3. Polecenie **ustawienia** > **warstwa cenowa i użycie** > **warstwa cenowa**  
4. Na powitania **wybierz warstwę cenową** bloku, wybierz opcję **podstawowe**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Scenariusz: Polecenia Cmdlet nierozpoznany podczas wykonywania elementu runbook
**Błąd:** zadania elementu runbook nie powiodło się z powodu błędu hello "``<cmdlet name>``: hello termin ``<cmdlet name>`` nie został rozpoznany jako nazwa polecenia cmdlet, funkcji, pliku skryptu lub program wykonywalny hello."

**Przyczyną błędu hello:** ten błąd występuje, gdy aparat programu PowerShell hello nie może znaleźć polecenia cmdlet hello jest używany w elemencie runbook.  Może to być spowodowane hello moduł zawierający hello polecenia cmdlet nie ma konta hello, istnieje konflikt nazw z nazwą elementu runbook lub polecenia cmdlet hello istnieje także w innym module i automatyzacji nie może rozpoznać nazwy hello.

**Porady dotyczące rozwiązywania problemów:** żadnego z następujących rozwiązań hello będzie naprawić hello:  

* Upewnij się, poprawnie wpisany hello nazwa polecenia cmdlet.  
* Upewnij się, polecenia cmdlet hello istnieje na koncie automatyzacji i że nie ma żadnych konfliktów. tooverify, jeśli polecenie cmdlet hello jest obecny, otwórz element runbook w trybie edycji i wyszukaj mają toofind w bibliotece hello lub uruchom polecenie cmdlet hello **Get-Command ``<CommandName>``** .  Po zweryfikowaniu to polecenie cmdlet hello jest konta toohello dostępne i czy nie ma konfliktów nazw z innych poleceń cmdlet lub elementy runbook, dodać toohello kanwy i upewnij się, że używasz prawidłowego parametru w elemencie runbook.  
* Jeśli występuje konflikt nazwy i polecenia cmdlet hello jest dostępny w dwóch różnych modułach, możesz rozwiązać ten problem przy użyciu w pełni kwalifikowana nazwa hello hello polecenia cmdlet. Na przykład można użyć **ModuleName\CmdletName**.  
* Jeśli wykonywanych hello runbook lokalnie w grupy hybrydowych procesów roboczych, a następnie upewnij się, że hello polecenia cmdlet i modułu jest zainstalowany na komputerze hello, który jest hostem hello hybrydowy proces roboczy.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Scenariusz: Długotrwała runbook spójnie zakończy się niepowodzeniem z wyjątkiem hello: "hello zadania nie może kontynuować wykonywania, ponieważ wielokrotnie został wykluczony z hello tego samego punktu kontrolnego".
**Przyczyną błędu hello:** , zachowanie projektu powodu toohello "Odpowiedni udział" Monitorowanie procesów w automatyzacji Azure, która automatycznie wstrzymuje wykonywanie elementu runbook, jeśli wykonywania dłuższy niż 3 godziny. Jednak hello zwracany komunikat o błędzie nie zapewnia "co dalej" Opcje. Element runbook może zostać zawieszone kilku powodów. Wstrzymuje wystąpić przede wszystkim z powodu tooerrors. Na przykład nieprzechwycony wyjątek w elemencie runbook, awarii sieci lub awarii na hello pracy hello runbook procesu roboczego elementu Runbook, będą wszystkie spowodować toobe runbook hello zawieszone, jak i rozpocząć od ostatniego punktu kontrolnego po wznowieniu.

**Porady dotyczące rozwiązywania problemów:** hello udokumentowane tooavoid rozwiązanie tego problemu jest punktów kontrolnych toouse w przepływie pracy.  toolearn więcej odwoływać się za[przepływów pracy programu PowerShell Learning](automation-powershell-workflow.md#checkpoints).  Bardziej szczegółowe wyjaśnienie "Odpowiedni udział" i punkt kontrolny można znaleźć w tym artykule blog [przy użyciu punktów kontrolnych w elementach Runbook](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).

## <a name="common-errors-when-importing-modules"></a>Typowe błędy podczas importowania modułów
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Scenariusz: Moduł nie powiedzie się tooimport lub poleceń cmdlet nie może zostać wykonana po zaimportowaniu
**Błąd:** modułu nie powiedzie się tooimport lub importuje pomyślnie, ale są wyodrębniane żadnych poleceń cmdlet.

**Przyczyną błędu hello:** niektóre typowe przyczyny, że moduł nie może pomyślnie zaimportować tooAzure automatyzacji są:  

* Struktura Hello jest niezgodna z hello struktury Automatyzacja wymagane przez jego toobe w.  
* Moduł Hello jest zależna od inny moduł, który nie został wdrożony tooyour konta automatyzacji.  
* Brak jego zależności w folderze hello Hello modułu.  
* Witaj **AzureRmAutomationModule nowy** polecenia cmdlet są używane tooupload hello modułu, a nie spowodowały hello magazynu pełną ścieżkę lub nie zostały załadowane modułu hello za pomocą publicznie dostępny adres URL.  

**Porady dotyczące rozwiązywania problemów:**  
Żadnego z następujących rozwiązań hello będzie naprawić hello:  

* Upewnij się, że ten moduł hello jest zgodna z formatem hello:  
  ModuleName.Zip  **->**  Nazwa_modułu lub numer wersji  **->**  (ModuleName.psm1, ModuleName.psd1)
* Otwórz plik psd1 hello i czy hello moduł nie ma żadnych zależności.  Jeśli tak, Przekaż te moduły toohello konta automatyzacji.  
* Upewnij się, czy wszystkie biblioteki przywoływanego znajdują się w folderze modułu hello.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Typowe błędy podczas pracy z konfiguracji żądanego stanu (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Scenariusz: Węzeł jest w stanie błędu z powodu błędu "Nie została odnaleziona"
**Błąd:** hello węzeł ma raport o **nie powiodło się** stanu i zawierający błąd powitania "hello próba tooget hello akcji z serwera https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction nie powiodło się, ponieważ prawidłowej konfiguracji ``<guid>`` nie można odnaleźć. "

**Przyczyną błędu hello:** ten błąd zazwyczaj występuje, gdy hello węzła jest przypisywana nazwa konfiguracji tooa (np. ABC) zamiast Nazwa konfiguracji węzła (np. ABC. Serwer sieci Web).  

**Porady dotyczące rozwiązywania problemów:**  

* Upewnij się, przypisujesz hello węzeł "Nazwa konfiguracji węzła" i nie hello "nazwy konfiguracji".  
* Można przypisać węzeł węzeł tooa konfiguracji za pomocą platformy Azure w portalu lub za pomocą polecenia cmdlet programu PowerShell.

  * W kolejności tooassign węzeł węzeł tooa konfiguracji przy użyciu portalu Azure, otwórz hello **węzłów DSC** bloku, wybierz węzeł i kliknij na **przypisać konfiguracji węzła** przycisku.  
  * W kolejności tooassign węzeł węzeł tooa konfiguracji przy użyciu polecenia cmdlet programu PowerShell, użyj **AzureRmAutomationDscNode zestaw** polecenia cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Scenariusz: Nie ma żadnych konfiguracji węzła (pliki MOF) zostały utworzone podczas kompilowania konfiguracji
**Błąd:** zadania kompilacji DSC zawiesza się z powodu błędu hello: "Kompilacja została ukończona pomyślnie, ale nie wygenerowano żadnych .mofs konfiguracji węzła".

**Przyczyną błędu hello:** po hello wyrażenie po hello **węzła** — słowo kluczowe w konfiguracji hello DSC ocenia zbyt$ wartość null, a następnie żadnych konfiguracji węzła nie zostaną zwrócone.    

**Porady dotyczące rozwiązywania problemów:**  
Żadnego z następujących rozwiązań hello będzie naprawić hello:  

* Upewnij się, że ten hello toohello następnego wyrażenia **węzła** — słowo kluczowe w definicji konfiguracji hello nie jest zbyt oceny $ wartości null.  
* Jeśli ConfigurationData podczas kompilowania konfiguracji hello, upewnij się, że przekazywane hello oczekiwanych wartości konfiguracji hello wymaga od [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Scenariusz: hello raportów węzłów DSC staje się zablokował stanu "w toku"
**Błąd:** agenta DSC danych wyjściowych "Nie odnaleziono wystąpienia z daną wartości właściwości."

**Przyczyną błędu hello:** przeprowadzono uaktualnienie z wersji platformy WMF i spowodować uszkodzenie usługi WMI.  

**Porady dotyczące rozwiązywania problemów:** postępuj zgodnie z instrukcjami hello hello [DSC znane problemy i ograniczenia](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix hello problem.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Scenariusz: Nie można toouse poświadczeń w konfiguracji DSC
**Błąd:** zadania kompilacji DSC zostało wstrzymane z powodu błędu hello: "Błąd System.InvalidOperationException właściwość poświadczenia i typ przetwarzania ``<some resource name>``: konwertowanie i przechowywanie zaszyfrowane hasło jako zwykły tekst jest dozwolone tylko wtedy, gdy PSDscAllowPlainTextPassword ustawiono tootrue."

**Przyczyną błędu hello:** zostały użyte poświadczenia w konfiguracji, ale nie dostarczył prawidłowego **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue dla każdego węzła Konfiguracja.  

**Porady dotyczące rozwiązywania problemów:**  

* Upewnij się, że toopass w odpowiednich hello **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue dla każdej wymienionej w konfiguracji hello konfiguracji węzła. Aby uzyskać więcej informacji, zobacz zbyt[zasoby w konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Następne kroki
Jeśli wykonano hello powyższe kroki rozwiązywania problemów i nie można odnaleźć hello odpowiedzi, możesz przejrzeć hello dodatkowe opcje pomocy technicznej poniżej.

* Uzyskaj pomoc od ekspertów platformy Azure. Przedstawia toohello Twojego problem [fora MSDN Azure lub przepełnienie stosu.](https://azure.microsoft.com/support/forums/).
* Plik zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witryny Microsoft Azure obsługuje](https://azure.microsoft.com/support/options/) i kliknij przycisk **uzyskać pomoc techniczną** w obszarze **technicznych i działem rozliczeń**.
* Opublikuj żądanie skryptu na [Centrum skryptów](https://azure.microsoft.com/documentation/scripts/) Jeśli szukasz rozwiązanie elementu runbook usługi Automatyzacja Azure lub modułu integracji.
* Opublikuj żądania opinii lub informacji o funkcji automatyzacji Azure na [User Voice](https://feedback.azure.com/forums/34192--general-feedback).
