---
title: aaaCreating lub importowanie elementu runbook automatyzacji Azure
description: "W tym artykule opisano sposób toocreate nowy element runbook w automatyzacji Azure lub jeden import z pliku."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Tworzenie lub importowanie elementu runbook automatyzacji Azure
Możesz dodać tooAzure elementu runbook automatyzacji przez [tworzenia nowej](#creating-a-new-runbook) lub importując istniejący element runbook z pliku lub hello [galerię elementów Runbook](automation-runbook-gallery.md). Ten artykuł zawiera informacje na temat tworzenia i importowania elementów runbook z pliku.  Można pobrać wszystkie szczegóły hello na uzyskiwanie dostępu do społeczności elementów runbook i modułów w [galerie elementów Runbook i modułów w automatyzacji Azure](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Tworzenie nowego elementu runbook
Możesz utworzyć nowy element runbook w automatyzacji Azure przy użyciu jednej z hello Azure portali lub środowiska Windows PowerShell. Po utworzeniu elementu runbook hello można edytować je przy użyciu informacji w [przepływu pracy programu PowerShell Learning](automation-powershell-workflow.md) i [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate nowy element runbook usługi Automatyzacja Azure z hello klasycznego portalu Azure
Może pracować tylko z [elementach runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) w hello portalu Azure.

1. W hello klasycznego portalu Azure kliknij przycisk, **nowy**, **usługi aplikacji**, **automatyzacji**, **Runbook**, **szybkie tworzenie**.
2. Wprowadź informacje wymagane hello, a następnie kliknij przycisk **Utwórz**. Nazwa elementu runbook Hello musi rozpoczynać się od litery i może zawierać litery, cyfry, podkreślenia i łączniki.
3. Tooedit hello runbook teraz, następnie kliknij przycisk **Edytuj element Runbook**. W przeciwnym razie kliknij przycisk **OK**.
4. Nowy element runbook będą wyświetlane na powitania **elementów Runbook** kartę.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate nowy element runbook usługi Automatyzacja Azure z hello portalu Azure
1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Z hello Centrum, wybierz **Runbook** tooopen hello listy elementów runbook.
3. Polecenie hello **Dodaj element runbook** przycisk, a następnie **Utwórz nowy element runbook**.
4. Wpisz **nazwa** hello elementu runbook i wybierz jego [typu](automation-runbook-types.md). Nazwa elementu runbook Hello musi rozpoczynać się od litery i może zawierać litery, cyfry, podkreślenia i łączniki.
5. Kliknij przycisk **Utwórz** toocreate hello elementu runbook i hello Otwórz Edytor.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate nowy element runbook usługi Automatyzacja Azure przy użyciu programu Windows PowerShell
Można użyć hello [AzureRmAutomationRunbook nowy](https://msdn.microsoft.com/library/mt619376.aspx) toocreate polecenia cmdlet pustą [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Można określić hello **nazwa** toocreate parametru pusty element runbook można później edytować, czy można określić hello **ścieżki** tooimport parametru plik elementu runbook. Witaj **typu** parametru również musi być uwzględniony toospecify, jeden z typów runbook hello czterech.

Hello następujące przykładowe polecenia Pokaż jak toocreate nowy pusty element runbook.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Importowanie elementu runbook z pliku do usługi Automatyzacja Azure
Nowy element runbook automatyzacji Azure można utworzyć, importując skrypt programu PowerShell lub przepływu pracy programu PowerShell (z rozszerzeniem .ps1) lub wyeksportowany graficzny element runbook (graphrunbook).  Należy określić hello [typu element runbook](automation-runbook-types.md) który zostanie utworzony na podstawie importu hello uwzględnieniu hello konta następujące zagadnienia.

* Plik graphrunbook można importować tylko do nowego [graficznym elementem runbook](automation-runbook-types.md#graphical-runbooks), i graficznych elementów runbook można tworzyć tylko z pliku graphrunbook.
* Plik .ps1 zawierającego przepływu pracy programu PowerShell można importować tylko do [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Witaj plik zawiera wiele przepływów pracy programu PowerShell, następnie hello import zakończy się niepowodzeniem. Należy zapisać plik własnych tooits każdego przepływu pracy i zaimportować każdy oddzielnie.
* Plik .ps1, który nie zawiera przepływu pracy mogą być importowane do albo [runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks) lub [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Jeśli jest importowany do elementu runbook przepływu pracy programu PowerShell, a następnie będzie on przekonwertowany tooa przepływu pracy i komentarze zostaną uwzględnione w runbook hello Określanie hello wprowadzonych zmian.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport elementu runbook z pliku za pomocą hello klasycznego portalu Azure
Możesz użyć powitania po tooimport procedury plik skryptu do automatyzacji Azure.  Należy pamiętać, że można importować tylko plik .ps1 do elementu runbook przepływu pracy programu PowerShell przy użyciu tego portalu.  W przypadku innych typów, należy użyć hello portalu Azure.

1. W portalu zarządzania Azure hello, wybierz **automatyzacji** , a następnie wybierz konto automatyzacji.
2. Kliknij przycisk **Importuj**.
3. Kliknij przycisk **Przeglądaj w poszukiwaniu pliku** i Znajdź tooimport pliku skryptu hello.
4. Tooedit hello runbook teraz, następnie kliknij przycisk **Edytuj element Runbook**. W przeciwnym razie kliknij przycisk OK.
5. Nowy element runbook Hello pojawią się na powitania **elementów Runbook** kartę hello konta automatyzacji.
6. Należy [publikowania elementu runbook hello](#publishing-a-runbook) przed jej uruchomieniem.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport elementu runbook z pliku za pomocą hello portalu Azure
Możesz użyć powitania po tooimport procedury plik skryptu do automatyzacji Azure.  

> [!NOTE]
> Należy pamiętać, że można importować tylko plik .ps1 do elementu runbook przepływu pracy programu PowerShell przy użyciu portalu hello.
> 
> 

1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Z hello Centrum, wybierz **Runbook** tooopen hello listy elementów runbook.
3. Polecenie hello **Dodaj element runbook** przycisk, a następnie **importu**.
4. Kliknij przycisk **pliku Runbook** tooselect hello pliku tooimport
5. Jeśli hello **nazwa** pole jest włączone, a następnie masz hello opcja toochange go.  Nazwa elementu runbook Hello musi rozpoczynać się od litery i może zawierać litery, cyfry, podkreślenia i łączniki.
6. Witaj [typ elementu runbook](automation-runbook-types.md) zostanie automatycznie wybrana, można jednak zmienić typ powitania po przejęciu hello ograniczenia mające zastosowanie do konta. 
7. Hello nowy element runbook będzie wyświetlana na liście hello elementów runbook dla hello konta automatyzacji.
8. Należy [publikowania elementu runbook hello](#publishing-a-runbook) przed jej uruchomieniem.

> [!NOTE]
> Po zaimportowaniu graficzny element runbook lub graficznym elementem runbook przepływu pracy programu PowerShell, masz hello opcja tooconvert toohello innego typu Jeśli. Nie można przekonwertować tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport elementu runbook z pliku skryptu za pomocą środowiska Windows PowerShell
Można użyć hello [AzureRMAutomationRunbook importu](https://msdn.microsoft.com/library/mt603735.aspx) tooimport polecenia cmdlet plik skryptu jako wersję roboczą elementu runbook przepływu pracy programu PowerShell. Jeśli istnieje już element runbook hello, importu hello zakończy się niepowodzeniem, jeśli nie używasz hello *-Force* parametru. 

Witaj następujące przykładowe polecenia pokazują, jak tooimport skryptu pliku do elementu runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Publikowanie elementu runbook
Podczas tworzenia lub zaimportować nowy element runbook należy opublikować przed jej uruchomieniem.  Każdy element runbook w automatyzacji ma wersję roboczą i opublikowaną wersję. Tylko wersję opublikowaną hello jest dostępne toobe uruchomić i tylko wersję roboczą hello można edytowane. Witaj wersję opublikowaną nie mają wpływu wersję roboczą toohello żadnych zmian. Gdy wersja robocza hello powinna zostać udostępniona, należy ją opublikować, która zastępuje hello wersję opublikowaną wersję roboczą hello.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish, a element runbook za pomocą hello klasycznego portalu Azure
1. Otwórz element runbook hello w hello klasycznego portalu Azure.
2. U góry hello hello ekranu, kliknij przycisk **autora**.
3. U dołu hello hello ekranu, kliknij przycisk **publikowania** , a następnie **tak** toohello komunikacie weryfikacyjnym.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish, a element runbook za pomocą hello portalu Azure
1. Otwórz element runbook hello w hello portalu Azure.
2. Kliknij przycisk hello **Edytuj** przycisku.
3. Kliknij przycisk hello **publikowania** przycisk, a następnie **tak** toohello wiadomości.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish elementu runbook za pomocą środowiska Windows PowerShell
Można użyć hello [AzureRmAutomationRunbook publikowania](https://msdn.microsoft.com/library/mt603705.aspx) toopublish polecenia cmdlet element runbook za pomocą środowiska Windows PowerShell. Hello następujące przykładowe polecenia Pokaż jak toopublish przykładowego elementu runbook.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Następne kroki
* toolearn o metody mogą korzystać z hello elementu Runbook i galerii modułu programu PowerShell, zobacz [galerie elementów Runbook i modułów w automatyzacji Azure](automation-runbook-gallery.md)
* Zobacz toolearn więcej informacji na temat edytowania elementów runbook programu PowerShell i przepływ pracy programu PowerShell w edytorze tekstową [edycji tekstową elementy runbook automatyzacji Azure](automation-edit-textual-runbook.md)
* toolearn więcej informacji na temat tworzenia graficznego elementu runbook, zobacz [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md)

