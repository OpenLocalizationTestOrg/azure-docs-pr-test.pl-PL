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
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="c44d3-103">Uruchamianie elementu runbook automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="c44d3-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="c44d3-104">w poniższej tabeli Hello pomoże określić hello metody toostart elementu runbook w automatyzacji Azure, która jest najbardziej odpowiedniego tooyour danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c44d3-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="c44d3-105">Ten artykuł zawiera szczegółowe informacje dotyczące uruchamiania elementu runbook z hello portalu Azure i programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c44d3-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="c44d3-106">Szczegółowe informacje na powitania innych metod znajdują się w dokumentacji, która są dostępne poniższe linki hello.</span><span class="sxs-lookup"><span data-stu-id="c44d3-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="c44d3-107">**— METODA**</span><span class="sxs-lookup"><span data-stu-id="c44d3-107">**METHOD**</span></span> | <span data-ttu-id="c44d3-108">**WŁAŚCIWOŚCI**</span><span class="sxs-lookup"><span data-stu-id="c44d3-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="c44d3-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c44d3-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="c44d3-110">Najprostsza metoda o interakcyjny interfejs użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c44d3-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="c44d3-111">Wartości parametru proste tooprovide formularza.</span><span class="sxs-lookup"><span data-stu-id="c44d3-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="c44d3-112">Łatwo śledzić stan zadania.</span><span class="sxs-lookup"><span data-stu-id="c44d3-112">Easily track job state.</span></span><br> <li><span data-ttu-id="c44d3-113">Dostęp uwierzytelniony dzięki funkcji logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c44d3-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="c44d3-114">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c44d3-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="c44d3-115">Wywoływanie z wiersza polecenia za pomocą poleceń cmdlet programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c44d3-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="c44d3-116">Można dołączyć do automatycznego rozwiązania z wielu kroków.</span><span class="sxs-lookup"><span data-stu-id="c44d3-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="c44d3-117">Uwierzytelniania żądań certyfikatów lub użytkownika OAuth główna / service podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c44d3-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="c44d3-118">Podaj wartości parametrów proste i złożone.</span><span class="sxs-lookup"><span data-stu-id="c44d3-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="c44d3-119">Śledź stan zadania.</span><span class="sxs-lookup"><span data-stu-id="c44d3-119">Track job state.</span></span><br> <li><span data-ttu-id="c44d3-120">Wymagany klient toosupport poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c44d3-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="c44d3-121">Interfejs API usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="c44d3-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="c44d3-122">Metoda najbardziej elastycznego, ale również większość złożone.</span><span class="sxs-lookup"><span data-stu-id="c44d3-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="c44d3-123">Wywoływanie z kodu niestandardowego, który może zgłaszać żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="c44d3-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="c44d3-124">Żądanie uwierzytelniony przy użyciu certyfikatu lub użytkownika Oauth główna / service podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c44d3-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="c44d3-125">Podaj wartości parametrów proste i złożone.</span><span class="sxs-lookup"><span data-stu-id="c44d3-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="c44d3-126">Śledź stan zadania.</span><span class="sxs-lookup"><span data-stu-id="c44d3-126">Track job state.</span></span> |
| [<span data-ttu-id="c44d3-127">Elementów Webhook</span><span class="sxs-lookup"><span data-stu-id="c44d3-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="c44d3-128">Uruchom element runbook z pojedynczego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="c44d3-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="c44d3-129">Uwierzytelniani tokenu zabezpieczającego w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="c44d3-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="c44d3-130">Klient nie może zastąpić wartości parametrów podczas tworzenia elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="c44d3-131">Element Runbook może definiować jeden parametr, który jest wypełniana szczegółów żądania HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="c44d3-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="c44d3-132">Nie możliwości tootrack stan zadania za pomocą adresu URL elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="c44d3-133">Odpowiedź tooAzure alertu</span><span class="sxs-lookup"><span data-stu-id="c44d3-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="c44d3-134">Uruchom element runbook w odpowiedzi tooAzure alertu.</span><span class="sxs-lookup"><span data-stu-id="c44d3-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="c44d3-135">Konfigurowanie elementu webhook dla elementu runbook, a następnie połącz tooalert.</span><span class="sxs-lookup"><span data-stu-id="c44d3-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="c44d3-136">Uwierzytelniani tokenu zabezpieczającego w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="c44d3-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="c44d3-137">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="c44d3-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="c44d3-138">Automatyczne uruchamianie elementu runbook z harmonogramem co godzinę, codziennie, co tydzień lub co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="c44d3-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="c44d3-139">Manipulowanie harmonogramu za pośrednictwem portalu Azure, poleceń cmdlet programu PowerShell lub interfejsu API Azure.</span><span class="sxs-lookup"><span data-stu-id="c44d3-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="c44d3-140">Podaj parametr wartości toobe używane z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="c44d3-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="c44d3-141">Z innego elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="c44d3-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="c44d3-142">Użyj elementu runbook jako działanie w innego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="c44d3-143">Przydatne w przypadku funkcji używany przez wiele elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="c44d3-144">Podaj parametr wartości toochild runbook i korzystanie z danych wyjściowych w nadrzędny element runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="c44d3-145">Witaj poniższym obrazie przedstawiono krok po kroku proces szczegółowy w cyklu życia hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="c44d3-146">Zawiera różne sposoby uruchamiania elementu runbook w automatyzacji Azure składniki wymagane do elementu runbook usługi Automatyzacja Azure tooexecute hybrydowy proces roboczy elementu Runbook i ich interakcje między poszczególnymi składnikami.</span><span class="sxs-lookup"><span data-stu-id="c44d3-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="c44d3-147">toolearn dotyczące wykonywania elementu runbook usługi Automatyzacja w centrum danych, można znaleźć zbyt[hybrydowych procesów roboczych elementu runbook](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="c44d3-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Architektura elementu Runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="c44d3-149">Uruchamianie elementu runbook z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c44d3-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="c44d3-150">Hello portalu Azure, wybierz **automatyzacji** , a następnie kliknij nazwę hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="c44d3-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="c44d3-151">W menu Centrum hello wybierz **elementów Runbook**.</span><span class="sxs-lookup"><span data-stu-id="c44d3-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="c44d3-152">Na powitania **Runbook** bloku, wybrać element runbook, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="c44d3-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="c44d3-153">Jeśli hello runbook ma parametry, będzie tooprovide zostanie wyświetlony monit o wartości z polem tekstowym dla każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="c44d3-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="c44d3-154">Zobacz [parametrów elementu Runbook](#Runbook-parameters) poniżej zawiera bardziej szczegółowe informacje o parametrach.</span><span class="sxs-lookup"><span data-stu-id="c44d3-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="c44d3-155">Na powitania **zadania** bloku można wyświetlić stan hello hello zadania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="c44d3-156">Uruchamianie elementu runbook przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c44d3-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="c44d3-157">Można użyć hello [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart element runbook za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c44d3-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="c44d3-158">Witaj następujący przykładowy kod uruchamia element runbook o nazwie Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="c44d3-159">Zwraca AzureRmAutomationRunbook rozpoczęcia zadania obiektów, których można używać tootrack jego stan po uruchomieniu elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="c44d3-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="c44d3-160">Następnie można użyć z tym obiektem zadania [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello stan zadania hello i [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c44d3-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="c44d3-161">powitania po przykładowy kod uruchamia element runbook o nazwie Test-Runbook, czeka, dopóki nie zostało ukończone, a następnie wyświetla dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c44d3-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="c44d3-162">Jeśli hello element runbook wymaga parametrów, a następnie należy podać je jako [hashtable](http://technet.microsoft.com/library/hh847780.aspx) Jeśli klucz hello hello hashtable odpowiada hello nazwy parametru i wartości hello jest wartość parametru hello.</span><span class="sxs-lookup"><span data-stu-id="c44d3-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="c44d3-163">Witaj poniższy przykład przedstawia sposób toostart elementu runbook z dwoma parametrami będącymi ciągami o nazwie FirstName i LastName, liczbą całkowitą o nazwie RepeatCount i parametrem logicznym o nazwie Show.</span><span class="sxs-lookup"><span data-stu-id="c44d3-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="c44d3-164">Aby uzyskać dodatkowe informacje na temat parametrów, zobacz [parametrów elementu Runbook](#Runbook-parameters) poniżej.</span><span class="sxs-lookup"><span data-stu-id="c44d3-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="c44d3-165">Parametry elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="c44d3-165">Runbook parameters</span></span>
<span data-ttu-id="c44d3-166">Po uruchomieniu elementu runbook z hello portalu Azure lub programu Windows PowerShell hello instrukcja jest wysyłana za pośrednictwem hello usługi sieci web automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="c44d3-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="c44d3-167">Ta usługa nie obsługuje parametrów o złożonych typach danych.</span><span class="sxs-lookup"><span data-stu-id="c44d3-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="c44d3-168">Jeśli potrzebujesz tooprovide wartość parametru złożonego, a następnie użytkownik musi wywołać go z wnętrza innego elementu runbook zgodnie z opisem w [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="c44d3-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="c44d3-169">specjalne funkcje dotyczące parametrów używających określonych typów danych, zgodnie z opisem w hello następujące sekcje zawierają Hello usługi sieci web usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="c44d3-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="c44d3-170">Nazwane wartości</span><span class="sxs-lookup"><span data-stu-id="c44d3-170">Named values</span></span>
<span data-ttu-id="c44d3-171">Jeśli hello parametr ma typ danych [object], wówczas można użyć powitania po jego listę nazwanych wartości toosend formatu JSON: *{Nazwa1: 'Wartość1', Nazwa2: 'Wartość2', nazwa3: "Wartość3"}*.</span><span class="sxs-lookup"><span data-stu-id="c44d3-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="c44d3-172">Te wartości muszą być typu prostego.</span><span class="sxs-lookup"><span data-stu-id="c44d3-172">These values must be simple types.</span></span> <span data-ttu-id="c44d3-173">Hello element runbook zostanie wyświetlony parametr hello jako [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) z właściwościami, które odpowiadają tooeach o nazwie wartość.</span><span class="sxs-lookup"><span data-stu-id="c44d3-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="c44d3-174">Należy wziąć pod uwagę hello następującego testu elementu runbook, który akceptuje parametr o nazwie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c44d3-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="c44d3-175">Witaj następujący tekst może zostać użyty dla parametru użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="c44d3-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="c44d3-176">Powoduje to hello następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c44d3-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="c44d3-177">Tablice</span><span class="sxs-lookup"><span data-stu-id="c44d3-177">Arrays</span></span>
<span data-ttu-id="c44d3-178">Jeśli parametr hello jest tablicą, taką jak [array] lub [string []], wówczas można użyć hello następujących toosend formatu JSON ona listę wartości: *[Wartość1, wartość2, Wartość3]*.</span><span class="sxs-lookup"><span data-stu-id="c44d3-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="c44d3-179">Te wartości muszą być typu prostego.</span><span class="sxs-lookup"><span data-stu-id="c44d3-179">These values must be simple types.</span></span>

<span data-ttu-id="c44d3-180">Należy wziąć pod uwagę hello następującego testu elementu runbook, który akceptuje parametr o nazwie *użytkownika*.</span><span class="sxs-lookup"><span data-stu-id="c44d3-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="c44d3-181">Witaj następujący tekst może zostać użyty dla parametru użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="c44d3-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="c44d3-182">Powoduje to hello następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c44d3-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="c44d3-183">Poświadczenia</span><span class="sxs-lookup"><span data-stu-id="c44d3-183">Credentials</span></span>
<span data-ttu-id="c44d3-184">Jeśli parametr hello ma typ danych **PSCredential**, wówczas można podać nazwę hello automatyzacji Azure [zasób poświadczeń](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="c44d3-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="c44d3-185">Element runbook Hello pobierze hello poświadczenia o nazwie hello, który określisz.</span><span class="sxs-lookup"><span data-stu-id="c44d3-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="c44d3-186">Należy wziąć pod uwagę hello następującego testu elementu runbook, który akceptuje parametr o nazwie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c44d3-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="c44d3-187">Witaj następujący tekst może zostać użyty dla parametru użytkownika hello przy założeniu, że wystąpił zasób poświadczeń o nazwie *moich poświadczeń*.</span><span class="sxs-lookup"><span data-stu-id="c44d3-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="c44d3-188">Zakładając, że hello użytkownika w poświadczeniu hello *jsmith*, powoduje to hello następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c44d3-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="c44d3-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c44d3-189">Next steps</span></span>
* <span data-ttu-id="c44d3-190">Architektura runbook Hello w artykule bieżącego zawiera ogólne omówienie elementów runbook Zarządzanie zasobów platformy Azure i lokalnymi z hello hybrydowy proces roboczy elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="c44d3-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="c44d3-191">toolearn dotyczące wykonywania elementu runbook usługi Automatyzacja w centrum danych, można znaleźć zbyt[hybrydowych procesów roboczych Runbook](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="c44d3-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="c44d3-192">toolearn więcej informacji na temat hello tworzenie toobe elementów runbook moduły używane przez inne elementy runbook do określonych lub wspólnych funkcji, można znaleźć zbyt[podrzędnych elementów Runbook](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="c44d3-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

