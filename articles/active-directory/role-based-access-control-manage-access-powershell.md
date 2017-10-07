---
title: "aaaManage opartej na rolach kontroli dostępu (RBAC) przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Jak toomanage RBAC z programem Azure PowerShell, w tym role, przypisywanie ról i usuwanie przypisań ról."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="63517-103">Zarządzanie kontrolą dostępu opartą na rolach za pomocą programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="63517-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="63517-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63517-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="63517-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="63517-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="63517-106">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="63517-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="63517-107">Kontrola dostępu oparta na rolach (RBAC) służy w hello portalu Azure i interfejs API zarządzania zasobów Azure toomanage dostępu tooyour subskrypcji na poziomie szczegółowych.</span><span class="sxs-lookup"><span data-stu-id="63517-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="63517-108">W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując toothem niektórych ról w określonym zakresie.</span><span class="sxs-lookup"><span data-stu-id="63517-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="63517-109">Przed użyciem programu PowerShell toomanage RBAC, należy hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="63517-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="63517-110">Program Azure PowerShell w wersji 0.8.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="63517-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="63517-111">tooinstall hello najnowszej wersji i powiąż go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63517-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="63517-112">Polecenia cmdlet Menedżera zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="63517-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="63517-113">Zainstaluj hello [poleceń cmdlet usługi Azure Resource Manager](/powershell/azure/overview) w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63517-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="63517-114">Lista ról</span><span class="sxs-lookup"><span data-stu-id="63517-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="63517-115">Wyświetl listę wszystkich dostępnych ról</span><span class="sxs-lookup"><span data-stu-id="63517-115">List all available roles</span></span>
<span data-ttu-id="63517-116">role RBAC toolist, które są dostępne do przypisania i toowhich operacji hello tooinspect przyznają dostęp, użyj `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="63517-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="63517-118">Akcje listy roli</span><span class="sxs-lookup"><span data-stu-id="63517-118">List actions of a role</span></span>
<span data-ttu-id="63517-119">działania hello toolist dla konkretnej roli przy użyciu `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="63517-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition dla konkretnej roli - RBAC](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="63517-121">Zobacz, kto ma dostęp</span><span class="sxs-lookup"><span data-stu-id="63517-121">See who has access</span></span>
<span data-ttu-id="63517-122">przydziały dostępu RBAC toolist, użyj `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="63517-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="63517-123">Lista przypisań ról w określonym zakresie</span><span class="sxs-lookup"><span data-stu-id="63517-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="63517-124">Znajduje wszystkie przypisania dostępu powitania dla określonej subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="63517-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="63517-125">Na przykład toosee hello wszystkich hello active przydziałów dla grupy zasobów, użyj `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="63517-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![Zrzut ekranu PowerShell-Get AzureRmRoleAssignment dla grupy zasobów - RBAC](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="63517-127">Lista ról przypisany użytkownik tooa</span><span class="sxs-lookup"><span data-stu-id="63517-127">List roles assigned tooa user</span></span>
<span data-ttu-id="63517-128">wszystkie role hello przypisanych tooa określony użytkownika i przypisanych grup toohello toowhich hello użytkownika, należy ról hello toolist użyj `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="63517-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![Zrzut ekranu PowerShell-Get AzureRmRoleAssignment dla użytkownika — RBAC](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="63517-130">Wyświetl listę przypisań ról administratora i coadmin klasycznym usługi</span><span class="sxs-lookup"><span data-stu-id="63517-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="63517-131">toolist dostępu przydziały hello subskrypcji klasycznego administratora i coadministrators, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="63517-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="63517-132">Udzielanie dostępu</span><span class="sxs-lookup"><span data-stu-id="63517-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="63517-133">Wyszukaj identyfikatory obiektów</span><span class="sxs-lookup"><span data-stu-id="63517-133">Search for object IDs</span></span>
<span data-ttu-id="63517-134">tooassign roli należy tooidentify zarówno hello obiektów (użytkowników, grupy lub aplikacji), jak i zakres hello.</span><span class="sxs-lookup"><span data-stu-id="63517-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="63517-135">Jeśli nie znasz hello identyfikator subskrypcji można znaleźć je w hello **subskrypcje** bloku na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="63517-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="63517-136">toolearn tooquery hello subskrypcji o identyfikatorze, zobacz temat [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="63517-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="63517-137">Użyj Identyfikatora obiektu hello tooget dla grupy usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="63517-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="63517-138">Identyfikator obiektu hello tooget nazwy głównej usługi Azure AD lub aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="63517-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="63517-139">Przypisz aplikację tooan rola w zakresie subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="63517-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="63517-140">toogrant aplikacji tooan dostępu w zakresie subskrypcji hello, użyj:</span><span class="sxs-lookup"><span data-stu-id="63517-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![Zrzut ekranu PowerShell — nowy AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="63517-142">Przypisywanie roli użytkownika tooa w zakresie grupy zasobów hello</span><span class="sxs-lookup"><span data-stu-id="63517-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="63517-143">toogrant dostęp tooa użytkownika w zakresie hello do grupy zasobów, użyj:</span><span class="sxs-lookup"><span data-stu-id="63517-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![Zrzut ekranu PowerShell — nowy AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="63517-145">Przypisz grupę tooa rola w zakresie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="63517-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="63517-146">toogrant grupy tooa dostępu w zakresie zasobów hello, użyj:</span><span class="sxs-lookup"><span data-stu-id="63517-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![Zrzut ekranu PowerShell — nowy AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="63517-148">Usuń dostęp</span><span class="sxs-lookup"><span data-stu-id="63517-148">Remove access</span></span>
<span data-ttu-id="63517-149">tooremove dostęp dla użytkowników, grup i aplikacji, użyj:</span><span class="sxs-lookup"><span data-stu-id="63517-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![Zrzut ekranu PowerShell-Remove AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="63517-151">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="63517-151">Create a custom role</span></span>
<span data-ttu-id="63517-152">toocreate niestandardowej roli zabezpieczeń, użyj hello ```New-AzureRmRoleDefinition``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="63517-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="63517-153">Istnieją dwie metody struktury hello rolę, za pomocą PSRoleDefinitionObject lub szablonu JSON.</span><span class="sxs-lookup"><span data-stu-id="63517-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="63517-154">Pobierz akcji dla dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="63517-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="63517-155">Tworząc role niestandardowe od początku, jest ważne tooknow hello wszystkie możliwe operacje z hello dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="63517-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="63517-156">Użyj hello ```Get-AzureRMProviderOperation``` polecenia tooget te informacje.</span><span class="sxs-lookup"><span data-stu-id="63517-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="63517-157">Na przykład jeśli chcesz toocheck wszystkie hello operacje dostępne dla maszyny wirtualnej, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="63517-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="63517-158">Tworzenie roli z PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="63517-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="63517-159">Korzystając z programu PowerShell toocreate niestandardowej roli zabezpieczeń, możesz rozpocząć od początku lub użyj jednej z hello [wbudowane role](role-based-access-built-in-roles.md) jako punktu wyjścia.</span><span class="sxs-lookup"><span data-stu-id="63517-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="63517-160">przykład Witaj w tej sekcji rozpoczyna się od wbudowanej roli i dostosowuje go z wyższego poziomu uprawnień.</span><span class="sxs-lookup"><span data-stu-id="63517-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="63517-161">Edytuj hello atrybuty tooadd hello *akcje*, *notActions*, lub *zakresy* , a następnie zapisz zmiany hello jako nową rolę.</span><span class="sxs-lookup"><span data-stu-id="63517-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="63517-162">Hello poniższy przykład rozpoczyna się od hello *Współautor·maszyny·wirtualnej* roli i używa tego toocreate niestandardowej roli zabezpieczeń o nazwie *Operator maszyny wirtualnej*.</span><span class="sxs-lookup"><span data-stu-id="63517-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="63517-163">Witaj nowa rola przyznaje tooall dostęp do odczytu dla operacji *Microsoft.Compute*, *Microsoft.Storage*, i *Microsoft.Network* dostęp do dostawcy i przyznaje zasobów toostart, ponownie uruchomić i monitorować maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="63517-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="63517-164">Rola niestandardowa Hello może służyć w dwóch subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="63517-164">hello custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="63517-166">Tworzenie roli przy użyciu szablonu JSON</span><span class="sxs-lookup"><span data-stu-id="63517-166">Create role with JSON template</span></span>
<span data-ttu-id="63517-167">Szablon JSON można jako definicji źródła hello hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="63517-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="63517-168">Witaj poniższy przykład tworzy niestandardową rolę, która umożliwia dostęp do odczytu toostorage i zasoby obliczeniowe, dostęp do toosupport i dodaje tej roli tootwo subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="63517-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="63517-169">Utwórz nowy plik `C:\CustomRoles\customrole1.json` z hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="63517-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="63517-170">Witaj Id powinna być ustawiona zbyt`null` na tworzenie początkowej roli jako nowy identyfikator jest generowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="63517-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="63517-171">tooadd hello roli toohello subskrypcje, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="63517-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="63517-172">Modyfikowanie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="63517-172">Modify a custom role</span></span>
<span data-ttu-id="63517-173">Podobne toocreating niestandardowej roli zabezpieczeń, można zmodyfikować istniejącą rolę niestandardowych za pomocą hello PSRoleDefinitionObject lub szablonu JSON.</span><span class="sxs-lookup"><span data-stu-id="63517-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="63517-174">Modyfikuj rolę z PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="63517-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="63517-175">toomodify niestandardowej roli zabezpieczeń, najpierw użyj hello `Get-AzureRmRoleDefinition` definicji roli hello tooretrieve poleceń.</span><span class="sxs-lookup"><span data-stu-id="63517-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="63517-176">Po drugie zmiany hello potrzeby toohello definicji roli.</span><span class="sxs-lookup"><span data-stu-id="63517-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="63517-177">Na koniec użyj hello `Set-AzureRmRoleDefinition` hello toosave polecenia zmodyfikować definicji roli.</span><span class="sxs-lookup"><span data-stu-id="63517-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="63517-178">Witaj poniższy przykład umożliwia dodanie hello `Microsoft.Insights/diagnosticSettings/*` toohello operacji *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="63517-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![Zrzut ekranu PowerShell-Set AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="63517-180">Witaj poniższy przykład umożliwia dodanie zakresy możliwe do przypisania toohello subskrypcji platformy Azure z hello *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="63517-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![Zrzut ekranu PowerShell-Set AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="63517-182">Modyfikuj rolę przy użyciu szablonu JSON</span><span class="sxs-lookup"><span data-stu-id="63517-182">Modify role with JSON template</span></span>
<span data-ttu-id="63517-183">Przy użyciu szablonu JSON w poprzednim hello, można łatwo zmodyfikować istniejący tooadd niestandardowej roli zabezpieczeń lub usunąć akcje.</span><span class="sxs-lookup"><span data-stu-id="63517-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="63517-184">Aktualizowanie hello JSON szablonu, a następnie dodaj hello odczytu działania dotyczące sieci, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="63517-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="63517-185">definicje Hello hello szablonu na liście są zbiorczo zastosowane tooan istniejącej definicji, co oznacza, że ta rola hello pojawi się dokładnie, jak określone w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="63517-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="63517-186">Należy również pole identyfikatora hello tooupdate o identyfikatorze hello hello roli.</span><span class="sxs-lookup"><span data-stu-id="63517-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="63517-187">Jeśli nie masz pewności, ta wartość jest, możesz użyć hello `Get-AzureRmRoleDefinition` tooget polecenia cmdlet te informacje.</span><span class="sxs-lookup"><span data-stu-id="63517-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="63517-188">tooupdate hello istniejącą rolę, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="63517-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="63517-189">Usunięcia niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="63517-189">Delete a custom role</span></span>
<span data-ttu-id="63517-190">toodelete niestandardowej roli zabezpieczeń, użyj hello `Remove-AzureRmRoleDefinition` polecenia.</span><span class="sxs-lookup"><span data-stu-id="63517-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="63517-191">Witaj poniższy przykład umożliwia usunięcie hello *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="63517-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![Zrzut ekranu PowerShell-Remove AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="63517-193">Lista ról niestandardowych</span><span class="sxs-lookup"><span data-stu-id="63517-193">List custom roles</span></span>
<span data-ttu-id="63517-194">toolist hello ról, które są dostępne do przypisania w zakresie, użyj hello `Get-AzureRmRoleDefinition` polecenia.</span><span class="sxs-lookup"><span data-stu-id="63517-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="63517-195">Poniższy przykład Hello zawiera listę wszystkich ról, które są dostępne do przypisania w ramach subskrypcji hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="63517-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="63517-197">W hello poniższy przykład, hello *Operator maszyny wirtualnej* rola niestandardowa nie jest dostępna w hello *Production4* subskrypcji, ponieważ nie ma subskrypcji hello  **AssignableScopes** hello roli.</span><span class="sxs-lookup"><span data-stu-id="63517-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="63517-199">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="63517-199">See also</span></span>
* <span data-ttu-id="63517-200">[Używanie programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="63517-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

