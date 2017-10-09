---
title: "Konfiguracja konta usługi Automatyzacja Azure aaaValidate | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfiguracji hello tooconfirm Twojego konta automatyzacji jest poprawnie skonfigurowana."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="263b6-103">Sprawdzanie uwierzytelniania konta Uruchom jako usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="263b6-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="263b6-104">Po pomyślnym utworzeniu konta automatyzacji, można wykonywać tooconfirm prosty test, możesz toosuccessfully uwierzytelniania usługi Azure Resource Manager lub Azure wdrożenie klasyczne z nowo utworzonych lub zaktualizowanych automatyzacji konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="263b6-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="263b6-105">Uwierzytelnianie konta Uruchom jako usługi Automation</span><span class="sxs-lookup"><span data-stu-id="263b6-105">Automation Run As authentication</span></span>
<span data-ttu-id="263b6-106">Za pomocą hello przykładowy kod poniżej[tworzenia elementu runbook programu PowerShell](automation-creating-importing-runbook.md) tooverify uwierzytelnianie przy użyciu hello Uruchom jako konta, a także w tooauthenticate z niestandardowych elementów runbook oraz zarządzanie tymi zasobami usługi Resource Manager przy użyciu konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="263b6-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="263b6-107">Zwróć uwagę, hello polecenie cmdlet używane do uwierzytelniania w elemencie runbook hello - **Add-AzureRmAccount**, używa hello *ServicePrincipalCertificate* zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="263b6-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="263b6-108">Uwierzytelnia się ono za pomocą certyfikatu nazwy głównej usługi, a nie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="263b6-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="263b6-109">Gdy możesz [uruchamiania elementu runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate konta Uruchom jako [zadanie elementu runbook](automation-runbook-execution.md) jest utworzony, bloku zadania hello jest wyświetlane, a stan zadania hello w hello **Podsumowanie zadania**kafelka.</span><span class="sxs-lookup"><span data-stu-id="263b6-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="263b6-110">Stan zadania Hello zostanie uruchomiona jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.</span><span class="sxs-lookup"><span data-stu-id="263b6-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="263b6-111">Będzie on przenoszony za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="263b6-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="263b6-112">Po zakończeniu zadania elementu runbook hello, możemy powinna zostać wyświetlona stan **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="263b6-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="263b6-113">toosee hello szczegółowe wyniki hello elementu runbook, kliknij na powitania **dane wyjściowe** kafelka.</span><span class="sxs-lookup"><span data-stu-id="263b6-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="263b6-114">Na powitania **dane wyjściowe** bloku, powinien zostać wyświetlony został pomyślnie uwierzytelniony i zwraca listę wszystkich zasobów we wszystkich grupach zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="263b6-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="263b6-115">Pamiętaj tylko tooremove hello blok kodu, począwszy od komentarza hello `#Get all ARM resources from all resource groups` kiedy ponowne użycie hello kodu dla elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="263b6-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="263b6-116">Uwierzytelnianie klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="263b6-116">Classic Run As authentication</span></span>
<span data-ttu-id="263b6-117">Za pomocą hello przykładowy kod poniżej[tworzenia elementu runbook programu PowerShell](automation-creating-importing-runbook.md) tooverify uwierzytelnianie przy użyciu hello Classic Uruchom jako konta, a także w tooauthenticate z niestandardowych elementów runbook i zarządzanie zasobami w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="263b6-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="263b6-118">Gdy możesz [uruchamiania elementu runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate konta Uruchom jako [zadanie elementu runbook](automation-runbook-execution.md) jest utworzony, bloku zadania hello jest wyświetlane, a stan zadania hello w hello **Podsumowanie zadania**kafelka.</span><span class="sxs-lookup"><span data-stu-id="263b6-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="263b6-119">Stan zadania Hello zostanie uruchomiona jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.</span><span class="sxs-lookup"><span data-stu-id="263b6-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="263b6-120">Będzie on przenoszony za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="263b6-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="263b6-121">Po zakończeniu zadania elementu runbook hello, możemy powinna zostać wyświetlona stan **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="263b6-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="263b6-122">toosee hello szczegółowe wyniki hello elementu runbook, kliknij na powitania **dane wyjściowe** kafelka.</span><span class="sxs-lookup"><span data-stu-id="263b6-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="263b6-123">Na powitania **dane wyjściowe** bloku, powinien zostać wyświetlony został pomyślnie uwierzytelniony i zwraca listę wszystkich maszyn wirtualnych platformy Azure przez VMName, które są wdrażane w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="263b6-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="263b6-124">Pamiętaj tylko polecenia cmdlet hello tooremove **Get AzureVM** kiedy ponowne użycie hello kodu dla elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="263b6-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="263b6-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="263b6-125">Next steps</span></span>
* <span data-ttu-id="263b6-126">tooget pracę z elementów runbook programu PowerShell, zobacz [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="263b6-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="263b6-127">Zobacz toolearn więcej informacji na temat tworzenia graficznego [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="263b6-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
