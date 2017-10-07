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
# <a name="update-automation-run-as-account-using-powershell"></a>Aktualizacja konta Uruchom jako usługi Automation przy użyciu programu PowerShell
Możesz za pomocą programu PowerShell tooupdate istniejącego konta automatyzacji:

* Utwórz konto usługi Automatyzacja, ale odrzucić konta Uruchom jako hello toocreate.
* Zasoby usługi Resource Manager toomanage konto automatyzacji jest już używana, i chcesz tooupdate hello konta tooinclude hello konta Uruchom jako dla uwierzytelniania elementu runbook.
* Używasz toomanage konta automatyzacji dla zasoby klasyczne i chcesz tooupdate go hello toouse konta w klasycznym Uruchom jako, zamiast tworzenia nowego konta i migrację z tooit elementy runbook i zasoby.   
* Ma toocreate Uruchom jako, a konto klasycznego Uruchom jako za pomocą certyfikatu wystawionego przez urząd certyfikacji (CA) przedsiębiorstwa.

## <a name="prerequisites"></a>Wymagania wstępne

* skrypt Hello można uruchomić tylko w systemie Windows 10 i Windows Server 2016 z modułami usługi Azure Resource Manager 2.01 lub nowszy. Nie jest obsługiwany przez wcześniejsze wersje systemu Windows.
* Program Azure PowerShell 1.0 lub nowszy. Aby uzyskać informacje o wersji hello PowerShell 1.0, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Konto automatyzacji, który jest określany jako wartość hello hello *— AutomationAccountName* i *- ApplicationDisplayName* parametrów w hello następującego skryptu programu PowerShell.

wartości tooget hello *SubscriptionID*, *ResourceGroup*, i *AutomationAccountName*, które są wymagane parametry hello skryptów, hello następujące:
1. W hello portalu Azure, wybierz konto Automatyzacja na powitania **konto automatyzacji** bloku, a następnie wybierz **wszystkie ustawienia**. 
2. Na powitania **wszystkie ustawienia** bloku, w obszarze **ustawienia konta**, wybierz pozycję **właściwości**. 
3. Należy pamiętać, wartości hello na powitania **właściwości** bloku.

![Blok "Właściwości" konto automatyzacji Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a>Tworzenie skryptu programu PowerShell konta Uruchom jako
Ten skrypt programu PowerShell obejmuje obsługę hello następujące konfiguracje:

* Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.
* Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.
* Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa.
* Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych.

W zależności od opcji konfiguracji hello wybranej hello skrypt tworzy hello następujące elementy.

**W przypadku kont Uruchom jako:**

* Tworzy Azure AD aplikacji toobe wyeksportowany z obu hello z podpisem własnym lub klucz publiczny certyfikatu przedsiębiorstwa, tworzy konto główne usługi dla aplikacji hello w usłudze Azure AD i przypisuje hello roli współautora dla konta hello w bieżącym Subskrypcja. Możesz zmienić to ustawienie tooOwner ani żadnych innych ról. Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).
* Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureRunAsCertificate* hello określono konto automatyzacji. zasób certyfikatu Hello przechowuje hello certyfikatu klucza prywatnego, który jest używany przez aplikację hello Azure AD.
* Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureRunAsConnection* hello określono konto automatyzacji. zasób połączenia Hello przechowuje identyfikator aplikacji hello, identyfikatora dzierżawcy, identyfikator subskrypcji i odcisk palca certyfikatu.

**W przypadku klasycznych kont Uruchom jako:**

* Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureClassicRunAsCertificate* hello określono konto automatyzacji. zasób certyfikatu Hello zawiera klucz prywatny certyfikatu hello używane przez hello certyfikat zarządzania.
* Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureClassicRunAsConnection* hello określono konto automatyzacji. zasób połączenia Hello przechowuje hello Nazwa subskrypcji, identyfikator subskrypcji i certyfikat nazwa zasobów.

>[!NOTE]
> Jeśli wybierzesz opcję tworzenia klasycznego konta Uruchom jako, po wykonaniu skryptu hello, przekazywanie hello publicznego zarządzania toohello (rozszerzenie nazwy pliku cer) magazynu certyfikatów dla subskrypcji hello tego konta automatyzacji hello został utworzony w.
> 

1. Zapisz hello następującego skryptu na komputerze. W tym przykładzie, zapisać go z nazwą pliku hello *RunAsAccount.ps1 nowy*.

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

2. Na komputerze, należy uruchomić **programu Windows PowerShell** z hello **Start** ekranu z podwyższonym poziomem uprawnień użytkownika.
3. Z hello z podwyższonym poziomem uprawnień, powłoka wiersza polecenia przejdź toohello folderu, który zawiera hello skryptu, który został utworzony w kroku 1.  
4. Uruchom skrypt hello przy użyciu wartości parametrów hello hello konfiguracji, które są wymagane.

    **Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Po wykonaniu skryptu hello, będzie tooauthenticate zostanie wyświetlony monit o systemie Azure. Zaloguj się przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello.
    >
    >

Po pomyślnym wykonaniu hello script należy zwrócić uwagę na następujące hello:
* Jeśli utworzono konto klasycznego Uruchom jako z publicznego certyfikatu z podpisem własnym (plik cer) hello skrypt tworzy i zapisuje go toohello folder plików tymczasowych na komputerze w obszarze profil użytkownika hello *%USERPROFILE%\AppData\Local\Temp*, używany sesji programu PowerShell hello tooexecute.
* Jeśli zostało utworzone klasyczne konto Uruchom jako z publicznym certyfikatem przedsiębiorstwa (plik CER), użyj tego certyfikatu. Wykonaj instrukcje hello [przekazywania toohello certyfikat interfejsu API zarządzania klasycznego portalu Azure](../azure-api-management-certs.md), a następnie sprawdź poprawność konfiguracji poświadczeń hello o zasoby klasyczne wdrożenia przy użyciu hello [przykładowy kod tooauthenticate z zasobów wdrożenia klasycznego Azure](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Jeśli tak, *nie* Utwórz konto klasycznego Uruchom jako, uwierzytelniania za pomocą zasoby usługi Resource Manager i sprawdzić poprawność konfiguracji poświadczeń hello przy użyciu hello [przykładowy kod w celu uwierzytelniania z usługi zarządzania zasoby](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat nazwy główne usług można znaleźć zbyt[obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).
* Aby uzyskać więcej informacji na temat certyfikatów i usług Azure można znaleźć zbyt[Omówienie certyfikatów dla usług w chmurze Azure](../cloud-services/cloud-services-certs-create.md).
