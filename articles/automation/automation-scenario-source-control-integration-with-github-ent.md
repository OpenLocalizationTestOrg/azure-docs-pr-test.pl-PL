---
title: "aaaAzure automatyzacji integracji kontroli źródła z systemem GitHub Enterprise | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello szczegóły dotyczące tooconfigure integracji z systemem GitHub Enterprise do kontroli źródła elementów runbook automatyzacji."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Scenariusz automatyzacji Azure - automatyzacji integracji kontroli źródła z systemem GitHub Enterprise

Automatyzacja obsługuje obecnie integracji kontroli źródła, co pozwala elementów runbook tooassociate w Twoim automatyzacji konta tooa GitHub repozytorium kontroli źródła.  Jednak klientów, którzy wdrożyli [GitHub Enterprise](https://enterprise.github.com/home) praktyk ich DevOps toosupport, również mają toouse jej cyklu życia hello toomanage elementów runbook, które są rozwinięte tooautomate procesy biznesowe i zarządzania usługami operacje.  

W tym scenariuszu masz komputerem z systemem Windows w centrum danych skonfigurowany jako hybrydowy proces roboczy elementu Runbook z modułów usługi Azure Resource Manager hello i zainstalować narzędzia Git.  Hello hybrydowego procesu roboczego maszyna ma Sklonowanie hello lokalnego repozytorium Git.  Po uruchomieniu na powitania hybrydowy proces roboczy hello runbook katalog Git hello jest zsynchronizowany i zawartość pliku hello elementu runbook są importowane do hello konta automatyzacji.

W tym artykule opisano sposób tooset tej konfiguracji w danym środowisku usługi Automatyzacja Azure. Rozpoczniemy konfigurując automatyzacji przy użyciu poświadczeń zabezpieczeń hello toosupport wymagane elementy runbook, w tym scenariuszu i wdrożenia hybrydowy proces roboczy elementu Runbook w Twoich danych Centrum elementów runbook hello toorun i dostęp do Twojego toosynchronize repozytorium GitHub Enterprise elementy runbook za pomocą konta automatyzacji.  


## <a name="getting-hello-scenario"></a>Pobieranie hello scenariusza

W tym scenariuszu składa się z dwóch elementów runbook programu PowerShell, które można importować bezpośrednio z hello [galerię elementów Runbook](automation-runbook-gallery.md) w portalu Azure hello lub pobrać z hello [galerii programu PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Elementy Runbook

Element Runbook | Opis| 
--------|------------|
RunAsCertificateToHybridWorker eksportu | Element Runbook eksportuje certyfikatu RunAs z automatyzacji konta tooa hybrydowy proces roboczy, aby elementy runbook na powitania proces roboczy mógł uwierzytelnić przy użyciu platformy Azure w elementach runbook tooimport kolejności do hello konta automatyzacji.| 
LocalGitFolderToAutomationAccount synchronizacji | Synchronizacje Runbook hello lokalnego folderu Git na powitania hybrydowego maszyny, a następnie zaimportuj hello plików elementu runbook (*.ps1) do hello konta automatyzacji.|

### <a name="credentials"></a>Poświadczenia

Poświadczenie | Opis|
-----------|------------|
GitHRWCredential | Zasób poświadczeń tworzenia toocontain hello w nazwę użytkownika i hasło dla użytkownika z uprawnienia toohello hybrydowy proces roboczy.|

## <a name="installing-and-configuring-this-scenario"></a>Instalowanie i konfigurowanie scenariusza

### <a name="prerequisites"></a>Wymagania wstępne

1. Element runbook Hello LocalGitFolderToAutomationAccount synchronizacji jest uwierzytelniany przy użyciu hello [konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md). 

2. Wymagany jest również obszaru roboczego programu Microsoft Operations Management Suite (OMS) z hello rozwiązania Automatyzacja Azure, włączona i skonfigurowana.  Jeśli nie masz, który jest skojarzony z tooinstall używane konto automatyzacji hello i skonfiguruj ten scenariusz, jest tworzony i skonfigurowana za użytkownika podczas wykonywania hello **OnPremiseHybridWorker.ps1 nowy** skryptu z hello hybrydowego proces roboczy elementu runbook.        

    > [!NOTE]
    > Obecnie hello następujących regionach obsługują tylko automatyzacji integracji z usługą OMS - **południowo-wschodnia Australia**, **wschodnie stany USA 2**, **Azja południowo-wschodnia**, i **zachodnie Europa**. 

3. Komputer, który może służyć jako dedykowanych procesów roboczych Runbook hybrydowych, również hostującego hello GitHub oprogramowania i obsługa plików runbook hello (*runbook*.ps1) w katalogu źródłowego na powitania pliku system toosynchronize między GitHub i Konto automatyzacji.

### <a name="import-and-publish-hello-runbooks"></a>Importowanie i publikować elementy runbook hello

Witaj tooimport *RunAsCertificateToHybridWorker eksportu* i *LocalGitFolderToAutomationAccount synchronizacji* elementów runbook z hello galerię elementów Runbook z konta usługi Automatyzacja w hello portalu Azure Postępuj zgodnie z procedurami hello w [Runbook importu z hello galerię elementów Runbook](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Publikowanie elementów runbook hello po ich zostały pomyślnie zaimportowane do konta automatyzacji.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Wdrażanie i konfigurowanie hybrydowy proces roboczy elementu Runbook

Jeśli nie masz Runbook Worker hybrydowego już wdrożone w centrum danych, należy zapoznać się z wymaganiami hello i wykonaj kroki instalacji zautomatyzowanej hello przy użyciu procedury hello w [Azure automatyzacji hybrydowe procesy robocze elementu Runbook - automatyzacji instalacji i Konfiguracja](automation-hybrid-runbook-worker.md#automated-deployment).  Po pomyślnym zainstalowaniu hello hybrydowy proces roboczy na komputerze, należy wykonać hello następujące kroki toocomplete toosupport jej konfiguracji w tym scenariuszu.

1. Zaloguj się na toohello hostingu hello hybrydowy proces roboczy elementu Runbook roli komputera przy użyciu konta, które ma lokalne uprawnienia administracyjne i Utwórz toohold hello Git runbook plików z katalogu.  Klonowanie katalogu toohello repozytorium Git hello wewnętrznego.
2. Jeśli nie masz już konto Uruchom jako tworzone lub mają toocreate nowy przeznaczony do tego celu, z hello portalu Azure Przejdź tooAutomation kont, wybierz konto automatyzacji i utworzyć [zasób poświadczeń](automation-credentials.md) który zawiera nazwę hello użytkownika i hasło dla użytkownika z uprawnienia toohello hybrydowy proces roboczy.  
3. Z Twojego konta automatyzacji [edytować hello runbook](automation-edit-textual-runbook.md)**RunAsCertificateToHybridWorker eksportu** i zmodyfikować hello wartości dla zmiennej hello *$Password* z silne hasło.    Po zmodyfikowaniu wartość powitania kliknij **publikowania** toohave hello wersję roboczą elementu runbook hello opublikowane. 
5. Uruchom element runbook hello **RunAsCertificateToHybridWorker eksportu**w hello **Uruchom element Runbook** bloku, w obszarze opcji hello **parametrów uruchomieniowych** opcję hello **Hybrydowy proces roboczy** w hello listy rozwijanej wybierz hello grupy hybrydowych procesów roboczych utworzony wcześniej w tym scenariuszu.  

    Eksportuje toohello certyfikatu hybrydowy proces roboczy, tak aby elementy runbook na proces roboczy hello mogą uwierzytelniać za pomocą platformy Azure przy użyciu hello Uruchom jako połączenia w kolejności toomanage zasobów platformy Azure (w szczególności w tym scenariuszu - importowania elementów runbook toohello konto automatyzacji).

4. Z Twojego konta automatyzacji wybierz hello utworzone wcześniej grupy hybrydowych procesów roboczych i [Określ konto Uruchom jako](automation-hrw-run-runbooks.md#runas-account) grupy hello hybrydowych procesów roboczych i zasób poświadczeń hello wybrać tylko lub już został utworzony.  To zapewnia, że ten element runbook synchronizacji hello można uruchomić polecenia usługi Git. 
5. Uruchom element runbook hello **LocalGitFolderToAutomationAccount synchronizacji**, podaj hello następujących wymaganych wartości parametru wejściowego w hello **Uruchom element Runbook** bloku, w obszarze opcji hello **Uruchom ustawienia** opcję hello **hybrydowy proces roboczy** w hello listy rozwijanej wybierz hello grupy hybrydowych procesów roboczych utworzony wcześniej w tym scenariuszu:
    * *Grupa zasobów* — Witaj Nazwa grupy zasobów skojarzonych z Twoim kontem automatyzacji
    * *AutomationAccountName* — Witaj nazwa konta automatyzacji
    * *GitPath* — Witaj lokalnego folderu lub pliku na powitania hybrydowy proces roboczy elementu Runbook gdzie Git jest skonfigurowany toopull najnowsze zmiany w

    To spowoduje synchronizowanie folderu lokalnego Git hello na powitania hybrydowego procesu roboczego komputera, a następnie zaimportowanie plików .ps1 hello z toohello katalogu źródłowego hello konta automatyzacji.

    ![Uruchom synchronizację LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Wyświetl szczegóły podsumowania zadania dla elementu runbook hello, wybierając ją z hello **elementów Runbook** bloku w konta automatyzacji, a następnie wybierz opcję hello **zadania** kafelka.  Upewnij się, zakończyła się pomyślnie, wybierając hello **wszystkie dzienniki** kafelków i recenzowania hello szczegółowy dziennik strumienia.  

## <a name="next-steps"></a>Następne kroki

-  Zobacz tooknow więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)
-  Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz artykuł [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Obsługa natywnych skryptów programu PowerShell w usłudze Azure Automation).
