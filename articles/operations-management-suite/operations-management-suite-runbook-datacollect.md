---
title: "aaaCollecting analizy dzienników danych do elementu runbook automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Samouczek krok po kroku, który przedstawiono tworzenie elementu runbook w automatyzacji Azure toocollect danych do repozytorium OMS hello do analizy przez analizy dzienników."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="fe461-103">Zbieranie danych w analizy dzienników z elementu runbook usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="fe461-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="fe461-104">Można zbierać znaczną ilość danych analizy dzienników z różnych źródeł w tym [źródeł danych](../log-analytics/log-analytics-data-sources.md) na agentach, a także [dane zbierane z platformy Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="fe461-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="fe461-105">Chociaż wymagających toocollect danych, która nie jest dostępny za pośrednictwem tych źródeł standardowe są scenariusze.</span><span class="sxs-lookup"><span data-stu-id="fe461-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="fe461-106">W takich przypadkach można użyć hello [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite danych tooLog Analytics za pomocą dowolnego klienta interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="fe461-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="fe461-107">Typowe tooperform metody tej kolekcji danych używa elementu runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="fe461-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="fe461-108">Ten samouczek przeprowadzi Cię przez proces hello tworzenie i Planowanie elementu runbook w automatyzacji Azure toowrite danych tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe461-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fe461-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe461-109">Prerequisites</span></span>
<span data-ttu-id="fe461-110">Ten scenariusz wymaga hello następujące zasoby skonfigurowane w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe461-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="fe461-111">Jednocześnie może być bezpłatne konto.</span><span class="sxs-lookup"><span data-stu-id="fe461-111">Both can be a free account.</span></span>

- <span data-ttu-id="fe461-112">[Obszar roboczy analizy dziennika](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fe461-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="fe461-113">[Konto usługi Automatyzacja Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fe461-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="fe461-114">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="fe461-114">Overview of scenario</span></span>
<span data-ttu-id="fe461-115">W tym samouczku przedstawiono tworzenie elementu runbook, który służy do zbierania informacji o automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="fe461-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="fe461-116">Elementy Runbook automatyzacji Azure są implementowane przy użyciu programu PowerShell, więc będzie rozpoczyna się od pisania i testowania skrypt w edytorze usługi Automatyzacja Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="fe461-117">Po zweryfikowaniu zbierasz hello wymagane informacje, będzie zapisu tego tooLog danych Analytics i sprawdź hello niestandardowego typu danych.</span><span class="sxs-lookup"><span data-stu-id="fe461-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="fe461-118">Na koniec zostanie utworzony element runbook hello toostart harmonogramu w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="fe461-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="fe461-119">Można skonfigurować usługi Automatyzacja Azure toosend zadania informacji tooLog Analytics bez tego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="fe461-120">Ten scenariusz jest głównie używane toosupport hello samouczek i zaleca się wysłanie hello danych tooa testu z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="fe461-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="fe461-121">1. Zainstaluj moduł interfejsu API modułów zbierających dane</span><span class="sxs-lookup"><span data-stu-id="fe461-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="fe461-122">Każdy [żądania z interfejsu API modułów zbierających dane HTTP hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) musi być prawidłowo sformatowany i Dołącz nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="fe461-123">Można to zrobić w elemencie runbook, ale może zmniejszyć ilość hello kod wymagany przy użyciu modułu, który ułatwia ten proces.</span><span class="sxs-lookup"><span data-stu-id="fe461-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="fe461-124">Jest jeden moduł, którego można używać [modułu OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) w hello galerii programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe461-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="fe461-125">toouse [modułu](../automation/automation-integration-modules.md) w elemencie runbook, musi być zainstalowany na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="fe461-126">Funkcje w hello module hello dowolnym elemencie runbook w hello można używać tego samego konta.</span><span class="sxs-lookup"><span data-stu-id="fe461-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="fe461-127">Można zainstalować nowy moduł, wybierając **zasoby** > **modułów** > **dodać moduł** na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="fe461-128">Hello galerii programu PowerShell jednak daje toodeploy opcja szybkiego modułu bezpośrednio konta automatyzacji tooyour dzięki tej opcji można użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="fe461-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Moduł OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="fe461-130">Przejdź za[galerii programu PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="fe461-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="fe461-131">Wyszukaj **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="fe461-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="fe461-132">Polecenie hello **tooAzure automatyzacji wdrażania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe461-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="fe461-133">Wybierz konto automatyzacji, a następnie kliknij przycisk **OK** tooinstall hello modułu.</span><span class="sxs-lookup"><span data-stu-id="fe461-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="fe461-134">2. Utwórz zmienne automatyzacji</span><span class="sxs-lookup"><span data-stu-id="fe461-134">2. Create Automation variables</span></span>
<span data-ttu-id="fe461-135">[Zmienne automatyzacji](..\automation\automation-variables.md) przechowywania wartości, które mogą być używane przez wszystkie elementy runbook na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="fe461-136">Tworzenia elementów runbook więcej elastyczne, umożliwiając toochange te wartości bez konieczności edytowania hello rzeczywistego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="fe461-137">Każde żądanie z hello interfejsu API modułów zbierających dane HTTP wymaga hello identyfikator i klucz obszaru roboczego OMS hello i zmiennej zasoby są idealne toostore te informacje.</span><span class="sxs-lookup"><span data-stu-id="fe461-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![Zmienne](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="fe461-139">W hello portalu Azure Przejdź tooyour konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="fe461-140">Wybierz **zmienne** w obszarze **zasobów udostępnionych**.</span><span class="sxs-lookup"><span data-stu-id="fe461-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="fe461-141">Kliknij przycisk **dodać zmienną** i Utwórz dwie zmienne hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe461-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="fe461-142">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fe461-142">Property</span></span> | <span data-ttu-id="fe461-143">Wartość Identyfikatora obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="fe461-143">Workspace ID Value</span></span> | <span data-ttu-id="fe461-144">Wartość klucza obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="fe461-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fe461-145">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fe461-145">Name</span></span> | <span data-ttu-id="fe461-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="fe461-146">WorkspaceId</span></span> | <span data-ttu-id="fe461-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="fe461-147">WorkspaceKey</span></span> |
| <span data-ttu-id="fe461-148">Typ</span><span class="sxs-lookup"><span data-stu-id="fe461-148">Type</span></span> | <span data-ttu-id="fe461-149">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fe461-149">String</span></span> | <span data-ttu-id="fe461-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fe461-150">String</span></span> |
| <span data-ttu-id="fe461-151">Wartość</span><span class="sxs-lookup"><span data-stu-id="fe461-151">Value</span></span> | <span data-ttu-id="fe461-152">Wklej hello identyfikator obszaru roboczego z obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fe461-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="fe461-153">Wklej się przy użyciu hello podstawowej lub dodatkowej klucz obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fe461-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="fe461-154">Zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="fe461-154">Encrypted</span></span> | <span data-ttu-id="fe461-155">Nie</span><span class="sxs-lookup"><span data-stu-id="fe461-155">No</span></span> | <span data-ttu-id="fe461-156">Tak</span><span class="sxs-lookup"><span data-stu-id="fe461-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="fe461-157">3. Tworzenie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fe461-157">3. Create runbook</span></span>

<span data-ttu-id="fe461-158">W portalu hello, w którym można edytować i przetestuj element runbook usługi Automatyzacja Azure występuje edytora.</span><span class="sxs-lookup"><span data-stu-id="fe461-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="fe461-159">Masz hello opcja toouse hello skryptu Edytor toowork z [PowerShell bezpośrednio](../automation/automation-edit-textual-runbook.md) lub [utworzyć graficzny element runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="fe461-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="fe461-160">W tym samouczku będzie działać z skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe461-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Edytowanie elementu Runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="fe461-162">Przejdź tooyour konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="fe461-163">Kliknij przycisk **Runbook** > **Dodaj element runbook** > **Utwórz nowy element runbook**.</span><span class="sxs-lookup"><span data-stu-id="fe461-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="fe461-164">Nazwa elementu runbook hello, wpisz **zbieranie automatyzacji zadania**.</span><span class="sxs-lookup"><span data-stu-id="fe461-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="fe461-165">Typ elementu runbook hello wybierz **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="fe461-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="fe461-166">Kliknij przycisk **Utwórz** toocreate hello elementu runbook, a następnie rozpocznij hello edytora.</span><span class="sxs-lookup"><span data-stu-id="fe461-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="fe461-167">Skopiuj i Wklej powitania po kodu na powitania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="fe461-168">Można znaleźć toohello komentarzy w skrypcie hello opis hello kodu.</span><span class="sxs-lookup"><span data-stu-id="fe461-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="fe461-169">4. Testowego elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fe461-169">4. Test runbook</span></span>
<span data-ttu-id="fe461-170">Automatyzacja Azure zawiera środowisko zbyt[przetestuj element runbook](../automation/automation-testing-runbook.md) przed opublikowaniem.</span><span class="sxs-lookup"><span data-stu-id="fe461-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="fe461-171">Można sprawdzić hello danych zbieranych przez element runbook hello i sprawdź, czy zapisuje tooLog Analytics zgodnie z oczekiwaniami przed jej opublikowaniem tooproduction.</span><span class="sxs-lookup"><span data-stu-id="fe461-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Testowego elementu runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="fe461-173">Kliknij przycisk **zapisać** toosave hello runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="fe461-174">Kliknij przycisk **okienku testu** tooopen hello runbook w środowisku testowym hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="fe461-175">Ponieważ element runbook ma parametry, możesz tooenter zostanie wyświetlony monit o wartości dla nich.</span><span class="sxs-lookup"><span data-stu-id="fe461-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="fe461-176">Wprowadź nazwę grupy zasobów hello hello i automatyzacji hello konta użytkownika będzie toocollect informacje o zadaniu z.</span><span class="sxs-lookup"><span data-stu-id="fe461-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="fe461-177">Kliknij przycisk **Start** toohello uruchomić hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="fe461-178">Hello runbook rozpocznie się ze stanem **w kolejce** przed przechodzi ona zbyt**systemem**.</span><span class="sxs-lookup"><span data-stu-id="fe461-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="fe461-179">Hello runbook powinien być wyświetlany pełne dane wyjściowe z zadania hello zbierane w formacie json.</span><span class="sxs-lookup"><span data-stu-id="fe461-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="fe461-180">Jeśli nie są wyświetlane żadne zadania, następnie mogły wystąpić żadne zadania utworzone na koncie automatyzacji hello w hello ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="fe461-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="fe461-181">Spróbuj uruchomić przy użyciu konta automatyzacji hello dowolnym elemencie runbook, a następnie wykonaj ponownie hello testu.</span><span class="sxs-lookup"><span data-stu-id="fe461-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="fe461-182">Upewnij się, że hello dane wyjściowe nie wyświetla się, że wszelkie błędy hello post tooLog polecenia Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe461-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="fe461-183">Powinien mieć następujące toohello podobne wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fe461-183">You should have a message similar toohello following.</span></span>

    ![Dane wyjściowe POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="fe461-185">5. Weryfikuj rekordy w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fe461-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="fe461-186">Po hello elementu runbook została ukończona w teście i upewnieniu się, dane wyjściowe hello został pomyślnie odebrany, może sprawdzić, czy rekordy hello zostały utworzone przy użyciu [wyszukiwania dziennika w analizy dzienników](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="fe461-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Wpisu w Dzienniku](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="fe461-188">W hello portalu Azure wybierz obszar roboczy analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fe461-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="fe461-189">Polecenie **dziennika wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="fe461-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="fe461-190">Witaj wpisz następujące polecenie `Type=AutomationJob_CL` i kliknij przycisk Wyszukaj hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="fe461-191">Należy pamiętać, że typ rekordu hello zawiera _CL, który nie jest określone w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="fe461-192">Ten sufiks jest tooindicate typu dziennika toohello automatycznie dołączany jest typem Dziennik niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="fe461-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="fe461-193">Powinny pojawić się jeden lub więcej rekordów zwrócił wskazujący, że ten element runbook hello działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="fe461-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="fe461-194">6. Publikowanie elementu runbook hello</span><span class="sxs-lookup"><span data-stu-id="fe461-194">6. Publish hello runbook</span></span>
<span data-ttu-id="fe461-195">Po upewnieniu się, że hello element runbook działa poprawnie, należy toopublish go, dlatego może być uruchomiony w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="fe461-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="fe461-196">Można kontynuować tooedit i testowanie elementu runbook hello bez modyfikowania hello opublikowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="fe461-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Publikowanie elementu runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="fe461-198">Zwraca tooyour konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fe461-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="fe461-199">Polecenie **Runbook** i wybierz **zbieranie automatyzacji zadania**.</span><span class="sxs-lookup"><span data-stu-id="fe461-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="fe461-200">Kliknij przycisk **Edytuj** , a następnie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="fe461-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="fe461-201">Kliknij przycisk **tak** gdy zadawane tooverify mają toooverwrite hello wcześniej publikowane wersji.</span><span class="sxs-lookup"><span data-stu-id="fe461-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="fe461-202">7. Ustaw opcje rejestrowania</span><span class="sxs-lookup"><span data-stu-id="fe461-202">7. Set logging options</span></span> 
<span data-ttu-id="fe461-203">Dla testu, zostały stanie tooview [pełne dane wyjściowe](../automation/automation-runbook-output-and-messages.md#message-streams) ponieważ wartość zmiennej hello $VerbosePreference w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="fe461-204">W środowisku produkcyjnym należy właściwości tooset hello rejestrowania dla elementu runbook hello Chcąc tooview pełne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="fe461-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="fe461-205">Dla elementu runbook hello jest używany w tym samouczku spowoduje to wyświetlenie danych json hello wysyłane tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe461-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Rejestrowanie i śledzenie](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="fe461-207">W elemencie runbook hello właściwości wybierz **rejestrowania i śledzenia** w obszarze **ustawienia elementu Runbook**.</span><span class="sxs-lookup"><span data-stu-id="fe461-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="fe461-208">Zmień ustawienia hello **rejestrowania rekordów pełnych** za**na**.</span><span class="sxs-lookup"><span data-stu-id="fe461-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="fe461-209">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fe461-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="fe461-210">8. Planowanie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fe461-210">8. Schedule runbook</span></span>
<span data-ttu-id="fe461-211">Witaj najczęściej sposób toostart elementu runbook, który służy do zbierania danych monitorowania jest tooschedule on toorun automatycznie.</span><span class="sxs-lookup"><span data-stu-id="fe461-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="fe461-212">Można to zrobić, tworząc [Harmonogram automatyzacji Azure](../automation/automation-schedules.md) i dołączania ich tooyour elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Planowanie elementu runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="fe461-214">Witaj właściwości dla elementu runbook, zaznacz **harmonogramy** w obszarze **zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fe461-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="fe461-215">Kliknij przycisk **Dodaj harmonogram** > **powiązania elementu runbook tooyour harmonogram** > **Utwórz nowy harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="fe461-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="fe461-216">Typ w hello następujące wartości hello harmonogram, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fe461-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="fe461-217">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fe461-217">Property</span></span> | <span data-ttu-id="fe461-218">Wartość</span><span class="sxs-lookup"><span data-stu-id="fe461-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="fe461-219">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fe461-219">Name</span></span> | <span data-ttu-id="fe461-220">Co godzinę AutomationJobs</span><span class="sxs-lookup"><span data-stu-id="fe461-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="fe461-221">Rozpoczyna się</span><span class="sxs-lookup"><span data-stu-id="fe461-221">Starts</span></span> | <span data-ttu-id="fe461-222">Wybierz wszystkie czas bieżący czas hello ostatnich co najmniej 5 minut.</span><span class="sxs-lookup"><span data-stu-id="fe461-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="fe461-223">Cykl</span><span class="sxs-lookup"><span data-stu-id="fe461-223">Recurrence</span></span> | <span data-ttu-id="fe461-224">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="fe461-224">Recurring</span></span> |
| <span data-ttu-id="fe461-225">Powtarzanie co</span><span class="sxs-lookup"><span data-stu-id="fe461-225">Recur every</span></span> | <span data-ttu-id="fe461-226">1 godzina</span><span class="sxs-lookup"><span data-stu-id="fe461-226">1 hour</span></span> |
| <span data-ttu-id="fe461-227">Wygaśnięcie zestawu</span><span class="sxs-lookup"><span data-stu-id="fe461-227">Set expiration</span></span> | <span data-ttu-id="fe461-228">Nie</span><span class="sxs-lookup"><span data-stu-id="fe461-228">No</span></span> |

<span data-ttu-id="fe461-229">Po utworzeniu harmonogramu hello należy wartości parametrów hello tooset, które będą używane w każdym uruchomieniu tego harmonogramu hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="fe461-230">Kliknij przycisk **Skonfiguruj parametry i parametry uruchomieniowe**.</span><span class="sxs-lookup"><span data-stu-id="fe461-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="fe461-231">Podaj wartości dla Twojego **ResourceGroupName** i **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="fe461-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="fe461-232">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe461-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="fe461-233">9. Sprawdź element runbook uruchamia zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="fe461-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="fe461-234">Zawsze, gdy element runbook jest uruchamiany, [tworzone jest zadanie](../automation/automation-runbook-execution.md) i wszelkie dane wyjściowe rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="fe461-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="fe461-235">W rzeczywistości są hello jest zbieranie tych samych zadań, które hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="fe461-236">Możesz sprawdzić, czy ten element runbook hello uruchamiany zgodnie z oczekiwaniami, sprawdzając hello zadania dla elementu runbook powitania po upływie hello czas rozpoczęcia harmonogramu hello.</span><span class="sxs-lookup"><span data-stu-id="fe461-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Zadania](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="fe461-238">Witaj właściwości dla elementu runbook, zaznacz **zadania** w obszarze **zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fe461-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="fe461-239">Powinny pojawić się, że dostęp do listy zadań dla każdego elementu runbook hello czas uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="fe461-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="fe461-240">Kliknij jeden z tooview zadania hello jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="fe461-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="fe461-241">Polecenie **wszystkie dzienniki** tooview hello dzienników i danych wyjściowych z hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fe461-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="fe461-242">Przewiń toohello toofind dolnej wprowadzania podobne toohello obraz poniżej.</span><span class="sxs-lookup"><span data-stu-id="fe461-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Pełne](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="fe461-244">Kliknij ten wpis tooview hello szczegółowe dane json, którego wysłano tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe461-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="fe461-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe461-245">Next steps</span></span>
- <span data-ttu-id="fe461-246">Użyj [Widok projektanta](../log-analytics/log-analytics-view-designer.md) toocreate wyświetlania widoku hello danych, aby zostały pobrane toohello analizy dzienników repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fe461-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="fe461-247">Pakiet w elemencie runbook [rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="fe461-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="fe461-248">Dowiedz się więcej o [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="fe461-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="fe461-249">Dowiedz się więcej o [usługi Automatyzacja Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="fe461-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="fe461-250">Dowiedz się więcej o hello [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="fe461-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
