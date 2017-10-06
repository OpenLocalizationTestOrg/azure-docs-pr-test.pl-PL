---
title: role niestandardowe aaaCreate dla Azure RBAC | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak role niestandardowe toodefine z kontroli dostępu dla bardziej precyzyjne zarządzanie tożsamościami w ramach subskrypcji platformy Azure."
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
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="36337-103">Tworzenie niestandardowych ról dla kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="36337-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="36337-104">Utwórz niestandardową rolę based kontroli dostępu (RBAC), jeśli żadna hello wbudowanych ról nie spełnia Twoje potrzeby określonym dostępu.</span><span class="sxs-lookup"><span data-stu-id="36337-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="36337-105">Role niestandardowe można tworzyć przy użyciu [programu Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfejsu wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) i hello [interfejsu API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="36337-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="36337-106">Podobnie jak wbudowane role można przypisać role niestandardowe toousers, grup i aplikacji w subskrypcji, grupy zasobów i zakresy zasobów.</span><span class="sxs-lookup"><span data-stu-id="36337-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="36337-107">Role niestandardowe są przechowywane w dzierżawie usługi Azure AD i mogą być udostępniane między subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="36337-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="36337-108">Poszczególni dzierżawcy można utworzyć zapasowej too2000 role niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="36337-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="36337-109">Witaj poniższy przykład przedstawia niestandardowej roli zabezpieczeń dotyczące monitorowania i ponowne uruchamianie maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="36337-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="36337-110">Akcje</span><span class="sxs-lookup"><span data-stu-id="36337-110">Actions</span></span>
<span data-ttu-id="36337-111">Witaj **akcje** określa właściwości niestandardowej roli zabezpieczeń hello Azure operacji toowhich hello rola przyznaje dostęp.</span><span class="sxs-lookup"><span data-stu-id="36337-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="36337-112">Jest kolekcją operacji ciągów, które identyfikują zabezpieczanego operacje dostawców zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36337-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="36337-113">Operacja ciągów wykonaj hello format `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="36337-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="36337-114">Ciągi operacji, które zawierają symbole wieloznaczne (\*) udzielić dostępu tooall operacje, które odpowiada hello operacji ciągu.</span><span class="sxs-lookup"><span data-stu-id="36337-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="36337-115">Na wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="36337-115">For instance:</span></span>

* <span data-ttu-id="36337-116">`*/read`udziela dostępu do operacji tooread dla wszystkich typów zasobów wszystkich dostawców zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36337-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="36337-117">`Microsoft.Compute/*`udziela dostępu do operacji tooall dla wszystkich typów zasobów dostawcy zasobów Microsoft.Compute hello.</span><span class="sxs-lookup"><span data-stu-id="36337-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="36337-118">`Microsoft.Network/*/read`udziela dostępu do operacji tooread dla wszystkich typów zasobów w dostawcę zasobów Microsoft.Network hello Azure.</span><span class="sxs-lookup"><span data-stu-id="36337-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="36337-119">`Microsoft.Compute/virtualMachines/*`udziela dostępu do operacji tooall maszyn wirtualnych i jego typów zasobów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="36337-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="36337-120">`Microsoft.Web/sites/restart/Action`udziela dostępu do witryn sieci Web toorestart.</span><span class="sxs-lookup"><span data-stu-id="36337-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="36337-121">Użyj `Get-AzureRmProviderOperation` (w programie PowerShell) lub `azure provider operations show` (w Azure CLI) operacji toolist dostawców zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36337-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="36337-122">Można także użyć tych poleceń tooverify, czy parametry operacji są prawidłowe i tooexpand symbolu wieloznacznego operacji ciągów.</span><span class="sxs-lookup"><span data-stu-id="36337-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Zrzut ekranu PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="36337-124">Azure CLI zrzut ekranu - azure dostawcy operacji Pokaż "Microsoft.Compute/virtualMachines/\*Action"</span><span class="sxs-lookup"><span data-stu-id="36337-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="36337-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="36337-125">NotActions</span></span>
<span data-ttu-id="36337-126">Użyj hello **NotActions** właściwość, o ile hello zestaw operacji, że chcesz tooallow łatwiej jest definiowana za pomocą z wyjątkiem operacji ograniczone.</span><span class="sxs-lookup"><span data-stu-id="36337-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="36337-127">Witaj dostępu przyznane przez niestandardowej roli zabezpieczeń jest obliczana przez odjęcie hello **NotActions** operacji hello **akcje** operacji.</span><span class="sxs-lookup"><span data-stu-id="36337-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="36337-128">Jeśli użytkownik ma przypisaną rolę, który wyklucza operacji w **NotActions**i ma przypisaną rolę drugiego, która udziela dostępu toohello tej samej operacji, hello użytkownika jest dozwolone tooperform tej operacji.</span><span class="sxs-lookup"><span data-stu-id="36337-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="36337-129">**NotActions** nie jest odmowy reguły — jest po prostu wygodny sposób toocreate zestaw dozwolonych operacji określonych operacji należy toobe wykluczone.</span><span class="sxs-lookup"><span data-stu-id="36337-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="36337-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="36337-130">AssignableScopes</span></span>
<span data-ttu-id="36337-131">Witaj **AssignableScopes** właściwości niestandardowej roli zabezpieczeń hello Określa zakresy hello (subskrypcji, grupy zasobów lub zasobów) w ramach których hello niestandardowej roli zabezpieczeń jest dostępne do przypisania.</span><span class="sxs-lookup"><span data-stu-id="36337-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="36337-132">Można udostępnić hello niestandardowej roli zabezpieczeń do przypisywania w tylko hello subskrypcji lub grupy zasobów, które wymagają, a nie użytkownika bałaganu środowisko reszty hello hello subskrypcji lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="36337-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="36337-133">Prawidłowe zakresy można przypisać należą:</span><span class="sxs-lookup"><span data-stu-id="36337-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="36337-134">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - sprawia, że rola hello jest dostępne do przypisania w dwóch subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="36337-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="36337-135">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - sprawia, że rola hello jest dostępne do przypisania w ramach jednej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="36337-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="36337-136">"/ subskrypcji i c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/sieci" - sprawia, że hello dostępne do przypisania tylko w grupie zasobów sieciowych hello roli.</span><span class="sxs-lookup"><span data-stu-id="36337-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="36337-137">Należy użyć co najmniej jednego subskrypcji, grupy zasobów lub identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="36337-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="36337-138">Kontrola dostępu role niestandardowe</span><span class="sxs-lookup"><span data-stu-id="36337-138">Custom roles access control</span></span>
<span data-ttu-id="36337-139">Witaj **AssignableScopes** właściwości niestandardowej roli zabezpieczeń hello również określać, kto może wyświetlać, modyfikowanie i usuwanie roli hello.</span><span class="sxs-lookup"><span data-stu-id="36337-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="36337-140">Który można utworzyć niestandardową rolę?</span><span class="sxs-lookup"><span data-stu-id="36337-140">Who can create a custom role?</span></span>
    <span data-ttu-id="36337-141">Właściciele (i administratorów dostępu użytkownika) subskrypcji, grupy zasobów i zasoby można tworzyć role niestandardowe do użycia w tych zakresów.</span><span class="sxs-lookup"><span data-stu-id="36337-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="36337-142">Hello tworzenie hello roli użytkownika musi tooperform stanie toobe `Microsoft.Authorization/roleDefinition/write` operację na wszystkich hello **AssignableScopes** hello roli.</span><span class="sxs-lookup"><span data-stu-id="36337-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="36337-143">Kto może zmodyfikować niestandardową rolę?</span><span class="sxs-lookup"><span data-stu-id="36337-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="36337-144">Właściciele (i administratorów dostępu użytkowników) z subskrypcji, grupy zasobów i zasoby można zmodyfikować role niestandardowe w tych zakresów.</span><span class="sxs-lookup"><span data-stu-id="36337-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="36337-145">Użytkownicy muszą hello stanie tooperform toobe `Microsoft.Authorization/roleDefinition/write` operację na wszystkich hello **AssignableScopes** z niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="36337-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="36337-146">Kto może wyświetlać role niestandardowe?</span><span class="sxs-lookup"><span data-stu-id="36337-146">Who can view custom roles?</span></span>
    <span data-ttu-id="36337-147">Wszystkie role wbudowane w Azure RBAC umożliwiają wyświetlanie ról, które są dostępne do przypisania.</span><span class="sxs-lookup"><span data-stu-id="36337-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="36337-148">Użytkownicy, którzy mogą wykonywać hello `Microsoft.Authorization/roleDefinition/read` operacji w zakresie mogą wyświetlać role RBAC hello, które są dostępne do przypisania w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="36337-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="36337-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="36337-149">See also</span></span>
* <span data-ttu-id="36337-150">[Kontroli dostępu opartej na rolach](role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36337-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="36337-151">Dowiedz się, jak toomanage do uzyskiwania dostępu do:</span><span class="sxs-lookup"><span data-stu-id="36337-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="36337-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36337-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="36337-153">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36337-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="36337-154">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="36337-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="36337-155">[Wbudowane role](role-based-access-built-in-roles.md): uzyskiwanie szczegółowych informacji o rolach hello, które standardowo w RBAC.</span><span class="sxs-lookup"><span data-stu-id="36337-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
