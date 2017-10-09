---
title: "aaaStarting i zatrzymywanie maszyn wirtualnych w usłudze Automatyzacja Azure — przepływ pracy programu PowerShell | Dokumentacja firmy Microsoft"
description: "Wersja graficznego elementów runbook toostart i Zatrzymaj klasycznych maszyn wirtualnych w tym scenariuszu usługi Automatyzacja Azure."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="38d02-103">Scenariusz automatyzacji Azure — uruchamianie i zatrzymywanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="38d02-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="38d02-104">Ten scenariusz automatyzacji Azure zawiera elementy runbook toostart i Zatrzymaj klasycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="38d02-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="38d02-105">Dla każdego z następujących hello można użyć tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="38d02-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="38d02-106">Używanie elementów runbook hello bez żadnych modyfikacji, we własnym środowisku.</span><span class="sxs-lookup"><span data-stu-id="38d02-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="38d02-107">Zmodyfikuj hello elementów runbook tooperform dostosować funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="38d02-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="38d02-108">Wywołaj hello elementów runbook z innego elementu runbook jako część ogólnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="38d02-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="38d02-109">Używanie elementów runbook hello jako elementu runbook toolearn samouczki tworzenia pojęcia.</span><span class="sxs-lookup"><span data-stu-id="38d02-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38d02-110">Element graficzny</span><span class="sxs-lookup"><span data-stu-id="38d02-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="38d02-111">Przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="38d02-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="38d02-112">Jest to hello wersji elementu runbook przepływu pracy programu PowerShell tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="38d02-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="38d02-113">Jest również dostępny za pomocą [graficznych elementów runbook](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="38d02-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="38d02-114">Pobieranie hello scenariusza</span><span class="sxs-lookup"><span data-stu-id="38d02-114">Getting hello scenario</span></span>
<span data-ttu-id="38d02-115">Ten scenariusz zawiera dwa elementy runbook przepływu pracy programu PowerShell, które można pobrać z następującego łącza hello.</span><span class="sxs-lookup"><span data-stu-id="38d02-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="38d02-116">Zobacz hello [wersji graficznego](automation-solution-startstopvm-graphical.md) tego scenariusza dla łącza toohello graficznych elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="38d02-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="38d02-117">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="38d02-117">Runbook</span></span> | <span data-ttu-id="38d02-118">Link</span><span class="sxs-lookup"><span data-stu-id="38d02-118">Link</span></span> | <span data-ttu-id="38d02-119">Typ</span><span class="sxs-lookup"><span data-stu-id="38d02-119">Type</span></span> | <span data-ttu-id="38d02-120">Opis</span><span class="sxs-lookup"><span data-stu-id="38d02-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="38d02-121">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-121">Start-AzureVMs</span></span> |[<span data-ttu-id="38d02-122">Uruchom maszyny wirtualne platformy Azure Classic</span><span class="sxs-lookup"><span data-stu-id="38d02-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="38d02-123">Przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="38d02-123">PowerShell Workflow</span></span> |<span data-ttu-id="38d02-124">Uruchamia wszystkie klasycznych maszyn wirtualnych w Azure subscriptionor wszystkich maszyn wirtualnych o nazwie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38d02-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="38d02-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="38d02-126">Zatrzymaj Azure klasycznych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="38d02-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="38d02-127">Przepływ pracy programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="38d02-127">PowerShell Workflow</span></span> |<span data-ttu-id="38d02-128">Powoduje zatrzymanie wszystkich maszyn wirtualnych w konto usługi Automatyzacja lub wszystkich maszyn wirtualnych o nazwie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38d02-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="38d02-129">Instalowanie i konfigurowanie hello scenariusza</span><span class="sxs-lookup"><span data-stu-id="38d02-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="38d02-130">1. Zainstaluj hello elementów runbook</span><span class="sxs-lookup"><span data-stu-id="38d02-130">1. Install hello runbooks</span></span>
<span data-ttu-id="38d02-131">Po pobraniu hello elementów runbook, można je zaimportować przy użyciu procedury hello w [importowanie elementu Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="38d02-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="38d02-132">2. Przejrzyj opis hello i wymagania</span><span class="sxs-lookup"><span data-stu-id="38d02-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="38d02-133">elementy runbook Hello obejmują tekst pomocy komentarze, który zawiera opis i wymagane zasoby.</span><span class="sxs-lookup"><span data-stu-id="38d02-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="38d02-134">Można także uzyskać hello tych samych informacji z tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="38d02-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="38d02-135">3. Konfigurowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="38d02-135">3. Configure assets</span></span>
<span data-ttu-id="38d02-136">elementy runbook Hello wymagają hello następujące zasoby, które należy utworzyć i umieścić odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="38d02-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="38d02-137">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="38d02-137">Asset Type</span></span> | <span data-ttu-id="38d02-138">Nazwa zasobu</span><span class="sxs-lookup"><span data-stu-id="38d02-138">Asset Name</span></span> | <span data-ttu-id="38d02-139">Opis</span><span class="sxs-lookup"><span data-stu-id="38d02-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="38d02-140">Poświadczenie</span><span class="sxs-lookup"><span data-stu-id="38d02-140">Credential</span></span> |<span data-ttu-id="38d02-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="38d02-141">AzureCredential</span></span> |<span data-ttu-id="38d02-142">Zawiera poświadczenia dla konta, które ma urząd toostart i zatrzymanie maszyny wirtualnej w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38d02-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="38d02-143">Alternatywnie można określić innego zasobu poświadczeń w hello **poświadczeń** parametru hello **Add-AzureAccount** działania.</span><span class="sxs-lookup"><span data-stu-id="38d02-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="38d02-144">Zmienna</span><span class="sxs-lookup"><span data-stu-id="38d02-144">Variable</span></span> |<span data-ttu-id="38d02-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="38d02-145">AzureSubscriptionId</span></span> |<span data-ttu-id="38d02-146">Zawiera identyfikator subskrypcji hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38d02-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="38d02-147">Przy użyciu hello scenariusza</span><span class="sxs-lookup"><span data-stu-id="38d02-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="38d02-148">Parametry</span><span class="sxs-lookup"><span data-stu-id="38d02-148">Parameters</span></span>
<span data-ttu-id="38d02-149">Witaj runbook mają hello następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="38d02-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="38d02-150">Należy podać wartości parametrów obowiązkowych i opcjonalnie można podać wartości innych parametrów w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="38d02-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="38d02-151">Parametr</span><span class="sxs-lookup"><span data-stu-id="38d02-151">Parameter</span></span> | <span data-ttu-id="38d02-152">Typ</span><span class="sxs-lookup"><span data-stu-id="38d02-152">Type</span></span> | <span data-ttu-id="38d02-153">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="38d02-153">Mandatory</span></span> | <span data-ttu-id="38d02-154">Opis</span><span class="sxs-lookup"><span data-stu-id="38d02-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="38d02-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="38d02-155">ServiceName</span></span> |<span data-ttu-id="38d02-156">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38d02-156">string</span></span> |<span data-ttu-id="38d02-157">Nie</span><span class="sxs-lookup"><span data-stu-id="38d02-157">No</span></span> |<span data-ttu-id="38d02-158">Jeśli podano wartość, wszystkich maszyn wirtualnych o tej nazwie Usługa jest uruchomiona lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="38d02-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="38d02-159">Jeśli wartość nie zostanie podana, klasycznych maszyn wirtualnych w hello subskrypcji platformy Azure jest uruchomiona lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="38d02-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="38d02-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="38d02-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="38d02-161">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38d02-161">string</span></span> |<span data-ttu-id="38d02-162">Nie</span><span class="sxs-lookup"><span data-stu-id="38d02-162">No</span></span> |<span data-ttu-id="38d02-163">Zawiera nazwę hello hello [zasób zmiennej](#installing-and-configuring-the-scenario) zawierający identyfikator subskrypcji hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38d02-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="38d02-164">Jeśli nie określisz wartości, *AzureSubscriptionId* jest używany.</span><span class="sxs-lookup"><span data-stu-id="38d02-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="38d02-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="38d02-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="38d02-166">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38d02-166">string</span></span> |<span data-ttu-id="38d02-167">Nie</span><span class="sxs-lookup"><span data-stu-id="38d02-167">No</span></span> |<span data-ttu-id="38d02-168">Zawiera nazwę hello hello [zasób poświadczeń](#installing-and-configuring-the-scenario) zawierający poświadczenia hello hello toouse elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="38d02-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="38d02-169">Jeśli nie określisz wartości, *AzureCredential* jest używany.</span><span class="sxs-lookup"><span data-stu-id="38d02-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="38d02-170">Uruchamianie hello elementów runbook</span><span class="sxs-lookup"><span data-stu-id="38d02-170">Starting hello runbooks</span></span>
<span data-ttu-id="38d02-171">Można użyć dowolnego z metody hello w [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) toostart albo hello elementów runbook, w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="38d02-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="38d02-172">następujące przykładowe polecenia Hello używa toorun środowiska Windows PowerShell **StartAzureVMs** toostart wszystkich maszyn wirtualnych o nazwie usługi hello *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="38d02-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="38d02-173">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="38d02-173">Output</span></span>
<span data-ttu-id="38d02-174">elementy runbook Hello będzie [output komunikat](automation-runbook-output-and-messages.md) dla każdej maszyny wirtualnej, wskazując czy hello uruchomienia lub zatrzymania instrukcji zostało pomyślnie przesłane.</span><span class="sxs-lookup"><span data-stu-id="38d02-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="38d02-175">Określony ciąg hello dane wyjściowe toodetermine hello wyników dla każdego elementu runbook można wyszukać.</span><span class="sxs-lookup"><span data-stu-id="38d02-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="38d02-176">ciągi danych wyjściowych Hello są wyświetlane w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="38d02-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="38d02-177">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="38d02-177">Runbook</span></span> | <span data-ttu-id="38d02-178">Warunek</span><span class="sxs-lookup"><span data-stu-id="38d02-178">Condition</span></span> | <span data-ttu-id="38d02-179">Komunikat</span><span class="sxs-lookup"><span data-stu-id="38d02-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38d02-180">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-180">Start-AzureVMs</span></span> |<span data-ttu-id="38d02-181">Maszyna wirtualna jest już uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="38d02-181">Virtual machine is already running</span></span> |<span data-ttu-id="38d02-182">MyVM jest już uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="38d02-182">MyVM is already running</span></span> |
| <span data-ttu-id="38d02-183">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-183">Start-AzureVMs</span></span> |<span data-ttu-id="38d02-184">Żądanie uruchomienia maszyny wirtualnej utworzone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="38d02-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="38d02-185">MyVM została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="38d02-185">MyVM has been started</span></span> |
| <span data-ttu-id="38d02-186">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-186">Start-AzureVMs</span></span> |<span data-ttu-id="38d02-187">Żądanie uruchomienia maszyny wirtualnej nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="38d02-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="38d02-188">Toostart MyVM nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="38d02-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="38d02-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-189">Stop-AzureVMs</span></span> |<span data-ttu-id="38d02-190">Maszyna wirtualna jest już zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="38d02-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="38d02-191">MyVM jest już zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="38d02-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="38d02-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-192">Stop-AzureVMs</span></span> |<span data-ttu-id="38d02-193">Zatrzymaj żądanie pomyślnie przesłano maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="38d02-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="38d02-194">MyVM została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="38d02-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="38d02-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="38d02-195">Stop-AzureVMs</span></span> |<span data-ttu-id="38d02-196">Żądanie zatrzymania maszyny wirtualnej nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="38d02-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="38d02-197">Toostop MyVM nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="38d02-197">MyVM failed toostop</span></span> |

<span data-ttu-id="38d02-198">Na przykład hello następującego fragmentu kodu z elementu runbook prób toostart wszystkich maszyn wirtualnych o nazwie usługi hello *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="38d02-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="38d02-199">Jeśli hello początkowym Niepowodzenie żądania, może zostać pobrany akcje błędu.</span><span class="sxs-lookup"><span data-stu-id="38d02-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="38d02-200">Szczegółowy podział</span><span class="sxs-lookup"><span data-stu-id="38d02-200">Detailed breakdown</span></span>
<span data-ttu-id="38d02-201">Poniżej znajduje się szczegółowy podział hello elementów runbook, w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="38d02-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="38d02-202">Informacje te można wykorzystać tooeither dostosować hello elementów runbook lub po prostu toolearn ich do tworzenia własnych scenariuszy automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="38d02-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="38d02-203">Parametry</span><span class="sxs-lookup"><span data-stu-id="38d02-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="38d02-204">Witaj przepływ pracy uruchamiany przez pobieranie hello wartości dla hello [parametrów wejściowych](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="38d02-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="38d02-205">Jeśli nie podano nazwy zasobów hello są używane domyślne nazwy.</span><span class="sxs-lookup"><span data-stu-id="38d02-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="38d02-206">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="38d02-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="38d02-207">Ten wiersz deklaruje, że hello hello runbook będą zwracać ciąg.</span><span class="sxs-lookup"><span data-stu-id="38d02-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="38d02-208">To nie jest wymagana, ale jest najlepszym rozwiązaniem w przypadku gdy hello runbook jest używany jako [podrzędnego elementu runbook](automation-child-runbooks.md) tak, aby nadrzędny element runbook będzie wiadomo, dane wyjściowe hello wpisz tooexpect.</span><span class="sxs-lookup"><span data-stu-id="38d02-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="38d02-209">Authentication</span><span class="sxs-lookup"><span data-stu-id="38d02-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="38d02-210">Następne wiersze Hello ustawić hello [poświadczenia](automation-credentials.md) i subskrypcji Azure, która będzie służyć do reszty hello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="38d02-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="38d02-211">Najpierw używamy **Get-AutomationPSCredential** tooget hello zawartości, który przechowuje poświadczenia hello z dostępem do toostart i zatrzymywanie maszyn wirtualnych w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38d02-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="38d02-212">**Dodaj-AzureAccount** następnie używa tego poświadczenia hello tooset zasobów.</span><span class="sxs-lookup"><span data-stu-id="38d02-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="38d02-213">dane wyjściowe Hello zostanie przypisana zmienna fikcyjny tooa, dzięki czemu nie jest zawarte w danych wyjściowych elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="38d02-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="38d02-214">zasób zmiennej Hello z subskrypcją hello identyfikator następnie są pobierane z **Get-AutomationVariable** i ustawić o subskrypcji hello **AzureSubscription wybierz**.</span><span class="sxs-lookup"><span data-stu-id="38d02-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="38d02-215">Pobierz maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="38d02-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="38d02-216">**Get-AzureVM** jest tooretrieve używanych maszyn wirtualnych hello hello element runbook będzie współpracować.</span><span class="sxs-lookup"><span data-stu-id="38d02-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="38d02-217">Jeśli wartość jest podana w hello **ServiceName** dane wejściowe są pobierane w zmiennej, a następnie tylko maszyny wirtualne hello o tej nazwie usługi.</span><span class="sxs-lookup"><span data-stu-id="38d02-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="38d02-218">Jeśli **ServiceName** jest pusta, a następnie są pobierane wszystkie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="38d02-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="38d02-219">Uruchamiania/zatrzymywania maszyn wirtualnych i Wyślij dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="38d02-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="38d02-220">Witaj następnego kroku wierszy za pomocą każdej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="38d02-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="38d02-221">Najpierw hello **PowerState** hello maszyny wirtualnej jest zaznaczone toosee Jeśli już jest uruchomiona lub zatrzymana, w zależności od hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="38d02-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="38d02-222">Jeśli jest już w stanie docelowym hello, wiadomość jest wysyłana toooutput i hello zakończenia elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="38d02-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="38d02-223">Jeśli nie, następnie **Start AzureVM** lub **Stop AzureVM** jest używane tooattempt toostart lub zatrzymania hello maszyny wirtualnej z wynikiem hello zmiennej przechowywanej tooa żądania hello.</span><span class="sxs-lookup"><span data-stu-id="38d02-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="38d02-224">Komunikat jest następnie wysyłana określenie toooutput czy toostart żądania hello lub Zatrzymaj zostało pomyślnie przesłane.</span><span class="sxs-lookup"><span data-stu-id="38d02-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38d02-225">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38d02-225">Next steps</span></span>
* <span data-ttu-id="38d02-226">toolearn więcej informacji na temat pracy z podrzędnych elementów runbook, zobacz [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="38d02-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="38d02-227">więcej informacji o toolearn output komunikaty podczas wykonywania elementu runbook i rejestrowanie toohelp Rozwiązywanie problemów z, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="38d02-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

