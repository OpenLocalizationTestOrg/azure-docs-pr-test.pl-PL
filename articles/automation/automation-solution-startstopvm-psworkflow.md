---
title: "Uruchamianie i zatrzymywanie maszyn wirtualnych w usłudze Automatyzacja Azure — przepływ pracy programu PowerShell | Dokumentacja firmy Microsoft"
description: "Wersja graficznego elementów runbook, aby uruchomić i zatrzymać klasycznych maszyn wirtualnych w tym scenariuszu usługi Automatyzacja Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="71def-103">Scenariusz automatyzacji Azure — uruchamianie i zatrzymywanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="71def-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="71def-104">Ten scenariusz automatyzacji Azure zawiera elementy runbook, aby uruchomić i zatrzymać klasycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="71def-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="71def-105">W tym scenariuszu można użyć dla dowolnego z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="71def-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="71def-106">Użyj elementów runbook bez żadnych modyfikacji w środowisku.</span><span class="sxs-lookup"><span data-stu-id="71def-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="71def-107">Modyfikowanie elementów runbook do wykonania funkcji niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="71def-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="71def-108">Wywoływanie elementów runbook z innego elementu runbook jako część ogólnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="71def-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="71def-109">Użyj elementów runbook jako samouczki, aby dowiedzieć się pojęcia dotyczące tworzenia elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="71def-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="71def-110">Element graficzny</span><span class="sxs-lookup"><span data-stu-id="71def-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="71def-111">Przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="71def-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="71def-112">To jest wersja elementu runbook przepływu pracy programu PowerShell tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="71def-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="71def-113">Jest również dostępny za pomocą [graficznych elementów runbook](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="71def-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="71def-114">Uzyskiwanie scenariusza</span><span class="sxs-lookup"><span data-stu-id="71def-114">Getting the scenario</span></span>
<span data-ttu-id="71def-115">W tym scenariuszu składa się z dwóch elementy runbook przepływu pracy programu PowerShell, które można pobrać z poniższych łączy.</span><span class="sxs-lookup"><span data-stu-id="71def-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="71def-116">Zobacz [wersji graficznego](automation-solution-startstopvm-graphical.md) tego scenariusza dla łącza do graficznych elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="71def-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="71def-117">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="71def-117">Runbook</span></span> | <span data-ttu-id="71def-118">Link</span><span class="sxs-lookup"><span data-stu-id="71def-118">Link</span></span> | <span data-ttu-id="71def-119">Typ</span><span class="sxs-lookup"><span data-stu-id="71def-119">Type</span></span> | <span data-ttu-id="71def-120">Opis</span><span class="sxs-lookup"><span data-stu-id="71def-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="71def-121">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-121">Start-AzureVMs</span></span> |[<span data-ttu-id="71def-122">Uruchom maszyny wirtualne platformy Azure Classic</span><span class="sxs-lookup"><span data-stu-id="71def-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="71def-123">Przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="71def-123">PowerShell Workflow</span></span> |<span data-ttu-id="71def-124">Uruchamia wszystkie klasycznych maszyn wirtualnych w Azure subscriptionor wszystkich maszyn wirtualnych o nazwie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="71def-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="71def-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="71def-126">Zatrzymaj Azure klasycznych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="71def-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="71def-127">Przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="71def-127">PowerShell Workflow</span></span> |<span data-ttu-id="71def-128">Powoduje zatrzymanie wszystkich maszyn wirtualnych w konto usługi Automatyzacja lub wszystkich maszyn wirtualnych o nazwie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="71def-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="71def-129">Instalowanie i konfigurowanie scenariusza</span><span class="sxs-lookup"><span data-stu-id="71def-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="71def-130">1. Zainstaluj elementy runbook</span><span class="sxs-lookup"><span data-stu-id="71def-130">1. Install the runbooks</span></span>
<span data-ttu-id="71def-131">Po pobraniu elementy runbook, można zaimportować je za pomocą procedury w [importowanie elementu Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="71def-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="71def-132">2. Przejrzyj opis i wymagania</span><span class="sxs-lookup"><span data-stu-id="71def-132">2. Review the description and requirements</span></span>
<span data-ttu-id="71def-133">Elementy runbook zawierają tekst pomocy komentarze, który zawiera opis i wymagane zasoby.</span><span class="sxs-lookup"><span data-stu-id="71def-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="71def-134">Można także uzyskać te same informacje z tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="71def-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="71def-135">3. Konfigurowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="71def-135">3. Configure assets</span></span>
<span data-ttu-id="71def-136">Elementy runbook wymagają następujące zasoby, które należy utworzyć i umieścić odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="71def-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="71def-137">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="71def-137">Asset Type</span></span> | <span data-ttu-id="71def-138">Nazwa zasobu</span><span class="sxs-lookup"><span data-stu-id="71def-138">Asset Name</span></span> | <span data-ttu-id="71def-139">Opis</span><span class="sxs-lookup"><span data-stu-id="71def-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="71def-140">Poświadczenie</span><span class="sxs-lookup"><span data-stu-id="71def-140">Credential</span></span> |<span data-ttu-id="71def-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="71def-141">AzureCredential</span></span> |<span data-ttu-id="71def-142">Zawiera poświadczenia dla konta, które ma uprawnienia do uruchamiania i zatrzymywania maszyn wirtualnych w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71def-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="71def-143">Alternatywnie można określić innego zasobu poświadczeń w **poświadczeń** parametr **Add-AzureAccount** działania.</span><span class="sxs-lookup"><span data-stu-id="71def-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="71def-144">Zmienna</span><span class="sxs-lookup"><span data-stu-id="71def-144">Variable</span></span> |<span data-ttu-id="71def-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="71def-145">AzureSubscriptionId</span></span> |<span data-ttu-id="71def-146">Zawiera identyfikator subskrypcji z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71def-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="71def-147">Przy użyciu tego scenariusza</span><span class="sxs-lookup"><span data-stu-id="71def-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="71def-148">Parametry</span><span class="sxs-lookup"><span data-stu-id="71def-148">Parameters</span></span>
<span data-ttu-id="71def-149">Elementy runbook każdy ma następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="71def-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="71def-150">Należy podać wartości parametrów obowiązkowych i opcjonalnie można podać wartości innych parametrów w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="71def-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="71def-151">Parametr</span><span class="sxs-lookup"><span data-stu-id="71def-151">Parameter</span></span> | <span data-ttu-id="71def-152">Typ</span><span class="sxs-lookup"><span data-stu-id="71def-152">Type</span></span> | <span data-ttu-id="71def-153">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="71def-153">Mandatory</span></span> | <span data-ttu-id="71def-154">Opis</span><span class="sxs-lookup"><span data-stu-id="71def-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="71def-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="71def-155">ServiceName</span></span> |<span data-ttu-id="71def-156">Ciąg</span><span class="sxs-lookup"><span data-stu-id="71def-156">string</span></span> |<span data-ttu-id="71def-157">Nie</span><span class="sxs-lookup"><span data-stu-id="71def-157">No</span></span> |<span data-ttu-id="71def-158">Jeśli podano wartość, wszystkich maszyn wirtualnych o tej nazwie Usługa jest uruchomiona lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="71def-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="71def-159">Jeśli wartość nie zostanie podana, klasycznych maszyn wirtualnych w subskrypcji platformy Azure jest uruchomiona lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="71def-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="71def-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="71def-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="71def-161">Ciąg</span><span class="sxs-lookup"><span data-stu-id="71def-161">string</span></span> |<span data-ttu-id="71def-162">Nie</span><span class="sxs-lookup"><span data-stu-id="71def-162">No</span></span> |<span data-ttu-id="71def-163">Zawiera nazwę [zasób zmiennej](#installing-and-configuring-the-scenario) zawierający identyfikator subskrypcji z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71def-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="71def-164">Jeśli nie określisz wartości, *AzureSubscriptionId* jest używany.</span><span class="sxs-lookup"><span data-stu-id="71def-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="71def-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="71def-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="71def-166">Ciąg</span><span class="sxs-lookup"><span data-stu-id="71def-166">string</span></span> |<span data-ttu-id="71def-167">Nie</span><span class="sxs-lookup"><span data-stu-id="71def-167">No</span></span> |<span data-ttu-id="71def-168">Zawiera nazwę [zasób poświadczeń](#installing-and-configuring-the-scenario) zawierający poświadczenia dla elementu runbook do użycia.</span><span class="sxs-lookup"><span data-stu-id="71def-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="71def-169">Jeśli nie określisz wartości, *AzureCredential* jest używany.</span><span class="sxs-lookup"><span data-stu-id="71def-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="71def-170">Uruchamianie elementów runbook</span><span class="sxs-lookup"><span data-stu-id="71def-170">Starting the runbooks</span></span>
<span data-ttu-id="71def-171">Można użyć dowolnej z metod w [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) uruchomić jeden z elementów runbook w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="71def-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="71def-172">Następujące przykładowe polecenia używa środowiska Windows PowerShell do uruchamiania **StartAzureVMs** na uruchomienie wszystkich maszyn wirtualnych przy użyciu nazwy usługi *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="71def-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="71def-173">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="71def-173">Output</span></span>
<span data-ttu-id="71def-174">Elementy runbook będą [output komunikat](automation-runbook-output-and-messages.md) dla każdej maszyny wirtualnej, wskazującą, czy instrukcję uruchomienia lub zatrzymania zostało pomyślnie przesłane.</span><span class="sxs-lookup"><span data-stu-id="71def-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="71def-175">Określony ciąg w danych wyjściowych, aby ustalić wyniku dla każdego elementu runbook można wyszukać.</span><span class="sxs-lookup"><span data-stu-id="71def-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="71def-176">W poniższej tabeli wymieniono ciągi danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="71def-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="71def-177">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="71def-177">Runbook</span></span> | <span data-ttu-id="71def-178">Warunek</span><span class="sxs-lookup"><span data-stu-id="71def-178">Condition</span></span> | <span data-ttu-id="71def-179">Komunikat</span><span class="sxs-lookup"><span data-stu-id="71def-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="71def-180">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-180">Start-AzureVMs</span></span> |<span data-ttu-id="71def-181">Maszyna wirtualna jest już uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="71def-181">Virtual machine is already running</span></span> |<span data-ttu-id="71def-182">MyVM jest już uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="71def-182">MyVM is already running</span></span> |
| <span data-ttu-id="71def-183">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-183">Start-AzureVMs</span></span> |<span data-ttu-id="71def-184">Żądanie uruchomienia maszyny wirtualnej utworzone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="71def-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="71def-185">MyVM została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="71def-185">MyVM has been started</span></span> |
| <span data-ttu-id="71def-186">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-186">Start-AzureVMs</span></span> |<span data-ttu-id="71def-187">Żądanie uruchomienia maszyny wirtualnej nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="71def-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="71def-188">Nie można uruchomić MyVM</span><span class="sxs-lookup"><span data-stu-id="71def-188">MyVM failed to start</span></span> |
| <span data-ttu-id="71def-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-189">Stop-AzureVMs</span></span> |<span data-ttu-id="71def-190">Maszyna wirtualna jest już zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="71def-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="71def-191">MyVM jest już zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="71def-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="71def-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-192">Stop-AzureVMs</span></span> |<span data-ttu-id="71def-193">Zatrzymaj żądanie pomyślnie przesłano maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="71def-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="71def-194">MyVM została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="71def-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="71def-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="71def-195">Stop-AzureVMs</span></span> |<span data-ttu-id="71def-196">Żądanie zatrzymania maszyny wirtualnej nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="71def-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="71def-197">Nie można zatrzymać MyVM</span><span class="sxs-lookup"><span data-stu-id="71def-197">MyVM failed to stop</span></span> |

<span data-ttu-id="71def-198">Na przykład poniższy fragment kodu z elementu runbook podejmowana jest próba uruchomienia wszystkich maszyn wirtualnych przy użyciu nazwy usługi *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="71def-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="71def-199">Jeśli jedna z błędów żądań start, może zostać pobrany akcje błędu.</span><span class="sxs-lookup"><span data-stu-id="71def-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="71def-200">Szczegółowy podział</span><span class="sxs-lookup"><span data-stu-id="71def-200">Detailed breakdown</span></span>
<span data-ttu-id="71def-201">Poniżej znajduje się szczegółowy podział elementów runbook w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="71def-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="71def-202">Te informacje można użyć do dostosowania elementy runbook albo też dowiedzieć się od nich używanych do tworzenia własnych scenariuszy automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="71def-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="71def-203">Parametry</span><span class="sxs-lookup"><span data-stu-id="71def-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="71def-204">Przepływ pracy rozpoczyna się od wartości dla pobrania [parametrów wejściowych](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="71def-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="71def-205">Jeśli nie podano nazwy zasobów są używane domyślne nazwy.</span><span class="sxs-lookup"><span data-stu-id="71def-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="71def-206">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="71def-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="71def-207">Ten wiersz deklaruje, że dane wyjściowe element runbook będzie ciąg.</span><span class="sxs-lookup"><span data-stu-id="71def-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="71def-208">To nie jest wymagana, ale jest najlepszym rozwiązaniem w przypadku gdy element runbook zostanie użyty jako [podrzędnego elementu runbook](automation-child-runbooks.md) tak, aby nadrzędny element runbook będzie wiedzieć, oczekiwany typ danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="71def-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="71def-209">Authentication</span><span class="sxs-lookup"><span data-stu-id="71def-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="71def-210">Następnej linii zestaw [poświadczenia](automation-credentials.md) i subskrypcji platformy Azure, który będzie używany w pozostałej części elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="71def-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="71def-211">Najpierw używamy **Get-AutomationPSCredential** można pobrać zawartości, który przechowuje poświadczenia z dostępem do uruchamiania i zatrzymywania maszyn wirtualnych w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71def-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="71def-212">**Dodaj-AzureAccount** następnie używa tego zasobu można ustawić poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="71def-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="71def-213">Dane wyjściowe jest przypisany do zmiennej zastępczego, dzięki czemu nie jest zawarte w danych wyjściowych elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="71def-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="71def-214">Zasób zmiennej z subskrypcją identyfikator następnie są pobierane z **Get-AutomationVariable** i subskrypcji ustawiony za pomocą **AzureSubscription wybierz**.</span><span class="sxs-lookup"><span data-stu-id="71def-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="71def-215">Pobierz maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="71def-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="71def-216">**Get-AzureVM** służy do pobierania element runbook będzie działać z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="71def-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="71def-217">Jeśli wartość jest podana w **ServiceName** wejściowych zmiennej, a następnie są pobierane tylko maszyn wirtualnych o tej nazwie usługi.</span><span class="sxs-lookup"><span data-stu-id="71def-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="71def-218">Jeśli **ServiceName** jest pusta, a następnie są pobierane wszystkie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="71def-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="71def-219">Uruchamiania/zatrzymywania maszyn wirtualnych i Wyślij dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="71def-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="71def-220">Następnym krokiem wierszy za pomocą każdej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71def-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="71def-221">Pierwszy **PowerState** maszyny wirtualnej jest sprawdzane w celu sprawdzenia, jeśli jest już uruchomiona lub zatrzymana, w zależności od elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="71def-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="71def-222">Jeśli jest już w stanie docelowej, do danych wyjściowych i zakończenia elementu runbook jest wysyłany komunikat.</span><span class="sxs-lookup"><span data-stu-id="71def-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="71def-223">Jeśli nie, następnie **Start AzureVM** lub **Stop AzureVM** służy próbę rozpocząć lub zatrzymać maszynę wirtualną w wyniku żądania przechowywane do zmiennej.</span><span class="sxs-lookup"><span data-stu-id="71def-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="71def-224">Komunikat jest następnie wysyłana do wyjściowego określenie, czy żądanie, aby uruchomić lub zatrzymać zostało pomyślnie przesłane.</span><span class="sxs-lookup"><span data-stu-id="71def-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71def-225">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71def-225">Next steps</span></span>
* <span data-ttu-id="71def-226">Aby dowiedzieć się więcej o pracy z podrzędnych elementów runbook, zobacz [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="71def-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="71def-227">Aby dowiedzieć się więcej o komunikaty wyjściowe podczas wykonywania elementu runbook i rejestrowanie do rozwiązywania problemów, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="71def-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

