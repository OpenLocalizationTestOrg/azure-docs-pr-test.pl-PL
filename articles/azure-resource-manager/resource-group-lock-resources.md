---
title: "zmiany tooprevent zasobów Azure aaaLock | Dokumentacja firmy Microsoft"
description: "Uniemożliwić użytkownikom aktualizowanie lub usuwanie kluczowych zasobów platformy Azure, stosując blokady dla wszystkich użytkowników i ról."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="e35ea-103">Blokowanie zasobów tooprevent nieoczekiwane zmiany</span><span class="sxs-lookup"><span data-stu-id="e35ea-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="e35ea-104">Jako administrator może być konieczne toolock subskrypcji, grupy zasobów lub tooprevent zasobów innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e35ea-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="e35ea-105">Można ustawić poziomu blokady hello także**CanNotDelete** lub **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="e35ea-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="e35ea-106">**CanNotDelete** oznacza, że autoryzowani użytkownicy mogą nadal odczytywać i modyfikować zasobu, ale nie można ich usunąć hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="e35ea-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="e35ea-107">**Tylko do odczytu** oznacza, że autoryzowani użytkownicy mogą odczytywać zasobu, ale nie można usunąć lub zaktualizować zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="e35ea-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="e35ea-108">Zastosowanie Ta blokada jest podobne toorestricting wszystkich uprawnień użytkowników toohello uprawnienia przyznane przez hello **czytnika** roli.</span><span class="sxs-lookup"><span data-stu-id="e35ea-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="e35ea-109">Sposób stosowania blokad</span><span class="sxs-lookup"><span data-stu-id="e35ea-109">How locks are applied</span></span>

<span data-ttu-id="e35ea-110">Po zastosowaniu blokady w zakresie nadrzędnym, wszystkie zasoby w tym zakresie dziedziczą hello tego samego blokady.</span><span class="sxs-lookup"><span data-stu-id="e35ea-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="e35ea-111">Nawet zasoby, które później zostaną dodane Dziedzicz blokady hello hello nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="e35ea-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="e35ea-112">Witaj najbardziej restrykcyjne blokady w dziedziczeniu hello pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="e35ea-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="e35ea-113">W przeciwieństwie do kontroli dostępu opartej na rolach możesz użyć tooapply blokady zarządzania ograniczenie we wszystkich użytkowników i ról.</span><span class="sxs-lookup"><span data-stu-id="e35ea-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="e35ea-114">toolearn o ustawianiu uprawnień dla użytkowników i ról, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e35ea-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="e35ea-115">Menedżer zasobów blokad zastosować tylko toooperations to zrobić w płaszczyźnie zarządzania hello, która składa się z operacji wysłany`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="e35ea-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="e35ea-116">Hello blokad nie ograniczają jak zasoby wykonywanie własnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="e35ea-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="e35ea-117">Zmiany zasobu jest ograniczony, ale operacje zasobów nie są ograniczone.</span><span class="sxs-lookup"><span data-stu-id="e35ea-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="e35ea-118">Na przykład blokady w bazie danych SQL tylko do odczytu uniemożliwia usuwanie lub modyfikowanie hello bazy danych, ale nie uniemożliwiać tworzenie, aktualizowanie lub usuwanie danych hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e35ea-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="e35ea-119">Transakcje danych są dozwolone, ponieważ te operacje nie są wysyłane za`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="e35ea-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="e35ea-120">Stosowanie **tylko do odczytu** może prowadzić toounexpected wyników, ponieważ niektóre operacje, które się wydawać odczytu operacje rzeczywiście wymagają dodatkowych czynności.</span><span class="sxs-lookup"><span data-stu-id="e35ea-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="e35ea-121">Na przykład wprowadzenie **tylko do odczytu** blokady na koncie magazynu uniemożliwia wyświetlanie kluczy hello wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e35ea-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="e35ea-122">Lista Hello operacji kluczy jest obsługiwana za pomocą żądania POST, ponieważ hello zwrócił się, że klucze są dostępne do zapisu.</span><span class="sxs-lookup"><span data-stu-id="e35ea-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="e35ea-123">Innym przykładem umieszczenie **tylko do odczytu** blokada na zasób usługi aplikacji — uniemożliwia wyświetlanie plików hello zasobu, ponieważ dostęp do zapisu wymaga interakcji Eksploratora serwera w usłudze Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e35ea-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="e35ea-124">Który można utworzyć lub usunąć blokady w organizacji</span><span class="sxs-lookup"><span data-stu-id="e35ea-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="e35ea-125">toocreate lub usunięcia blokady zarządzania, należy mieć dostęp zbyt`Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje.</span><span class="sxs-lookup"><span data-stu-id="e35ea-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="e35ea-126">Witaj wbudowanych ról, tylko **właściciela** i **Administrator dostępu użytkowników** otrzymują te akcje.</span><span class="sxs-lookup"><span data-stu-id="e35ea-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="e35ea-127">Portal</span><span class="sxs-lookup"><span data-stu-id="e35ea-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="e35ea-128">Szablon</span><span class="sxs-lookup"><span data-stu-id="e35ea-128">Template</span></span>
<span data-ttu-id="e35ea-129">Witaj poniższy przykład przedstawia szablon, który tworzy blokady na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="e35ea-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="e35ea-130">Konto magazynu Hello, na które tooapply blokady hello jest podać jako parametr.</span><span class="sxs-lookup"><span data-stu-id="e35ea-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="e35ea-131">Witaj nazwy blokady hello jest tworzony przez łączenie hello Nazwa zasobu z **/Microsoft.Authorization/** i hello w takim przypadku nazwa blokady hello **myLock**.</span><span class="sxs-lookup"><span data-stu-id="e35ea-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="e35ea-132">podano typ Hello jest toohello określonego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="e35ea-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="e35ea-133">W przypadku magazynu wartość too"Microsoft.Storage/storageaccounts/providers/locks typu hello".</span><span class="sxs-lookup"><span data-stu-id="e35ea-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="e35ea-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e35ea-134">PowerShell</span></span>
<span data-ttu-id="e35ea-135">Zablokuj należy wdrożyć zasobów przy użyciu programu Azure PowerShell przy użyciu hello [AzureRmResourceLock nowy](/powershell/module/azurerm.resources/new-azurermresourcelock) polecenia.</span><span class="sxs-lookup"><span data-stu-id="e35ea-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="e35ea-136">toolock zasobu, podaj nazwę hello hello zasobów, jego typ zasobu i jego nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e35ea-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="e35ea-137">toolock grupę zasobów, podaj nazwę hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e35ea-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="e35ea-138">tooget informacji na temat blokowania, użyj [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="e35ea-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="e35ea-139">tooget Użyj wszystkich blokad hello w Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="e35ea-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="e35ea-140">tooget wszystkie blokady dla zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e35ea-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="e35ea-141">tooget wszystkie blokady dla grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e35ea-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="e35ea-142">Program Azure PowerShell udostępnia inne polecenia blokad pracy, takich jak [AzureRmResourceLock zestaw](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate blokady, i [AzureRmResourceLock Usuń](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete blokady.</span><span class="sxs-lookup"><span data-stu-id="e35ea-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="e35ea-143">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e35ea-143">Azure CLI</span></span>

<span data-ttu-id="e35ea-144">Zablokuj należy wdrożyć zasobów przy użyciu wiersza polecenia platformy Azure przy użyciu hello [utworzyć blokady az](/cli/azure/lock#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="e35ea-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="e35ea-145">toolock zasobu, podaj nazwę hello hello zasobów, jego typ zasobu i jego nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e35ea-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="e35ea-146">toolock grupę zasobów, podaj nazwę hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e35ea-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="e35ea-147">tooget informacji na temat blokowania, użyj [listy blokady az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="e35ea-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="e35ea-148">tooget Użyj wszystkich blokad hello w Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="e35ea-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="e35ea-149">tooget wszystkie blokady dla zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e35ea-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="e35ea-150">tooget wszystkie blokady dla grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e35ea-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="e35ea-151">Interfejs wiersza polecenia platformy Azure udostępnia innych poleceń blokad pracy, takich jak [az blokady aktualizacji](/cli/azure/lock#update) tooupdate blokady, i [usunąć blokady az](/cli/azure/lock#delete) toodelete blokady.</span><span class="sxs-lookup"><span data-stu-id="e35ea-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="e35ea-152">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="e35ea-152">REST API</span></span>
<span data-ttu-id="e35ea-153">Można zablokować wdrożonych zasobów z hello [interfejsu API REST zarządzania blokad](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="e35ea-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="e35ea-154">Witaj interfejsu API REST umożliwia toocreate i usuwa blokady i pobierania informacji o istniejących blokad.</span><span class="sxs-lookup"><span data-stu-id="e35ea-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="e35ea-155">toocreate blokady, uruchom:</span><span class="sxs-lookup"><span data-stu-id="e35ea-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="e35ea-156">zakres Hello może być subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="e35ea-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="e35ea-157">Witaj Nazwa blokady jest dowolne toocall hello blokady.</span><span class="sxs-lookup"><span data-stu-id="e35ea-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="e35ea-158">Wersja interfejsu api, można użyć **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="e35ea-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="e35ea-159">W żądaniu hello obejmują obiekt JSON, który określa właściwości hello hello blokady.</span><span class="sxs-lookup"><span data-stu-id="e35ea-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="e35ea-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e35ea-160">Next steps</span></span>
* <span data-ttu-id="e35ea-161">Aby uzyskać więcej informacji na temat pracy z blokowania zasobów, zobacz [blokady w dół Your Azure zasobów](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="e35ea-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="e35ea-162">toolearn o logicznego organizowania zasobów, zobacz [używanie tagów tooorganize zasobów](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="e35ea-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="e35ea-163">toochange grupę zasobów zasób znajduje się w temacie [przeniesienie zasobów toonew zasobów grupy](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e35ea-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="e35ea-164">Ograniczenia i konwencje można stosować w subskrypcji z niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="e35ea-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="e35ea-165">Aby uzyskać więcej informacji, zobacz [zasady toomanage zasobów i kontroli dostępu](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e35ea-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="e35ea-166">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e35ea-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

