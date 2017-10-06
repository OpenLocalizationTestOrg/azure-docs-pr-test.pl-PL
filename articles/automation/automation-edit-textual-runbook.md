---
title: "aaaEditing tekstową elementy runbook automatyzacji Azure"
description: "Ten artykuł zawiera różne procedury dotyczące pracy z elementami runbook programu PowerShell i przepływ pracy programu PowerShell w automatyzacji Azure za pomocą edytora tekstową hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Edytowanie tekstową elementy runbook automatyzacji Azure
Witaj edytor tekstowy w automatyzacji Azure mogą być używane tooedit [elementy runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks) i [elementach runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). To ustawienie hello typowych funkcji innych edytory kodu, takie jak intellisense i kolor kodowanie dzięki funkcjom tooassist dodatkowe funkcje specjalne możesz podczas uzyskiwania dostępu do zasobów toorunbooks wspólnej.  Ten artykuł zawiera szczegółowy opis kroków do wykonywania różnych funkcji z tego edytora.

Edytor tekstowy Hello zawiera kod tooinsert funkcji działań, zasoby i podrzędnych elementów runbook do elementu runbook. Zamiast wpisywać kod hello samodzielnie, możesz wybrać z listy dostępnych zasobów i mają odpowiedni kod hello wstawione do elementu runbook hello.

Każdy element runbook automatyzacji Azure ma dwie wersje: roboczą i opublikowaną. Edytuj hello wersję roboczą elementu hello runbook, a następnie ją opublikować, tak aby można było wykonać. Nie można edytować Hello opublikowanej wersji. Zobacz [publikowanie elementu runbook](automation-creating-importing-runbook.md#publishing-a-runbook) Aby uzyskać więcej informacji.

toowork z [graficznych elementów Runbook](automation-runbook-types.md#graphical-runbooks), zobacz [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>Element runbook za pomocą portalu Azure hello tooedit
Użyj hello następujące procedury tooopen elementu runbook do edycji w hello edytor tekstowy.

1. W portalu Azure hello wybierz konto automatyzacji.
2. Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.
3. Kliknij nazwę hello elementu hello runbook mają tooedit a następnie kliknij przycisk hello **Edytuj** przycisku.
4. Wykonaj hello wymagane edycji.
5. Kliknij przycisk **zapisać** po zakończeniu edycji.
6. Kliknij przycisk **publikowania** Jeśli chcesz hello najnowszą wersję roboczą elementu toobe runbook hello opublikowane.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert polecenia cmdlet do elementu runbook
1. W hello kanwy hello edytor tekstowy umieść kursor hello gdzie tooplace hello cmdlet.
2. Rozwiń węzeł hello **poleceń cmdlet** węzła w hello formant biblioteki.
3. Rozwiń hello moduł zawierający hello polecenie cmdlet ma toouse.
4. Tooinsert polecenia cmdlet powitania kliknij prawym przyciskiem myszy i wybierz **dodać toocanvas**.  Jeśli polecenie cmdlet hello ma więcej niż jeden zestaw parametrów, hello domyślny zestaw zostanie dodany.  Można również rozwinąć hello polecenia cmdlet tooselect innym parametrem ustawić.
5. Kod powitania dla polecenia cmdlet hello jest wstawiany z jego całą listę parametrów.
6. Wpisz odpowiednią wartość w miejscu typu danych hello ujęte w nawiasy klamrowe <> dla wymaganych parametrów.  Usuń wszystkie parametry, które nie są potrzebne.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>Kod tooinsert dla podrzędnego elementu runbook do elementu runbook
1. W hello kanwy hello edytor tekstowy, umieść kursor hello miejscu tooplace hello kodu dla hello [podrzędnego elementu runbook](automation-child-runbooks.md).
2. Rozwiń węzeł hello **elementów Runbook** węzła w hello formant biblioteki.
3. Tooinsert runbook powitania kliknij prawym przyciskiem myszy i wybierz **dodać toocanvas**.
4. Kod Hello hello podrzędnego elementu runbook jest wstawiany z żadnych symboli zastępczych dla wszystkich parametrów elementu runbook.
5. Zastąp symbole zastępcze hello odpowiednie wartości dla każdego parametru.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert zasób do elementu runbook
1. W hello kanwy hello edytor tekstowy umieść kursor hello gdzie kodu hello tooplace hello podrzędnego elementu runbook.
2. Rozwiń węzeł hello **zasoby** węzła w hello formant biblioteki.
3. Rozwiń węzeł hello hello typu zawartości, który ma.
4. Tooinsert zasobów powitania kliknij prawym przyciskiem myszy i wybierz **dodać toocanvas**.  Dla [zasoby zmiennej](automation-variables.md), wybierz opcję **Dodaj "Pobierz zmienną" toocanvas** lub **dodać toocanvas "Ustaw zmienną"** w zależności od tego, czy mają tooget lub ustaw zmienną hello.
5. Kod Hello zasobów hello są wstawiane do hello elementu runbook.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>Element runbook za pomocą portalu Azure hello tooedit
Użyj hello następujące procedury tooopen elementu runbook do edycji w hello edytor tekstowy.

1. Hello portalu Azure, wybierz **automatyzacji** , a następnie kliknij nazwę hello konta automatyzacji.
2. Wybierz hello **elementów Runbook** kartę.
3. Kliknij nazwę hello elementu hello runbook tooedit a następnie wybrać hello **autora** kartę.
4. Kliknij przycisk hello **Edytuj** przycisk u dołu hello hello ekranu.
5. Wykonaj hello wymagane edycji.
6. Kliknij przycisk **zapisać** po zakończeniu edycji.
7. Kliknij przycisk **publikowania** Jeśli chcesz hello najnowszą wersję roboczą elementu toobe runbook hello opublikowane.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert działania do elementu Runbook
1. W hello kanwy hello edytor tekstowy umieść kursor hello gdzie tooplace hello działania.
2. U dołu hello hello ekranu, kliknij przycisk **Wstaw** , a następnie **działania**.
3. W hello **modułu integracji** kolumny, hello wybierz moduł, który zawiera hello działania.
4. W hello **działania** okienku, wybierz działanie.
5. W hello **opis** kolumny, opis hello Uwaga hello działania. Opcjonalnie możesz kliknąć wyświetlić szczegółowe toolaunch pomocy dla działania hello w przeglądarce hello.
6. Kliknij strzałkę w prawo hello.  Jeśli hello działanie ma parametry, zostaną wyświetlone w celu poinformowania użytkownika.
7. Kliknij przycisk wyboru hello.  Kod toorun hello działania zostanie wstawiony do hello elementu runbook.
8. Jeśli działanie hello wymaga parametrów, wpisz odpowiednią wartość w miejscu typu danych hello ujęte w nawiasy klamrowe <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>Kod tooinsert dla podrzędnego elementu runbook do elementu runbook
1. W hello kanwy hello edytor tekstowy, umieść kursor hello miejscu tooplace hello [podrzędnego elementu runbook](automation-child-runbooks.md).
2. U dołu hello hello ekranu, kliknij przycisk **Wstaw** , a następnie **Runbook**.
3. Zaznacz hello runbook tooinsert hello środkowej kolumnie i kliknij przycisk strzałki w prawo hello.
4. Jeśli hello runbook ma parametry, zostaną wyświetlone w celu poinformowania użytkownika.
5. Kliknij przycisk wyboru hello.  Kod toorun hello wybrane runbook zostanie wstawiony do bieżącego elementu runbook hello.
6. Jeśli hello runbook wymaga parametrów, wpisz odpowiednią wartość w miejscu typu danych hello ujęte w nawiasy klamrowe <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert zasób do elementu runbook
1. W hello kanwy hello edytor tekstowy umieść kursor hello gdzie tooplace hello działania tooretrieve hello zasobów.
2. U dołu hello hello ekranu, kliknij przycisk **Wstaw** , a następnie **ustawienie**.
3. W hello **ustawienie akcji** kolumny, hello wybierz akcję, która ma.
4. Wybierz z hello dostępnych zasobów w hello środkowej kolumnie.
5. Kliknij przycisk wyboru hello.  Kod tooget lub zestaw zasobów hello zostanie wstawiony do hello elementu runbook.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit runbook usługi Automatyzacja Azure przy użyciu programu Windows PowerShell
tooedit elementu runbook w programie Windows PowerShell możesz użyć dowolnego edytora hello i zapisać go tooa pliku .ps1. Można użyć hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) polecenia cmdlet tooretrieve hello zawartość elementu hello runbook, a następnie [AzureAutomationRunbookDefinition zestaw](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) istniejących hello tooreplace polecenia cmdlet Wersja robocza elementu runbook z hello zmodyfikować jeden.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve hello zawartość elementu Runbook przy użyciu Windows PowerShell
Witaj następujące przykładowe polecenia pokazują, jak tooretrieve hello skrypt dla elementu runbook i zapisać go w pliku skryptu tooa. W tym przykładzie jest pobierana wersja robocza hello. Jest również możliwe tooretrieve hello opublikowana wersja elementu hello runbook mimo że nie można zmienić tej wersji.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange hello zawartość elementu Runbook przy użyciu Windows PowerShell
Witaj następujące przykładowe polecenia pokazują, jak tooreplace hello istniejącą zawartość elementu runbook zawartością pliku skryptu hello. Należy pamiętać, że to jest hello samo przykładowe procedury jak w [tooimport elementu runbook z pliku skryptu za pomocą programu Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Pokrewne artykuły:
* [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)
* [Learning przepływu pracy programu PowerShell](automation-powershell-workflow.md)
* [Graficzny tworzenia w programie usługi Automatyzacja Azure](automation-graphical-authoring-intro.md)
* [Certyfikaty](automation-certificates.md)
* [Połączenia](automation-connections.md)
* [Poświadczenia](automation-credentials.md)
* [Harmonogramy](automation-schedules.md)
* [Zmienne](automation-variables.md)
