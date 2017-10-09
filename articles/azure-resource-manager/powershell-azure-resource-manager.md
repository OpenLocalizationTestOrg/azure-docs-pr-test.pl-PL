---
title: "aaaManage Azure rozwiązania przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell i Menedżera zasobów toomanage zasobów."
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
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="91d65-103">Zarządzanie zasobami za pomocą programu Azure PowerShell i Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91d65-104">Portal</span><span class="sxs-lookup"><span data-stu-id="91d65-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="91d65-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91d65-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="91d65-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="91d65-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="91d65-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="91d65-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="91d65-108">W tym artykule dowiesz się, jak toomanage rozwiązań z programu Azure PowerShell i Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="91d65-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="91d65-109">Jeśli nie masz doświadczenia z usługą Resource Manager, zobacz [omówienie Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="91d65-110">Ten temat koncentruje się na zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="91d65-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="91d65-111">Wykonasz następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="91d65-111">You will:</span></span>

1. <span data-ttu-id="91d65-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-112">Create a resource group</span></span>
2. <span data-ttu-id="91d65-113">Dodaj grupę zasobów toohello zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="91d65-114">Dodaj zasób toohello tag</span><span class="sxs-lookup"><span data-stu-id="91d65-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="91d65-115">Wykonywanie zapytań względem zasobów na podstawie nazw lub wartości tagów</span><span class="sxs-lookup"><span data-stu-id="91d65-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="91d65-116">Zastosuj i Usuń blokadę hello zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="91d65-117">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-117">Delete a resource group</span></span>

<span data-ttu-id="91d65-118">W tym artykule nie pokazuje sposób toodeploy subskrypcji tooyour szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91d65-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="91d65-119">Informacje, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="91d65-120">Wprowadzenie do programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="91d65-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="91d65-121">Jeśli nie zainstalowano programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91d65-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="91d65-122">W przeszłości hello mieć zainstalowany program Azure PowerShell, ale nie zaktualizowano on niedawno, można zainstalować hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="91d65-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="91d65-123">Można aktualizować wersji hello za pośrednictwem hello tej samej metody używane tooinstall go.</span><span class="sxs-lookup"><span data-stu-id="91d65-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="91d65-124">Na przykład jeśli użyto hello Instalatora platformy sieci Web, uruchom ją ponownie i wyszukać aktualizację.</span><span class="sxs-lookup"><span data-stu-id="91d65-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="91d65-125">Użyj wersji hello modułu zasobów Azure toocheck hello poniższe polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="91d65-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="91d65-126">Ten temat został zaktualizowany na potrzeby wersji 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="91d65-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="91d65-127">Jeśli masz starszą wersję środowiska mogą nie odpowiadać hello kroki opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="91d65-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="91d65-128">Aby uzyskać dokumentację poleceń cmdlet hello w tej wersji, zobacz [AzureRM.Resources modułu](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="91d65-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="91d65-129">Zaloguj się za tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91d65-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="91d65-130">Przed rozpoczęciem pracy rozwiązania, należy zalogować się tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="91d65-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="91d65-131">toolog w tooyour konto platformy Azure, użyj hello **Login-AzureRmAccount** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91d65-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="91d65-132">polecenia cmdlet Hello monituje o hello poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91d65-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="91d65-133">Po zalogowaniu pobraniu ustawienia konta tak, aby były dostępne tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91d65-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="91d65-134">polecenia cmdlet Hello zwraca informacje dotyczące Twojego konta i hello toouse subskrypcji hello zadań.</span><span class="sxs-lookup"><span data-stu-id="91d65-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="91d65-135">Jeśli masz więcej niż jedną subskrypcję, możesz przełączyć tooa innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="91d65-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="91d65-136">Po pierwsze Zobacz wszystkie subskrypcje powitania dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="91d65-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="91d65-137">Zwraca włączyć i wyłączyć subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="91d65-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="91d65-138">tooswitch tooa inną subskrypcję, podaj nazwę subskrypcji hello z hello **Set-AzureRmContext** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91d65-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="91d65-139">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-139">Create a resource group</span></span>
<span data-ttu-id="91d65-140">Przed wdrożeniem żadnej subskrypcji tooyour zasobów, należy utworzyć grupę zasobów, która będzie zawierać hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="91d65-141">toocreate grupę zasobów, użyj hello **New-AzureRmResourceGroup** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91d65-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="91d65-142">polecenie Hello używa hello **nazwa** toospecify parametru nazwę grupy zasobów hello i hello **lokalizacji** toospecify parametru jego lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="91d65-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="91d65-143">dane wyjściowe Hello znajduje się w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="91d65-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="91d65-144">Grupa zasobów tooretrieve hello później, należy użyć hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="91d65-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="91d65-145">tooget hello wszystkich grup zasobów w ramach subskrypcji, nie należy określać nazwy:</span><span class="sxs-lookup"><span data-stu-id="91d65-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="91d65-146">Dodaj grupę zasobów tooa zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-146">Add resources tooa resource group</span></span>
<span data-ttu-id="91d65-147">tooadd grupę zasobów toohello zasobów, można użyć hello **AzureRmResource nowy** polecenia cmdlet lub polecenia cmdlet, który jest typem toohello określonego zasobu tworzysz (takich jak **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="91d65-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="91d65-148">Może być łatwiejsze toouse polecenia cmdlet, które jest tooa określonego typu zasobu, ponieważ zawiera on parametrów hello właściwości, które są potrzebne dla nowego zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="91d65-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="91d65-149">toouse **AzureRmResource nowy**, musisz znać wszystkie tooset właściwości hello bez monitowania o nich.</span><span class="sxs-lookup"><span data-stu-id="91d65-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="91d65-150">Jednak dodawanie zasobów za pomocą poleceń cmdlet może spowodować przyszłych pomyłek, ponieważ hello nowy zasób nie istnieje w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91d65-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="91d65-151">Firma Microsoft zaleca Definiowanie hello infrastrukturę Twojego rozwiązania Azure w ramach szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91d65-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="91d65-152">Szablony umożliwiają tooreliably i wielokrotnie wdrażać rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="91d65-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="91d65-153">W tym temacie Tworzenie konta magazynu za pomocą polecenia cmdlet programu PowerShell, ale później wygenerowanie szablonu z grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="91d65-154">Witaj następujące polecenie cmdlet tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="91d65-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="91d65-155">Zamiast przy użyciu nazwy hello pokazano w przykładzie hello, Podaj unikatową nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="91d65-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="91d65-156">Nazwa Hello musi należeć do zakresu od 3 do 24 znaków i zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="91d65-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="91d65-157">Jeśli używasz nazwę hello pokazano w przykładzie hello, wystąpi błąd, ponieważ ta nazwa jest już używana.</span><span class="sxs-lookup"><span data-stu-id="91d65-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="91d65-158">Tooretrieve tego zasobu później, należy użyć hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="91d65-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="91d65-159">Dodaj tag</span><span class="sxs-lookup"><span data-stu-id="91d65-159">Add a tag</span></span>

<span data-ttu-id="91d65-160">Znaczniki umożliwiają tooorganize zasobów zgodnie z toodifferent właściwości.</span><span class="sxs-lookup"><span data-stu-id="91d65-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="91d65-161">Na przykład organizacja może mieć kilka zasoby w różnych grup zasobów należących toohello samego działu.</span><span class="sxs-lookup"><span data-stu-id="91d65-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="91d65-162">Możesz zastosować działu tagu i wartość toothose zasobów toomark ich jako należące toohello tej samej kategorii.</span><span class="sxs-lookup"><span data-stu-id="91d65-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="91d65-163">Alternatywnie można oznaczyć, czy zasób jest używany w środowisku produkcyjnym lub testowym.</span><span class="sxs-lookup"><span data-stu-id="91d65-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="91d65-164">W tym temacie należy zastosować tagi tooonly jeden zasób, ale w danym środowisku prawdopodobnie sens się, że tooapply znaczniki tooall zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="91d65-165">Witaj następującego polecenia cmdlet stosuje się dwa konta magazynu tooyour tagów:</span><span class="sxs-lookup"><span data-stu-id="91d65-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="91d65-166">Tagi są aktualizowane jako pojedynczego obiektu.</span><span class="sxs-lookup"><span data-stu-id="91d65-166">Tags are updated as a single object.</span></span> <span data-ttu-id="91d65-167">tooadd tag zasobu tooa, która zawiera już znaczników, najpierw pobrać hello znaczników.</span><span class="sxs-lookup"><span data-stu-id="91d65-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="91d65-168">Dodaj hello nowego tagu toohello obiekt, który zawiera hello znaczników i zastosuj je ponownie wszystkie hello tagi toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="91d65-169">Wyszukaj zasoby</span><span class="sxs-lookup"><span data-stu-id="91d65-169">Search for resources</span></span>

<span data-ttu-id="91d65-170">Użyj hello **AzureRmResource Znajdź** zasoby tooretrieve polecenia cmdlet dla różnych warunki.</span><span class="sxs-lookup"><span data-stu-id="91d65-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="91d65-171">tooget zasobów według nazwy, podaj hello **ResourceNameContains** parametru:</span><span class="sxs-lookup"><span data-stu-id="91d65-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="91d65-172">tooget wszystkie zasoby hello w grupie zasobów, zawierają hello **ResourceGroupNameContains** parametru:</span><span class="sxs-lookup"><span data-stu-id="91d65-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="91d65-173">tooget wszystkie zasoby hello o nazwie tagu i wartości, zawierają hello **TagName** i **TagValue** parametry:</span><span class="sxs-lookup"><span data-stu-id="91d65-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="91d65-174">zasoby hello tooall z określonego typu zasobu, zawierają hello **ResourceType** parametru:</span><span class="sxs-lookup"><span data-stu-id="91d65-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="91d65-175">Zablokowanie zasobu</span><span class="sxs-lookup"><span data-stu-id="91d65-175">Lock a resource</span></span>

<span data-ttu-id="91d65-176">Gdy potrzebne są toomake się, że krytycznego zasobu nie zostanie przypadkowo usunięty lub zmodyfikowany, zastosuj toohello zablokować zasobu.</span><span class="sxs-lookup"><span data-stu-id="91d65-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="91d65-177">Można określić **CanNotDelete** lub **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="91d65-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="91d65-178">toocreate lub usunięcia blokady zarządzania, należy mieć dostęp zbyt`Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje.</span><span class="sxs-lookup"><span data-stu-id="91d65-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="91d65-179">Witaj wbudowanych ról tylko właściciel i Administrator dostępu użytkowników są przyznawane te akcje.</span><span class="sxs-lookup"><span data-stu-id="91d65-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="91d65-180">tooapply blokady, użyj następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="91d65-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="91d65-181">Witaj zablokowane w hello poprzedzających przykład nie można usunąć zasobu do momentu usunięcia blokady hello.</span><span class="sxs-lookup"><span data-stu-id="91d65-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="91d65-182">tooremove blokady, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="91d65-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="91d65-183">Aby uzyskać więcej informacji na temat ustawienie blokady, zobacz [blokowania zasobów z usługi Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="91d65-184">Usuwanie zasobów lub grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="91d65-184">Remove resources or resource group</span></span>
<span data-ttu-id="91d65-185">Można usunąć zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="91d65-186">Usuń grupę zasobów, należy również usunąć wszystkie zasoby hello w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="91d65-187">toodelete zasobów z hello grupy zasobów, użyj hello **AzureRmResource Usuń** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91d65-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="91d65-188">To polecenie cmdlet usuwa hello zasobów, ale nie powoduje usunięcia hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="91d65-189">toodelete grupy zasobów i wszystkie jego zasoby, używać hello **Remove-AzureRmResourceGroup** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91d65-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="91d65-190">Dla obu poleceń cmdlet, zostanie wyświetlona prośba tooconfirm mają tooremove hello zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="91d65-191">Jeśli operacja hello pomyślnie usuwa hello zasób lub grupa zasobów, zwraca **True**.</span><span class="sxs-lookup"><span data-stu-id="91d65-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="91d65-192">Uruchamianie skryptów Menedżera zasobów w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="91d65-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="91d65-193">W tym temacie opisano sposób tooperform podstawowe operacje na zasoby przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91d65-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="91d65-194">W przypadku bardziej zaawansowanych scenariuszy zarządzania są zazwyczaj mają toocreate skryptu i ponownie użyć tego skryptu, zgodnie z potrzebami lub zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="91d65-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="91d65-195">[Automatyzacja Azure](../automation/automation-intro.md) umożliwia możesz tooautomate często używane skryptów, które zarządzają rozwiązań platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91d65-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="91d65-196">Witaj poniższe tematy przedstawiają sposób wykonywania zadań zarządzania toouse usługi Automatyzacja Azure Resource Manager i tooeffectively środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="91d65-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="91d65-197">Aby uzyskać informacje dotyczące tworzenia elementu runbook, zobacz [Moje pierwszego elementu runbook programu PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="91d65-198">Aby uzyskać informacje na temat pracy z galerii skryptów, zobacz [galerie elementów Runbook i modułów w automatyzacji Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="91d65-199">Dla elementów runbook uruchamianie i zatrzymywanie maszyn wirtualnych, zobacz [scenariusz automatyzacji Azure: toocreate formacie JSON przy użyciu tagów harmonogram uruchamiania maszyny Wirtualnej platformy Azure i zamykania](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="91d65-200">Dla elementów runbook uruchamianie i zatrzymywanie maszyn wirtualnych po godzinach pracy, zobacz [uruchamiania/zatrzymywania maszyn wirtualnych, podczas rozwiązania poza godzinami szczytu w automatyzacji](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91d65-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91d65-201">Next steps</span></span>
* <span data-ttu-id="91d65-202">toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [Authoring Azure Resource Manager szablony](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="91d65-203">toolearn o wdrażanie szablonów, zobacz [wdrażanie aplikacji przy użyciu szablonu usługi Resource Manager Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="91d65-204">Można przenieść istniejące zasoby tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="91d65-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="91d65-205">Aby uzyskać przykłady, zobacz [tooNew przeniesienia zasobów grupy zasobów lub subskrypcji](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="91d65-206">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="91d65-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

