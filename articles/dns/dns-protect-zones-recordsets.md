---
title: Ochrona strefy DNS i rekordy | Dokumentacja firmy Microsoft
description: "Jak chronić stref DNS i zestawy rekordów w systemie Microsoft Azure DNS."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="4df3b-103">Jak chronić stref DNS i rekordów</span><span class="sxs-lookup"><span data-stu-id="4df3b-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="4df3b-104">Strefy DNS i rekordy są kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="4df3b-105">Usunięcie strefy DNS lub nawet tylko pojedynczego rekordu DNS może spowodować awarię usług całkowitej.</span><span class="sxs-lookup"><span data-stu-id="4df3b-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="4df3b-106">Dlatego ważne jest krytyczne strefy DNS i rekordy są chronione przed nieautoryzowanym lub przypadkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="4df3b-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="4df3b-107">W tym artykule opisano, jak usługi Azure DNS umożliwia ochronę stref DNS oraz rekordów na takie zmiany.</span><span class="sxs-lookup"><span data-stu-id="4df3b-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="4df3b-108">Trwa stosowanie dwie funkcje zaawansowane zabezpieczenia udostępniane przez usługi Azure Resource Manager: [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) i [blokowania zasobów](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4df3b-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="4df3b-109">Kontrola dostępu oparta na rolach</span><span class="sxs-lookup"><span data-stu-id="4df3b-109">Role-based access control</span></span>

<span data-ttu-id="4df3b-110">Azure opartej na rolach kontroli dostępu (RBAC) umożliwia precyzyjne zarządzanie dostępem dla platformy Azure użytkowników, grup i zasobów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="4df3b-111">Przy użyciu funkcji RBAC, można przyznać dokładnie takiego dostępu użytkownicy muszą wykonać swoje zadania.</span><span class="sxs-lookup"><span data-stu-id="4df3b-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="4df3b-112">Aby uzyskać więcej informacji o sposobie RBAC ułatwia zarządzanie dostępem, zobacz [co to jest kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4df3b-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="4df3b-113">Roli "Współautor strefę DNS"</span><span class="sxs-lookup"><span data-stu-id="4df3b-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="4df3b-114">Roli "Współautor strefę DNS" to wbudowana rola dostarczany przez platformę Azure do zarządzania zasobami DNS.</span><span class="sxs-lookup"><span data-stu-id="4df3b-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="4df3b-115">Przypisywanie użytkownikowi lub grupie uprawnienia współautora strefy DNS umożliwia tej grupy do zarządzania zasobów DNS, ale nie zasobów innego typu.</span><span class="sxs-lookup"><span data-stu-id="4df3b-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="4df3b-116">Na przykład załóżmy, że grupa zasobów "myzones" zawiera pięć stref dla Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4df3b-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="4df3b-117">Udzielenie DNS administrator "Współautora strefę DNS" uprawnień do tej grupy zasobów, umożliwia pełną kontrolę nad tych stref DNS.</span><span class="sxs-lookup"><span data-stu-id="4df3b-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="4df3b-118">Ponadto pozwala uniknąć, udzielanie niepotrzebnych uprawnień, na przykład administrator usługi DNS nie można utworzyć ani zatrzymać maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4df3b-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="4df3b-119">Najprostszym sposobem, aby przypisać uprawnienia RBAC jest [za pośrednictwem portalu Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4df3b-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="4df3b-120">Otwarcie bloku "Kontrola dostępu (IAM)" dla grupy zasobów, następnie kliknij przycisk "Dodaj", a następnie wybierz roli "Współautor strefę DNS" i wybierz wymagane użytkowników lub grupy, aby udzielić uprawnień.</span><span class="sxs-lookup"><span data-stu-id="4df3b-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Poziom grupy zasobów RBAC za pośrednictwem portalu Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="4df3b-122">Uprawnienia można również [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4df3b-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4df3b-123">Odpowiednik polecenia jest także [dostępne za pośrednictwem interfejsu wiersza polecenia Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4df3b-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="4df3b-124">Poziomu strefy RBAC</span><span class="sxs-lookup"><span data-stu-id="4df3b-124">Zone level RBAC</span></span>

<span data-ttu-id="4df3b-125">Reguły Azure RBAC można zastosować do subskrypcji, grupy zasobów lub do pojedynczego zasobu.</span><span class="sxs-lookup"><span data-stu-id="4df3b-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="4df3b-126">W przypadku usługi Azure DNS tego zasobu można poszczególnych stref DNS, lub nawet poszczególnych zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="4df3b-127">Na przykład załóżmy, że grupa zasobów "myzones" zawiera strefy "contoso.com" i subzone "customers.contoso.com" tworzonych rekordy CNAME dla każdego konta klienta.</span><span class="sxs-lookup"><span data-stu-id="4df3b-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="4df3b-128">Konto używane do zarządzania te rekordy CNAME należy przypisać uprawnienia do tworzenia rekordów w strefie "customers.contoso.com" tylko, nie powinny mieć dostępu do innych stref.</span><span class="sxs-lookup"><span data-stu-id="4df3b-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="4df3b-129">Uprawnienia na poziomie strefy RBAC można otrzymać za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4df3b-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="4df3b-130">Otwarcie bloku "Kontrola dostępu (IAM)" dla strefy, kliknij przycisk "Dodaj", a następnie wybierz roli "Współautor strefę DNS" i wybierz wymaganych użytkowników lub grupy, aby udzielić uprawnień.</span><span class="sxs-lookup"><span data-stu-id="4df3b-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Strefa DNS RBAC poziomu portalu Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="4df3b-132">Uprawnienia można również [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4df3b-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="4df3b-133">Odpowiednik polecenia jest także [dostępne za pośrednictwem interfejsu wiersza polecenia Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4df3b-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="4df3b-134">Poziom RBAC zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="4df3b-134">Record set level RBAC</span></span>

<span data-ttu-id="4df3b-135">Firma Microsoft wykonaj krok dalej.</span><span class="sxs-lookup"><span data-stu-id="4df3b-135">We can go one step further.</span></span> <span data-ttu-id="4df3b-136">Należy wziąć pod uwagę administratora poczty dla Contoso Corporation, który wymaga dostępu do rekordów MX i TXT w wierzchołku strefy "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="4df3b-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="4df3b-137">Nie musi ona dostęp do innych rekordów MX lub TXT lub rekordy innego typu.</span><span class="sxs-lookup"><span data-stu-id="4df3b-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="4df3b-138">Usługa Azure DNS umożliwia przypisanie uprawnienia na poziomie zestawu rekordów, aby precyzyjnie rekordy, które administrator poczty musi mieć dostęp do.</span><span class="sxs-lookup"><span data-stu-id="4df3b-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="4df3b-139">Administrator poczty otrzymuje dokładnie kontroli ona należy i nie może wprowadzić inne zmiany.</span><span class="sxs-lookup"><span data-stu-id="4df3b-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="4df3b-140">Zestaw rekordów uprawnień na poziomie RBAC można skonfigurować za pośrednictwem portalu Azure za pomocą przycisku "Użytkowników" w bloku zestawu rekordów:</span><span class="sxs-lookup"><span data-stu-id="4df3b-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![Poziom RBAC za pośrednictwem portalu Azure zestawu rekordów](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="4df3b-142">Zestaw rekordów uprawnień na poziomie RBAC można też [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4df3b-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="4df3b-143">Odpowiednik polecenia jest także [dostępne za pośrednictwem interfejsu wiersza polecenia Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4df3b-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="4df3b-144">Role niestandardowe</span><span class="sxs-lookup"><span data-stu-id="4df3b-144">Custom roles</span></span>

<span data-ttu-id="4df3b-145">Wbudowane roli "Współautor strefę DNS" umożliwia pełną kontrolę nad zasobów DNS.</span><span class="sxs-lookup"><span data-stu-id="4df3b-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="4df3b-146">Istnieje również możliwość tworzenia własnego klienta Azure role, do zapewnienia jeszcze bardziej precyzyjną system kontroli.</span><span class="sxs-lookup"><span data-stu-id="4df3b-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="4df3b-147">Należy wziąć pod uwagę ponownie przykład, w której zostaje utworzony rekord CNAME w strefie "customers.contoso.com" dla każdego konta klienta Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4df3b-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="4df3b-148">Konto używane do zarządzania tymi CNAME powinien mieć uprawnienie do zarządzania tylko rekordy CNAME.</span><span class="sxs-lookup"><span data-stu-id="4df3b-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="4df3b-149">Następnie nie może zmodyfikować rekordy z innych typów (np. zmiana rekordów MX) lub wykonywania operacji na poziomie strefy takich jak usuwanie strefy.</span><span class="sxs-lookup"><span data-stu-id="4df3b-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="4df3b-150">W poniższym przykładzie przedstawiono niestandardową definicję roli do zarządzania tylko rekordy CNAME:</span><span class="sxs-lookup"><span data-stu-id="4df3b-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="4df3b-151">Właściwość akcje definiuje następujące uprawnienia dotyczące DNS:</span><span class="sxs-lookup"><span data-stu-id="4df3b-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="4df3b-152">`Microsoft.Network/dnsZones/CNAME/*`przyznaje pełną kontrolę nad rekordy CNAME</span><span class="sxs-lookup"><span data-stu-id="4df3b-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="4df3b-153">`Microsoft.Network/dnsZones/read`udziela uprawnień do odczytu stref DNS, ale nie można zmodyfikować, umożliwiając Zobacz strefy, w którym jest tworzona CNAME.</span><span class="sxs-lookup"><span data-stu-id="4df3b-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="4df3b-154">Pozostałe akcje są kopiowane z [wbudowana Rola współautora strefy DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="4df3b-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="4df3b-155">Aby zapobiec usuwanie zestawów rekordów podczas jednocześnie ich aktualizacji nie jest skuteczną kontrolę przy użyciu niestandardowej roli zabezpieczeń RBAC.</span><span class="sxs-lookup"><span data-stu-id="4df3b-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="4df3b-156">Uniemożliwia zestawy rekordów usuwany, ale go nie uniemożliwia ich jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="4df3b-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="4df3b-157">Dozwolone modyfikacje obejmują dodawanie i usuwanie rekordów z zestawu rekordów, łącznie z usunięciem wszystkich rekordów, aby pozostawić "empty" zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="4df3b-158">Jest to ten sam efekt co usunięcie zestawu z punktu widzenia rozpoznawania DNS rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4df3b-159">Definicje ról niestandardowych obecnie nie można zdefiniować za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4df3b-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="4df3b-160">Można utworzyć niestandardową rolę, na podstawie tej definicji roli przy użyciu programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4df3b-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="4df3b-161">Go można również utworzyć za pomocą wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="4df3b-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="4df3b-162">Następnie można przypisać rolę w taki sam sposób jak wbudowane role, zgodnie z opisem we wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4df3b-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="4df3b-163">Aby uzyskać więcej informacji na temat sposobu tworzenia, zarządzania i przypisz role niestandardowe, zobacz [role niestandardowe w Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4df3b-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="4df3b-164">Blokowania zasobów</span><span class="sxs-lookup"><span data-stu-id="4df3b-164">Resource locks</span></span>

<span data-ttu-id="4df3b-165">Oprócz RBAC usługi Azure Resource Manager obsługuje innego rodzaju kontrolę zabezpieczeń, to znaczy możliwość zasobów 'lock'.</span><span class="sxs-lookup"><span data-stu-id="4df3b-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="4df3b-166">Gdzie RBAC zasady umożliwiają kontrolowanie akcji konkretnych użytkowników i grup, blokowania zasobów są stosowane do zasobu i obowiązują we wszystkich użytkowników i ról.</span><span class="sxs-lookup"><span data-stu-id="4df3b-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="4df3b-167">Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="4df3b-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="4df3b-168">Istnieją dwa typy zasobów blokady: **DoNotDelete** i **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="4df3b-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="4df3b-169">Mogą być stosowane do strefy DNS lub do poszczególnych zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="4df3b-170">W poniższych sekcjach opisano kilka typowych scenariuszy i sposobu ich obsługi przy użyciu blokady zasobu.</span><span class="sxs-lookup"><span data-stu-id="4df3b-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="4df3b-171">Ochrona przed wszystkimi zmianami</span><span class="sxs-lookup"><span data-stu-id="4df3b-171">Protecting against all changes</span></span>

<span data-ttu-id="4df3b-172">Aby zapobiec jakichkolwiek zmian, należy zastosować blokady tylko do odczytu do strefy.</span><span class="sxs-lookup"><span data-stu-id="4df3b-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="4df3b-173">Zapobiega to zostanie utworzony i istniejących zestawów rekordów, zmodyfikowane lub usunięte nowych zestawów rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="4df3b-174">Blokad zasobów na poziomie strefy można tworzyć za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4df3b-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="4df3b-175">W bloku strefy DNS, kliknij przycisk "Blokady", następnie "Dodaj":</span><span class="sxs-lookup"><span data-stu-id="4df3b-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Blokad zasobów na poziomie strefy za pośrednictwem portalu Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="4df3b-177">Poziomu strefy zasób, którego blokad można również utworzyć za pomocą programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4df3b-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="4df3b-178">Konfigurowanie blokad zasobów platformy Azure nie jest obecnie obsługiwane za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4df3b-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="4df3b-179">Ochrona poszczególne rekordy</span><span class="sxs-lookup"><span data-stu-id="4df3b-179">Protecting individual records</span></span>

<span data-ttu-id="4df3b-180">Aby zapobiec istniejącego rekordu DNS ustawiona przed zmianami, dotyczą blokady tylko do odczytu zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="4df3b-181">Stosowanie blokady DoNotDelete do zestawu rekordów nie jest skutecznej kontroli.</span><span class="sxs-lookup"><span data-stu-id="4df3b-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="4df3b-182">Zapobiega zestawu przed usunięciem rekordów, ale go nie uniemożliwia jej jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="4df3b-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="4df3b-183">Dozwolone modyfikacje obejmują dodawanie i usuwanie rekordów z zestawu rekordów, łącznie z usunięciem wszystkich rekordów, aby pozostawić "empty" zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="4df3b-184">Jest to ten sam efekt co usunięcie zestawu z punktu widzenia rozpoznawania DNS rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4df3b-185">Zestaw rekordów zasobów na poziomie blokad można obecnie tylko skonfigurowany przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4df3b-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="4df3b-186">Nie są obsługiwane w portalu Azure lub interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="4df3b-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="4df3b-187">Ochrona przed usunięciem strefy</span><span class="sxs-lookup"><span data-stu-id="4df3b-187">Protecting against zone deletion</span></span>

<span data-ttu-id="4df3b-188">Po usunięciu strefę w usłudze Azure DNS, również zostaną usunięte wszystkie zestawy rekordów w strefie.</span><span class="sxs-lookup"><span data-stu-id="4df3b-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="4df3b-189">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="4df3b-189">This operation cannot be undone.</span></span>  <span data-ttu-id="4df3b-190">Wpływają firma może mieć przypadkowego usunięcia strefy krytyczne.</span><span class="sxs-lookup"><span data-stu-id="4df3b-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="4df3b-191">W związku z tym jest bardzo ważne, aby chronić przed usunięciem przypadkowemu strefy.</span><span class="sxs-lookup"><span data-stu-id="4df3b-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="4df3b-192">Zastosowanie blokady DoNotDelete do strefy zapobiega strefy przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="4df3b-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="4df3b-193">Jednak ponieważ blokady są dziedziczone przez zasoby podrzędne, uniemożliwia także żadnych zestawów rekordów w strefie przed usunięciem, który może być niepożądane.</span><span class="sxs-lookup"><span data-stu-id="4df3b-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="4df3b-194">Ponadto zgodnie z opisem w powyższej Uwaga, jest również żadnego efektu, ponieważ nadal można usunąć rekordy z istniejących zestawów rekordów.</span><span class="sxs-lookup"><span data-stu-id="4df3b-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="4df3b-195">Alternatywnie należy rozważyć stosowanie blokady DoNotDelete do rekordu w strefie, takiego jak zestaw rekordów SOA.</span><span class="sxs-lookup"><span data-stu-id="4df3b-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="4df3b-196">Ponieważ nie można usunąć strefy bez także usuwanie zestawów rekordów, chroni to przed usunięciem strefy, umożliwiając zestawów rekordów w strefie, można zmodyfikować za darmo.</span><span class="sxs-lookup"><span data-stu-id="4df3b-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="4df3b-197">Jeśli podjęto próbę usunięcia strefy, usługi Azure Resource Manager wykrywa to spowoduje również usunięcie zestawu rekordów SOA i blokuje połączenia, ponieważ SOA jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="4df3b-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="4df3b-198">Brak zestawów rekordów są usuwane.</span><span class="sxs-lookup"><span data-stu-id="4df3b-198">No record sets are deleted.</span></span>

<span data-ttu-id="4df3b-199">Następujące polecenie programu PowerShell tworzy DoNotDelete blokadą rekord SOA strefy danego:</span><span class="sxs-lookup"><span data-stu-id="4df3b-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4df3b-200">Innym sposobem uniknięcia strefy przypadkowego usunięcia jest przy użyciu niestandardowej roli zabezpieczeń zapewniające operatora i konta usług używane do zarządzania stref ma strefy usunąć uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4df3b-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="4df3b-201">Gdy chcesz usunąć strefę, można wymusić delete dwuetapową, pierwszy udzielającym strefy uprawnienia do usuwania (w zakresie strefy, aby uniemożliwić usunięcie niewłaściwy strefy) i drugi usunąć strefę.</span><span class="sxs-lookup"><span data-stu-id="4df3b-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="4df3b-202">Takie podejście drugi ma tę zaletę, jego działanie dla wszystkich stref, które uzyskują do tych kont bez konieczności Pamiętaj, aby utworzyć wszystkie blokady.</span><span class="sxs-lookup"><span data-stu-id="4df3b-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="4df3b-203">Ma ona wadą czy kont z uprawnienia do usuwania strefy, takich jak właściciel subskrypcji może nadal przypadkowo usunąć strefę krytyczne.</span><span class="sxs-lookup"><span data-stu-id="4df3b-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="4df3b-204">Istnieje możliwość użycia obu podejść — blokowania zasobów i role niestandardowe — w tym samym czasie jako podejściu obrony zabezpieczeń do ochrony strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="4df3b-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4df3b-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4df3b-205">Next steps</span></span>

* <span data-ttu-id="4df3b-206">Aby uzyskać więcej informacji na temat pracy z RBAC, zobacz [wprowadzenie do zarządzania dostępem w portalu Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4df3b-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="4df3b-207">Aby uzyskać więcej informacji na temat pracy z blokowania zasobów, zobacz [blokowania zasobów z usługi Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4df3b-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

