---
title: "Blokowanie zasobów platformy Azure, aby zapobiec zmianom | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="0e0b5-103">Blokowanie zasobów, aby uniemożliwić nieoczekiwane zmiany</span><span class="sxs-lookup"><span data-stu-id="0e0b5-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="0e0b5-104">Jako administrator może być konieczne zablokować subskrypcji, grupy zasobów lub zasobów uniemożliwić innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="0e0b5-105">Można ustawić poziom blokady **CanNotDelete** lub **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="0e0b5-106">**CanNotDelete** oznacza, że autoryzowani użytkownicy mogą nadal odczytywać i modyfikować zasobu, ale ich nie można usunąć tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="0e0b5-107">**Tylko do odczytu** oznacza, że autoryzowani użytkownicy mogą odczytywać zasobu, ale nie można usunąć lub zaktualizować zasobu.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="0e0b5-108">Stosowanie Ta blokada jest podobny do ograniczania wszystkim uprawnionym użytkownikom uprawnienia przyznane przez **czytnika** roli.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="0e0b5-109">Sposób stosowania blokad</span><span class="sxs-lookup"><span data-stu-id="0e0b5-109">How locks are applied</span></span>

<span data-ttu-id="0e0b5-110">Po zastosowaniu blokady w zakresie nadrzędnym, wszystkie zasoby w ramach tego zakresu dziedziczą tego samego blokady.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="0e0b5-111">Nawet zasoby, które później zostaną dodane dziedziczą blokady z obiektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="0e0b5-112">Najbardziej restrykcyjne blokady w dziedziczenia ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="0e0b5-113">W przeciwieństwie do kontroli dostępu opartej na rolach blokady zarządzania służy do stosowania ograniczenia we wszystkich użytkowników i ról.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="0e0b5-114">Aby dowiedzieć się więcej o ustawianiu uprawnień dla użytkowników i ról, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b5-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="0e0b5-115">Menedżer zasobów blokad mają zastosowanie tylko do operacji, które pojawiają się w płaszczyźnie zarządzania, która składa się z operacji wysyłane do `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="0e0b5-116">Blokad nie ograniczają jak zasoby wykonywanie własnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="0e0b5-117">Zmiany zasobu jest ograniczony, ale operacje zasobów nie są ograniczone.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="0e0b5-118">Na przykład tylko do odczytu blokady na bazę danych SQL pozwala usuwanie i modyfikowanie bazy danych, ale go nie uniemożliwiają tworzenie, aktualizowanie lub usuwanie danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="0e0b5-119">Transakcje danych są dozwolone, ponieważ te operacje nie są wysyłane do `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="0e0b5-120">Stosowanie **tylko do odczytu** może prowadzić do nieoczekiwanych wyników, ponieważ niektóre operacje, które się wydawać odczytu operacje rzeczywiście wymagają dodatkowych czynności.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="0e0b5-121">Na przykład wprowadzenie **tylko do odczytu** blokady na koncie magazynu uniemożliwia wyświetlanie kluczy wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="0e0b5-122">Listy kluczy operacji jest obsługiwany za pomocą żądania POST, ponieważ zwrócony klucze są dostępne do zapisu.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="0e0b5-123">Innym przykładem umieszczenie **tylko do odczytu** blokada na zasób usługi aplikacji uniemożliwia wyświetlanie plików dla zasobu, ponieważ dostęp do zapisu wymaga interakcji Eksploratora serwera w usłudze Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="0e0b5-124">Który można utworzyć lub usunąć blokady w organizacji</span><span class="sxs-lookup"><span data-stu-id="0e0b5-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="0e0b5-125">Aby utworzyć lub usunąć blokady zarządzania, musi mieć dostęp do `Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="0e0b5-126">Wbudowanych ról, tylko **właściciela** i **Administrator dostępu użytkowników** otrzymują te akcje.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="0e0b5-127">Portal</span><span class="sxs-lookup"><span data-stu-id="0e0b5-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="0e0b5-128">Szablon</span><span class="sxs-lookup"><span data-stu-id="0e0b5-128">Template</span></span>
<span data-ttu-id="0e0b5-129">W poniższym przykładzie przedstawiono szablon, który tworzy blokady na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="0e0b5-130">Konto magazynu, do którego jest stosowana blokada jest podać jako parametr.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="0e0b5-131">Nazwa blokady jest tworzony przez łączenie Nazwa zasobu z **/Microsoft.Authorization/** i nazwy blokady, w tym przypadku **myLock**.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="0e0b5-132">Typ określony jest specyficzne dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="0e0b5-133">Dla magazynu ustawienia typu "Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="0e0b5-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="0e0b5-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e0b5-134">PowerShell</span></span>
<span data-ttu-id="0e0b5-135">Zablokuj należy wdrożyć zasobów przy użyciu programu Azure PowerShell przy użyciu [AzureRmResourceLock nowy](/powershell/module/azurerm.resources/new-azurermresourcelock) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="0e0b5-136">Aby zablokować zasobu, należy podać nazwę zasobu, jego typ zasobu i jego nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="0e0b5-137">Aby zablokować grupę zasobów, podaj nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="0e0b5-138">Aby uzyskać informacje o blokadę, użyj [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="0e0b5-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="0e0b5-139">Aby uzyskać wszystkie blokady w ramach subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="0e0b5-140">Aby uzyskać wszystkie blokady dla zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="0e0b5-141">Aby uzyskać wszystkie blokady dla grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="0e0b5-142">Program Azure PowerShell udostępnia inne polecenia blokad pracy, takich jak [AzureRmResourceLock zestaw](/powershell/module/azurerm.resources/set-azurermresourcelock) zaktualizować blokady, i [AzureRmResourceLock Usuń](/powershell/module/azurerm.resources/remove-azurermresourcelock) można usunąć blokadę.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="0e0b5-143">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e0b5-143">Azure CLI</span></span>

<span data-ttu-id="0e0b5-144">Zablokuj należy wdrożyć zasobów przy użyciu wiersza polecenia platformy Azure przy użyciu [utworzyć blokady az](/cli/azure/lock#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="0e0b5-145">Aby zablokować zasobu, należy podać nazwę zasobu, jego typ zasobu i jego nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="0e0b5-146">Aby zablokować grupę zasobów, podaj nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="0e0b5-147">Aby uzyskać informacje o blokadę, użyj [listy blokady az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="0e0b5-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="0e0b5-148">Aby uzyskać wszystkie blokady w ramach subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="0e0b5-149">Aby uzyskać wszystkie blokady dla zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="0e0b5-150">Aby uzyskać wszystkie blokady dla grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="0e0b5-151">Interfejsu wiersza polecenia platformy Azure udostępnia inne polecenia blokad pracy, takich jak [az blokady aktualizacji](/cli/azure/lock#update) zaktualizować blokady, i [usunąć blokady az](/cli/azure/lock#delete) do usunięcia blokady.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="0e0b5-152">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="0e0b5-152">REST API</span></span>
<span data-ttu-id="0e0b5-153">Można zablokować wdrożonych zasobów z [interfejsu API REST zarządzania blokad](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="0e0b5-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="0e0b5-154">Interfejs API REST umożliwia tworzenie i usuwanie blokad i pobierania informacji o istniejące blokady.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="0e0b5-155">Aby utworzyć blokadę, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="0e0b5-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="0e0b5-156">Zakres może być subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="0e0b5-157">Nazwa blokady jest dowolne wywołać blokady.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="0e0b5-158">Wersja interfejsu api, można użyć **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="0e0b5-159">W żądaniu obejmują obiekt JSON, który określa właściwości blokady.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="0e0b5-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e0b5-160">Next steps</span></span>
* <span data-ttu-id="0e0b5-161">Aby uzyskać więcej informacji na temat pracy z blokowania zasobów, zobacz [blokady w dół Your Azure zasobów](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="0e0b5-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="0e0b5-162">Aby dowiedzieć się więcej na temat logicznie organizowania zasobów, zobacz [przy użyciu tagów do organizowania zasobów](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="0e0b5-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="0e0b5-163">Aby zmienić grupę zasobów, zasób znajduje się w, zobacz [przenoszenia zasobów do nowej grupy zasobów](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="0e0b5-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="0e0b5-164">Ograniczenia i konwencje można stosować w subskrypcji z niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="0e0b5-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="0e0b5-165">Aby uzyskać więcej informacji, zobacz [Use Policy to manage resources and control access](resource-manager-policy.md) (Zarządzanie zasobami i kontrola dostępu przy użyciu zasad).</span><span class="sxs-lookup"><span data-stu-id="0e0b5-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="0e0b5-166">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="0e0b5-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

