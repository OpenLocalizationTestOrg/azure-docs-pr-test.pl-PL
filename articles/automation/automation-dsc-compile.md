---
title: aaaCompiling konfiguracji DSC automatyzacji Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób konfiguracji konfiguracji żądanego stanu (DSC) toocompile automatyzacji Azure."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="2bbef-103">Kompilowanie konfiguracji DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="2bbef-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="2bbef-104">Konfiguracje konfiguracji żądanego stanu (DSC) na dwa sposoby automatyzacji Azure można kompilować: w hello portalu Azure i przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bbef-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="2bbef-105">Witaj Poniższa tabela pomoże określić kiedy toouse, którego metoda oparta na powitania właściwości każdej:</span><span class="sxs-lookup"><span data-stu-id="2bbef-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="2bbef-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2bbef-106">Azure portal</span></span>

* <span data-ttu-id="2bbef-107">Najprostszą metodą z interaktywnego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="2bbef-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="2bbef-108">Wartości parametru proste tooprovide formularza</span><span class="sxs-lookup"><span data-stu-id="2bbef-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="2bbef-109">Łatwo śledzić stan zadania</span><span class="sxs-lookup"><span data-stu-id="2bbef-109">Easily track job state</span></span>
* <span data-ttu-id="2bbef-110">Dostęp uwierzytelniony dzięki funkcji logowania do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2bbef-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="2bbef-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bbef-111">Windows PowerShell</span></span>

* <span data-ttu-id="2bbef-112">Wywoływanie z wiersza polecenia za pomocą poleceń cmdlet środowiska Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bbef-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="2bbef-113">Może być uwzględniony w zautomatyzowane rozwiązanie z wielu kroków</span><span class="sxs-lookup"><span data-stu-id="2bbef-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="2bbef-114">Podaj wartości parametrów proste i złożone</span><span class="sxs-lookup"><span data-stu-id="2bbef-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="2bbef-115">Śledź stan zadania</span><span class="sxs-lookup"><span data-stu-id="2bbef-115">Track job state</span></span>
* <span data-ttu-id="2bbef-116">Toosupport klienta wymaganych poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bbef-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="2bbef-117">ConfigurationData — dostęp próbny</span><span class="sxs-lookup"><span data-stu-id="2bbef-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="2bbef-118">Kompiluj konfiguracje, które używają poświadczeń</span><span class="sxs-lookup"><span data-stu-id="2bbef-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="2bbef-119">Po podjęciu decyzji dotyczącej Metoda kompilacji, można użyć odpowiednich procedur hello poniżej toostart kompilowanie.</span><span class="sxs-lookup"><span data-stu-id="2bbef-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="2bbef-120">Kompilowanie Konfiguracja DSC o hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2bbef-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="2bbef-121">Twoje konto usługi Automatyzacja kliknij **konfiguracji DSC**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="2bbef-122">Kliknij przycisk tooopen konfiguracji jego bloku.</span><span class="sxs-lookup"><span data-stu-id="2bbef-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="2bbef-123">Kliknij przycisk **skompilować**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-123">Click **Compile**.</span></span>
4. <span data-ttu-id="2bbef-124">W przypadku konfiguracji hello nie ma parametrów, będzie zostanie wyświetlony monit o tooconfirm czy toocompile go.</span><span class="sxs-lookup"><span data-stu-id="2bbef-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="2bbef-125">Jeśli konfiguracja hello ma parametry, hello **skompilować konfiguracji** zostanie otwarty blok, więc można podać wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="2bbef-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="2bbef-126">Zobacz hello [ **podstawowe parametry** ](#basic-parameters) sekcji poniżej, aby uzyskać więcej informacji o parametrach.</span><span class="sxs-lookup"><span data-stu-id="2bbef-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="2bbef-127">Witaj **zadania kompilacji** bloku jest otwarty, dzięki czemu można śledzić stan zadania kompilacji hello i hello konfiguracje węzłów (MOF konfiguracji dokumenty) powodowała ona toobe umieszczane na powitania serwera ściągania usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbef-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="2bbef-128">Kompilowanie konfiguracji DSC, przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bbef-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="2bbef-129">Można użyć [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart kompilowania przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bbef-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="2bbef-130">powitania po przykładowy kod uruchamia kompilacji konfiguracji DSC o nazwie **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="2bbef-131">`Start-AzureRmAutomationDscCompilationJob`Zwraca wartość typu kompilacji zadania obiektów, których można używać tootrack jego stan.</span><span class="sxs-lookup"><span data-stu-id="2bbef-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="2bbef-132">Następnie można użyć tego obiektu zadania kompilacji [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello stan zadania kompilacji hello, i [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview jego strumieni (dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="2bbef-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="2bbef-133">powitania po przykładowy kod uruchamia kompilacji hello **SampleConfig** konfiguracji, czeka, dopóki nie zostało ukończone, a następnie wyświetla jego strumieni.</span><span class="sxs-lookup"><span data-stu-id="2bbef-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="2bbef-134">Podstawowe parametry</span><span class="sxs-lookup"><span data-stu-id="2bbef-134">Basic Parameters</span></span>
<span data-ttu-id="2bbef-135">Deklaracji parametru w konfiguracji DSC, w tym typy parametrów i właściwości działania hello takie same jak elementy runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbef-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="2bbef-136">Zobacz [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) toolearn więcej informacji na temat parametrów elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="2bbef-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="2bbef-137">Witaj poniższy przykład korzysta z dwóch parametrów o nazwie **FeatureName** i **IsPresent**, toodetermine hello wartości właściwości w hello **ParametersExample.sample** węzła Konfiguracja generowanych podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2bbef-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="2bbef-138">Można skompilować konfiguracji DSC, używanego podstawowych parametrów w portalu usługi Konfiguracja DSC automatyzacji Azure hello lub przy użyciu programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2bbef-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="2bbef-139">Portal</span><span class="sxs-lookup"><span data-stu-id="2bbef-139">Portal</span></span>

<span data-ttu-id="2bbef-140">W portalu hello można wprowadzić wartości parametrów po kliknięciu przycisku **skompilować**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![tekst alternatywny](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="2bbef-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bbef-142">PowerShell</span></span>

<span data-ttu-id="2bbef-143">PowerShell wymaga parametrów w [hashtable](http://technet.microsoft.com/library/hh847780.aspx) gdzie klucz hello odpowiada nazwie parametru hello i hello jest równa wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="2bbef-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="2bbef-144">Aby dowiedzieć się, jak przekazywanie PSCredentials jako parametrów, zobacz <a href="#credential-assets"> **zasoby poświadczeń** </a> poniżej.</span><span class="sxs-lookup"><span data-stu-id="2bbef-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="2bbef-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="2bbef-145">ConfigurationData</span></span>
<span data-ttu-id="2bbef-146">**ConfigurationData** pozwala tooseparate strukturalnych konfiguracji z dowolnym środowisku określonej konfiguracji podczas korzystania z usługi Konfiguracja DSC środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bbef-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="2bbef-147">Zobacz [oddzielenie "Co" od "Where" w konfiguracji DSC środowiska PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn więcej informacji na temat **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="2bbef-148">Można użyć **ConfigurationData** podczas kompilowania w konfiguracji DSC automatyzacji Azure przy użyciu programu Azure PowerShell, ale nie w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbef-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="2bbef-149">Witaj następującej konfiguracji DSC przykład używa **ConfigurationData** za pośrednictwem hello **$ConfigurationData** i **$AllNodes** słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="2bbef-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="2bbef-150">Należy również hello [ **xWebAdministration** modułu](https://www.powershellgallery.com/packages/xWebAdministration/) w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="2bbef-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="2bbef-151">Można skompilować konfiguracji DSC hello powyżej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bbef-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="2bbef-152">Witaj poniżej PowerShell dodaje dwie toohello konfiguracji węzła serwera ściągania usługi Konfiguracja DSC automatyzacji Azure: **ConfigurationDataSample.MyVM1** i **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="2bbef-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="2bbef-153">Elementy zawartości</span><span class="sxs-lookup"><span data-stu-id="2bbef-153">Assets</span></span>

<span data-ttu-id="2bbef-154">Odwołania do zasobów są hello tej samej konfiguracji DSC automatyzacji Azure i elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="2bbef-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="2bbef-155">Zobacz hello poniżej, aby uzyskać więcej informacji:</span><span class="sxs-lookup"><span data-stu-id="2bbef-155">See hello following for more information:</span></span>

* [<span data-ttu-id="2bbef-156">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="2bbef-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="2bbef-157">Połączenia</span><span class="sxs-lookup"><span data-stu-id="2bbef-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="2bbef-158">Poświadczenia</span><span class="sxs-lookup"><span data-stu-id="2bbef-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="2bbef-159">Zmienne</span><span class="sxs-lookup"><span data-stu-id="2bbef-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="2bbef-160">Zasoby poświadczeń</span><span class="sxs-lookup"><span data-stu-id="2bbef-160">Credential Assets</span></span>

<span data-ttu-id="2bbef-161">Podczas konfiguracji DSC automatyzacji Azure mogą odwoływać się zasoby poświadczeń przy użyciu **Get-AzureRmAutomationCredential**, zasoby poświadczeń może również zostać przekazane za za pomocą parametrów, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2bbef-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="2bbef-162">Jeśli konfiguracja przyjmuje parametr **PSCredential** wpisz, a następnie potrzebna nazwa ciąg hello toopass zasób poświadczenia usługi Automatyzacja Azure jako wartość tego parametru, a nie obiektu PSCredential.</span><span class="sxs-lookup"><span data-stu-id="2bbef-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="2bbef-163">Tle hello zasób poświadczenia usługi Automatyzacja Azure hello o tej nazwie zostanie pobrana i przekazany toohello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2bbef-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="2bbef-164">Przechowywanie poświadczeń zabezpieczone w konfiguracji węzłów (MOF konfiguracji dokumenty) wymaga szyfrowania poświadczeń hello w pliku MOF konfiguracji węzła hello.</span><span class="sxs-lookup"><span data-stu-id="2bbef-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="2bbef-165">Automatyzacja Azure dalsze przyjmuje jednym kroku i szyfruje hello całego pliku MOF.</span><span class="sxs-lookup"><span data-stu-id="2bbef-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="2bbef-166">Jednak obecnie musi wskazujemy DSC środowiska PowerShell szkodzi dla poświadczeń toobe wyjściowych w postaci zwykłego tekstu podczas generowania MOF konfiguracji węzła, ponieważ DSC programu PowerShell nie może ustalić, czy usługi Automatyzacja Azure będzie szyfrowania całego pliku MOF powitania po jego Generowanie za pomocą zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2bbef-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="2bbef-167">Można określić DSC środowiska PowerShell jest poprawny dla poświadczeń toobe wyjściowych w postaci zwykłego tekstu w konfiguracji węzła hello wygenerowane za pomocą [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="2bbef-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="2bbef-168">Należy przekazać `PSDscAllowPlainTextPassword = $true` za pośrednictwem **ConfigurationData** dla każdego węzła bloku, którego nazwa występującego w konfiguracji hello DSC i używa poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2bbef-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="2bbef-169">Witaj poniższy przykład przedstawia konfiguracji DSC, która używa zasób poświadczenia usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="2bbef-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="2bbef-170">Można skompilować konfiguracji DSC hello powyżej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bbef-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="2bbef-171">Witaj poniżej PowerShell dodaje dwie toohello konfiguracji węzła serwera ściągania usługi Konfiguracja DSC automatyzacji Azure: **CredentialSample.MyVM1** i **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="2bbef-172">Importowanie konfiguracji węzła</span><span class="sxs-lookup"><span data-stu-id="2bbef-172">Importing node configurations</span></span>

<span data-ttu-id="2bbef-173">Możesz również zaimportować configuratons węzła (za), który ma być kompilowana poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbef-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="2bbef-174">Jedną z zalet tego jest może być podpisana confiturations tego węzła.</span><span class="sxs-lookup"><span data-stu-id="2bbef-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="2bbef-175">Konfiguracja węzła podpisem jest weryfikowany lokalnie w węźle zarządzanym przez agenta hello DSC, zapewnienie, że są stosowane toohello węzła konfiguracji hello pochodzi z autoryzowanego źródła.</span><span class="sxs-lookup"><span data-stu-id="2bbef-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="2bbef-176">Można użyć importu podpisany konfiguracji do konta usługi Automatyzacja Azure, ale automatyzacji Azure nie obsługuje obecnie kompilowanie konfiguracje podpisem.</span><span class="sxs-lookup"><span data-stu-id="2bbef-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="2bbef-177">Plik konfiguracji węzła nie może być większa niż 1 MB tooallow go zaimportować do usługi Automatyzacja Azure toobe.</span><span class="sxs-lookup"><span data-stu-id="2bbef-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="2bbef-178">Aby dowiedzieć się jak konfiguracje węzłów toosign na https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="2bbef-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="2bbef-179">Importowanie konfiguracji węzła, w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="2bbef-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="2bbef-180">Twoje konto usługi Automatyzacja kliknij **konfiguracji węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Konfiguracje węzłów DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="2bbef-182">W hello **konfiguracji węzłów DSC** bloku, kliknij przycisk **dodać NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="2bbef-183">W hello **importu** bloku, kliknij hello folderu ikona dalej toohello **pliku konfiguracji węzła** toobrowse pole tekstowe dla pliku konfiguracji węzła (MOF) na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2bbef-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Przeglądaj w poszukiwaniu pliku lokalnego](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="2bbef-185">Wprowadź nazwę w hello **Nazwa konfiguracji** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="2bbef-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="2bbef-186">Ta nazwa musi odpowiadać nazwie hello hello konfiguracji, z którego został skompilowany hello konfiguracji węzła.</span><span class="sxs-lookup"><span data-stu-id="2bbef-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="2bbef-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bbef-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="2bbef-188">Importowanie konfiguracji węzła, przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bbef-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="2bbef-189">Można użyć hello [AzureRmAutomationDscNodeConfiguration importu](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport polecenia cmdlet konfiguracji węzła, na koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="2bbef-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



