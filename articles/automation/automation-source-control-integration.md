---
title: "aaaSource integracji kontroli usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano integracji kontroli źródła z usługi GitHub automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Integracja kontroli źródła w usłudze Automatyzacja Azure
Integracja kontroli źródła umożliwia elementów runbook tooassociate w Twoim automatyzacji konta tooa GitHub repozytorium kontroli źródła. Kontrola źródła umożliwia tooeasily współpracować z zespołem, śledzenie zmian i przywracać wersje tooearlier elementów runbook. Umożliwia na przykład kontroli źródła należy toosync różnych gałęziach w kontroli źródła tooyour rozwoju, testowym lub produkcyjnym kont automatyzacji, dzięki czemu można łatwo toopromote kod, który był testowany w środowisku produkcyjnym tooyour programowanie automatyzacji konto.

Kontrola źródła pozwala toopush kodu z kontrolą toosource usługi Automatyzacja Azure lub ściągnąć elementy runbook z tooAzure kontroli źródła automatyzacji. W tym artykule opisano, jak kontrolować tooset źródła w środowisku usługi Automatyzacja Azure. Firma Microsoft uruchomi przez skonfigurowanie usługi Automatyzacja Azure tooaccess repozytorium GitHub i przeprowadzenie różne operacje, które można wykonać za pomocą integracji kontroli źródła. 

> [!NOTE]
> Kontrola źródła obsługuje ściąganie i wypychanie [elementach runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) oraz [elementy runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks). [Graficznych elementów runbook](automation-runbook-types.md#graphical-runbooks) nie są jeszcze obsługiwane.<br><br>
> 
> 

Istnieją dwa kontroli źródła wymagane tooconfigure prostych krokach dla Twojego konta automatyzacji i tylko jeden Jeśli masz już konto usługi GitHub. Są to:

## <a name="step-1--create-a-github-repository"></a>Krok 1: Tworzenie repozytorium GitHub
Jeśli masz już konto GitHub i repozytorium, który ma tooAzure toolink automatyzacji, a następnie istniejących tooyour logowania konta i uruchomić z kroku 2 poniżej. W przeciwnym razie przejdź zbyt[GitHub](https://github.com/), załóż nowe konto i [utworzyć nowe repozytorium](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Krok 2 — Konfiguracja systemu kontroli źródła w usłudze Automatyzacja Azure
1. W bloku konta usługi Automatyzacja hello w hello portalu Azure, kliknij przycisk **ustawić kontroli źródła.** 
   
    ![Konfigurowanie kontroli źródła](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Witaj **kontroli źródła** zostanie otwarty blok, którego można skonfigurować szczegółowe informacje o koncie usługi GitHub. Poniżej znajduje się lista hello tooconfigure parametry:  
   
   | **Parametr** | **Opis** |
   |:--- |:--- |
   | Wybierz źródło |Wybierz źródło hello. Obecnie tylko **GitHub** jest obsługiwana. |
   | Autoryzacja |Kliknij przycisk hello **autoryzacji** repozytorium GitHub tooyour dostępu przycisk toogrant automatyzacji Azure. Jeśli jest już zalogowany tooyour konto GitHub w innym oknie, hello są używane poświadczenia tego konta. Po autoryzacji zakończy się pomyślnie, bloku hello zostaną wyświetlone w obszarze nazwy użytkownika usługi GitHub **właściwości autoryzacji**. |
   | Wybierz repozytorium |Wybierz repozytorium GitHub z listy hello dostępne repozytoriów. |
   | Wybierz gałąź |Wybierz gałąź z listy hello gałęzie dostępne. Tylko hello **wzorca** gałęzi jest wyświetlany, jeśli nie utworzono żadnych gałęziach. |
   | Ścieżka folderu Runbook |Ścieżka folderu runbook Hello Określa ścieżkę hello w repozytorium GitHub hello, z którego mają toopush lub pobierania kodu. Należy podać w formacie hello **/nazwa folderu/nazwa podfolderu**. Tylko elementy runbook w ścieżce folderu elementów runbook hello zostaną zsynchronizowane tooyour konta automatyzacji. Elementy Runbook w podfolderach hello ścieżce folderu elementów runbook hello będzie **nie** zsynchronizowane. Użyj  **/**  toosync hello wszystkich elementów runbook w obszarze hello repozytorium. |
3. Na przykład, jeśli masz repozytorium o nazwie **PowerShellScripts** zawiera folder o nazwie **RootFolder**, który zawiera folder o nazwie **podfolder**. Program hello następujące ciągi toosync na poziomie każdego folderu:
   
   1. elementy runbook toosync z **repozytorium**, ścieżka folderu runbook*/*
   2. elementy runbook toosync z **RootFolder**, jest na ścieżce folderu elementów runbook */RootFolder*
   3. elementy runbook toosync z **podfolder**, jest na ścieżce folderu elementów runbook */RootFolder/podfolder*.
4. Po skonfigurowaniu hello parametry są wyświetlane na powitania **bloku ustawić kontroli źródła.**  
   
    ![Skonfiguruj bloku](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Po kliknięciu przycisku OK integracji kontroli źródła została skonfigurowana pod kątem Twoje konto usługi Automatyzacja i powinien zostać zaktualizowany z informacjami w witrynie GitHub. Możesz teraz kliknąć w tej części tooview wszystkie do kontroli źródła synchronizacji historii zadań.  
   
    ![Wartości repozytorium](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Po skonfigurowaniu kontroli źródła hello następujące automatyzacji zasoby zostaną utworzone na Twoim koncie automatyzacji:  
   Dwa [zasoby zmiennej](automation-variables.md) są tworzone.  
   
   * Zmienna Hello **Microsoft.Azure.Automation.SourceControl.Connection** zawiera wartości hello hello parametrów połączenia, jak pokazano poniżej.  
     
     | **Parametr** | **Wartość** |
     |:--- |:--- |
     | Nazwa |Microsoft.Azure.Automation.SourceControl.Connection |
     | Typ |Ciąg |
     | Wartość |{"Gałęzi":\<*nazwę gałęzi*>, "RunbookFolderPath":\<*ścieżce folderu elementów Runbook*>, "Typ dostawcy":\<*ma wartość 1 GitHub*>, "Repository":\<*nazwę repozytorium*>, "Nazwa_użytkownika":\<*GitHub Twoja nazwa użytkownika*>} |

    * Zmienna Hello **Microsoft.Azure.Automation.SourceControl.OAuthToken**, zawiera hello bezpiecznego zaszyfrowaną wartość OAuthToken Twojego.  

    |**Parametr**            |**Wartość** |
    |:---|:---|
    | Nazwa  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Typ | Unknown(Encrypted) |
    | Wartość | <*Zaszyfrowane OAuthToken*> |  

    ![Zmienne](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Kontrola źródła automatyzacji** jest dodawana jako tooyour autoryzowanych aplikacji konto GitHub. Aplikacja hello tooview: ze strony głównej GitHub Przejdź tooyour **profilu** > **ustawienia** > **aplikacji**. Ta aplikacja umożliwia toosync usługi Automatyzacja Azure z tooan repozytorium GitHub konta automatyzacji.  

    ![Git aplikacji](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Za pomocą kontroli źródła w automatyzacji
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Zaewidencjonowanie elementu runbook z formantu toosource usługi Automatyzacja Azure
Zaewidencjonowanie elementu Runbook pozwala toopush hello zmiany tooa runbook automatyzacji Azure w Twoim repozytorium kontroli źródła. Poniżej przedstawiono kroki hello toocheck w elemencie runbook:

1. Z Twojego konta automatyzacji [Utwórz nowy element runbook tekstową](automation-first-runbook-textual.md), lub [Edytuj istniejący, tekstowy element runbook](automation-edit-textual-runbook.md). Ten element runbook może być przepływu pracy programu PowerShell lub runbook skrypt programu PowerShell.  
2. Po przeprowadzeniu edycji elementu runbook, zapisać go i kliknij przycisk **zaewidencjonowania** z hello **Edytuj** bloku.  
   
    ![Przycisk zaewidencjonowania](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Zaewidencjonuj usługi Automatyzacja Azure spowoduje zastąpienie hello kod, który już istnieje w kontroli źródła. jest Hello instrukcji odpowiednik wiersza polecenia Git toocheck w **git Dodaj + zatwierdzenia git + git push**  

1. Po kliknięciu **zaewidencjonowania**, zostanie wyświetlony monit z potwierdzeniem, kliknij przycisk Tak toocontinue.  
   
    ![Komunikat zaewidencjonowania](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Zaewidencjonuj uruchamia hello runbook kontroli źródła: **MicrosoftAzureAutomationAccountToGitHubV1 synchronizacji**. Ten element runbook łączy tooGitHub i wypchnięcia zmiany z repozytorium tooyour automatyzacji Azure. Witaj tooview zaewidencjonowania Historia zadania, przejdź wstecz toohello **integracji kontroli źródła** i kliknij polecenie tooopen hello synchronizacji repozytorium bloku. Blok ten zawiera wszystkich zadań kontroli źródła.  Wybierz zadanie hello tooview i kliknij tooview hello szczegóły.  
   
    ![Zaewidencjonowanie elementu Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Elementy runbook kontroli źródła są specjalne elementy runbook automatyzacji, który nie można wyświetlić ani edytować. Podczas ich nie zostaną wyświetlone na liście elementów runbook, zobaczysz zadania synchronizacji pojawia się na liście zadań.
   > 
   > 
3. Nazwa Hello elementu runbook hello zmodyfikowane są wysyłane jako parametr wejściowy toohello ewidencjonowania elementu runbook. Możesz [wyświetlania szczegółów zadania hello](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) rozwijając elementu runbook w **synchronizacji repozytorium** bloku.  
   
    ![Dane wejściowe zaewidencjonowania](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Po zakończeniu zadania hello tooview hello zmiany, należy odświeżyć repozytorium GitHub.  Powinien być zatwierdzenia w repozytorium z następującym komunikatem zatwierdzania: **zaktualizowane *nazwy elementu Runbook* automatyzacji Azure.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Synchronizacja elementów runbook tooAzure kontroli źródła automatyzacji
przycisk synchronizacji Hello w bloku synchronizacji repozytorium hello umożliwia toopull hello wszystkie elementy runbook w ścieżce folderu elementów runbook hello z tooyour Twojego repozytorium konta automatyzacji. Witaj tego samego repozytorium może być zsynchronizowane toomore niż jedno konto automatyzacji. Poniżej przedstawiono hello kroki toosync elementu runbook:

1. Z hello konta automatyzacji skonfigurowanie kontroli źródła, otwórz hello **bloku synchronizacji integracji/repozytorium kontroli źródła** i kliknij przycisk **synchronizacji** , a następnie zostanie wyświetlony monit o potwierdzenie Kliknij przycisk **tak** toocontinue.  
   
    ![Przycisk synchronizacji](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Synchronizacja rozpoczyna się hello runbook: **MicrosoftAzureAutomationAccountFromGitHubV1 synchronizacji**. Ten element runbook łączy tooGitHub i pobiera zmiany hello z tooAzure Twojego repozytorium automatyzacji. Powinny pojawić się nowe zadanie na powitania **synchronizacji repozytorium** bloku dla tej akcji. tooview szczegóły zadania synchronizacji hello, kliknij przycisk tooopen hello zadania szczegóły blok.  
   
    ![Synchronizacja elementu Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Synchronizacja z kontroli źródła zastępuje wersję roboczą hello hello elementów runbook, który obecnie istnieje na koncie automatyzacji dla **wszystkie** elementy runbook, które są obecnie w kontroli źródła. Witaj Git toosync instrukcji odpowiednik wiersza polecenia jest **ściągnięcia programu git**


## <a name="troubleshooting-source-control-problems"></a>Rozwiązywanie problemów z kontroli źródła
Jeśli wystąpią jakieś błędy z zadaniem ewidencjonowania lub synchronizacji, powinny być zawieszone, stan zadania hello i można wyświetlić więcej szczegółów na temat błędu hello w bloku zadania hello.  Witaj **wszystkie dzienniki** opisano części wszystkie hello PowerShell strumienie skojarzone z tym zadaniem. Pozwoli to zapewnić, że ze szczegółami hello potrzebne toohelp Rozwiąż wszelkie problemy z zaewidencjonowania lub synchronizacji. Zostanie również wyświetlona hello sekwencję akcji, które wystąpiły podczas synchronizowania lub sprawdzanie — w elemencie runbook.  

![Obraz AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Rozłączanie kontroli źródła
toodisconnect z Twoim kontem usługi GitHub, otwórz blok synchronizacji repozytorium hello i kliknij polecenie **rozłączenia**. Po odłączeniu kontroli źródła na Twoim koncie automatyzacji elementów runbook, które zostały wcześniej synchronizowany pozostaje, ale hello bloku repozytorium synchronizacji nie zostaną włączone.  

  ![Przycisk Rozłącz](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat integracji kontroli źródła zobacz następujące zasoby hello:  

* [Automatyzacja Azure: Integracji kontroli źródła w usłudze Automatyzacja Azure](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Głos systemu kontroli źródła ulubionych](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Automatyzacja Azure: Integracja kontroli źródła elementu Runbook za pomocą programu Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

