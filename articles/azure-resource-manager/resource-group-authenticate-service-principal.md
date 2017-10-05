---
title: "Utwórz tożsamość aplikacji usługi Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tworzenia aplikacji usługi Azure Active Directory i nazwy głównej usługi i przyznać jej dostęp do zasobów za pomocą kontroli dostępu opartej na rolach przy użyciu programu Azure PowerShell. Widoczny jest sposób uwierzytelniania aplikacji za pomocą hasła lub certyfikatu."
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
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="2ec89-104">Use Azure PowerShell to create a service principal to access resources (Tworzenie jednostki usługi używanej do uzyskiwania dostępu do zasobów przy użyciu programu Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="2ec89-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="2ec89-105">Jeśli aplikacji lub skryptu, który ma dostęp do zasobów, można skonfigurować tożsamości aplikacji i uwierzytelniania w aplikacji przy użyciu własne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="2ec89-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="2ec89-106">Ta tożsamość jest określany jako nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="2ec89-106">This identity is known as a service principal.</span></span> <span data-ttu-id="2ec89-107">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="2ec89-107">This approach enables you to:</span></span>

* <span data-ttu-id="2ec89-108">Przypisanie uprawnień do tożsamości aplikacji, które są inne niż własnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2ec89-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="2ec89-109">Zazwyczaj te uprawnienia są ograniczone do dokładnie co aplikacja powinna wykonać.</span><span class="sxs-lookup"><span data-stu-id="2ec89-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="2ec89-110">Użyj certyfikatu do uwierzytelnienia, podczas wykonywania skryptu instalacji nienadzorowanej.</span><span class="sxs-lookup"><span data-stu-id="2ec89-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="2ec89-111">W tym temacie przedstawiono sposób użycia [programu Azure PowerShell](/powershell/azure/overview) skonfigurować wszystkie elementy potrzebne do uruchamiana własne poświadczenia i tożsamości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="2ec89-112">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="2ec89-112">Required permissions</span></span>
<span data-ttu-id="2ec89-113">Do ukończenia tego tematu, należy posiadać odpowiednie uprawnienia w usłudze Azure Active Directory i Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec89-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="2ec89-114">W szczególności należy utworzyć aplikację w usłudze Azure Active Directory i przypisać nazwę główną usługi do roli.</span><span class="sxs-lookup"><span data-stu-id="2ec89-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="2ec89-115">Najłatwiejszym sposobem sprawdzenia, czy Twoje konto ma odpowiednie uprawnienia, jest skorzystanie z portalu.</span><span class="sxs-lookup"><span data-stu-id="2ec89-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="2ec89-116">Zobacz [, czy wymagane uprawnienia](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="2ec89-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="2ec89-117">Teraz przejdź do sekcji w celu uwierzytelniania z:</span><span class="sxs-lookup"><span data-stu-id="2ec89-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="2ec89-118">hasło</span><span class="sxs-lookup"><span data-stu-id="2ec89-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="2ec89-119">certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="2ec89-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="2ec89-120">certyfikat od urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="2ec89-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="2ec89-121">Polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ec89-121">PowerShell commands</span></span>

<span data-ttu-id="2ec89-122">Aby skonfigurować nazwy głównej usługi, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="2ec89-123">Polecenie</span><span class="sxs-lookup"><span data-stu-id="2ec89-123">Command</span></span> | <span data-ttu-id="2ec89-124">Opis</span><span class="sxs-lookup"><span data-stu-id="2ec89-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="2ec89-125">Nowe AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="2ec89-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="2ec89-126">Tworzy nazwę główną usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ec89-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="2ec89-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="2ec89-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="2ec89-128">Przypisuje określonej roli RBAC określony podmiot zabezpieczeń w podanym zakresie.</span><span class="sxs-lookup"><span data-stu-id="2ec89-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="2ec89-129">Tworzenie nazwy głównej usługi z hasłem</span><span class="sxs-lookup"><span data-stu-id="2ec89-129">Create service principal with password</span></span>

<span data-ttu-id="2ec89-130">Aby utworzyć nazwy głównej usługi roli współautora dla Twojej subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="2ec89-131">Przykład zostanie uśpiony na 20 sekund, pewien czas dla nowej usługi głównej propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2ec89-132">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu."</span><span class="sxs-lookup"><span data-stu-id="2ec89-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="2ec89-133">Poniższy skrypt można określić zakres innych niż domyślne subskrypcji i ponowi próbę przypisania roli, jeśli wystąpi błąd:</span><span class="sxs-lookup"><span data-stu-id="2ec89-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="2ec89-134">Kilka elementów należy pamiętać o skrypt:</span><span class="sxs-lookup"><span data-stu-id="2ec89-134">A few items to note about the script:</span></span>

* <span data-ttu-id="2ec89-135">Aby udzielić dostępu tożsamości do subskrypcji domyślne, nie należy podać parametry grupa zasobów lub subskrypcji o identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="2ec89-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="2ec89-136">Określ parametr ResourceGroup tylko wtedy, gdy chcesz ograniczyć zakres przypisania roli do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ec89-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="2ec89-137">W tym przykładzie należy dodać nazwy głównej usługi do roli współautora.</span><span class="sxs-lookup"><span data-stu-id="2ec89-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="2ec89-138">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="2ec89-139">Skrypt zostanie uśpiony na 15 sekund, pewien czas dla nowej usługi głównej propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2ec89-140">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu."</span><span class="sxs-lookup"><span data-stu-id="2ec89-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="2ec89-141">Aby udzielić dostępu główną usługi do więcej subskrypcji lub grupy zasobów, należy uruchomić `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.</span><span class="sxs-lookup"><span data-stu-id="2ec89-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="2ec89-142">Podaj poświadczenia, za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ec89-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="2ec89-143">Teraz musisz zalogować się jako aplikacji w celu wykonania operacji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="2ec89-144">Dla nazwy użytkownika użyj `ApplicationId` utworzonej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="2ec89-145">Hasła należy użyć jednej określone podczas tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="2ec89-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="2ec89-146">Identyfikator dzierżawcy nie jest liter, dlatego można ją osadzić bezpośrednio w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="2ec89-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="2ec89-147">Można pobrać Identyfikatora dzierżawy, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="2ec89-148">Tworzenie nazwy głównej usługi o certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="2ec89-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="2ec89-149">Aby utworzyć nazwy głównej usługi o certyfikat z podpisem własnym i roli współautora dla Twojej subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="2ec89-150">Przykład zostanie uśpiony na 20 sekund, pewien czas dla nowej usługi głównej propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2ec89-151">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu."</span><span class="sxs-lookup"><span data-stu-id="2ec89-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="2ec89-152">Poniższy skrypt można określić zakres innych niż domyślne subskrypcji i ponowi próbę przypisania roli, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="2ec89-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="2ec89-153">Musi mieć Azure PowerShell 2.0 w systemie Windows 10 lub Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2ec89-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="2ec89-154">Kilka elementów należy pamiętać o skrypt:</span><span class="sxs-lookup"><span data-stu-id="2ec89-154">A few items to note about the script:</span></span>

* <span data-ttu-id="2ec89-155">Aby udzielić dostępu tożsamości do subskrypcji domyślne, nie należy podać parametry grupa zasobów lub subskrypcji o identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="2ec89-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="2ec89-156">Określ parametr ResourceGroup tylko wtedy, gdy chcesz ograniczyć zakres przypisania roli do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ec89-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="2ec89-157">W tym przykładzie należy dodać nazwy głównej usługi do roli współautora.</span><span class="sxs-lookup"><span data-stu-id="2ec89-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="2ec89-158">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="2ec89-159">Skrypt zostanie uśpiony na 15 sekund, pewien czas dla nowej usługi głównej propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2ec89-160">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu."</span><span class="sxs-lookup"><span data-stu-id="2ec89-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="2ec89-161">Aby udzielić dostępu główną usługi do więcej subskrypcji lub grupy zasobów, należy uruchomić `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.</span><span class="sxs-lookup"><span data-stu-id="2ec89-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="2ec89-162">Jeśli użytkownik **bez zainstalowanego systemu Windows 10 lub Windows Server 2016 Technical Preview**, należy pobrać [generator certyfikatu z podpisem własnym](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) z Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="2ec89-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="2ec89-163">Wyodrębnij jego zawartość i zaimportuj polecenia cmdlet, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="2ec89-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="2ec89-164">W skrypcie Zastąp następujące dwa wiersze w celu wygenerowania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2ec89-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="2ec89-165">Podaj certyfikat przy użyciu zautomatyzowanego skryptu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ec89-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="2ec89-166">Gdy zalogujesz się jako nazwy głównej usługi, należy podać identyfikator dzierżawcy katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="2ec89-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="2ec89-167">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="2ec89-168">Jeśli masz tylko jedną subskrypcję, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="2ec89-169">Identyfikator aplikacji i Identyfikatora dzierżawcy nie są poufne, więc można go osadzić bezpośrednio w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="2ec89-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="2ec89-170">Można pobrać Identyfikatora dzierżawy, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="2ec89-171">Aby uzyskać identyfikator aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="2ec89-172">Tworzenie nazwy głównej usługi o certyfikat od urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="2ec89-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="2ec89-173">Aby używać certyfikatu wystawionego przez urząd certyfikacji, tworzenie nazwy głównej usługi, użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="2ec89-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="2ec89-174">Kilka elementów należy pamiętać o skrypt:</span><span class="sxs-lookup"><span data-stu-id="2ec89-174">A few items to note about the script:</span></span>

* <span data-ttu-id="2ec89-175">Obejmuje dostęp do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="2ec89-176">W tym przykładzie należy dodać nazwy głównej usługi do roli współautora.</span><span class="sxs-lookup"><span data-stu-id="2ec89-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="2ec89-177">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="2ec89-178">Skrypt zostanie uśpiony na 15 sekund, pewien czas dla nowej usługi głównej propagację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2ec89-179">Jeśli skrypt nie oczekuje się wystarczająco długi, zobacz błąd z informacją: "PrincipalNotFound: podmiot zabezpieczeń {id} nie istnieje w katalogu."</span><span class="sxs-lookup"><span data-stu-id="2ec89-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="2ec89-180">Aby udzielić dostępu główną usługi do więcej subskrypcji lub grupy zasobów, należy uruchomić `New-AzureRMRoleAssignment` polecenie cmdlet ponownie z różnymi zakresami.</span><span class="sxs-lookup"><span data-stu-id="2ec89-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="2ec89-181">Podaj certyfikat przy użyciu zautomatyzowanego skryptu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ec89-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="2ec89-182">Gdy zalogujesz się jako nazwy głównej usługi, należy podać identyfikator dzierżawcy katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="2ec89-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="2ec89-183">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ec89-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="2ec89-184">Identyfikator aplikacji i Identyfikatora dzierżawcy nie są poufne, więc można go osadzić bezpośrednio w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="2ec89-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="2ec89-185">Można pobrać Identyfikatora dzierżawy, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="2ec89-186">Aby uzyskać identyfikator aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="2ec89-187">Zmiana poświadczeń</span><span class="sxs-lookup"><span data-stu-id="2ec89-187">Change credentials</span></span>

<span data-ttu-id="2ec89-188">Aby zmienić poświadczenia dla aplikacji usługi AD, albo z powodu naruszenia zabezpieczeń lub wygaśnięcia poświadczeń, należy użyć [AzureRmADAppCredential Usuń](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) i [AzureRmADAppCredential nowy](/powershell/module/azurerm.resources/new-azurermadappcredential) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ec89-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="2ec89-189">Aby usunąć wszystkie poświadczenia dla aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="2ec89-190">Aby dodać hasło, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="2ec89-191">Aby dodać wartość certyfikatu, Utwórz certyfikat z podpisem własnym, jak pokazano w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="2ec89-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="2ec89-192">Następnie należy użyć:</span><span class="sxs-lookup"><span data-stu-id="2ec89-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="2ec89-193">Zapisz token dostępu w celu uproszczenia dziennika w</span><span class="sxs-lookup"><span data-stu-id="2ec89-193">Save access token to simplify log in</span></span>
<span data-ttu-id="2ec89-194">Aby uniknąć, podając poświadczenia główne usługi za każdym razem, należy zalogować się, można zapisać tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2ec89-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="2ec89-195">Aby użyć bieżącego tokenu dostępu w późniejszym sesji, zapisywanie profilu.</span><span class="sxs-lookup"><span data-stu-id="2ec89-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="2ec89-196">Otwórz profilu i przejrzyj jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="2ec89-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="2ec89-197">Zwróć uwagę, że zawiera on tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2ec89-197">Notice that it contains an access token.</span></span> <span data-ttu-id="2ec89-198">Zamiast ręcznego zalogować się ponownie później, po prostu załadować profilu.</span><span class="sxs-lookup"><span data-stu-id="2ec89-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="2ec89-199">Wygaśnięcia tokenu dostępu, dzięki użyciu zapisywanego profilu działa tylko dla, tak długo, jak token jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="2ec89-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="2ec89-200">Alternatywnie można wywołać operacji REST z programu PowerShell, aby się zalogować.</span><span class="sxs-lookup"><span data-stu-id="2ec89-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="2ec89-201">Z odpowiedzi uwierzytelniania można pobrać tokenu dostępu do użycia z innych operacji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="2ec89-202">Na przykład pobierania tokenu dostępu za pomocą operacji REST, zobacz [generowania tokenu dostępu](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="2ec89-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="2ec89-203">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="2ec89-203">Debug</span></span>

<span data-ttu-id="2ec89-204">Podczas tworzenia nazwy głównej usługi, mogą wystąpić następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="2ec89-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="2ec89-205">**"Authentication_Unauthorized"** lub **"subskrypcji nie znaleziono w kontekście".**</span><span class="sxs-lookup"><span data-stu-id="2ec89-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="2ec89-206">— Został wyświetlony ten błąd, gdy Twoje konto nie ma [wymagane uprawnienia](#required-permissions) w usłudze Azure Active Directory w celu rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="2ec89-207">Zwykle zostanie wyświetlony ten błąd, gdy tylko Administrator użytkowników w usłudze Azure Active Directory można zarejestrować aplikacji, a konto użytkownika nie jest administratorem.</span><span class="sxs-lookup"><span data-stu-id="2ec89-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="2ec89-208">Skontaktuj się z administratorem, albo przypisanie do roli administratora lub aby użytkownicy mogli zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ec89-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="2ec89-209">Twoje konto **"nie ma autoryzacji do wykonania akcji"Microsoft.Authorization/roleAssignments/write"w zakresie"/subscriptions/ {guid}"."**  — Zostanie wyświetlony ten błąd, gdy Twoje konto nie ma wystarczających uprawnień, aby przypisać rolę do tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2ec89-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="2ec89-210">Poproś administratora subskrypcji możesz dodać do roli Administrator dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ec89-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="2ec89-211">Przykładowe aplikacje</span><span class="sxs-lookup"><span data-stu-id="2ec89-211">Sample applications</span></span>
<span data-ttu-id="2ec89-212">Aby uzyskać informacje o zalogowanie się jako aplikacji za pomocą różnych platform zobacz:</span><span class="sxs-lookup"><span data-stu-id="2ec89-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="2ec89-213">.NET</span><span class="sxs-lookup"><span data-stu-id="2ec89-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="2ec89-214">Java</span><span class="sxs-lookup"><span data-stu-id="2ec89-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="2ec89-215">Node.js</span><span class="sxs-lookup"><span data-stu-id="2ec89-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="2ec89-216">Python</span><span class="sxs-lookup"><span data-stu-id="2ec89-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="2ec89-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="2ec89-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="2ec89-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ec89-218">Next steps</span></span>
* <span data-ttu-id="2ec89-219">Aby uzyskać szczegółowe instrukcje dotyczące integrowania aplikacji na platformie Azure do zarządzania zasobami, zobacz [przewodnik dewelopera do autoryzacji przy użyciu interfejsu API Menedżera zasobów Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="2ec89-220">Aby uzyskać bardziej szczegółowy opis aplikacji i nazwy główne usług, zobacz [obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="2ec89-221">Aby uzyskać więcej informacji na temat uwierzytelniania usługi Azure Active Directory, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="2ec89-222">Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić dla użytkowników, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="2ec89-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

