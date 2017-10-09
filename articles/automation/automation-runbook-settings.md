---
title: Ustawienia aaaRunbook | Dokumentacja firmy Microsoft
description: "W tym artykule opisano hello ustawienia konfiguracji dla elementu runbook automatyzacji Azure i w jaki sposób toochange je za pomocą obu hello portalu zarządzania Azure i programu Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Ustawienia elementu Runbook
Każdy element runbook automatyzacji Azure ma wiele ustawień, które ułatwiają toobe zidentyfikowane i toochange jego zachowania podczas rejestrowania. Każde z tych ustawień opisano poniżej; dołączono przez procedury dotyczące toomodify je.

## <a name="settings"></a>Ustawienia
### <a name="name-and-description"></a>Nazwa i opis
Nie można zmienić nazwy hello elementu runbook, po jego utworzeniu. Hello opis jest opcjonalny i może być zapasowej too512 znaków.

### <a name="tags"></a>Tagi
Tagi dopuszczać możesz tooassign unikatowych słów i wyrażeń toohelp identyfikacji elementu runbook. Na przykład podczas przesyłania runbook toohello [galerii programu PowerShell](https://www.powershellgallery.com/), należy określić tooidentify tagi określonej kategorii hello runbook powinien być wyświetlany w. Można określić wiele znaczników elementu runbook, oddzielając je przecinkami.

### <a name="logging"></a>Rejestrowanie
Domyślnie rekordy pełne i postępu nie są zapisywane toojob historii. Ustawienia hello toolog określonego elementu runbook można zmienić tych rekordów. Aby uzyskać więcej informacji o tych rekordów, zobacz [Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Zmiana ustawień elementu runbook

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Zmiana ustawień elementu runbook z hello portalu Azure
Możesz zmienić ustawienia elementu runbook w portalu Azure hello w hello **ustawienia** bloku hello elementu runbook.

1. Hello portalu Azure, wybierz **automatyzacji** , a następnie kliknij nazwę hello konta automatyzacji.
2. Wybierz hello **elementów Runbook** kartę.
3. Kliknij nazwę hello elementu runbook i są bloku ustawienia ukierunkowanej toohello hello elementu runbook. W tym miejscu można określić lub zmodyfikować tagi, hello opis elementu runbook, konfigurowanie rejestrowania i ustawień śledzenia i dostęp do pomocy technicznej toohelp narzędzia do rozwiązywania problemów.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Zmiana ustawień elementu runbook przy użyciu programu Windows PowerShell
Można użyć hello [AzureRmAutomationRunbook zestaw](https://msdn.microsoft.com/library/mt603786.aspx) polecenia cmdlet toochange hello ustawienia elementu runbook. Jeśli chcesz toospecify wiele tagów można albo udostępnić tablica lub jeden ciąg parametr tagi toohello wartości rozdzielone przecinkami. Możesz uzyskać bieżące znaczniki hello z hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Witaj następujące przykładowe polecenia pokazują, jak tooset hello właściwości elementu runbook. W tym przykładzie dodaje trzy znaczniki istniejących toohello znaczniki i określa, że powinny być rejestrowane rekordów pełnych.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Następne kroki
* toolearn toocreate i pobrać dane wyjściowe i komunikaty o błędach z elementami runbook, zobacz temat [Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md) 
* toounderstand jak wyświetlić tooadd elementu runbook, który został już opracowany przez społeczność hello lub inne źródło lub toocreate własne runbook [Tworzenie lub importowanie elementu Runbook](automation-creating-importing-runbook.md) 

