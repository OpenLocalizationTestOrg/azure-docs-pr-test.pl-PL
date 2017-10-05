---
title: "Zbieranie danych analizy dzienników z elementem runbook automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Samouczek krok po kroku, który przedstawiono tworzenie elementu runbook automatyzacji Azure w celu zbierania danych analizy dzienników do repozytorium OMS do analizy."
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="fc5f4-103">Zbieranie danych w analizy dzienników z elementu runbook usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="fc5f4-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="fc5f4-104">Można zbierać znaczną ilość danych analizy dzienników z różnych źródeł w tym [źródeł danych](../log-analytics/log-analytics-data-sources.md) na agentach, a także [dane zbierane z platformy Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="fc5f4-105">Chociaż wymagających zbierania danych, która nie jest dostępny za pośrednictwem tych źródeł standardowe są scenariusze.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="fc5f4-106">W takich przypadkach można użyć [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md) można zapisać danych do analizy dzienników za pomocą dowolnego klienta interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="fc5f4-107">Częstą metodą do wykonania tej kolekcji danych używa elementu runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="fc5f4-108">Ten samouczek przeprowadzi Cię przez proces tworzenia i Planowanie elementu runbook automatyzacji Azure można zapisać danych do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fc5f4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fc5f4-109">Prerequisites</span></span>
<span data-ttu-id="fc5f4-110">Ten scenariusz wymaga następujących zasobów, które są skonfigurowane w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="fc5f4-111">Jednocześnie może być bezpłatne konto.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-111">Both can be a free account.</span></span>

- <span data-ttu-id="fc5f4-112">[Obszar roboczy analizy dziennika](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="fc5f4-113">[Konto usługi Automatyzacja Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="fc5f4-114">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="fc5f4-114">Overview of scenario</span></span>
<span data-ttu-id="fc5f4-115">W tym samouczku przedstawiono tworzenie elementu runbook, który służy do zbierania informacji o automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="fc5f4-116">Elementy Runbook automatyzacji Azure są implementowane przy użyciu programu PowerShell, więc będzie rozpoczyna się od pisania i testowania skrypt w edytorze usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="fc5f4-117">Po upewnieniu się, że zbierasz wymagane informacje, będzie zapisu danych do analizy dzienników i sprawdź niestandardowego typu danych.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="fc5f4-118">Na koniec utworzysz harmonogram uruchamiania elementu runbook w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="fc5f4-119">Można skonfigurować do wysyłania informacji o zadania do analizy dzienników bez tego elementu runbook usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="fc5f4-120">Ten scenariusz jest głównie używana do obsługi tego samouczka i zaleca się wysłanie danych do obszaru roboczego testu.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="fc5f4-121">1. Zainstaluj moduł interfejsu API modułów zbierających dane</span><span class="sxs-lookup"><span data-stu-id="fc5f4-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="fc5f4-122">Każdy [żądania z interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) musi być prawidłowo sformatowany i Dołącz nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="fc5f4-123">Można to zrobić w elemencie runbook, ale zmniejsza ilość kodu wymagane przy użyciu modułu, który ułatwia ten proces.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="fc5f4-124">Jest jeden moduł, którego można używać [modułu OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) w galerii programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="fc5f4-125">Aby użyć [modułu](../automation/automation-integration-modules.md) w elemencie runbook, musi być zainstalowany na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="fc5f4-126">Dowolnym elemencie runbook na tym samym koncie można następnie użyć funkcji w module.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="fc5f4-127">Można zainstalować nowy moduł, wybierając **zasoby** > **modułów** > **dodać moduł** na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="fc5f4-128">Galerii programu PowerShell zapewnia jednak szybkie możliwość wdrożenia modułu bezpośrednio na Twoje konto usługi Automatyzacja, dzięki czemu można użyć tej opcji na potrzeby tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Moduł OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="fc5f4-130">Przejdź do [galerii programu PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="fc5f4-131">Wyszukaj **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="fc5f4-132">Polecenie **Wdróż automatyzacji Azure** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="fc5f4-133">Wybierz konto automatyzacji, a następnie kliknij przycisk **OK** do zainstalowania modułu.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="fc5f4-134">2. Utwórz zmienne automatyzacji</span><span class="sxs-lookup"><span data-stu-id="fc5f4-134">2. Create Automation variables</span></span>
<span data-ttu-id="fc5f4-135">[Zmienne automatyzacji](..\automation\automation-variables.md) przechowywania wartości, które mogą być używane przez wszystkie elementy runbook na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="fc5f4-136">Tworzenia elementów runbook bardziej elastyczne, umożliwiając Zmień wartości tych bez konieczności edytowania rzeczywistego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="fc5f4-137">Każde żądanie z interfejsu API modułów zbierających dane HTTP wymaga identyfikator i klucz obszaru roboczego OMS i zasoby zmiennej idealnie nadają się do przechowywania tych informacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Zmienne](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="fc5f4-139">W portalu Azure przejdź do swojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="fc5f4-140">Wybierz **zmienne** w obszarze **zasobów udostępnionych**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="fc5f4-141">Kliknij przycisk **dodać zmienną** i Utwórz dwie zmienne w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="fc5f4-142">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fc5f4-142">Property</span></span> | <span data-ttu-id="fc5f4-143">Wartość Identyfikatora obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="fc5f4-143">Workspace ID Value</span></span> | <span data-ttu-id="fc5f4-144">Wartość klucza obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="fc5f4-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc5f4-145">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fc5f4-145">Name</span></span> | <span data-ttu-id="fc5f4-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="fc5f4-146">WorkspaceId</span></span> | <span data-ttu-id="fc5f4-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="fc5f4-147">WorkspaceKey</span></span> |
| <span data-ttu-id="fc5f4-148">Typ</span><span class="sxs-lookup"><span data-stu-id="fc5f4-148">Type</span></span> | <span data-ttu-id="fc5f4-149">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fc5f4-149">String</span></span> | <span data-ttu-id="fc5f4-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fc5f4-150">String</span></span> |
| <span data-ttu-id="fc5f4-151">Wartość</span><span class="sxs-lookup"><span data-stu-id="fc5f4-151">Value</span></span> | <span data-ttu-id="fc5f4-152">Wklej identyfikator obszaru roboczego z obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="fc5f4-153">Wklej za pomocą podstawowej lub dodatkowej klucz obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="fc5f4-154">Zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="fc5f4-154">Encrypted</span></span> | <span data-ttu-id="fc5f4-155">Nie</span><span class="sxs-lookup"><span data-stu-id="fc5f4-155">No</span></span> | <span data-ttu-id="fc5f4-156">Tak</span><span class="sxs-lookup"><span data-stu-id="fc5f4-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="fc5f4-157">3. Tworzenie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fc5f4-157">3. Create runbook</span></span>

<span data-ttu-id="fc5f4-158">Automatyzacja Azure ma edytora w portalu, w którym można edytować i przetestuj element runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="fc5f4-159">Istnieje możliwość użycia Edytor skryptów do pracy z [PowerShell bezpośrednio](../automation/automation-edit-textual-runbook.md) lub [utworzyć graficzny element runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="fc5f4-160">W tym samouczku będzie działać z skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Edytowanie elementu Runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="fc5f4-162">Przejdź do swojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="fc5f4-163">Kliknij przycisk **Runbook** > **Dodaj element runbook** > **Utwórz nowy element runbook**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="fc5f4-164">Wpisz nazwę elementu runbook **zbieranie automatyzacji zadania**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="fc5f4-165">Wybierz typ elementu runbook **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="fc5f4-166">Kliknij przycisk **Utwórz** do tworzenia elementu runbook i uruchomić edytora.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="fc5f4-167">Skopiuj i wklej następujący kod do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="fc5f4-168">Zapoznaj się z komentarzami w skrypcie wyjaśnienie kodu.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="fc5f4-169">4. Testowego elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fc5f4-169">4. Test runbook</span></span>
<span data-ttu-id="fc5f4-170">Automatyzacja Azure zawiera środowisko do [przetestuj element runbook](../automation/automation-testing-runbook.md) przed opublikowaniem.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="fc5f4-171">Można sprawdzić danych zbieranych przez element runbook i sprawdź, czy zapisuje do analizy dzienników zgodnie z oczekiwaniami przed opublikowaniem go do produkcji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Testowego elementu runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="fc5f4-173">Kliknij przycisk **zapisać** można zapisać elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="fc5f4-174">Kliknij przycisk **okienku testu** można otworzyć elementu runbook w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="fc5f4-175">Ponieważ element runbook ma parametry, zostanie wyświetlony monit o wprowadź wartości dla nich.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="fc5f4-176">Wprowadź nazwę grupy zasobów i automatyzację konta, którego będziesz zbierać informacje o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="fc5f4-177">Kliknij przycisk **Start** do uruchomienia elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="fc5f4-178">Element runbook rozpocznie się ze stanem **w kolejce** przed trafia do **systemem**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="fc5f4-179">Element runbook powinien być wyświetlany pełne dane wyjściowe z zadania zbierane w formacie json.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="fc5f4-180">Jeśli nie są wyświetlane żadne zadania, następnie mogły wystąpić żadne zadania utworzone w ramach konta usługi Automatyzacja w ciągu ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="fc5f4-181">Spróbuj uruchomić przy użyciu konta automatyzacji dowolnym elemencie runbook, a następnie wykonaj test ponownie.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="fc5f4-182">Upewnij się, czy dane wyjściowe nie wyświetla wszelkie błędy w poleceniu post do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="fc5f4-183">Należy dobrze komunikat podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-183">You should have a message similar to the following.</span></span>

    ![Dane wyjściowe POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="fc5f4-185">5. Weryfikuj rekordy w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fc5f4-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="fc5f4-186">Po elementu runbook została ukończona w teście i upewnieniu się, że dane wyjściowe został pomyślnie odebrany, można sprawdzić, czy rekordy zostały utworzone przy użyciu [wyszukiwania dziennika w analizy dzienników](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Wpisu w Dzienniku](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="fc5f4-188">W portalu Azure wybierz obszar roboczy analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="fc5f4-189">Polecenie **dziennika wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="fc5f4-190">Wpisz następujące polecenie `Type=AutomationJob_CL` i kliknij przycisk wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="fc5f4-191">Należy pamiętać, że typ rekordu zawiera _CL, który nie jest podany w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="fc5f4-192">Ten sufiks jest automatycznie dołączane do typ dziennika, aby wskazać, że typ dziennik niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="fc5f4-193">Powinny pojawić się jeden lub więcej rekordów zwrócił wskazujący, że element runbook działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="fc5f4-194">6. Publikowanie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fc5f4-194">6. Publish the runbook</span></span>
<span data-ttu-id="fc5f4-195">Po upewnieniu się, że element runbook działa poprawnie, należy opublikować go, dlatego może być uruchomiony w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="fc5f4-196">Można nadal edytować i przetestowania elementu runbook bez modyfikowania opublikowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Publikowanie elementu runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="fc5f4-198">Wróć do swojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-198">Return to your automation account.</span></span>
2. <span data-ttu-id="fc5f4-199">Polecenie **Runbook** i wybierz **zbieranie automatyzacji zadania**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="fc5f4-200">Kliknij przycisk **Edytuj** , a następnie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="fc5f4-201">Kliknij przycisk **tak** po otrzymaniu monitu, aby sprawdzić, czy chcesz zastąpić poprzednio opublikowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="fc5f4-202">7. Ustaw opcje rejestrowania</span><span class="sxs-lookup"><span data-stu-id="fc5f4-202">7. Set logging options</span></span> 
<span data-ttu-id="fc5f4-203">Dla testu, można było wyświetlić [pełne dane wyjściowe](../automation/automation-runbook-output-and-messages.md#message-streams) ponieważ wartość zmiennej $VerbosePreference w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="fc5f4-204">W środowisku produkcyjnym należy ustawić właściwości rejestrowania dla elementu runbook, jeśli chcesz wyświetlić pełne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="fc5f4-205">Dla elementu runbook używane w tym samouczku spowoduje to wyświetlenie danych json są wysyłane do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Rejestrowanie i śledzenie](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="fc5f4-207">We właściwościach elementu runbook wybierz **rejestrowania i śledzenia** w obszarze **ustawienia elementu Runbook**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="fc5f4-208">Zmień ustawienia **rejestrowania rekordów pełnych** do **na**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="fc5f4-209">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="fc5f4-210">8. Planowanie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fc5f4-210">8. Schedule runbook</span></span>
<span data-ttu-id="fc5f4-211">Najczęściej uruchomienia elementu runbook, który służy do zbierania danych monitorowania jest można zaplanować automatyczne uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="fc5f4-212">Można to zrobić, tworząc [Harmonogram automatyzacji Azure](../automation/automation-schedules.md) i dołączenie go do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Planowanie elementu runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="fc5f4-214">We właściwościach elementu runbook, zaznacz **harmonogramy** w obszarze **zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="fc5f4-215">Kliknij przycisk **Dodaj harmonogram** > **Połącz harmonogram z elementem runbook** > **Utwórz nowy harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="fc5f4-216">Wpisz następujące wartości harmonogramu i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="fc5f4-217">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fc5f4-217">Property</span></span> | <span data-ttu-id="fc5f4-218">Wartość</span><span class="sxs-lookup"><span data-stu-id="fc5f4-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="fc5f4-219">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fc5f4-219">Name</span></span> | <span data-ttu-id="fc5f4-220">Co godzinę AutomationJobs</span><span class="sxs-lookup"><span data-stu-id="fc5f4-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="fc5f4-221">Rozpoczyna się</span><span class="sxs-lookup"><span data-stu-id="fc5f4-221">Starts</span></span> | <span data-ttu-id="fc5f4-222">Wybierz, w przypadku co najmniej pięć minut późniejsza niż bieżąca godzina.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="fc5f4-223">Cykl</span><span class="sxs-lookup"><span data-stu-id="fc5f4-223">Recurrence</span></span> | <span data-ttu-id="fc5f4-224">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="fc5f4-224">Recurring</span></span> |
| <span data-ttu-id="fc5f4-225">Powtarzanie co</span><span class="sxs-lookup"><span data-stu-id="fc5f4-225">Recur every</span></span> | <span data-ttu-id="fc5f4-226">1 godzina</span><span class="sxs-lookup"><span data-stu-id="fc5f4-226">1 hour</span></span> |
| <span data-ttu-id="fc5f4-227">Wygaśnięcie zestawu</span><span class="sxs-lookup"><span data-stu-id="fc5f4-227">Set expiration</span></span> | <span data-ttu-id="fc5f4-228">Nie</span><span class="sxs-lookup"><span data-stu-id="fc5f4-228">No</span></span> |

<span data-ttu-id="fc5f4-229">Po utworzeniu harmonogramu, należy określić wartości parametrów, które będzie używane przy każdym tego harmonogramu uruchamiania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="fc5f4-230">Kliknij przycisk **Skonfiguruj parametry i parametry uruchomieniowe**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="fc5f4-231">Podaj wartości dla Twojego **ResourceGroupName** i **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="fc5f4-232">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="fc5f4-233">9. Sprawdź element runbook uruchamia zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="fc5f4-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="fc5f4-234">Zawsze, gdy element runbook jest uruchamiany, [tworzone jest zadanie](../automation/automation-runbook-execution.md) i wszelkie dane wyjściowe rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="fc5f4-235">W rzeczywistości są tych samych zadań, które zbiera elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="fc5f4-236">Możesz sprawdzić, czy element runbook uruchamiany zgodnie z oczekiwaniami po upływie czas rozpoczęcia harmonogramu, sprawdzając zadania dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Zadania](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="fc5f4-238">We właściwościach elementu runbook, zaznacz **zadania** w obszarze **zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="fc5f4-239">Powinna zostać wyświetlona lista zadań dla każdej godziny uruchomienia elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="fc5f4-240">Kliknij jeden z zadań, aby wyświetlić jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="fc5f4-241">Polecenie **wszystkie dzienniki** Sprawdź dzienniki i dane wyjściowe z elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="fc5f4-242">Przewiń w dół, aby odnaleźć wpisu, podobnie jak na poniższym obrazie.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Pełne](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="fc5f4-244">Kliknij ten wpis, aby wyświetlić dane szczegółowe json, który został wysłany do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="fc5f4-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc5f4-245">Next steps</span></span>
- <span data-ttu-id="fc5f4-246">Użyj [Widok projektanta](../log-analytics/log-analytics-view-designer.md) utworzyć widok wyświetlanie danych zebranych w repozytorium analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="fc5f4-247">Pakiet w elemencie runbook [rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) do dystrybucji do klientów.</span><span class="sxs-lookup"><span data-stu-id="fc5f4-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="fc5f4-248">Dowiedz się więcej o [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="fc5f4-249">Dowiedz się więcej o [usługi Automatyzacja Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="fc5f4-250">Dowiedz się więcej o [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="fc5f4-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>