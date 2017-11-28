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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="bcee9-104">Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="bcee9-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="bcee9-105">Gdy aplikacja lub skrypt, który wymaga tooaccess zasobów, można skonfigurować tożsamości dla aplikacji hello i uwierzytelniania aplikacji hello z własne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="bcee9-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="bcee9-106">Ta tożsamość jest określany jako nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="bcee9-106">This identity is known as a service principal.</span></span> <span data-ttu-id="bcee9-107">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="bcee9-107">This approach enables you to:</span></span>

* <span data-ttu-id="bcee9-108">Przypisz uprawnienia toohello tożsamości aplikacji, które są inne niż własnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="bcee9-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="bcee9-109">Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.</span><span class="sxs-lookup"><span data-stu-id="bcee9-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="bcee9-110">Użyj certyfikatu do uwierzytelnienia, podczas wykonywania skryptu instalacji nienadzorowanej.</span><span class="sxs-lookup"><span data-stu-id="bcee9-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="bcee9-111">W tym temacie opisano sposób toouse [programu Azure PowerShell](/powershell/azure/overview) tooset się wszystkie elementy potrzebne do toorun aplikacji w ramach własnej poświadczeń i tożsamości.</span><span class="sxs-lookup"><span data-stu-id="bcee9-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="bcee9-112">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="bcee9-112">Required permissions</span></span>
<span data-ttu-id="bcee9-113">toocomplete tego tematu, należy posiadać odpowiednie uprawnienia w usłudze Azure Active Directory i Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcee9-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="bcee9-114">W szczególności muszą być stanie toocreate aplikację w hello Azure Active Directory i przypisz rolę tooa główna usługi hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="bcee9-115">Hello jest czy Twoje konto ma odpowiednie uprawnienia za pośrednictwem portalu hello najprostszym toocheck sposób.</span><span class="sxs-lookup"><span data-stu-id="bcee9-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="bcee9-116">Zobacz [, czy wymagane uprawnienia](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="bcee9-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="bcee9-117">Rozpoczęta tooa sekcji w celu uwierzytelniania z:</span><span class="sxs-lookup"><span data-stu-id="bcee9-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="bcee9-118">hasło</span><span class="sxs-lookup"><span data-stu-id="bcee9-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="bcee9-119">certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="bcee9-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="bcee9-120">certyfikat od urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="bcee9-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="bcee9-121">Polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcee9-121">PowerShell commands</span></span>

<span data-ttu-id="bcee9-122">tooset się nazwy głównej usługi, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="bcee9-123">Polecenie</span><span class="sxs-lookup"><span data-stu-id="bcee9-123">Command</span></span> | <span data-ttu-id="bcee9-124">Opis</span><span class="sxs-lookup"><span data-stu-id="bcee9-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="bcee9-125">Nowe AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="bcee9-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="bcee9-126">Tworzy nazwę główną usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bcee9-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="bcee9-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="bcee9-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="bcee9-128">Przypisuje hello określony RBAC roli toohello określony podmiot zabezpieczeń, na powitania określony zakres.</span><span class="sxs-lookup"><span data-stu-id="bcee9-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="bcee9-129">Tworzenie nazwy głównej usługi z hasłem</span><span class="sxs-lookup"><span data-stu-id="bcee9-129">Create service principal with password</span></span>

<span data-ttu-id="bcee9-130">toocreate Użyj nazwy głównej usługi z hello roli współautora dla Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="bcee9-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="bcee9-131">przykład Witaj zostanie uśpiony na 20 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="bcee9-132">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."</span><span class="sxs-lookup"><span data-stu-id="bcee9-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="bcee9-133">Hello poniższy skrypt pozwala toospecify zakresu innego niż hello domyślne subskrypcji, oraz liczbę ponownych prób hello przypisania roli, jeśli wystąpi błąd:</span><span class="sxs-lookup"><span data-stu-id="bcee9-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="bcee9-134">Kilka elementów toonote dotyczące skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="bcee9-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="bcee9-135">toogrant hello tożsamości dostępu toohello Domyślna subskrypcja nie ma potrzeby tooprovide ResourceGroup lub SubscriptionId parametrów.</span><span class="sxs-lookup"><span data-stu-id="bcee9-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="bcee9-136">Parametr hello ResourceGroup tylko wtedy, gdy chcesz toolimit hello zakres grupy zasobów tooa przypisania roli hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="bcee9-137">W tym przykładzie możesz dodać roli współautora toohello główna usługi hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="bcee9-138">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="bcee9-139">skrypt Hello zostanie uśpiony na 15 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="bcee9-140">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."</span><span class="sxs-lookup"><span data-stu-id="bcee9-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="bcee9-141">Jeśli potrzebujesz toogrant hello usługi głównej dostępu toomore subskrypcji lub grupy zasobów, uruchom hello `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.</span><span class="sxs-lookup"><span data-stu-id="bcee9-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="bcee9-142">Podaj poświadczenia, za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcee9-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="bcee9-143">Teraz należy toolog w jako operacji tooperform aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="bcee9-144">Dla nazwy użytkownika hello, użyj hello `ApplicationId` utworzonej dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="bcee9-145">Hello hasła należy użyć hello jedną określone podczas tworzenia konta hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="bcee9-146">Hello identyfikator dzierżawcy nie jest liter, dlatego można ją osadzić bezpośrednio w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="bcee9-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="bcee9-147">Identyfikator dzierżawy hello tooretrieve, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="bcee9-148">Tworzenie nazwy głównej usługi o certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="bcee9-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="bcee9-149">toocreate Użyj nazwy głównej usługi o certyfikat z podpisem własnym i hello roli współautora dla Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="bcee9-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="bcee9-150">przykład Witaj zostanie uśpiony na 20 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="bcee9-151">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."</span><span class="sxs-lookup"><span data-stu-id="bcee9-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="bcee9-152">Hello poniższy skrypt pozwala toospecify zakresu innego niż hello domyślne subskrypcji, oraz liczbę ponownych prób hello przypisania roli, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="bcee9-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="bcee9-153">Musi mieć Azure PowerShell 2.0 w systemie Windows 10 lub Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bcee9-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="bcee9-154">Kilka elementów toonote dotyczące skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="bcee9-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="bcee9-155">toogrant hello tożsamości dostępu toohello Domyślna subskrypcja nie ma potrzeby tooprovide ResourceGroup lub SubscriptionId parametrów.</span><span class="sxs-lookup"><span data-stu-id="bcee9-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="bcee9-156">Parametr hello ResourceGroup tylko wtedy, gdy chcesz toolimit hello zakres grupy zasobów tooa przypisania roli hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="bcee9-157">W tym przykładzie możesz dodać roli współautora toohello główna usługi hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="bcee9-158">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="bcee9-159">skrypt Hello zostanie uśpiony na 15 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="bcee9-160">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."</span><span class="sxs-lookup"><span data-stu-id="bcee9-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="bcee9-161">Jeśli potrzebujesz toogrant hello usługi głównej dostępu toomore subskrypcji lub grupy zasobów, uruchom hello `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.</span><span class="sxs-lookup"><span data-stu-id="bcee9-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="bcee9-162">Jeśli użytkownik **bez zainstalowanego systemu Windows 10 lub Windows Server 2016 Technical Preview**, należy toodownload hello [generator certyfikatu z podpisem własnym](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) z Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="bcee9-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="bcee9-163">Wyodrębnij jego zawartość i zaimportuj hello polecenia cmdlet, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="bcee9-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="bcee9-164">W skrypcie hello Zastąp następujące dwa wiersze toogenerate hello certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="bcee9-165">Podaj certyfikat przy użyciu zautomatyzowanego skryptu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcee9-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="bcee9-166">Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="bcee9-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="bcee9-167">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="bcee9-168">Jeśli masz tylko jedną subskrypcję, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="bcee9-169">aplikacji Hello identyfikator i identyfikator dzierżawy nie są liter, więc można go osadzić bezpośrednio w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="bcee9-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="bcee9-170">Identyfikator dzierżawy hello tooretrieve, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="bcee9-171">Identyfikator aplikacji hello tooretrieve, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="bcee9-172">Tworzenie nazwy głównej usługi o certyfikat od urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="bcee9-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="bcee9-173">toouse certyfikat wystawiony przez urząd certyfikacji toocreate nazwy głównej usługi, hello Użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="bcee9-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="bcee9-174">Kilka elementów toonote dotyczące skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="bcee9-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="bcee9-175">Dostęp jest toohello zakresie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bcee9-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="bcee9-176">W tym przykładzie możesz dodać roli współautora toohello główna usługi hello.</span><span class="sxs-lookup"><span data-stu-id="bcee9-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="bcee9-177">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="bcee9-178">skrypt Hello zostanie uśpiony na 15 sekund tooallow trochę czasu, zanim hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="bcee9-179">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu hello."</span><span class="sxs-lookup"><span data-stu-id="bcee9-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="bcee9-180">Jeśli potrzebujesz toogrant hello usługi głównej dostępu toomore subskrypcji lub grupy zasobów, uruchom hello `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.</span><span class="sxs-lookup"><span data-stu-id="bcee9-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="bcee9-181">Podaj certyfikat przy użyciu zautomatyzowanego skryptu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcee9-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="bcee9-182">Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="bcee9-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="bcee9-183">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bcee9-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="bcee9-184">aplikacji Hello identyfikator i identyfikator dzierżawy nie są liter, więc można go osadzić bezpośrednio w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="bcee9-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="bcee9-185">Identyfikator dzierżawy hello tooretrieve, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="bcee9-186">Identyfikator aplikacji hello tooretrieve, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="bcee9-187">Zmiana poświadczeń</span><span class="sxs-lookup"><span data-stu-id="bcee9-187">Change credentials</span></span>

<span data-ttu-id="bcee9-188">toochange hello poświadczenia dla aplikacji usługi AD, albo z powodu naruszenia zabezpieczeń lub wygaśnięcia poświadczeń, użyj hello [AzureRmADAppCredential Usuń](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) i [AzureRmADAppCredential nowy](/powershell/module/azurerm.resources/new-azurermadappcredential) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bcee9-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="bcee9-189">tooremove wszystkie hello poświadczenia dla aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="bcee9-190">tooadd hasła, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="bcee9-191">tooadd wartość certyfikatu, utworzyć certyfikatu z podpisem własnym, jak pokazano w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="bcee9-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="bcee9-192">Następnie należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bcee9-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="bcee9-193">Zapisz dostępu token toosimplify logowania</span><span class="sxs-lookup"><span data-stu-id="bcee9-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="bcee9-194">tooavoid udostępnienie hello usługi głównej poświadczeń za każdym razem, gdy musi toolog w, można zapisać hello tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bcee9-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="bcee9-195">toouse hello bieżącego tokenu dostępu w sesji nowsze zapisać hello profilu.</span><span class="sxs-lookup"><span data-stu-id="bcee9-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="bcee9-196">Otwieranie profilu hello i przejrzyj jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="bcee9-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="bcee9-197">Zwróć uwagę, że zawiera on tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bcee9-197">Notice that it contains an access token.</span></span> <span data-ttu-id="bcee9-198">Zamiast ręcznego zalogować się ponownie później, po prostu załadować hello profilu.</span><span class="sxs-lookup"><span data-stu-id="bcee9-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="bcee9-199">token dostępu Hello wygasa, więc za pomocą profilu zapisanych działa tylko dla, tak długo, jak hello token jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="bcee9-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="bcee9-200">Alternatywnie można wywołać operacji REST z toolog programu PowerShell w.</span><span class="sxs-lookup"><span data-stu-id="bcee9-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="bcee9-201">Z odpowiedzi uwierzytelniania hello można pobrać tokenu dostępu hello do użytku z innymi operacjami.</span><span class="sxs-lookup"><span data-stu-id="bcee9-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="bcee9-202">Na przykład pobierania tokenu dostępu hello przez wywołanie operacji REST, zobacz [generowania tokenu dostępu](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="bcee9-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="bcee9-203">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="bcee9-203">Debug</span></span>

<span data-ttu-id="bcee9-204">Mogą wystąpić następujące błędy podczas tworzenia nazwy głównej usługi hello:</span><span class="sxs-lookup"><span data-stu-id="bcee9-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="bcee9-205">**"Authentication_Unauthorized"** lub **"subskrypcji nie znaleziono w kontekście hello".**</span><span class="sxs-lookup"><span data-stu-id="bcee9-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="bcee9-206">— Został wyświetlony ten błąd, gdy Twoje konto nie ma hello [wymagane uprawnienia](#required-permissions) na hello Azure Active Directory tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcee9-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="bcee9-207">Zwykle zostanie wyświetlony ten błąd, gdy tylko Administrator użytkowników w usłudze Azure Active Directory można zarejestrować aplikacji, a konto użytkownika nie jest administratorem. Poproś tooeither Twojego administratora przypisać możesz tooan rolę administratora lub tooenable użytkowników tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcee9-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="bcee9-208">Twoje konto **"nie ma autoryzacji tooperform akcji"Microsoft.Authorization/roleAssignments/write"w zakresie"/subscriptions/ {guid}"."**  — Zostanie wyświetlony ten błąd, gdy Twoje konto nie ma wystarczających uprawnień tooassign tożsamości tooan roli.</span><span class="sxs-lookup"><span data-stu-id="bcee9-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="bcee9-209">Skontaktuj się z tooadd administratora subskrypcji możesz tooUser dostępu do roli administratora.</span><span class="sxs-lookup"><span data-stu-id="bcee9-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="bcee9-210">Przykładowe aplikacje</span><span class="sxs-lookup"><span data-stu-id="bcee9-210">Sample applications</span></span>
<span data-ttu-id="bcee9-211">Aby uzyskać informacje o zalogowanie się jako aplikacji hello za pomocą różnych platform zobacz:</span><span class="sxs-lookup"><span data-stu-id="bcee9-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="bcee9-212">.NET</span><span class="sxs-lookup"><span data-stu-id="bcee9-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="bcee9-213">Java</span><span class="sxs-lookup"><span data-stu-id="bcee9-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="bcee9-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="bcee9-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="bcee9-215">Python</span><span class="sxs-lookup"><span data-stu-id="bcee9-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="bcee9-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="bcee9-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="bcee9-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcee9-217">Next steps</span></span>
* <span data-ttu-id="bcee9-218">Aby uzyskać szczegółowe instrukcje dotyczące integrowania aplikacji na platformie Azure do zarządzania zasobami, zobacz [tooauthorization przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager hello](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="bcee9-219">Aby uzyskać bardziej szczegółowy opis aplikacji i nazwy główne usług, zobacz [obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="bcee9-220">Aby uzyskać więcej informacji na temat uwierzytelniania usługi Azure Active Directory, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="bcee9-221">Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić toousers, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="bcee9-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

