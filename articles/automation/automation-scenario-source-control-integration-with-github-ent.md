---
title: "Integracja kontroli źródła usługi Automatyzacja Azure z systemem GitHub Enterprise | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano szczegóły dotyczące sposobu konfigurowania integracji z systemem GitHub Enterprise dla kontroli źródła elementów runbook automatyzacji."
services: automation
documentationCenter: 
authors: georgewallace
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
ms.openlocfilehash: cf72c6d05e2872bea84b8a7218bd318d5b8c9694
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Scenariusz automatyzacji Azure - automatyzacji integracji kontroli źródła z systemem GitHub Enterprise

Automatyzacja obsługuje obecnie integracji kontroli źródła, dzięki czemu można skojarzyć elementów runbook do Twojego konta automatyzacji do repozytorium GitHub kontroli źródła.  Jednakże klienci, którzy wdrożyli [systemem GitHub Enterprise](https://enterprise.github.com/home) do obsługi swoje praktyki DevOps, również chcesz jej używać do zarządzania cyklem życia elementów runbook, które są opracowywane automatyzować procesy biznesowe i obsługę operacji zarządzania.  

W tym scenariuszu masz komputerem z systemem Windows w centrum danych skonfigurowany jako hybrydowy proces roboczy elementu Runbook z modułów usługi Azure Resource Manager i zainstalować narzędzia Git.  Maszynie hybrydowego procesu roboczego ma Sklonowanie lokalnego repozytorium Git.  Po uruchomieniu elementu runbook na hybrydowy proces roboczy jest zsynchronizowany katalog Git i zawartość pliku elementu runbook są importowane do konta automatyzacji.

W tym artykule opisano sposób konfigurowania tej konfiguracji w danym środowisku usługi Automatyzacja Azure. Rozpoczniemy konfigurując automatyzacji przy użyciu poświadczeń zabezpieczeń wymagane do obsługi tego scenariusza i wdrażania hybrydowego procesu roboczego elementu Runbook w centrum danych do uruchamiania elementów runbook i dostępu do repozytorium GitHub Enterprise, aby zsynchronizować elementów runbook za pomocą konta automatyzacji elementów runbook.  


## <a name="getting-the-scenario"></a>Uzyskiwanie scenariusza

W tym scenariuszu składa się z dwóch elementów runbook programu PowerShell, które można importować bezpośrednio z [galerię elementów Runbook](automation-runbook-gallery.md) w portalu Azure lub pobrać z [galerii programu PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Elementy Runbook

Element Runbook | Opis| 
--------|------------|
RunAsCertificateToHybridWorker eksportu | Element Runbook umożliwia wyeksportowanie RunAs certyfikatu z konta automatyzacji do hybrydowy proces roboczy, aby mógł uwierzytelnić elementów runbook w procesie roboczym, z platformy Azure, aby można było zaimportować elementy runbook do konta automatyzacji.| 
LocalGitFolderToAutomationAccount synchronizacji | Element Runbook synchronizuje folder lokalny Git na maszynie hybrydowych, a następnie zaimportować pliki runbook (*.ps1) do konta automatyzacji.|

### <a name="credentials"></a>Poświadczenia

Poświadczenie | Opis|
-----------|------------|
GitHRWCredential | Zasób poświadczeń, możesz utworzyć zawierać nazwę użytkownika i hasło dla użytkownika z uprawnieniami do hybrydowy proces roboczy.|

## <a name="installing-and-configuring-this-scenario"></a>Instalowanie i konfigurowanie scenariusza

### <a name="prerequisites"></a>Wymagania wstępne

1. Element runbook LocalGitFolderToAutomationAccount synchronizacji jest uwierzytelniany przy użyciu [konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md). 

2. Wymagany jest również obszaru roboczego programu Microsoft Operations Management Suite (OMS) z rozwiązaniem usługi Automatyzacja Azure, włączona i skonfigurowana.  Jeśli nie masz, który jest skojarzony z kontem automatyzacji używane do instalowania i konfigurowania tego scenariusza, jest tworzony i skonfigurowana za użytkownika podczas wykonywania **OnPremiseHybridWorker.ps1 nowy** skryptu z hybrydowy proces roboczy elementu runbook.        

    > [!NOTE]
    > Obecnie w następujących regionach obsługują tylko automatyzacji integracji z usługą OMS - **południowo-wschodnia Australia**, **wschodnie stany USA 2**, **Azja południowo-wschodnia**, i **Europa**. 

3. Komputer, który może służyć jako dedykowanych procesów roboczych Runbook hybrydowych, również hostującego oprogramowania GitHub i obsługa plików elementu runbook (*runbook*.ps1) w katalogu źródłowym, na synchronizowanie z serwisu GitHub i Twoje konto usługi Automatyzacja w systemie plików.

### <a name="import-and-publish-the-runbooks"></a>Importowanie i publikować elementy runbook

Aby zaimportować *RunAsCertificateToHybridWorker eksportu* i *LocalGitFolderToAutomationAccount synchronizacji* elementów runbook z galerii elementu Runbook z konta usługi Automatyzacja w portalu Azure, wykonaj procedury opisane w [importowanie elementu Runbook z galerii Runbook](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Elementy runbook należy opublikować po ich zostały pomyślnie zaimportowane do konta automatyzacji.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Wdrażanie i konfigurowanie hybrydowy proces roboczy elementu Runbook

Jeśli nie masz Runbook Worker hybrydowego już wdrożone w centrum danych, należy zapoznać się z wymaganiami i postępuj zgodnie z instrukcjami instalacji zautomatyzowanej przy użyciu procedury w [Azure automatyzacji hybrydowe procesy robocze elementu Runbook - automatyzacji instalacji i konfiguracji](automation-hybrid-runbook-worker.md#automated-deployment).  Po pomyślnym zainstalowaniu hybrydowy proces roboczy na komputerze, wykonaj następujące kroki, aby ukończyć jej Konfigurowanie tego scenariusza.

1. Zaloguj się komputerze, na którym rola hybrydowy proces roboczy elementu Runbook przy użyciu konta, które ma lokalne uprawnienia administracyjne i Utwórz katalog do przechowywania plików Git elementu runbook.  Klonowanie wewnętrzny repozytorium Git do katalogu.
2. Jeśli nie masz już konto Uruchom jako tworzone lub chcesz utworzyć nową jedną dedykowanego dla tego celu, w portalu Azure przejdź do konta automatyzacji, wybierz konto automatyzacji i utworzyć [zasób poświadczeń](automation-credentials.md) zawierający nazwę użytkownika i hasło dla użytkownika z uprawnieniami do hybrydowy proces roboczy.  
3. Z Twojego konta automatyzacji [edytować element runbook](automation-edit-textual-runbook.md)**RunAsCertificateToHybridWorker eksportu** i zmodyfikować wartość zmiennej *$Password* silnym hasłem.  Po zmodyfikowaniu wartość, kliknij przycisk **publikowania** ma wersję roboczą elementu runbook opublikowane. 
5. Uruchamiania elementu runbook **RunAsCertificateToHybridWorker eksportu**, a następnie w **Uruchom element Runbook** bloku, w obszarze opcji **parametrów uruchomieniowych** wybierz opcję **hybrydowy proces roboczy** i na liście rozwijanej wybierz utworzony wcześniej w tym scenariuszu grupy hybrydowych procesów roboczych.  

    Eksportuje ten certyfikat do hybrydowy proces roboczy, aby elementy runbook na proces roboczy może uwierzytelnić się przy użyciu platformy Azure przy użyciu połączenia Uruchom jako w celu zarządzania zasobami Azure (w szczególności w tym scenariuszu - import konta automatyzacji elementów runbook).

4. Wybierz wcześniej utworzoną grupę hybrydowych procesów roboczych z konta automatyzacji i [Określ konto Uruchom jako](automation-hrw-run-runbooks.md#runas-account) grupy hybrydowych procesów roboczych i wybranego zasobu poświadczeń tylko lub już został utworzony.  Gwarantuje to, że synchronizacja elementu runbook można uruchomić polecenia usługi Git. 
5. Uruchomić element runbook **LocalGitFolderToAutomationAccount synchronizacji**, podaj następujące wymagane wartości parametru wejściowego i w **Uruchom element Runbook** bloku, w obszarze opcji **parametrów uruchomieniowych** wybierz opcję **hybrydowy proces roboczy** i na liście rozwijanej wybierz utworzony wcześniej w tym scenariuszu grupy hybrydowych procesów roboczych:
    * *Grupa zasobów* — Nazwa grupy zasobów skojarzonych z Twoim kontem automatyzacji
    * *AutomationAccountName* — nazwa konta automatyzacji
    * *GitPath* — lokalny folder lub plik na hybrydowy proces roboczy elementu Runbook, gdzie Git jest skonfigurowany do pobierania najnowszych zmian

    To spowoduje synchronizowanie folderu Git lokalnego na komputerze hybrydowego procesu roboczego i następnie importowanie tych plików .ps1 w katalogu źródłowym na koncie automatyzacji.

    ![Uruchom synchronizację LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Wyświetl szczegóły podsumowania zadania dla elementu runbook, wybierając ją z **elementów Runbook** bloku w konta automatyzacji, a następnie wybierz **zadania** kafelka.  Upewnij się, zakończyła się pomyślnie, wybierając **wszystkie dzienniki** kafelków i przeglądanie strumienia szczegółowy dziennik.  

## <a name="next-steps"></a>Następne kroki

-  Aby dowiedzieć się więcej na temat typów elementów Runbook, ich zalet i ograniczeń, zobacz [Azure Automation runbook types](automation-runbook-types.md) (Typy elementów Runbook usługi Azure Automation).
-  Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Obsługa natywnych skryptów programu PowerShell w usłudze Azure Automation).
