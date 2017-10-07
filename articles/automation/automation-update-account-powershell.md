---
title: "aaaCreate automatyzacji konta Uruchom jako Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooupgrade Twojego konta automatyzacji z hello toocreate programu PowerShell, Uruchom jako konta Jeśli podczas tworzenia początkowej z portalu hello nie wykonał w tym kroku."
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
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="13fbb-103">Aktualizacja konta Uruchom jako usługi Automation przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="13fbb-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="13fbb-104">Możesz za pomocą programu PowerShell tooupdate istniejącego konta automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="13fbb-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="13fbb-105">Utwórz konto usługi Automatyzacja, ale odrzucić konta Uruchom jako hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="13fbb-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="13fbb-106">Zasoby usługi Resource Manager toomanage konto automatyzacji jest już używana, i chcesz tooupdate hello konta tooinclude hello konta Uruchom jako dla uwierzytelniania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="13fbb-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="13fbb-107">Używasz toomanage konta automatyzacji dla zasoby klasyczne i chcesz tooupdate go hello toouse konta w klasycznym Uruchom jako, zamiast tworzenia nowego konta i migrację z tooit elementy runbook i zasoby.</span><span class="sxs-lookup"><span data-stu-id="13fbb-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="13fbb-108">Ma toocreate Uruchom jako, a konto klasycznego Uruchom jako za pomocą certyfikatu wystawionego przez urząd certyfikacji (CA) przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="13fbb-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13fbb-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13fbb-109">Prerequisites</span></span>

* <span data-ttu-id="13fbb-110">skrypt Hello można uruchomić tylko w systemie Windows 10 i Windows Server 2016 z modułami usługi Azure Resource Manager 2.01 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="13fbb-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="13fbb-111">Nie jest obsługiwany przez wcześniejsze wersje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="13fbb-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="13fbb-112">Program Azure PowerShell 1.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="13fbb-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="13fbb-113">Aby uzyskać informacje o wersji hello PowerShell 1.0, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="13fbb-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="13fbb-114">Konto automatyzacji, który jest określany jako wartość hello hello *— AutomationAccountName* i *- ApplicationDisplayName* parametrów w hello następującego skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13fbb-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="13fbb-115">wartości tooget hello *SubscriptionID*, *ResourceGroup*, i *AutomationAccountName*, które są wymagane parametry hello skryptów, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13fbb-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="13fbb-116">W hello portalu Azure, wybierz konto Automatyzacja na powitania **konto automatyzacji** bloku, a następnie wybierz **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="13fbb-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="13fbb-117">Na powitania **wszystkie ustawienia** bloku, w obszarze **ustawienia konta**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="13fbb-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="13fbb-118">Należy pamiętać, wartości hello na powitania **właściwości** bloku.</span><span class="sxs-lookup"><span data-stu-id="13fbb-118">Note hello values on hello **Properties** blade.</span></span>

![Blok "Właściwości" konto automatyzacji Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="13fbb-120">Tworzenie skryptu programu PowerShell konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="13fbb-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="13fbb-121">Ten skrypt programu PowerShell obejmuje obsługę hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="13fbb-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="13fbb-122">Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="13fbb-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="13fbb-123">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="13fbb-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="13fbb-124">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="13fbb-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="13fbb-125">Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="13fbb-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="13fbb-126">W zależności od opcji konfiguracji hello wybranej hello skrypt tworzy hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="13fbb-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="13fbb-127">**W przypadku kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="13fbb-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="13fbb-128">Tworzy Azure AD aplikacji toobe wyeksportowany z obu hello z podpisem własnym lub klucz publiczny certyfikatu przedsiębiorstwa, tworzy konto główne usługi dla aplikacji hello w usłudze Azure AD i przypisuje hello roli współautora dla konta hello w bieżącym Subskrypcja.</span><span class="sxs-lookup"><span data-stu-id="13fbb-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="13fbb-129">Możesz zmienić to ustawienie tooOwner ani żadnych innych ról.</span><span class="sxs-lookup"><span data-stu-id="13fbb-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="13fbb-130">Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="13fbb-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="13fbb-131">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="13fbb-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="13fbb-132">zasób certyfikatu Hello przechowuje hello certyfikatu klucza prywatnego, który jest używany przez aplikację hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13fbb-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="13fbb-133">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="13fbb-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="13fbb-134">zasób połączenia Hello przechowuje identyfikator aplikacji hello, identyfikatora dzierżawcy, identyfikator subskrypcji i odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="13fbb-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="13fbb-135">**W przypadku klasycznych kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="13fbb-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="13fbb-136">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureClassicRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="13fbb-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="13fbb-137">zasób certyfikatu Hello zawiera klucz prywatny certyfikatu hello używane przez hello certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="13fbb-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="13fbb-138">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureClassicRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="13fbb-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="13fbb-139">zasób połączenia Hello przechowuje hello Nazwa subskrypcji, identyfikator subskrypcji i certyfikat nazwa zasobów.</span><span class="sxs-lookup"><span data-stu-id="13fbb-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="13fbb-140">Jeśli wybierzesz opcję tworzenia klasycznego konta Uruchom jako, po wykonaniu skryptu hello, przekazywanie hello publicznego zarządzania toohello (rozszerzenie nazwy pliku cer) magazynu certyfikatów dla subskrypcji hello tego konta automatyzacji hello został utworzony w.</span><span class="sxs-lookup"><span data-stu-id="13fbb-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="13fbb-141">Zapisz hello następującego skryptu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="13fbb-141">Save hello following script on your computer.</span></span> <span data-ttu-id="13fbb-142">W tym przykładzie, zapisać go z nazwą pliku hello *RunAsAccount.ps1 nowy*.</span><span class="sxs-lookup"><span data-stu-id="13fbb-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="13fbb-143">Na komputerze, należy uruchomić **programu Windows PowerShell** z hello **Start** ekranu z podwyższonym poziomem uprawnień użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13fbb-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="13fbb-144">Z hello z podwyższonym poziomem uprawnień, powłoka wiersza polecenia przejdź toohello folderu, który zawiera hello skryptu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="13fbb-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="13fbb-145">Uruchom skrypt hello przy użyciu wartości parametrów hello hello konfiguracji, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="13fbb-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="13fbb-146">**Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="13fbb-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="13fbb-147">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="13fbb-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="13fbb-148">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa**</span><span class="sxs-lookup"><span data-stu-id="13fbb-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="13fbb-149">**Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych**</span><span class="sxs-lookup"><span data-stu-id="13fbb-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="13fbb-150">Po wykonaniu skryptu hello, będzie tooauthenticate zostanie wyświetlony monit o systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="13fbb-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="13fbb-151">Zaloguj się przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="13fbb-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="13fbb-152">Po pomyślnym wykonaniu hello script należy zwrócić uwagę na następujące hello:</span><span class="sxs-lookup"><span data-stu-id="13fbb-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="13fbb-153">Jeśli utworzono konto klasycznego Uruchom jako z publicznego certyfikatu z podpisem własnym (plik cer) hello skrypt tworzy i zapisuje go toohello folder plików tymczasowych na komputerze w obszarze profil użytkownika hello *%USERPROFILE%\AppData\Local\Temp*, używany sesji programu PowerShell hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="13fbb-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="13fbb-154">Jeśli zostało utworzone klasyczne konto Uruchom jako z publicznym certyfikatem przedsiębiorstwa (plik CER), użyj tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="13fbb-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="13fbb-155">Wykonaj instrukcje hello [przekazywania toohello certyfikat interfejsu API zarządzania klasycznego portalu Azure](../azure-api-management-certs.md), a następnie sprawdź poprawność konfiguracji poświadczeń hello o zasoby klasyczne wdrożenia przy użyciu hello [przykładowy kod tooauthenticate z zasobów wdrożenia klasycznego Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="13fbb-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="13fbb-156">Jeśli tak, *nie* Utwórz konto klasycznego Uruchom jako, uwierzytelniania za pomocą zasoby usługi Resource Manager i sprawdzić poprawność konfiguracji poświadczeń hello przy użyciu hello [przykładowy kod w celu uwierzytelniania z usługi zarządzania zasoby](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="13fbb-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13fbb-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13fbb-157">Next steps</span></span>
* <span data-ttu-id="13fbb-158">Aby uzyskać więcej informacji na temat nazwy główne usług można znaleźć zbyt[obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="13fbb-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="13fbb-159">Aby uzyskać więcej informacji na temat certyfikatów i usług Azure można znaleźć zbyt[Omówienie certyfikatów dla usług w chmurze Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="13fbb-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
