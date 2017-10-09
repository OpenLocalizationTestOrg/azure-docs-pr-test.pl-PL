---
title: Element runbook automatyzacji Azure aaaStarting | Dokumentacja firmy Microsoft
description: "Zawiera podsumowanie hello różnych metod, które mogą być używane toostart elementu runbook automatyzacji Azure i zawiera szczegółowe informacje o wykorzystaniu zarówno hello portalu Azure i programu Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Uruchamianie elementu runbook automatyzacji Azure
w poniższej tabeli Hello pomoże określić hello metody toostart elementu runbook w automatyzacji Azure, która jest najbardziej odpowiedniego tooyour danego scenariusza. Ten artykuł zawiera szczegółowe informacje dotyczące uruchamiania elementu runbook z hello portalu Azure i programu Windows PowerShell. Szczegółowe informacje na powitania innych metod znajdują się w dokumentacji, która są dostępne poniższe linki hello.

| **— METODA** | **WŁAŚCIWOŚCI** |
| --- | --- |
| [Azure Portal](#starting-a-runbook-with-the-azure-portal) |<li>Najprostsza metoda o interakcyjny interfejs użytkownika.<br> <li>Wartości parametru proste tooprovide formularza.<br> <li>Łatwo śledzić stan zadania.<br> <li>Dostęp uwierzytelniony dzięki funkcji logowania do platformy Azure. |
| [Środowisko Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Wywoływanie z wiersza polecenia za pomocą poleceń cmdlet programu Windows PowerShell.<br> <li>Można dołączyć do automatycznego rozwiązania z wielu kroków.<br> <li>Uwierzytelniania żądań certyfikatów lub użytkownika OAuth główna / service podmiotu zabezpieczeń.<br> <li>Podaj wartości parametrów proste i złożone.<br> <li>Śledź stan zadania.<br> <li>Wymagany klient toosupport poleceń cmdlet programu PowerShell. |
| [Interfejs API usługi Automatyzacja Azure](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>Metoda najbardziej elastycznego, ale również większość złożone.<br> <li>Wywoływanie z kodu niestandardowego, który może zgłaszać żądania HTTP.<br> <li>Żądanie uwierzytelniony przy użyciu certyfikatu lub użytkownika Oauth główna / service podmiotu zabezpieczeń.<br> <li>Podaj wartości parametrów proste i złożone.<br> <li>Śledź stan zadania. |
| [Elementów Webhook](automation-webhooks.md) |<li>Uruchom element runbook z pojedynczego żądania HTTP.<br> <li>Uwierzytelniani tokenu zabezpieczającego w adresie URL.<br> <li>Klient nie może zastąpić wartości parametrów podczas tworzenia elementu webhook. Element Runbook może definiować jeden parametr, który jest wypełniana szczegółów żądania HTTP hello.<br> <li>Nie możliwości tootrack stan zadania za pomocą adresu URL elementu webhook. |
| [Odpowiedź tooAzure alertu](../log-analytics/log-analytics-alerts.md) |<li>Uruchom element runbook w odpowiedzi tooAzure alertu.<br> <li>Konfigurowanie elementu webhook dla elementu runbook, a następnie połącz tooalert.<br> <li>Uwierzytelniani tokenu zabezpieczającego w adresie URL. |
| [Harmonogram](automation-schedules.md) |<li>Automatyczne uruchamianie elementu runbook z harmonogramem co godzinę, codziennie, co tydzień lub co miesiąc.<br> <li>Manipulowanie harmonogramu za pośrednictwem portalu Azure, poleceń cmdlet programu PowerShell lub interfejsu API Azure.<br> <li>Podaj parametr wartości toobe używane z harmonogramem. |
| [Z innego elementu Runbook](automation-child-runbooks.md) |<li>Użyj elementu runbook jako działanie w innego elementu runbook.<br> <li>Przydatne w przypadku funkcji używany przez wiele elementów runbook.<br> <li>Podaj parametr wartości toochild runbook i korzystanie z danych wyjściowych w nadrzędny element runbook. |

Witaj poniższym obrazie przedstawiono krok po kroku proces szczegółowy w cyklu życia hello elementu runbook. Zawiera różne sposoby uruchamiania elementu runbook w automatyzacji Azure składniki wymagane do elementu runbook usługi Automatyzacja Azure tooexecute hybrydowy proces roboczy elementu Runbook i ich interakcje między poszczególnymi składnikami. toolearn dotyczące wykonywania elementu runbook usługi Automatyzacja w centrum danych, można znaleźć zbyt[hybrydowych procesów roboczych elementu runbook](automation-hybrid-runbook-worker.md)

![Architektura elementu Runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Uruchamianie elementu runbook z hello portalu Azure
1. Hello portalu Azure, wybierz **automatyzacji** , a następnie kliknij nazwę hello konta automatyzacji.
2. W menu Centrum hello wybierz **elementów Runbook**.
3. Na powitania **Runbook** bloku, wybrać element runbook, a następnie kliknij przycisk **Start**.
4. Jeśli hello runbook ma parametry, będzie tooprovide zostanie wyświetlony monit o wartości z polem tekstowym dla każdego parametru. Zobacz [parametrów elementu Runbook](#Runbook-parameters) poniżej zawiera bardziej szczegółowe informacje o parametrach.
5. Na powitania **zadania** bloku można wyświetlić stan hello hello zadania elementu runbook.

## <a name="starting-a-runbook-with-windows-powershell"></a>Uruchamianie elementu runbook przy użyciu programu Windows PowerShell
Można użyć hello [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart element runbook za pomocą środowiska Windows PowerShell. Witaj następujący przykładowy kod uruchamia element runbook o nazwie Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Zwraca AzureRmAutomationRunbook rozpoczęcia zadania obiektów, których można używać tootrack jego stan po uruchomieniu elementu runbook hello. Następnie można użyć z tym obiektem zadania [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello stan zadania hello i [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget dane wyjściowe. powitania po przykładowy kod uruchamia element runbook o nazwie Test-Runbook, czeka, dopóki nie zostało ukończone, a następnie wyświetla dane wyjściowe.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Jeśli hello element runbook wymaga parametrów, a następnie należy podać je jako [hashtable](http://technet.microsoft.com/library/hh847780.aspx) Jeśli klucz hello hello hashtable odpowiada hello nazwy parametru i wartości hello jest wartość parametru hello. Witaj poniższy przykład przedstawia sposób toostart elementu runbook z dwoma parametrami będącymi ciągami o nazwie FirstName i LastName, liczbą całkowitą o nazwie RepeatCount i parametrem logicznym o nazwie Show. Aby uzyskać dodatkowe informacje na temat parametrów, zobacz [parametrów elementu Runbook](#Runbook-parameters) poniżej.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Parametry elementu Runbook
Po uruchomieniu elementu runbook z hello portalu Azure lub programu Windows PowerShell hello instrukcja jest wysyłana za pośrednictwem hello usługi sieci web automatyzacji Azure. Ta usługa nie obsługuje parametrów o złożonych typach danych. Jeśli potrzebujesz tooprovide wartość parametru złożonego, a następnie użytkownik musi wywołać go z wnętrza innego elementu runbook zgodnie z opisem w [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md).

specjalne funkcje dotyczące parametrów używających określonych typów danych, zgodnie z opisem w hello następujące sekcje zawierają Hello usługi sieci web usługi Automatyzacja Azure.

### <a name="named-values"></a>Nazwane wartości
Jeśli hello parametr ma typ danych [object], wówczas można użyć powitania po jego listę nazwanych wartości toosend formatu JSON: *{Nazwa1: 'Wartość1', Nazwa2: 'Wartość2', nazwa3: "Wartość3"}*. Te wartości muszą być typu prostego. Hello element runbook zostanie wyświetlony parametr hello jako [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) z właściwościami, które odpowiadają tooeach o nazwie wartość.

Należy wziąć pod uwagę hello następującego testu elementu runbook, który akceptuje parametr o nazwie użytkownika.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Witaj następujący tekst może zostać użyty dla parametru użytkownika hello.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Powoduje to hello następujące dane wyjściowe.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Tablice
Jeśli parametr hello jest tablicą, taką jak [array] lub [string []], wówczas można użyć hello następujących toosend formatu JSON ona listę wartości: *[Wartość1, wartość2, Wartość3]*. Te wartości muszą być typu prostego.

Należy wziąć pod uwagę hello następującego testu elementu runbook, który akceptuje parametr o nazwie *użytkownika*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Witaj następujący tekst może zostać użyty dla parametru użytkownika hello.

```
["Joe","Smith",2,true]
```

Powoduje to hello następujące dane wyjściowe.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Poświadczenia
Jeśli parametr hello ma typ danych **PSCredential**, wówczas można podać nazwę hello automatyzacji Azure [zasób poświadczeń](automation-credentials.md). Element runbook Hello pobierze hello poświadczenia o nazwie hello, który określisz.

Należy wziąć pod uwagę hello następującego testu elementu runbook, który akceptuje parametr o nazwie poświadczeń.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Witaj następujący tekst może zostać użyty dla parametru użytkownika hello przy założeniu, że wystąpił zasób poświadczeń o nazwie *moich poświadczeń*.

```
My Credential
```

Zakładając, że hello użytkownika w poświadczeniu hello *jsmith*, powoduje to hello następujące dane wyjściowe.

```
jsmith
```

## <a name="next-steps"></a>Następne kroki
* Architektura runbook Hello w artykule bieżącego zawiera ogólne omówienie elementów runbook Zarządzanie zasobów platformy Azure i lokalnymi z hello hybrydowy proces roboczy elementu Runbook.  toolearn dotyczące wykonywania elementu runbook usługi Automatyzacja w centrum danych, można znaleźć zbyt[hybrydowych procesów roboczych Runbook](automation-hybrid-runbook-worker.md).
* toolearn więcej informacji na temat hello tworzenie toobe elementów runbook moduły używane przez inne elementy runbook do określonych lub wspólnych funkcji, można znaleźć zbyt[podrzędnych elementów Runbook](automation-child-runbooks.md).

