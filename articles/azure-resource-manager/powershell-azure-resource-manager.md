---
title: "Zarządzaj rozwiązaniami Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell i Menedżera zasobów do zarządzania zasobami."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="086e1-103">Zarządzanie zasobami za pomocą programu Azure PowerShell i Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="086e1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="086e1-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="086e1-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="086e1-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="086e1-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="086e1-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="086e1-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="086e1-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="086e1-108">W tym artykule Dowiedz się jak zarządzać rozwiązań z programu Azure PowerShell i Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="086e1-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="086e1-109">Jeśli nie masz doświadczenia z usługą Resource Manager, zobacz [omówienie Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="086e1-110">Ten temat koncentruje się na zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="086e1-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="086e1-111">Wykonasz następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="086e1-111">You will:</span></span>

1. <span data-ttu-id="086e1-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-112">Create a resource group</span></span>
2. <span data-ttu-id="086e1-113">Dodaj zasób do grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="086e1-114">Dodaj tag do zasobu</span><span class="sxs-lookup"><span data-stu-id="086e1-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="086e1-115">Wykonywanie zapytań względem zasobów na podstawie nazw lub wartości tagów</span><span class="sxs-lookup"><span data-stu-id="086e1-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="086e1-116">Zastosuj i Usuń blokada na zasób</span><span class="sxs-lookup"><span data-stu-id="086e1-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="086e1-117">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-117">Delete a resource group</span></span>

<span data-ttu-id="086e1-118">W tym artykule nie pokazuje sposób wdrażania szablonu usługi Resource Manager do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="086e1-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="086e1-119">Informacje, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="086e1-120">Wprowadzenie do programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="086e1-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="086e1-121">Jeśli nie zainstalowano programu Azure PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="086e1-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="086e1-122">Jeśli mieć zainstalowany program Azure PowerShell w przeszłości, ale nie zaktualizowano on niedawno, należy rozważyć zainstalowanie najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="086e1-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="086e1-123">Należy zaktualizować wersję za pomocą tej samej metody, które zostały użyte do zainstalowania go.</span><span class="sxs-lookup"><span data-stu-id="086e1-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="086e1-124">Na przykład użycie Instalatora platformy sieci Web, uruchom ją ponownie i wyszukać aktualizację.</span><span class="sxs-lookup"><span data-stu-id="086e1-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="086e1-125">Aby sprawdzić swoją wersję modułu zasobów Azure, użyj następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="086e1-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="086e1-126">Ten temat został zaktualizowany na potrzeby wersji 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="086e1-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="086e1-127">Jeśli masz starszą wersję środowiska mogą nie odpowiadać kroki opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="086e1-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="086e1-128">Aby uzyskać dokumentację poleceń cmdlet w tej wersji, zobacz [AzureRM.Resources modułu](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="086e1-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="086e1-129">Zaloguj się do konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="086e1-129">Log in to your Azure account</span></span>
<span data-ttu-id="086e1-130">Przed rozpoczęciem pracy rozwiązania, należy zalogować się do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="086e1-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="086e1-131">Aby zalogować się do konta platformy Azure, użyj **Login-AzureRmAccount** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="086e1-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="086e1-132">Polecenie cmdlet wyświetla monit o podanie poświadczeń logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="086e1-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="086e1-133">Po zalogowaniu pobiera ono ustawienia konta, aby były dostępne dla programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="086e1-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="086e1-134">Polecenie cmdlet zwraca informacje dotyczące konta i subskrypcji do użycia dla zadania.</span><span class="sxs-lookup"><span data-stu-id="086e1-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="086e1-135">Jeśli masz więcej niż jedną subskrypcję, możesz przełączyć się do innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="086e1-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="086e1-136">Po pierwsze Zobacz wszystkie subskrypcje dla swojego konta.</span><span class="sxs-lookup"><span data-stu-id="086e1-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="086e1-137">Zwraca włączyć i wyłączyć subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="086e1-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="086e1-138">Aby przełączyć się do innej subskrypcji, należy podać nazwę subskrypcji z **Set-AzureRmContext** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="086e1-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="086e1-139">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-139">Create a resource group</span></span>
<span data-ttu-id="086e1-140">Przed wdrożeniem żadnych zasobów w Twojej subskrypcji, należy utworzyć grupę zasobów, która będzie zawierać zasoby.</span><span class="sxs-lookup"><span data-stu-id="086e1-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="086e1-141">Aby utworzyć grupę zasobów, użyj **New-AzureRmResourceGroup** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="086e1-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="086e1-142">Używa polecenia **nazwa** parametr, aby określić nazwę grupy zasobów i **lokalizacji** parametru w celu określenia lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="086e1-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="086e1-143">Dane wyjściowe znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="086e1-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="086e1-144">Aby pobrać grupę zasobów później, należy użyć następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="086e1-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="086e1-145">Aby uzyskać wszystkie grupy zasobów w ramach subskrypcji, nie należy określać nazwy:</span><span class="sxs-lookup"><span data-stu-id="086e1-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="086e1-146">Dodaj zasoby do grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-146">Add resources to a resource group</span></span>
<span data-ttu-id="086e1-147">Aby dodać zasobu do grupy zasobów, można użyć **AzureRmResource nowy** polecenia cmdlet lub polecenia cmdlet, które są specyficzne dla typu zasobu tworzysz (takich jak **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="086e1-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="086e1-148">Użytkownik może łatwiej, użyj polecenia cmdlet, które są specyficzne dla typu zasobu, ponieważ uwzględnia on również parametry dla właściwości, które są potrzebne dla nowego zasobu.</span><span class="sxs-lookup"><span data-stu-id="086e1-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="086e1-149">Aby użyć **AzureRmResource nowy**, musisz znać wszystkie właściwości można ustawić bez konieczności podawania dla nich.</span><span class="sxs-lookup"><span data-stu-id="086e1-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="086e1-150">Jednak dodawanie zasobów za pomocą poleceń cmdlet może spowodować przyszłych pomyłek, ponieważ nowy zasób nie istnieje w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="086e1-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="086e1-151">Firma Microsoft zaleca Definiowanie infrastruktury dla rozwiązania Azure w ramach szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="086e1-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="086e1-152">Szablony umożliwiają niezawodne i wielokrotnego wdrażania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="086e1-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="086e1-153">W tym temacie Tworzenie konta magazynu za pomocą polecenia cmdlet programu PowerShell, ale później wygenerowanie szablonu z grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="086e1-154">Następujące polecenie cmdlet tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="086e1-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="086e1-155">Zamiast nazwy pokazano w przykładzie, Podaj unikatową nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="086e1-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="086e1-156">Nazwa musi mieć od 3 do 24 znaków i zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="086e1-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="086e1-157">Jeśli używasz nazwę pokazano w przykładzie, wystąpi błąd, ponieważ ta nazwa jest już używana.</span><span class="sxs-lookup"><span data-stu-id="086e1-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="086e1-158">Jeśli potrzebujesz do odtworzenia tego zasobu, należy użyć następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="086e1-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="086e1-159">Dodaj tag</span><span class="sxs-lookup"><span data-stu-id="086e1-159">Add a tag</span></span>

<span data-ttu-id="086e1-160">Znaczniki umożliwiają organizowania zasobów zgodnie z innej właściwości.</span><span class="sxs-lookup"><span data-stu-id="086e1-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="086e1-161">Na przykład może mieć kilka zasobów w różnych grup zasobów należących do tego samego działu.</span><span class="sxs-lookup"><span data-stu-id="086e1-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="086e1-162">Tag działu i wartości można zastosować do tych zasobów, aby oznaczyć je jako należące do tej samej kategorii.</span><span class="sxs-lookup"><span data-stu-id="086e1-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="086e1-163">Alternatywnie można oznaczyć, czy zasób jest używany w środowisku produkcyjnym lub testowym.</span><span class="sxs-lookup"><span data-stu-id="086e1-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="086e1-164">W tym temacie tagi są stosowane tylko do jednego zasobu, ale w danym środowisku prawdopodobnie warto dodawania tagów do wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="086e1-165">Następujące polecenie cmdlet ma zastosowanie dwa tagi do konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="086e1-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="086e1-166">Tagi są aktualizowane jako pojedynczego obiektu.</span><span class="sxs-lookup"><span data-stu-id="086e1-166">Tags are updated as a single object.</span></span> <span data-ttu-id="086e1-167">Aby dodać tag do zasobu, która zawiera już znaczników, należy najpierw pobrać istniejące znaczniki.</span><span class="sxs-lookup"><span data-stu-id="086e1-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="086e1-168">Dodaj nowy znacznik do obiektu, który zawiera istniejące znaczniki i ponownie zastosuj wszystkie tagi do zasobu.</span><span class="sxs-lookup"><span data-stu-id="086e1-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="086e1-169">Wyszukaj zasoby</span><span class="sxs-lookup"><span data-stu-id="086e1-169">Search for resources</span></span>

<span data-ttu-id="086e1-170">Użyj **AzureRmResource Znajdź** polecenia cmdlet można pobrać zasobów do wyszukiwania różnych warunków.</span><span class="sxs-lookup"><span data-stu-id="086e1-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="086e1-171">Aby uzyskać za pomocą nazwy zasobu, należy podać **ResourceNameContains** parametru:</span><span class="sxs-lookup"><span data-stu-id="086e1-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="086e1-172">Aby uzyskać wszystkie zasoby w grupie zasobów, należy podać **ResourceGroupNameContains** parametru:</span><span class="sxs-lookup"><span data-stu-id="086e1-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="086e1-173">Aby pobrać wszystkich zasobów o nazwie tagu i wartości, należy podać **TagName** i **TagValue** parametry:</span><span class="sxs-lookup"><span data-stu-id="086e1-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="086e1-174">Do wszystkich zasobów z określonego typu zasobu, należy podać **ResourceType** parametru:</span><span class="sxs-lookup"><span data-stu-id="086e1-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="086e1-175">Zablokowanie zasobu</span><span class="sxs-lookup"><span data-stu-id="086e1-175">Lock a resource</span></span>

<span data-ttu-id="086e1-176">Aby upewnić się, że krytyczne zasobów nie zostanie przypadkowo usunięty lub zmodyfikowany, zastosuj blokady do zasobu.</span><span class="sxs-lookup"><span data-stu-id="086e1-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="086e1-177">Można określić **CanNotDelete** lub **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="086e1-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="086e1-178">Aby utworzyć lub usunąć blokady zarządzania, musi mieć dostęp do `Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje.</span><span class="sxs-lookup"><span data-stu-id="086e1-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="086e1-179">Wbudowanych ról tylko właściciel i Administrator dostępu użytkowników są przyznawane te akcje.</span><span class="sxs-lookup"><span data-stu-id="086e1-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="086e1-180">Aby zastosować blokady, należy użyć następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="086e1-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="086e1-181">Nie można usunąć zablokowanych zasobu w poprzednim przykładzie, aż do usunięcia blokady.</span><span class="sxs-lookup"><span data-stu-id="086e1-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="086e1-182">Aby usunąć blokadę, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="086e1-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="086e1-183">Aby uzyskać więcej informacji na temat ustawienie blokady, zobacz [blokowania zasobów z usługi Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="086e1-184">Usuwanie zasobów lub grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="086e1-184">Remove resources or resource group</span></span>
<span data-ttu-id="086e1-185">Można usunąć zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="086e1-186">Usuń grupę zasobów, należy również usunąć wszystkie zasoby w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="086e1-187">Aby usunąć zasób z grupy zasobów, użyj **AzureRmResource Usuń** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="086e1-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="086e1-188">To polecenie cmdlet Usuwa zasób, ale nie powoduje usunięcia grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="086e1-189">Aby usunąć grupę zasobów i wszystkie jego zasoby, używać **Remove-AzureRmResourceGroup** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="086e1-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="086e1-190">Dla obu poleceń cmdlet zostanie wyświetlona prośba o potwierdzenie, że chcesz usunąć zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="086e1-191">Jeśli operacja pomyślnie Usuwa zasób lub grupa zasobów, zwraca **True**.</span><span class="sxs-lookup"><span data-stu-id="086e1-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="086e1-192">Uruchamianie skryptów Menedżera zasobów w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="086e1-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="086e1-193">W tym temacie przedstawiono sposób wykonywania podstawowych operacji dotyczących zasobów przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="086e1-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="086e1-194">W przypadku bardziej zaawansowanych scenariuszy zarządzania zwykle chcesz utworzyć skrypt, a następnie ponownie użyć tego skryptu, zgodnie z potrzebami lub zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="086e1-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="086e1-195">[Automatyzacja Azure](../automation/automation-intro.md) zapewnia sposobem zautomatyzowania często używanych skryptów, które zarządzają rozwiązań platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="086e1-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="086e1-196">W następujących tematach opisano, jak używać usługi Automatyzacja Azure Resource Manager i programu PowerShell do skutecznie wykonywać zadania zarządzania:</span><span class="sxs-lookup"><span data-stu-id="086e1-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="086e1-197">Aby uzyskać informacje dotyczące tworzenia elementu runbook, zobacz [Moje pierwszego elementu runbook programu PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="086e1-198">Aby uzyskać informacje na temat pracy z galerii skryptów, zobacz [galerie elementów Runbook i modułów w automatyzacji Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="086e1-199">Dla elementów runbook uruchamianie i zatrzymywanie maszyn wirtualnych, zobacz [scenariusz automatyzacji Azure: formacie JSON przy użyciu tagów, aby utworzyć harmonogram uruchamiania maszyny Wirtualnej platformy Azure i zamykania](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="086e1-200">Dla elementów runbook uruchamianie i zatrzymywanie maszyn wirtualnych po godzinach pracy, zobacz [uruchamiania/zatrzymywania maszyn wirtualnych, podczas rozwiązania poza godzinami szczytu w automatyzacji](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="086e1-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="086e1-201">Next steps</span></span>
* <span data-ttu-id="086e1-202">Aby uzyskać informacje dotyczące tworzenia szablonów usługi Resource Manager, zobacz [Authoring Azure Resource Manager szablony](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="086e1-203">Informacje na temat wdrażania szablonów, zobacz [wdrażanie aplikacji przy użyciu szablonu usługi Resource Manager Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="086e1-204">Można przenieść istniejące zasoby do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="086e1-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="086e1-205">Aby uzyskać przykłady, zobacz [przeniesienia zasobów do nowej grupy zasobów lub subskrypcji](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="086e1-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="086e1-206">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="086e1-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

