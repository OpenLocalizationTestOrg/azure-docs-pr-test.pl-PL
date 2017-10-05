---
title: "Zarządzanie kontrolą dostępu na podstawie ról (RBAC) przy użyciu interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie zarządzania opartego na rolach kontrola dostępu (RBAC) przy użyciu interfejsu wiersza polecenia platformy Azure za pomocą listę ról i akcje ról i przypisywania ról do zakresów subskrypcji i aplikacji."
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
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="304a0-103">Zarządzanie oparte na rolach kontrola dostępu przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="304a0-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="304a0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="304a0-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="304a0-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="304a0-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="304a0-106">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="304a0-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="304a0-107">Kontrola dostępu oparta na rolach (RBAC) w portalu Azure i interfejsu API usługi Azure Resource Manager umożliwia zarządzanie dostępem do Twojej subskrypcji i zasobów na poziomie szczegółowych.</span><span class="sxs-lookup"><span data-stu-id="304a0-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="304a0-108">W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując niektóre role do ich w określonym zakresie.</span><span class="sxs-lookup"><span data-stu-id="304a0-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="304a0-109">Zanim użyjesz Azure interfejsu wiersza polecenia (CLI) do zarządzania RBAC, musi mieć następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="304a0-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="304a0-110">Azure CLI w wersji 0.8.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="304a0-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="304a0-111">Aby zainstalować najnowszą wersję i skojarzyć go z subskrypcją platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="304a0-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="304a0-112">Usługa Azure Resource Manager w interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="304a0-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="304a0-113">Przejdź do [przy użyciu wiersza polecenia platformy Azure przy użyciu Menedżera zasobów](../xplat-cli-azure-resource-manager.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="304a0-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="304a0-114">Lista ról</span><span class="sxs-lookup"><span data-stu-id="304a0-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="304a0-115">Wyświetl listę wszystkich dostępnych ról</span><span class="sxs-lookup"><span data-stu-id="304a0-115">List all available roles</span></span>
<span data-ttu-id="304a0-116">Aby wyświetlić listę wszystkich dostępnych ról, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="304a0-117">W poniższym przykładzie przedstawiono listę *wszystkie dostępne role*.</span><span class="sxs-lookup"><span data-stu-id="304a0-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Zrzut ekranu wiersza polecenia — Lista roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="304a0-119">Akcje listy roli</span><span class="sxs-lookup"><span data-stu-id="304a0-119">List actions of a role</span></span>
<span data-ttu-id="304a0-120">Aby wyświetlić listę akcji roli, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="304a0-121">W poniższym przykładzie przedstawiono akcje *współautora* i *Współautor·maszyny·wirtualnej* ról.</span><span class="sxs-lookup"><span data-stu-id="304a0-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Zrzut ekranu wiersza polecenia — Pokaż roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="304a0-123">Dostęp do listy</span><span class="sxs-lookup"><span data-stu-id="304a0-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="304a0-124">Lista przypisań ról skuteczne w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="304a0-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="304a0-125">Aby wyświetlić listę przypisań ról, które istnieją w grupie zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="304a0-126">W poniższym przykładzie przedstawiono przypisań ról w *pharma sprzedaży projecforcast* grupy.</span><span class="sxs-lookup"><span data-stu-id="304a0-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Zrzut ekranu wiersza polecenia — Lista przypisywanie roli azure przez grupę - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="304a0-128">Lista przypisań ról dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="304a0-128">List role assignments for a user</span></span>
<span data-ttu-id="304a0-129">Aby wyświetlić listę przypisań ról określonego użytkownika i przydziałów, które są przypisane do grupy użytkowników, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="304a0-130">Możesz też sprawdzić przypisań ról, które są dziedziczone z grupy, modyfikując polecenia:</span><span class="sxs-lookup"><span data-stu-id="304a0-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="304a0-131">W poniższym przykładzie przedstawiono przypisań ról, które są przypisywane do  *sameert@aaddemo.com*  użytkownika.</span><span class="sxs-lookup"><span data-stu-id="304a0-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="304a0-132">W tym role, które są przypisywane bezpośrednio do użytkownika i role, które są dziedziczone z grupy.</span><span class="sxs-lookup"><span data-stu-id="304a0-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Zrzut ekranu wiersza polecenia — Lista przypisywanie roli azure przez użytkownika - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="304a0-134">Udzielanie dostępu</span><span class="sxs-lookup"><span data-stu-id="304a0-134">Grant access</span></span>
<span data-ttu-id="304a0-135">Aby udzielić dostępu po zidentyfikowaniu rolę, którą chcesz przypisać, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="304a0-136">Przypisz rolę do grupy w zakresie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="304a0-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="304a0-137">Aby przypisać rolę do grupy w zakresie subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="304a0-138">W poniższym przykładzie przypisano *czytnika* rolę *zespołu Christine Koch* w *subskrypcji* zakresu.</span><span class="sxs-lookup"><span data-stu-id="304a0-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć grupy — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="304a0-140">Przypisywanie roli do aplikacji w zakresie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="304a0-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="304a0-141">Aby przypisać rolę do aplikacji w zakresie subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="304a0-142">Poniższy przykład przyznaje *współautora* rolę *usługi Azure AD* aplikacji w wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="304a0-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć przez aplikację](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="304a0-144">Przypisywanie roli użytkownika w zakresie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="304a0-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="304a0-145">Aby przypisać rolę do użytkownika w zakresie grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="304a0-146">Poniższy przykład przyznaje *współautora maszyny wirtualnej* rolę  *samert@aaddemo.com*  użytkownika na *Pharma-sprzedaży-ProjectForcast* zakres grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="304a0-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć przez użytkownika — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="304a0-148">Przypisywanie roli do grupy w zakresie zasobów</span><span class="sxs-lookup"><span data-stu-id="304a0-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="304a0-149">Aby przypisać rolę do grupy w zakresie zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="304a0-150">Poniższy przykład przyznaje *współautora maszyny wirtualnej* rolę *usługi Azure AD* na *podsieci*.</span><span class="sxs-lookup"><span data-stu-id="304a0-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć grupy — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="304a0-152">Usuń dostęp</span><span class="sxs-lookup"><span data-stu-id="304a0-152">Remove access</span></span>
<span data-ttu-id="304a0-153">Aby usunąć przypisanie roli, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="304a0-154">Poniższy przykład umożliwia usunięcie *Współautor·maszyny·wirtualnej* przypisania roli z  *sammert@aaddemo.com*  użytkownika na *Pharma-sprzedaży-ProjectForcast* zasobów Grupa.</span><span class="sxs-lookup"><span data-stu-id="304a0-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="304a0-155">Przykład następnie usuwa przypisanie roli z grupy dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="304a0-155">The example then removes the role assignment from a group on the subscription.</span></span>

![Zrzut ekranu wiersza polecenia - usunięcia przypisania roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="304a0-157">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="304a0-157">Create a custom role</span></span>
<span data-ttu-id="304a0-158">Aby utworzyć niestandardową rolę, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="304a0-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="304a0-159">W poniższym przykładzie tworzona rola niestandardowa o nazwie *Operator maszyny wirtualnej*.</span><span class="sxs-lookup"><span data-stu-id="304a0-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="304a0-160">Tę rolę niestandardową nieograniczony dostęp do wszystkich operacji odczytu z *Microsoft.Compute*, *Microsoft.Storage*, i *Microsoft.Network* dostawców zasobów i udziela dostępu do Uruchom ponowne uruchomienie i monitorowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="304a0-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="304a0-161">Tę rolę niestandardową można w dwóch subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="304a0-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="304a0-162">W tym przykładzie używany jest plik JSON jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="304a0-162">This example uses a JSON file as an input.</span></span>

![JSON - niestandardową definicję roli — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Tworzenie roli azure wiersza poleceń Azure RBAC - — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="304a0-165">Modyfikowanie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="304a0-165">Modify a custom role</span></span>
<span data-ttu-id="304a0-166">Aby zmodyfikować rolę niestandardową, należy najpierw użyć `azure role show` polecenie, aby pobrać definicji roli.</span><span class="sxs-lookup"><span data-stu-id="304a0-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="304a0-167">Po drugie wprowadź żądane zmiany w pliku definicji roli.</span><span class="sxs-lookup"><span data-stu-id="304a0-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="304a0-168">Na koniec użyj `azure role set` można zapisać definicji roli zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="304a0-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="304a0-169">W poniższym przykładzie dodano *Microsoft.Insights/diagnosticSettings/* operacji **akcje**oraz uzyskać subskrypcję platformy Azure **AssignableScopes** z Rola niestandardowa Operator maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304a0-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - zmodyfikować niestandardową definicję roli — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Zrzut ekranu wiersza polecenia - azure roli set - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="304a0-172">Usunięcia niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="304a0-172">Delete a custom role</span></span>
<span data-ttu-id="304a0-173">Aby usunąć rolę niestandardową, należy najpierw użyć `azure role show` polecenie w celu ustalenia **identyfikator** roli.</span><span class="sxs-lookup"><span data-stu-id="304a0-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="304a0-174">Następnie należy użyć `azure role delete` polecenie, aby usunąć rolę, określając **identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="304a0-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="304a0-175">Poniższy przykład umożliwia usunięcie *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="304a0-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![Zrzut ekranu wiersza polecenia - usunięcia roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="304a0-177">Lista ról niestandardowych</span><span class="sxs-lookup"><span data-stu-id="304a0-177">List custom roles</span></span>
<span data-ttu-id="304a0-178">Aby wyświetlić listę ról, które są dostępne do przypisania w zakresie, należy użyć `azure role list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="304a0-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="304a0-179">Polecenie wyświetla listę wszystkich ról, które są dostępne do przypisania w wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="304a0-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Zrzut ekranu wiersza polecenia — Lista roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="304a0-181">W poniższym przykładzie *Operator maszyny wirtualnej* rola niestandardowa nie jest dostępna w *Production4* subskrypcji, ponieważ nie ma subskrypcji **AssignableScopes** roli.</span><span class="sxs-lookup"><span data-stu-id="304a0-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Zrzut ekranu wiersza polecenia — Lista azure roli dla role niestandardowe - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="304a0-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="304a0-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

