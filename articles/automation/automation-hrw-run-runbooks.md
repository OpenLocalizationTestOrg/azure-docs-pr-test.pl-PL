---
title: elementy runbook aaaRun na Azure procesu roboczego Runbook automatyzacji hybrydowe | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera informacje dotyczące wykonywania elementów runbook na komputerach w lokalnym centrum danych lub dostawcy chmury z rolą hybrydowy proces roboczy elementu Runbook hello."
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
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="4d573-103">Uruchomione elementy runbook na hybrydowy proces roboczy elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="4d573-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="4d573-104">Nie ma różnic w strukturze hello elementów runbook, które są uruchamiane w automatyzacji Azure oraz te, które uruchamiane na hybrydowy proces roboczy elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="4d573-105">Elementy Runbook korzystające z każdym najprawdopodobniej różnią się znacznie jednak ponieważ elementy runbook, zwykle przeznaczonych dla hybrydowego procesu roboczego elementu Runbook zarządzanie zasobami na komputerze lokalnym hello sam lub względem zasobów w środowisku lokalnym hello, których jest wdrożona, podczas elementów runbook w automatyzacji Azure zazwyczaj zarządzać zasobami w hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="4d573-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="4d573-106">Można edytować element runbook dla hybrydowego procesu roboczego Runbook automatyzacji Azure, ale mogą mieć trudności, Jeśli spróbujesz tootest hello runbook w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="4d573-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="4d573-107">Moduły PowerShell Hello, które uzyskują dostęp do zasobów lokalnych hello może nie być zainstalowana w Twoim środowisku usługi Automatyzacja Azure w takim przypadku, hello testu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="4d573-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="4d573-108">Po zainstalowaniu hello wymagane moduły, a następnie hello element runbook zostanie uruchomiony, ale nie będą mogli tooaccess zasoby lokalne do ukończenia testu.</span><span class="sxs-lookup"><span data-stu-id="4d573-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="4d573-109">Uruchamianie elementu runbook na hybrydowy proces roboczy elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="4d573-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="4d573-110">[Uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) opisano różne metody uruchamiania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="4d573-111">Dodaje hybrydowy proces roboczy elementu Runbook **RunOn** opcja, w którym można określić nazwę hello grupy hybrydowego procesu roboczego elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="4d573-112">Jeśli określono grupę hello runbook jest pobierane i wykonywane przez pracowników hello w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="4d573-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="4d573-113">Jeśli ta opcja nie jest określona, następnie jest uruchamiany w automatyzacji Azure normalnie.</span><span class="sxs-lookup"><span data-stu-id="4d573-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="4d573-114">Po uruchomieniu elementu runbook w portalu Azure hello prezentowany **Uruchom na** opcja, w którym można wybrać **Azure** lub **hybrydowy proces roboczy**.</span><span class="sxs-lookup"><span data-stu-id="4d573-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="4d573-115">W przypadku wybrania **hybrydowy proces roboczy**, hello grupy można wybrać z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="4d573-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="4d573-116">Użyj hello **RunOn** parametru.</span><span class="sxs-lookup"><span data-stu-id="4d573-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="4d573-117">Możesz użyć hello następujące polecenia toostart elementu runbook o nazwie Test-Runbook na hybrydowego grupy procesów roboczych elementu Runbook o nazwie MyHybridGroup przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d573-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="4d573-118">Witaj **RunOn** parametru dodano toohello **Start AzureAutomationRunbook** polecenia cmdlet w wersji od 0.9.1 Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d573-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="4d573-119">Należy [pobrać najnowszą wersję hello](https://azure.microsoft.com/downloads/) Jeśli masz wcześniejszą zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="4d573-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="4d573-120">Wystarczy tooinstall tej wersji stacji roboczej, na którym jest uruchamiany hello elementu runbook z programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d573-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="4d573-121">Nie trzeba tooinstall go na komputerze pracownika hello o ile nie mają elementów runbook toostart z tego komputera.</span><span class="sxs-lookup"><span data-stu-id="4d573-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="4d573-122">Obecnie nie można uruchomić elementu runbook na hybrydowy proces roboczy elementu Runbook z innego elementu runbook, ponieważ wymagałoby to hello najnowszą wersję programu Azure Powershell toobe zainstalowane na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="4d573-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="4d573-123">najnowszą wersję Hello jest automatycznie aktualizowana w automatyzacji Azure i automatycznie wkrótce przesuwana toohello pracowników.</span><span class="sxs-lookup"><span data-stu-id="4d573-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="4d573-124">Uprawnienia elementów Runbook</span><span class="sxs-lookup"><span data-stu-id="4d573-124">Runbook permissions</span></span>
<span data-ttu-id="4d573-125">Elementów Runbook uruchomionych na hybrydowy proces roboczy elementu Runbook nie można Użyj hello sama metoda, która jest zazwyczaj używana w przypadku elementów runbook uwierzytelniania tooAzure zasobów, ponieważ uzyskują dostęp do zasobów poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="4d573-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="4d573-126">Hello runbook albo zapewniają własnym uwierzytelnianiem toolocal zasobów lub można określić tooprovide konta RunAs kontekstu użytkownika dla wszystkich elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="4d573-127">Uwierzytelnianie elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="4d573-127">Runbook authentication</span></span>
<span data-ttu-id="4d573-128">Domyślnie elementów runbook zostanie uruchomiony w kontekście hello hello lokalnego konta systemowego na powitania na komputerze lokalnym, więc użytkownik musi podać własne tooresources uwierzytelniania, który będzie miał dostęp.</span><span class="sxs-lookup"><span data-stu-id="4d573-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="4d573-129">Można użyć [poświadczeń](http://msdn.microsoft.com/library/dn940015.aspx) i [certyfikatu](http://msdn.microsoft.com/library/dn940013.aspx) zasoby w elemencie runbook za pomocą poleceń cmdlet, które pozwalają toospecify poświadczeń, można uwierzytelniać toodifferent zasobów.</span><span class="sxs-lookup"><span data-stu-id="4d573-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="4d573-130">Witaj poniższy przykład przedstawia części elementu runbook, który powoduje ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="4d573-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="4d573-131">Pobiera poświadczenia na podstawie nazwy zasobów i hello poświadczeń komputera hello z zasób zmiennej, a następnie używa tych wartości w poleceniu cmdlet Restart-Computer hello.</span><span class="sxs-lookup"><span data-stu-id="4d573-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="4d573-132">Można też skorzystać [InlineScript](automation-powershell-workflow.md#inlinescript), co pozwala toorun bloków kodu na innym komputerze z poświadczeń określonych przez hello [typowy parametr PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d573-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="4d573-133">Konto Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="4d573-133">RunAs account</span></span>
<span data-ttu-id="4d573-134">Zamiast zapewnienia uwierzytelniania ich własnych zasobów toolocal elementów runbook, można określić **RunAs** konto do grupy hybrydowych procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="4d573-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="4d573-135">Należy określić [zasób poświadczeń](automation-credentials.md) mający dostęp do zasobów toolocal i wszystkich elementów runbook działać w ramach tych poświadczeń, podczas uruchamiania na hybrydowy proces roboczy elementu Runbook w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="4d573-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="4d573-136">Nazwa użytkownika Hello poświadczenia hello musi być w jednym z następujących formatów hello:</span><span class="sxs-lookup"><span data-stu-id="4d573-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="4d573-137">domena azwa_użytkownika</span><span class="sxs-lookup"><span data-stu-id="4d573-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="4d573-138">Nazwa użytkownika (dla kont lokalnych toohello na komputerze lokalnym)</span><span class="sxs-lookup"><span data-stu-id="4d573-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="4d573-139">Użyj hello następujące procedury toospecify konto Uruchom jako dla grupy hybrydowych procesów roboczych:</span><span class="sxs-lookup"><span data-stu-id="4d573-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="4d573-140">Utwórz [zasób poświadczeń](automation-credentials.md) z zasobami toolocal dostępu.</span><span class="sxs-lookup"><span data-stu-id="4d573-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="4d573-141">Otwórz konto automatyzacji hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4d573-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="4d573-142">Wybierz hello **hybrydowego procesu roboczego grupy** Kafelek, a następnie wybierz grupę hello.</span><span class="sxs-lookup"><span data-stu-id="4d573-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="4d573-143">Wybierz **wszystkie ustawienia** , a następnie **ustawienia grupy hybrydowego procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="4d573-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="4d573-144">Zmień **Uruchom jako** z **domyślne** za**niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="4d573-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="4d573-145">Wybierz poświadczenie hello i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4d573-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="4d573-146">Konto Uruchom jako automatyzacji</span><span class="sxs-lookup"><span data-stu-id="4d573-146">Automation Run As account</span></span>
<span data-ttu-id="4d573-147">Jako część procesu kompilacji automatycznego wdrażania zasobów na platformie Azure może wymagać dostępu tooon lokalnych systemów toosupport zadań lub zestaw kroków w sekwencji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4d573-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="4d573-148">toosupport uwierzytelnianie na platformie Azure przy użyciu konta Uruchom jako hello, należy tooinstall hello Uruchom jako certyfikat konta.</span><span class="sxs-lookup"><span data-stu-id="4d573-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="4d573-149">Witaj, po runbook programu PowerShell *RunAsCertificateToHybridWorker eksportu*, eksportuje hello Uruchom jako certyfikat z konta usługi Automatyzacja Azure i pliki do pobrania i importuje go do magazynu certyfikatów komputera lokalnego hello na Hybrydowy proces roboczy podłączony toohello tego samego konta.</span><span class="sxs-lookup"><span data-stu-id="4d573-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="4d573-150">Po ukończeniu tego kroku sprawdza to, czy Proces roboczy hello można pomyślnie uwierzytelnić tooAzure hello konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="4d573-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

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
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="4d573-151">Zapisz hello *RunAsCertificateToHybridWorker eksportu* runbook tooyour komputera z `.ps1` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="4d573-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="4d573-152">Zaimportuj go do Twojego konta automatyzacji i edytować runbook hello, zmiana hello wartość zmiennej hello `$Password` z własnego hasła.</span><span class="sxs-lookup"><span data-stu-id="4d573-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="4d573-153">Publikowanie, a następnie uruchom element runbook hello przeznaczonych dla grupy hybrydowego procesu roboczego hello Uruchom i uwierzytelniania przy użyciu konta Uruchom jako hello elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="4d573-154">Hello zadania strumienia raporty hello próba tooimport hello certyfikat do magazynu komputer lokalny hello i jest zgodny z wielu wierszy w zależności od liczby kont automatyzacji są zdefiniowane w ramach subskrypcji i jeśli uwierzytelnianie zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4d573-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="4d573-155">Rozwiązywanie problemów z elementów runbook na hybrydowy proces roboczy elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="4d573-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="4d573-156">Dzienniki są przechowywane lokalnie na każdym hybrydowy proces roboczy na C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="4d573-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="4d573-157">Hybrydowy proces roboczy rejestruje także błędów i zdarzeń w dzienniku zdarzeń systemu Windows hello w obszarze **aplikacji i usług Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="4d573-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="4d573-158">Zdarzenia związane z toorunbooks wykonana w wątku roboczym hello są zapisywane zbyt**aplikacji i usług Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="4d573-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="4d573-159">Witaj **Microsoft SMA** dziennika zawiera wiele więcej zdarzeń powiązanych toohello runbook zadania wciśnięcia toohello procesu roboczego hello przetwarzanie i elementu hello runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="4d573-160">Podczas hello **automatyzacji Microsoft** dziennika zdarzeń nie ma wiele zdarzeń przy użyciu szczegółów z hello rozwiązywania problemów z wykonanie elementu runbook, znajduje się co najmniej wyniki hello hello zadanie elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="4d573-161">[Element Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md) są wysyłane tooAzure automatyzacji z hybrydowych procesów roboczych tylko, takich jak zadania elementu runbook są uruchamiane w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="4d573-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="4d573-162">Można również włączyć hello pełne i strumieni postępu hello sam sposób jak dla innych elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="4d573-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="4d573-163">Jeśli elementy runbook nie są pomyślnie wykonywane i hello zadanie podsumowania przedstawia stan **zawieszone**, zapoznaj się z tematem hello Rozwiązywanie problemów z artykułu [hybrydowy proces roboczy elementu Runbook: kończy zadanie elementu runbook ze stanem Zawieszone](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="4d573-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="4d573-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d573-164">Next steps</span></span>
* <span data-ttu-id="4d573-165">Zobacz toolearn więcej informacji na temat różnych metod hello, które mogą być używane toostart elementu runbook [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4d573-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="4d573-166">Zobacz toounderstand hello różne procedury do pracy z programu PowerShell i przepływ pracy programu PowerShell elementów runbook w automatyzacji Azure za pomocą hello edytor tekstowy, [edytowanie elementu Runbook automatyzacji Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="4d573-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
