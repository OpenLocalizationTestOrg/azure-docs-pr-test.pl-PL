---
title: "tożsamość aaaCreate dla aplikacji platformy Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse programu Azure PowerShell toocreate aplikację usługi Azure Active Directory i nazwy głównej usługi i przyznać dostęp do tooresources za pomocą dostępu opartej na rolach kontroli. Widoczny jest sposób tooauthenticate aplikacji za pomocą hasła lub certyfikatu."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi

Gdy aplikacja lub skrypt, który wymaga tooaccess zasobów, można skonfigurować tożsamości dla aplikacji hello i uwierzytelniania aplikacji hello z własne poświadczenia. Ta tożsamość jest określany jako nazwy głównej usługi. Takie podejście umożliwia:

* Przypisz uprawnienia toohello tożsamości aplikacji, które są inne niż własnych uprawnień. Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.
* Użyj certyfikatu do uwierzytelnienia, podczas wykonywania skryptu instalacji nienadzorowanej.

W tym temacie opisano sposób toouse [programu Azure PowerShell](/powershell/azure/overview) tooset się wszystkie elementy potrzebne do toorun aplikacji w ramach własnej poświadczeń i tożsamości.

## <a name="required-permissions"></a>Wymagane uprawnienia
toocomplete tego tematu, należy posiadać odpowiednie uprawnienia w usłudze Azure Active Directory i Twojej subskrypcji platformy Azure. W szczególności muszą być stanie toocreate aplikację w hello Azure Active Directory i przypisz rolę tooa główna usługi hello. 

Hello jest czy Twoje konto ma odpowiednie uprawnienia za pośrednictwem portalu hello najprostszym toocheck sposób. Zobacz [, czy wymagane uprawnienia](resource-group-create-service-principal-portal.md#required-permissions).

Rozpoczęta tooa sekcji w celu uwierzytelniania z:

* [hasło](#create-service-principal-with-password)
* [certyfikat z podpisem własnym](#create-service-principal-with-self-signed-certificate)
* [certyfikat od urzędu certyfikacji](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Polecenia programu PowerShell

tooset się nazwy głównej usługi, należy użyć:

| Polecenie | Opis |
| ------- | ----------- | 
| [Nowe AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Tworzy nazwę główną usługi Azure Active Directory |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Przypisuje hello określony RBAC roli toohello określony podmiot zabezpieczeń, na powitania określony zakres. |


## <a name="create-service-principal-with-password"></a>Tworzenie nazwy głównej usługi z hasłem

toocreate Użyj nazwy głównej usługi z hello roli współautora dla Twojej subskrypcji: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

przykład Witaj zostanie uśpiony na 20 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."

Hello poniższy skrypt pozwala toospecify zakresu innego niż hello domyślne subskrypcji, oraz liczbę ponownych prób hello przypisania roli, jeśli wystąpi błąd:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Kilka elementów toonote dotyczące skryptu hello:

* toogrant hello tożsamości dostępu toohello Domyślna subskrypcja nie ma potrzeby tooprovide ResourceGroup lub SubscriptionId parametrów.
* Parametr hello ResourceGroup tylko wtedy, gdy chcesz toolimit hello zakres grupy zasobów tooa przypisania roli hello.
*  W tym przykładzie możesz dodać roli współautora toohello główna usługi hello. Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).
* skrypt Hello zostanie uśpiony na 15 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."
* Jeśli potrzebujesz toogrant hello usługi głównej dostępu toomore subskrypcji lub grupy zasobów, uruchom hello `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.


### <a name="provide-credentials-through-powershell"></a>Podaj poświadczenia, za pomocą programu PowerShell
Teraz należy toolog w jako operacji tooperform aplikacji hello. Dla nazwy użytkownika hello, użyj hello `ApplicationId` utworzonej dla aplikacji hello. Hello hasła należy użyć hello jedną określone podczas tworzenia konta hello. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

Hello identyfikator dzierżawcy nie jest liter, dlatego można ją osadzić bezpośrednio w skrypcie. Identyfikator dzierżawy hello tooretrieve, należy użyć:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Tworzenie nazwy głównej usługi o certyfikat z podpisem własnym

toocreate Użyj nazwy głównej usługi o certyfikat z podpisem własnym i hello roli współautora dla Twojej subskrypcji: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

przykład Witaj zostanie uśpiony na 20 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."

Hello poniższy skrypt pozwala toospecify zakresu innego niż hello domyślne subskrypcji, oraz liczbę ponownych prób hello przypisania roli, jeśli wystąpi błąd. Musi mieć Azure PowerShell 2.0 w systemie Windows 10 lub Windows Server 2016.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Kilka elementów toonote dotyczące skryptu hello:

* toogrant hello tożsamości dostępu toohello Domyślna subskrypcja nie ma potrzeby tooprovide ResourceGroup lub SubscriptionId parametrów.
* Parametr hello ResourceGroup tylko wtedy, gdy chcesz toolimit hello zakres grupy zasobów tooa przypisania roli hello.
* W tym przykładzie możesz dodać roli współautora toohello główna usługi hello. Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).
* skrypt Hello zostanie uśpiony na 15 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."
* Jeśli potrzebujesz toogrant hello usługi głównej dostępu toomore subskrypcji lub grupy zasobów, uruchom hello `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.

Jeśli użytkownik **bez zainstalowanego systemu Windows 10 lub Windows Server 2016 Technical Preview**, należy toodownload hello [generator certyfikatu z podpisem własnym](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) z Microsoft Script Center. Wyodrębnij jego zawartość i zaimportuj hello polecenia cmdlet, które są potrzebne.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
W skrypcie hello Zastąp następujące dwa wiersze toogenerate hello certyfikatu hello.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Podaj certyfikat przy użyciu zautomatyzowanego skryptu PowerShell
Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD. Dzierżawa jest wystąpieniem usługi Azure Active Directory. Jeśli masz tylko jedną subskrypcję, należy użyć:

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

aplikacji Hello identyfikator i identyfikator dzierżawy nie są liter, więc można go osadzić bezpośrednio w skrypcie. Identyfikator dzierżawy hello tooretrieve, należy użyć:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Identyfikator aplikacji hello tooretrieve, należy użyć:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Tworzenie nazwy głównej usługi o certyfikat od urzędu certyfikacji
toouse certyfikat wystawiony przez urząd certyfikacji toocreate nazwy głównej usługi, hello Użyj następującego skryptu:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Kilka elementów toonote dotyczące skryptu hello:

* Dostęp jest toohello zakresie subskrypcji.
* W tym przykładzie możesz dodać roli współautora toohello główna usługi hello. Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).
* skrypt Hello zostanie uśpiony na 15 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."
* Jeśli potrzebujesz toogrant hello usługi głównej dostępu toomore subskrypcji lub grupy zasobów, uruchom hello `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.

### <a name="provide-certificate-through-automated-powershell-script"></a>Podaj certyfikat przy użyciu zautomatyzowanego skryptu PowerShell
Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD. Dzierżawa jest wystąpieniem usługi Azure Active Directory.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

aplikacji Hello identyfikator i identyfikator dzierżawy nie są liter, więc można go osadzić bezpośrednio w skrypcie. Identyfikator dzierżawy hello tooretrieve, należy użyć:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Identyfikator aplikacji hello tooretrieve, należy użyć:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Zmiana poświadczeń

toochange hello poświadczenia dla aplikacji usługi AD, albo z powodu naruszenia zabezpieczeń lub wygaśnięcia poświadczeń, użyj hello [AzureRmADAppCredential Usuń](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) i [AzureRmADAppCredential nowy](/powershell/module/azurerm.resources/new-azurermadappcredential) polecenia cmdlet.

tooremove wszystkie hello poświadczenia dla aplikacji, należy użyć:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd hasła, należy użyć:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd wartość certyfikatu, utworzyć certyfikatu z podpisem własnym, jak pokazano w tym temacie. Następnie należy użyć:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Zapisz dostępu token toosimplify logowania
tooavoid udostępnienie hello usługi głównej poświadczeń za każdym razem, gdy musi toolog w, można zapisać hello tokenu dostępu.

toouse hello bieżącego tokenu dostępu w sesji nowsze zapisać hello profilu.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Otwieranie profilu hello i przejrzyj jego zawartość. Zwróć uwagę, że zawiera on tokenu dostępu. Zamiast ręcznego zalogować się ponownie później, po prostu załadować hello profilu.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> token dostępu Hello wygasa, więc za pomocą profilu zapisanych działa tylko dla, tak długo, jak hello token jest prawidłowy.
>  

Alternatywnie można wywołać operacji REST z toolog programu PowerShell w. Z odpowiedzi uwierzytelniania hello można pobrać tokenu dostępu hello do użytku z innymi operacjami. Na przykład pobierania tokenu dostępu hello przez wywołanie operacji REST, zobacz [generowania tokenu dostępu](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Debugowanie

Mogą wystąpić następujące błędy podczas tworzenia nazwy głównej usługi hello:

* **"Authentication_Unauthorized"** lub **"subskrypcji nie znaleziono w kontekście hello".** — Został wyświetlony ten błąd, gdy Twoje konto nie ma hello [wymagane uprawnienia](#required-permissions) na hello Azure Active Directory tooregister aplikacji. Zwykle zostanie wyświetlony ten błąd, gdy tylko Administrator użytkowników w usłudze Azure Active Directory można zarejestrować aplikacji, a konto użytkownika nie jest administratorem. Poproś tooeither Twojego administratora przypisać możesz tooan rolę administratora lub tooenable użytkowników tooregister aplikacji.

* Twoje konto **"nie ma autoryzacji tooperform akcji"Microsoft.Authorization/roleAssignments/write"w zakresie"/subscriptions/ {guid}"."**  — Zostanie wyświetlony ten błąd, gdy Twoje konto nie ma wystarczających uprawnień tooassign tożsamości tooan roli. Skontaktuj się z tooadd administratora subskrypcji możesz tooUser dostępu do roli administratora.

## <a name="sample-applications"></a>Przykładowe aplikacje
Aby uzyskać informacje o zalogowanie się jako aplikacji hello za pomocą różnych platform zobacz:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe instrukcje dotyczące integrowania aplikacji na platformie Azure do zarządzania zasobami, zobacz [tooauthorization przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager hello](resource-manager-api-authentication.md).
* Aby uzyskać bardziej szczegółowy opis aplikacji i nazwy główne usług, zobacz [obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md). 
* Aby uzyskać więcej informacji na temat uwierzytelniania usługi Azure Active Directory, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić toousers, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).

