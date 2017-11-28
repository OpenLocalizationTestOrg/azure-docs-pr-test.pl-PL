---
title: Uruchom elementy runbook na procesu roboczego Runbook hybrydowego automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera informacje dotyczące wykonywania elementów runbook na komputerach w lokalnym centrum danych lub dostawcy chmury z rolą hybrydowy proces roboczy elementu Runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="250de-103">Uruchomione elementy runbook na hybrydowy proces roboczy elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="250de-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="250de-104">Nie ma różnic w strukturze elementów runbook, które są uruchamiane w automatyzacji Azure oraz te, które uruchamiane na hybrydowy proces roboczy elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="250de-105">Elementy Runbook korzystające z każdym najprawdopodobniej różnią się znacznie jednak ponieważ elementy runbook, elementów docelowych hybrydowy proces roboczy elementu Runbook, zwykle zarządzać zasobami na komputerze lokalnym lub w odniesieniu do zasobów w środowisku lokalnym, w których jest wdrożona, gdy elementy runbook automatyzacji Azure zazwyczaj zarządzać zasobami w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="250de-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="250de-106">Można edytować element runbook dla hybrydowego procesu roboczego Runbook automatyzacji Azure, ale mogą mieć trudności, Jeśli spróbujesz testu elementu runbook w edytorze.</span><span class="sxs-lookup"><span data-stu-id="250de-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="250de-107">Moduły programu PowerShell, które uzyskują dostęp do zasobów lokalnych może nie być zainstalowana w Twoim środowisku usługi Automatyzacja Azure w takim przypadku, testu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="250de-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="250de-108">Po zainstalowaniu wymaganych modułów, następnie element runbook zostanie uruchomiony, ale nie będzie możliwy dostęp do zasobów lokalnych do ukończenia testowej.</span><span class="sxs-lookup"><span data-stu-id="250de-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="250de-109">Uruchamianie elementu runbook na hybrydowy proces roboczy elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="250de-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="250de-110">[Uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) opisano różne metody uruchamiania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="250de-111">Dodaje hybrydowy proces roboczy elementu Runbook **RunOn** opcja, w którym można określić nazwę grupy hybrydowego procesu roboczego elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="250de-112">Jeśli zostanie określona grupa, element runbook jest pobierane i wykonywane przez pracowników w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="250de-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="250de-113">Jeśli ta opcja nie jest określona, następnie jest uruchamiany w automatyzacji Azure normalnie.</span><span class="sxs-lookup"><span data-stu-id="250de-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="250de-114">Po uruchomieniu elementu runbook w portalu Azure, jest wyświetlana **Uruchom na** opcja, w którym można wybrać **Azure** lub **hybrydowy proces roboczy**.</span><span class="sxs-lookup"><span data-stu-id="250de-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="250de-115">W przypadku wybrania **hybrydowy proces roboczy**, a następnie z listy rozwijanej można wybrać grupy.</span><span class="sxs-lookup"><span data-stu-id="250de-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="250de-116">Użyj **RunOn** parametru.</span><span class="sxs-lookup"><span data-stu-id="250de-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="250de-117">Następujące polecenie służy do uruchomienia elementu runbook o nazwie Test-Runbook na hybrydowego grupy procesów roboczych elementu Runbook o nazwie MyHybridGroup przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="250de-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="250de-118">**RunOn** parametr został dodany do **Start AzureAutomationRunbook** polecenia cmdlet w wersji od 0.9.1 Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="250de-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="250de-119">Należy [Pobierz najnowszą wersję](https://azure.microsoft.com/downloads/) Jeśli masz wcześniejszą zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="250de-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="250de-120">Musisz zainstalować tę wersję stacji roboczej, na którym jest uruchamiany element runbook z programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="250de-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="250de-121">Nie należy go zainstalować na komputerze pracownika, chyba że użytkownik zamierza uruchamiania elementów runbook z tego komputera.</span><span class="sxs-lookup"><span data-stu-id="250de-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="250de-122">Obecnie nie można uruchomić elementu runbook na hybrydowy proces roboczy elementu Runbook z innego elementu runbook, ponieważ wymagałoby to najnowsza wersja programu Azure Powershell do zainstalowania na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="250de-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="250de-123">Najnowsza wersja jest automatycznie aktualizowana w automatyzacji Azure i automatycznie przesuwana pracownikom wkrótce.</span><span class="sxs-lookup"><span data-stu-id="250de-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="250de-124">Uprawnienia elementów Runbook</span><span class="sxs-lookup"><span data-stu-id="250de-124">Runbook permissions</span></span>
<span data-ttu-id="250de-125">Elementów Runbook uruchomionych na hybrydowy proces roboczy elementu Runbook nie można użyć tej samej metody, która jest zwykle używana do elementów runbook uwierzytelniania do zasobów platformy Azure, ponieważ uzyskują dostęp do zasobów poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="250de-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="250de-126">Element runbook można ustalić uwierzytelniania do zasobów lokalnych, lub można określić konto Uruchom jako, aby zapewnić kontekstu użytkownika dla wszystkich elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="250de-127">Uwierzytelnianie elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="250de-127">Runbook authentication</span></span>
<span data-ttu-id="250de-128">Domyślnie elementy runbook zostanie uruchomiony w kontekście konta systemu lokalnego na komputerze lokalnym, użytkownik musi podać własne uwierzytelniania do zasobów, które będą miały dostęp.</span><span class="sxs-lookup"><span data-stu-id="250de-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="250de-129">Można użyć [poświadczeń](http://msdn.microsoft.com/library/dn940015.aspx) i [certyfikatu](http://msdn.microsoft.com/library/dn940013.aspx) zasoby w elemencie runbook za pomocą poleceń cmdlet, które pozwalają określić poświadczenia, można uwierzytelniać do różnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="250de-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="250de-130">Poniższy przykład przedstawia części elementu runbook, który powoduje ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="250de-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="250de-131">Pobiera poświadczenia z zasobu poświadczeń i nazwę komputera z zasób zmiennej, a następnie używa tych wartości w poleceniu cmdlet Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="250de-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="250de-132">Można też skorzystać [InlineScript](automation-powershell-workflow.md#inlinescript), co pozwala uruchamiać bloków kodu na innym komputerze przy użyciu poświadczeń, określony przez [typowy parametr PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="250de-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="250de-133">Konto Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="250de-133">RunAs account</span></span>
<span data-ttu-id="250de-134">Zamiast zapewnienia uwierzytelniania do zasobów lokalnych elementów runbook, można określić **RunAs** konto do grupy hybrydowych procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="250de-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="250de-135">Należy określić [zasób poświadczeń](automation-credentials.md) mający dostęp do zasobów lokalnych i wszystkich elementów runbook działać w ramach tych poświadczeń, podczas uruchamiania na hybrydowy proces roboczy elementu Runbook w grupie.</span><span class="sxs-lookup"><span data-stu-id="250de-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="250de-136">Nazwa użytkownika dla poświadczenia musi być w jednym z następujących formatów:</span><span class="sxs-lookup"><span data-stu-id="250de-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="250de-137">domena azwa_użytkownika</span><span class="sxs-lookup"><span data-stu-id="250de-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="250de-138">Nazwa użytkownika (dla kont lokalnych dla komputera lokalnego)</span><span class="sxs-lookup"><span data-stu-id="250de-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="250de-139">Aby określić konto Uruchom jako dla grupy hybrydowych procesów roboczych, użyj poniższej procedury:</span><span class="sxs-lookup"><span data-stu-id="250de-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="250de-140">Utwórz [zasób poświadczeń](automation-credentials.md) z dostępem do zasobów lokalnych.</span><span class="sxs-lookup"><span data-stu-id="250de-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="250de-141">Otwórz konto usługi Automatyzacja w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="250de-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="250de-142">Wybierz **hybrydowego procesu roboczego grupy** Kafelek, a następnie wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="250de-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="250de-143">Wybierz **wszystkie ustawienia** , a następnie **ustawienia grupy hybrydowego procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="250de-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="250de-144">Zmień **Uruchom jako** z **domyślne** do **niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="250de-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="250de-145">Wybierz poświadczenie, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="250de-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="250de-146">Konto Uruchom jako automatyzacji</span><span class="sxs-lookup"><span data-stu-id="250de-146">Automation Run As account</span></span>
<span data-ttu-id="250de-147">W ramach procesu kompilacji automatycznego wdrażania zasobów na platformie Azure mogą wymagać dostępu do lokalnego systemów do obsługi zadań lub zestaw kroków w sekwencji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="250de-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="250de-148">Do obsługi uwierzytelniania przy użyciu konta Uruchom jako platformy Azure, należy zainstalować certyfikat konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="250de-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="250de-149">Następujący element runbook programu PowerShell *RunAsCertificateToHybridWorker eksportu*, umożliwia wyeksportowanie certyfikatu uruchom jako z konta usługi Automatyzacja Azure i pliki do pobrania i zaimportowanie go do magazynu certyfikatów komputera lokalnego na hybrydowy proces roboczy podłączony do tego samego konta.</span><span class="sxs-lookup"><span data-stu-id="250de-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="250de-150">Po ukończeniu tego kroku sprawdza to, czy Proces roboczy może pomyślnie wykonać uwierzytelnienia na platformie Azure przy użyciu konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="250de-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="250de-151">Zapisz *RunAsCertificateToHybridWorker eksportu* runbook na komputerze z `.ps1` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="250de-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="250de-152">Zaimportuj go do Twojego konta automatyzacji i edytować element runbook, zmiana wartości zmiennej `$Password` z własnego hasła.</span><span class="sxs-lookup"><span data-stu-id="250de-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="250de-153">Publikowanie, a następnie uruchom korzystających z uwierzytelniania przy użyciu konta Uruchom jako elementy runbook, które grupy hybrydowego procesu roboczego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="250de-154">Strumień zadań zgłasza próba zaimportowania certyfikatu w magazynie komputera lokalnego i jest zgodny z wielu wierszy w zależności od liczby kont automatyzacji są zdefiniowane w ramach subskrypcji i jeśli uwierzytelnianie zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="250de-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="250de-155">Rozwiązywanie problemów z elementów runbook na hybrydowy proces roboczy elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="250de-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="250de-156">Dzienniki są przechowywane lokalnie na każdym hybrydowy proces roboczy na C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="250de-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="250de-157">Hybrydowy proces roboczy rejestruje także błędów i zdarzeń w dzienniku zdarzeń systemu Windows w obszarze **aplikacji i usług Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="250de-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="250de-158">Zdarzenia związane z elementami runbook wykonywane w procesie roboczym są zapisywane w **aplikacji i usług Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="250de-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="250de-159">**Microsoft SMA** dziennika zawiera wiele więcej zdarzeń związanych z zadania elementu runbook do elementu roboczego i przetwarzania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="250de-160">Gdy **automatyzacji Microsoft** dziennika zdarzeń nie ma wiele zdarzeń ze szczegółami pomoc w rozwiązywaniu problemów z wykonanie elementu runbook, można znaleźć co najmniej wyniki zadania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="250de-161">[Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md) są wysyłane do usługi Automatyzacja Azure z hybrydowych procesów roboczych, podobnie jak zadania elementów runbook działają w chmurze.</span><span class="sxs-lookup"><span data-stu-id="250de-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="250de-162">Można również włączyć pełne i postępu strumienie tak samo jak dla innych elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="250de-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="250de-163">Jeśli elementy runbook nie są pomyślnie wykonywane zadanie podsumowania przedstawia stan **zawieszone**, przejrzyj artykuł dotyczący rozwiązywania problemów [hybrydowy proces roboczy elementu Runbook: kończy zadanie elementu runbook o stanie Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="250de-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="250de-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="250de-164">Next steps</span></span>
* <span data-ttu-id="250de-165">Aby dowiedzieć się więcej na temat różnych metod, które mogą służyć do uruchamiania elementu runbook, zobacz [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="250de-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="250de-166">Aby poznać różne procedury dotyczące pracy z elementami runbook programu PowerShell i przepływ pracy programu PowerShell w automatyzacji Azure za pomocą edytor tekstowy, zobacz [edytowanie elementu Runbook automatyzacji Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="250de-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>