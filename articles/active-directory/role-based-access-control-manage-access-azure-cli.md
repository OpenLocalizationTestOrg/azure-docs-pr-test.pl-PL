---
title: "aaaManage opartej na rolach kontrola dostępu (RBAC) przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage opartej na rolach kontrola dostępu (RBAC) przy użyciu wiersza polecenia Azure hello interfejsu listę ról i roli akcje i przypisywanie ról toohello zakresy subskrypcji i aplikacji."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="1fc5f-103">Zarządzanie oparte na rolach kontrola dostępu przy użyciu hello interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1fc5f-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fc5f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fc5f-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="1fc5f-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1fc5f-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="1fc5f-106">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="1fc5f-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="1fc5f-107">Kontrola dostępu oparta na rolach (RBAC) służy w hello portalu Azure i interfejsu API usługi Azure Resource Manager toomanage dostępu tooyour subskrypcji i zasobów na poziomie szczegółowych.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="1fc5f-108">W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując toothem niektórych ról w określonym zakresie.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="1fc5f-109">Przed użyciem hello Azure interfejsu wiersza polecenia (CLI) toomanage RBAC, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="1fc5f-110">Azure CLI w wersji 0.8.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="1fc5f-111">tooinstall hello najnowszej wersji i powiąż go z subskrypcją platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1fc5f-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="1fc5f-112">Usługa Azure Resource Manager w interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="1fc5f-113">Przejdź za[hello Using Azure CLI z hello Resource Manager](../xplat-cli-azure-resource-manager.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="1fc5f-114">Lista ról</span><span class="sxs-lookup"><span data-stu-id="1fc5f-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="1fc5f-115">Wyświetl listę wszystkich dostępnych ról</span><span class="sxs-lookup"><span data-stu-id="1fc5f-115">List all available roles</span></span>
<span data-ttu-id="1fc5f-116">toolist wszystkie dostępne role, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="1fc5f-117">Witaj poniższy przykład przedstawia listę hello *wszystkie dostępne role*.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Zrzut ekranu wiersza polecenia — Lista roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="1fc5f-119">Akcje listy roli</span><span class="sxs-lookup"><span data-stu-id="1fc5f-119">List actions of a role</span></span>
<span data-ttu-id="1fc5f-120">Akcje hello toolist roli, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="1fc5f-121">Hello poniższy przykład przedstawia hello akcje hello *współautora* i *Współautor·maszyny·wirtualnej* ról.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Zrzut ekranu wiersza polecenia — Pokaż roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="1fc5f-123">Dostęp do listy</span><span class="sxs-lookup"><span data-stu-id="1fc5f-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="1fc5f-124">Lista przypisań ról skuteczne w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="1fc5f-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="1fc5f-125">przypisania ról hello toolist, które istnieją w grupie zasobów, użyj:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="1fc5f-126">Witaj poniższy przykład przedstawia przypisań ról hello w hello *pharma sprzedaży projecforcast* grupy.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Zrzut ekranu wiersza polecenia — Lista przypisywanie roli azure przez grupę - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="1fc5f-128">Lista przypisań ról dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="1fc5f-128">List role assignments for a user</span></span>
<span data-ttu-id="1fc5f-129">przypisania ról hello toolist dla określonego użytkownika i hello przypisań grup tooa użytkowników, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="1fc5f-130">Możesz też sprawdzić przypisań ról, które są dziedziczone z grupy, modyfikując hello polecenia:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="1fc5f-131">Witaj poniższy przykład przedstawia hello przypisań ról, którym udzielono toohello  *sameert@aaddemo.com*  użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="1fc5f-132">W tym role, które są przypisywane bezpośrednio toohello użytkowników i role, które są dziedziczone z grupy.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Zrzut ekranu wiersza polecenia — Lista przypisywanie roli azure przez użytkownika - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="1fc5f-134">Udzielanie dostępu</span><span class="sxs-lookup"><span data-stu-id="1fc5f-134">Grant access</span></span>
<span data-ttu-id="1fc5f-135">toogrant dostępu po zidentyfikowaniu hello roli, które mają tooassign za pomocą:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="1fc5f-136">Przypisz toogroup roli, w zakresie subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="1fc5f-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="1fc5f-137">tooassign grupy tooa ról w zakresie subskrypcji hello, użyj:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1fc5f-138">Witaj w poniższym przykładzie przypisano hello *czytnika* roli zbyt*zespołu Christine Koch* na powitania *subskrypcji* zakresu.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć grupy — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="1fc5f-140">Przypisz aplikację tooan rola w zakresie subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="1fc5f-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="1fc5f-141">tooassign aplikacją tooan rola w zakresie subskrypcji hello, użyj:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1fc5f-142">Witaj w przykładzie poniżej zezwolenie hello *współautora* tooan roli *usługi Azure AD* wybrać aplikację na powitania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć przez aplikację](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="1fc5f-144">Przypisywanie roli użytkownika tooa w zakresie grupy zasobów hello</span><span class="sxs-lookup"><span data-stu-id="1fc5f-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="1fc5f-145">tooassign tooa roli użytkownika w zakresie hello do grupy zasobów, użyj:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="1fc5f-146">Witaj poniższy przykład przyznaje hello *współautora maszyny wirtualnej* roli zbyt *samert@aaddemo.com*  użytkownika na powitania *Pharma-sprzedaży-ProjectForcast* zakres grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć przez użytkownika — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="1fc5f-148">Przypisz grupę tooa rola w zakresie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="1fc5f-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="1fc5f-149">tooassign grupy tooa ról w zakresie zasobów hello, użyj:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="1fc5f-150">Witaj w przykładzie poniżej zezwolenie hello *współautora maszyny wirtualnej* tooan roli *usługi Azure AD* na *podsieci*.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć grupy — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="1fc5f-152">Usuń dostęp</span><span class="sxs-lookup"><span data-stu-id="1fc5f-152">Remove access</span></span>
<span data-ttu-id="1fc5f-153">Użyj tooremove przypisania roli:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="1fc5f-154">Hello poniższy przykład umożliwia usunięcie hello *Współautor·maszyny·wirtualnej* przypisania roli z hello  *sammert@aaddemo.com*  użytkownika na powitania *Pharma-sprzedaży-ProjectForcast* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="1fc5f-155">przykład Witaj następnie usuwa przypisanie roli hello grupy na powitania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Zrzut ekranu wiersza polecenia - usunięcia przypisania roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="1fc5f-157">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="1fc5f-157">Create a custom role</span></span>
<span data-ttu-id="1fc5f-158">toocreate niestandardowej roli zabezpieczeń, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="1fc5f-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="1fc5f-159">Witaj poniższy przykład powoduje utworzenie niestandardowej roli zabezpieczeń o nazwie *Operator maszyny wirtualnej*.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="1fc5f-160">Tę rolę niestandardową przyznaje tooall dostęp do odczytu dla operacji *Microsoft.Compute*, *Microsoft.Storage*, i *Microsoft.Network* dostęp do dostawcy i przyznaje zasobów toostart, ponownie uruchomić i monitorować maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="1fc5f-161">Tę rolę niestandardową można w dwóch subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="1fc5f-162">W tym przykładzie używany jest plik JSON jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-162">This example uses a JSON file as an input.</span></span>

![JSON - niestandardową definicję roli — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Tworzenie roli azure wiersza poleceń Azure RBAC - — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="1fc5f-165">Modyfikowanie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="1fc5f-165">Modify a custom role</span></span>
<span data-ttu-id="1fc5f-166">toomodify niestandardowej roli zabezpieczeń, należy najpierw użyć hello `azure role show` polecenia tooretrieve definicji roli.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="1fc5f-167">Po drugie upewnij się plik definicji roli hello żądane zmiany toohello.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="1fc5f-168">Na koniec użyj `azure role set` toosave hello zmodyfikował definicję roli.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="1fc5f-169">Witaj poniższy przykład umożliwia dodanie hello *Microsoft.Insights/diagnosticSettings/* toohello operacji **akcje**i toohello subskrypcji platformy Azure **AssignableScopes**roli niestandardowych hello Operator maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - zmodyfikować niestandardową definicję roli — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Zrzut ekranu wiersza polecenia - azure roli set - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="1fc5f-172">Usunięcia niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="1fc5f-172">Delete a custom role</span></span>
<span data-ttu-id="1fc5f-173">toodelete niestandardowej roli zabezpieczeń, należy najpierw użyć hello `azure role show` hello toodetermine polecenia **identyfikator** hello roli.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="1fc5f-174">Następnie należy użyć hello `azure role delete` roli hello toodelete polecenie, określając hello **identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="1fc5f-175">Witaj poniższy przykład umożliwia usunięcie hello *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Zrzut ekranu wiersza polecenia - usunięcia roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="1fc5f-177">Lista ról niestandardowych</span><span class="sxs-lookup"><span data-stu-id="1fc5f-177">List custom roles</span></span>
<span data-ttu-id="1fc5f-178">toolist hello ról, które są dostępne do przypisania w zakresie, użyj hello `azure role list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="1fc5f-179">Witaj następujące polecenie wyświetla listę wszystkich ról, które są dostępne do przypisania w ramach subskrypcji hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Zrzut ekranu wiersza polecenia — Lista roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="1fc5f-181">W hello poniższy przykład, hello *Operator maszyny wirtualnej* rola niestandardowa nie jest dostępna w hello *Production4* subskrypcji, ponieważ nie ma subskrypcji hello  **AssignableScopes** hello roli.</span><span class="sxs-lookup"><span data-stu-id="1fc5f-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Zrzut ekranu wiersza polecenia — Lista azure roli dla role niestandardowe - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="1fc5f-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1fc5f-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

