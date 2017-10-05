---
title: "Tworzenie niestandardowych ról dla Azure RBAC | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zdefiniować role niestandardowe z kontroli dostępu dla bardziej precyzyjne zarządzanie tożsamościami w ramach subskrypcji platformy Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8e72f2c8095d13c4b6df3c6576bd58806a3c0f2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="a3470-103">Tworzenie niestandardowych ról dla kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="a3470-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="a3470-104">Utwórz niestandardową rolę based kontroli dostępu (RBAC), jeśli żadna wbudowanych ról nie spełnia Twoje potrzeby określonym dostępu.</span><span class="sxs-lookup"><span data-stu-id="a3470-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="a3470-105">Role niestandardowe można tworzyć przy użyciu [programu Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfejsu wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) i [interfejsu API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a3470-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="a3470-106">Podobnie jak wbudowane role role niestandardowe można przypisać do użytkowników, grup i aplikacji w subskrypcji, grupy zasobów i zakresy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a3470-106">Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="a3470-107">Role niestandardowe są przechowywane w dzierżawie usługi Azure AD i mogą być udostępniane między subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="a3470-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="a3470-108">Każdy Dzierżawca może tworzyć role niestandardowe do 2000.</span><span class="sxs-lookup"><span data-stu-id="a3470-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="a3470-109">W poniższym przykładzie przedstawiono niestandardowej roli zabezpieczeń dotyczące monitorowania i ponowne uruchamianie maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="a3470-109">The following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="a3470-110">Akcje</span><span class="sxs-lookup"><span data-stu-id="a3470-110">Actions</span></span>
<span data-ttu-id="a3470-111">**Akcje** operacje platformy Azure, do których rola przyznaje dostęp określa właściwości niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a3470-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="a3470-112">Jest kolekcją operacji ciągów, które identyfikują zabezpieczanego operacje dostawców zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a3470-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="a3470-113">Operacja ciągów wykonaj format `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="a3470-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="a3470-114">Ciągi operacji, które zawierają symbole wieloznaczne (\*) udzielić dostępu do wszystkich operacji, które zgodny z ciągiem operacji.</span><span class="sxs-lookup"><span data-stu-id="a3470-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="a3470-115">Na wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="a3470-115">For instance:</span></span>

* <span data-ttu-id="a3470-116">`*/read`przyznaje dostęp do odczytu dla operacji dla wszystkich typów zasobów wszystkich dostawców zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a3470-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="a3470-117">`Microsoft.Compute/*`zapewnia dostęp do wszystkich operacji dla wszystkich typów zasobów w dostawcy zasobów Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="a3470-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="a3470-118">`Microsoft.Network/*/read`przyznaje dostęp do odczytu dla operacji dla wszystkich typów zasobów Microsoft.Network dostawcy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a3470-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="a3470-119">`Microsoft.Compute/virtualMachines/*`przyznaje dostęp do wszystkich operacji maszyn wirtualnych i jego podrzędny typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="a3470-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="a3470-120">`Microsoft.Web/sites/restart/Action`udziela dostępu do ponownego uruchomienia witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a3470-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="a3470-121">Użyj `Get-AzureRmProviderOperation` (w programie PowerShell) lub `azure provider operations show` (w Azure CLI) do operacji listy dostawców zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a3470-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="a3470-122">Może również używać tych poleceń, sprawdź, czy parametry operacji są prawidłowe i rozwiń ciągi operacji symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="a3470-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Zrzut ekranu PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="a3470-124">Azure CLI zrzut ekranu - azure dostawcy operacji Pokaż "Microsoft.Compute/virtualMachines/\*Action"</span><span class="sxs-lookup"><span data-stu-id="a3470-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="a3470-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="a3470-125">NotActions</span></span>
<span data-ttu-id="a3470-126">Użyj **NotActions** właściwości, jeśli zestaw działań, które mają być dozwolone łatwiej jest definiowana za pomocą z wyjątkiem operacji ograniczone.</span><span class="sxs-lookup"><span data-stu-id="a3470-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="a3470-127">Prawa dostępu przyznane przez niestandardowej roli zabezpieczeń jest obliczana przez odjęcie **NotActions** operacji **akcje** operacji.</span><span class="sxs-lookup"><span data-stu-id="a3470-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="a3470-128">Jeśli użytkownik ma przypisaną rolę, który wyklucza operacji w **NotActions**i ma przypisaną rolę drugiego, która udziela dostępu do tej samej operacji, użytkownik może wykonać tej operacji.</span><span class="sxs-lookup"><span data-stu-id="a3470-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user is allowed to perform that operation.</span></span> <span data-ttu-id="a3470-129">**NotActions** nie jest odmowy reguły — jest po prostu wygodny sposób utworzyć zestaw dozwolonych operacji podczas określonych operacji muszą być wykluczone.</span><span class="sxs-lookup"><span data-stu-id="a3470-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="a3470-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="a3470-130">AssignableScopes</span></span>
<span data-ttu-id="a3470-131">**AssignableScopes** właściwości niestandardowej roli określa zakresów (subskrypcji, grupy zasobów lub zasobów) w obrębie których są dostępne do przypisania roli niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="a3470-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="a3470-132">Udostępnienie tworzona rola niestandardowa przydziału w subskrypcji lub grupy zasobów, które wymagają i nie zajmowały czynności użytkownika dla pozostałej części subskrypcji lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a3470-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="a3470-133">Prawidłowe zakresy można przypisać należą:</span><span class="sxs-lookup"><span data-stu-id="a3470-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="a3470-134">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - sprawia, że rola jest dostępne do przypisania w dwóch subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a3470-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="a3470-135">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - sprawia, że rola jest dostępne do przypisania w ramach jednej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a3470-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="a3470-136">"/ subskrypcji i c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/sieci" - sprawia, że rola dostępne do przypisania tylko w grupie zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="a3470-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="a3470-137">Należy użyć co najmniej jednego subskrypcji, grupy zasobów lub identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="a3470-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="a3470-138">Kontrola dostępu role niestandardowe</span><span class="sxs-lookup"><span data-stu-id="a3470-138">Custom roles access control</span></span>
<span data-ttu-id="a3470-139">**AssignableScopes** właściwości niestandardowej roli również określać, kto może wyświetlać, modyfikowanie i usuwanie roli.</span><span class="sxs-lookup"><span data-stu-id="a3470-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="a3470-140">Który można utworzyć niestandardową rolę?</span><span class="sxs-lookup"><span data-stu-id="a3470-140">Who can create a custom role?</span></span>
    <span data-ttu-id="a3470-141">Właściciele (i administratorów dostępu użytkownika) subskrypcji, grupy zasobów i zasoby można tworzyć role niestandardowe do użycia w tych zakresów.</span><span class="sxs-lookup"><span data-stu-id="a3470-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="a3470-142">Tworzenie roli użytkownika musi mieć możliwość wykonania `Microsoft.Authorization/roleDefinition/write` operację na wszystkich **AssignableScopes** roli.</span><span class="sxs-lookup"><span data-stu-id="a3470-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="a3470-143">Kto może zmodyfikować niestandardową rolę?</span><span class="sxs-lookup"><span data-stu-id="a3470-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="a3470-144">Właściciele (i administratorów dostępu użytkowników) z subskrypcji, grupy zasobów i zasoby można zmodyfikować role niestandardowe w tych zakresów.</span><span class="sxs-lookup"><span data-stu-id="a3470-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="a3470-145">Użytkownicy muszą mieć możliwość wykonania `Microsoft.Authorization/roleDefinition/write` operację na wszystkich **AssignableScopes** z niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a3470-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="a3470-146">Kto może wyświetlać role niestandardowe?</span><span class="sxs-lookup"><span data-stu-id="a3470-146">Who can view custom roles?</span></span>
    <span data-ttu-id="a3470-147">Wszystkie role wbudowane w Azure RBAC umożliwiają wyświetlanie ról, które są dostępne do przypisania.</span><span class="sxs-lookup"><span data-stu-id="a3470-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="a3470-148">Użytkownicy, którzy mogą wykonywać `Microsoft.Authorization/roleDefinition/read` operacji w zakresie mogą wyświetlać role RBAC, które są dostępne do przypisania w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="a3470-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="a3470-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a3470-149">See also</span></span>
* <span data-ttu-id="a3470-150">[Kontroli dostępu opartej na rolach](role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a3470-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="a3470-151">Dowiedz się, jak Zarządzaj dostępem za pomocą:</span><span class="sxs-lookup"><span data-stu-id="a3470-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="a3470-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3470-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="a3470-153">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a3470-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="a3470-154">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="a3470-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="a3470-155">[Wbudowane role](role-based-access-built-in-roles.md): uzyskiwanie szczegółowych informacji dotyczących ról, które standardowo w RBAC.</span><span class="sxs-lookup"><span data-stu-id="a3470-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
