---
title: aaaProtecting strefy DNS i rekordy | Dokumentacja firmy Microsoft
description: "Jak stref DNS tooprotect zestawami rekordów i w systemie Microsoft Azure DNS."
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
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="3da50-103">Jak tooprotect DNS strefy i rejestruje</span><span class="sxs-lookup"><span data-stu-id="3da50-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="3da50-104">Strefy DNS i rekordy są kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="3da50-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="3da50-105">Usunięcie strefy DNS lub nawet tylko pojedynczego rekordu DNS może spowodować awarię usług całkowitej.</span><span class="sxs-lookup"><span data-stu-id="3da50-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="3da50-106">Dlatego ważne jest krytyczne strefy DNS i rekordy są chronione przed nieautoryzowanym lub przypadkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="3da50-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="3da50-107">W tym artykule opisano, w jaki sposób usługi Azure DNS umożliwia tooprotect możesz stref DNS, a rekordy na takie zmiany.</span><span class="sxs-lookup"><span data-stu-id="3da50-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="3da50-108">Trwa stosowanie dwie funkcje zaawansowane zabezpieczenia udostępniane przez usługi Azure Resource Manager: [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) i [blokowania zasobów](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="3da50-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="3da50-109">Kontrola dostępu oparta na rolach</span><span class="sxs-lookup"><span data-stu-id="3da50-109">Role-based access control</span></span>

<span data-ttu-id="3da50-110">Azure opartej na rolach kontroli dostępu (RBAC) umożliwia precyzyjne zarządzanie dostępem dla platformy Azure użytkowników, grup i zasobów.</span><span class="sxs-lookup"><span data-stu-id="3da50-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="3da50-111">Przy użyciu funkcji RBAC, można przyznać dokładnie hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="3da50-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="3da50-112">Aby uzyskać więcej informacji o sposobie RBAC ułatwia zarządzanie dostępem, zobacz [co to jest kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3da50-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="3da50-113">roli "Współautor strefę DNS" Hello</span><span class="sxs-lookup"><span data-stu-id="3da50-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="3da50-114">roli "Współautor strefę DNS" Hello jest wbudowana dostarczany przez platformę Azure do zarządzania zasobami DNS.</span><span class="sxs-lookup"><span data-stu-id="3da50-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="3da50-115">Przypisywanie użytkowników tooa uprawnienia współautora strefy DNS lub grupy umożliwia zasobów DNS toomanage grupy, ale nie zasoby innego typu.</span><span class="sxs-lookup"><span data-stu-id="3da50-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="3da50-116">Na przykład załóżmy, że hello grupy zasobów "myzones" zawiera pięć stref dla Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="3da50-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="3da50-117">Udzielającym hello DNS administratora "Współautora strefę DNS" uprawnienia toothat grupy zasobów, umożliwia pełną kontrolę nad tych stref DNS.</span><span class="sxs-lookup"><span data-stu-id="3da50-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="3da50-118">Ponadto pozwala uniknąć, udzielanie niepotrzebnych uprawnień, na przykład administrator DNS hello nie można utworzyć ani zatrzymać maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3da50-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="3da50-119">uprawnienia RBAC tooassign najprostszy sposób Hello jest [za pośrednictwem portalu Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3da50-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="3da50-120">Otwarcie bloku hello "kontroli dostępu (IAM)" dla grupy zasobów hello, a następnie kliknij przycisk "Dodaj", a następnie wybierz roli "Współautor strefę DNS" hello i wybierz hello wymagane użytkowników lub grup toogrant uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3da50-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Poziom grupy zasobów RBAC za pośrednictwem hello portalu Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="3da50-122">Uprawnienia można również [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="3da50-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="3da50-123">polecenie równoważne Hello jest również [dostępne za pośrednictwem interfejsu wiersza polecenia Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="3da50-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="3da50-124">Poziomu strefy RBAC</span><span class="sxs-lookup"><span data-stu-id="3da50-124">Zone level RBAC</span></span>

<span data-ttu-id="3da50-125">Reguły Azure RBAC można subskrypcji zastosowane tooa zasobów grupy lub tooan pojedynczego zasobu.</span><span class="sxs-lookup"><span data-stu-id="3da50-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="3da50-126">W przypadku hello Azure DNS ten zasób może być poszczególnych stref DNS, lub nawet poszczególnych zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="3da50-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="3da50-127">Na przykład załóżmy, że grupa zasobów hello "myzones" zawiera hello strefy "contoso.com" i subzone "customers.contoso.com" tworzonych rekordy CNAME dla każdego konta klienta.</span><span class="sxs-lookup"><span data-stu-id="3da50-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="3da50-128">toomanage konto używane Hello te rekordy CNAME należy przypisać uprawnienia toocreate rekordy w strefie "customers.contoso.com" hello tylko, nie powinien być toohello dostępu do innych stref.</span><span class="sxs-lookup"><span data-stu-id="3da50-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="3da50-129">Uprawnienia na poziomie strefy RBAC można można przyznać za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3da50-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="3da50-130">Otwarcie bloku "Kontrola dostępu (IAM)" hello strefy hello, a następnie kliknij przycisk "Dodaj", a następnie wybierz roli "Współautor strefę DNS" hello i wybierz hello wymagane użytkowników lub grup toogrant uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3da50-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Strefa DNS RBAC poziomu za pomocą hello portalu Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="3da50-132">Uprawnienia można również [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="3da50-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="3da50-133">polecenie równoważne Hello jest również [dostępne za pośrednictwem interfejsu wiersza polecenia Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="3da50-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="3da50-134">Poziom RBAC zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="3da50-134">Record set level RBAC</span></span>

<span data-ttu-id="3da50-135">Firma Microsoft wykonaj krok dalej.</span><span class="sxs-lookup"><span data-stu-id="3da50-135">We can go one step further.</span></span> <span data-ttu-id="3da50-136">Należy wziąć pod uwagę administratora wiadomości powitania dla Contoso Corporation, który potrzebuje dostępu toohello MX i rekordów TXT na powitania wierzchołku strefy "contoso.com" hello.</span><span class="sxs-lookup"><span data-stu-id="3da50-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="3da50-137">Użytkownik nie musi dostęp do tooany innych rekordów MX lub TXT lub rekordy tooany innego typu.</span><span class="sxs-lookup"><span data-stu-id="3da50-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="3da50-138">Usługa Azure DNS umożliwia możesz tooassign uprawnień na powitania zestawu rekordów poziomu, tooprecisely hello rekordów, które hello administratora poczty musi mieć dostęp do.</span><span class="sxs-lookup"><span data-stu-id="3da50-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="3da50-139">Witaj administratora poczty jest uprawnienie do dokładnie hello kontroli nich i jest toomake innych zmian.</span><span class="sxs-lookup"><span data-stu-id="3da50-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="3da50-140">Zestaw rekordów uprawnień na poziomie RBAC można skonfigurować za pośrednictwem portalu Azure za pomocą przycisku użytkowników"hello" w bloku zestawu rekordów hello hello:</span><span class="sxs-lookup"><span data-stu-id="3da50-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Poziom RBAC za pośrednictwem portalu Azure hello zestawu rekordów](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="3da50-142">Zestaw rekordów uprawnień na poziomie RBAC można też [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="3da50-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="3da50-143">polecenie równoważne Hello jest również [dostępne za pośrednictwem interfejsu wiersza polecenia Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="3da50-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="3da50-144">Role niestandardowe</span><span class="sxs-lookup"><span data-stu-id="3da50-144">Custom roles</span></span>

<span data-ttu-id="3da50-145">wbudowane roli "Współautor strefę DNS" Hello umożliwia pełną kontrolę nad zasobów DNS.</span><span class="sxs-lookup"><span data-stu-id="3da50-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="3da50-146">Jego jest również możliwe toobuild własnego klienta Azure ról, tooprovide nawet precyzyjny system kontroli.</span><span class="sxs-lookup"><span data-stu-id="3da50-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="3da50-147">Rozważmy przykład Witaj, w której zostaje utworzony rekord CNAME w hello strefy "customers.contoso.com" dla każdego konta klienta Contoso Corporation ponownie.</span><span class="sxs-lookup"><span data-stu-id="3da50-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="3da50-148">toomanage konto używane Hello tych rekordów CNAME może być przyznany tylko rekordy CNAME toomanage uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3da50-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="3da50-149">Jest następnie rekordy toomodify innych typów (np. zmiana rekordów MX) lub wykonywania operacji na poziomie strefy takich jak usuwanie strefy.</span><span class="sxs-lookup"><span data-stu-id="3da50-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="3da50-150">Witaj poniższy przykład przedstawia niestandardową definicję roli do zarządzania tylko rekordy CNAME:</span><span class="sxs-lookup"><span data-stu-id="3da50-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="3da50-151">Hello właściwości akcje definiuje hello następujące uprawnienia dotyczące DNS:</span><span class="sxs-lookup"><span data-stu-id="3da50-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="3da50-152">`Microsoft.Network/dnsZones/CNAME/*`przyznaje pełną kontrolę nad rekordy CNAME</span><span class="sxs-lookup"><span data-stu-id="3da50-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="3da50-153">`Microsoft.Network/dnsZones/read`przyznaje stref DNS tooread uprawnień, ale nie toomodify ich włączenie możesz toosee hello strefy, w których hello jest tworzony CNAME.</span><span class="sxs-lookup"><span data-stu-id="3da50-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="3da50-154">pozostałe akcje są kopiowane z hello Hello [wbudowana Rola współautora strefy DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="3da50-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="3da50-155">Przy użyciu niestandardowych tooprevent roli RBAC usunięcie rekordu ustawia podczas jednocześnie ich toobe aktualizacji nie jest skutecznej kontroli.</span><span class="sxs-lookup"><span data-stu-id="3da50-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="3da50-156">Uniemożliwia zestawy rekordów usuwany, ale go nie uniemożliwia ich jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="3da50-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="3da50-157">Dozwolone modyfikacje obejmują dodawanie i usuwanie rekordów z zestawu rekordów hello, łącznie z usunięciem wszystkich rekordów tooleave "empty" zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="3da50-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="3da50-158">To ustawienie hello sam efekt co usunięcie rekordu hello ustawić z punktu widzenia rozpoznawania DNS.</span><span class="sxs-lookup"><span data-stu-id="3da50-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="3da50-159">Definicje ról niestandardowych obecnie nie można zdefiniować za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3da50-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="3da50-160">Można utworzyć niestandardową rolę, na podstawie tej definicji roli przy użyciu programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3da50-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="3da50-161">Go można również utworzyć za pomocą interfejsu wiersza polecenia Azure hello:</span><span class="sxs-lookup"><span data-stu-id="3da50-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="3da50-162">Hello roli można następnie przypisać w hello sam sposób jak wbudowane role, zgodnie z opisem we wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="3da50-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="3da50-163">Aby uzyskać więcej informacji na temat sposobu toocreate, zarządzania i przypisz role niestandardowe, zobacz [role niestandardowe w Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3da50-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="3da50-164">Blokowania zasobów</span><span class="sxs-lookup"><span data-stu-id="3da50-164">Resource locks</span></span>

<span data-ttu-id="3da50-165">W tooRBAC dodanie usługi Azure Resource Manager obsługuje innego rodzaju kontrolę zabezpieczeń, to znaczy hello możliwości too'lock "zasobów.</span><span class="sxs-lookup"><span data-stu-id="3da50-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="3da50-166">Jeżeli zasady RBAC pozwalają akcje hello toocontrol konkretnych użytkowników i grup, blokowania zasobów są stosowane toohello zasobów i obowiązują we wszystkich użytkowników i ról.</span><span class="sxs-lookup"><span data-stu-id="3da50-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="3da50-167">Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3da50-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="3da50-168">Istnieją dwa typy zasobów blokady: **DoNotDelete** i **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="3da50-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="3da50-169">Te mogą być stosowane tooa strefy DNS lub tooan poszczególnych zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="3da50-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="3da50-170">Witaj poniższych sekcjach opisano kilka typowych scenariuszy i w jaki sposób toosupport ich przy użyciu blokady zasobu.</span><span class="sxs-lookup"><span data-stu-id="3da50-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="3da50-171">Ochrona przed wszystkimi zmianami</span><span class="sxs-lookup"><span data-stu-id="3da50-171">Protecting against all changes</span></span>

<span data-ttu-id="3da50-172">tooprevent trwa zmian, zastosuj strefy toohello blokady tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3da50-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="3da50-173">Zapobiega to zostanie utworzony i istniejących zestawów rekordów, zmodyfikowane lub usunięte nowych zestawów rekordów.</span><span class="sxs-lookup"><span data-stu-id="3da50-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="3da50-174">Blokad zasobów na poziomie strefy można tworzyć za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3da50-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="3da50-175">W bloku strefy DNS hello, kliknij przycisk "Blokady", następnie "Dodaj":</span><span class="sxs-lookup"><span data-stu-id="3da50-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Blokad zasobów na poziomie strefy za pośrednictwem hello portalu Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="3da50-177">Poziomu strefy zasób, którego blokad można również utworzyć za pomocą programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3da50-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="3da50-178">Konfigurowanie blokad zasobów platformy Azure nie jest obecnie obsługiwane za pośrednictwem hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3da50-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="3da50-179">Ochrona poszczególne rekordy</span><span class="sxs-lookup"><span data-stu-id="3da50-179">Protecting individual records</span></span>

<span data-ttu-id="3da50-180">tooprevent istniejącego rekordu DNS ustawiona przed zmianami, mają zastosowanie tylko do odczytu zestawu rekordów toohello blokady.</span><span class="sxs-lookup"><span data-stu-id="3da50-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="3da50-181">Stosowanie tooa blokady DoNotDelete zestawu rekordów nie jest skutecznej kontroli.</span><span class="sxs-lookup"><span data-stu-id="3da50-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="3da50-182">Zapobiega zestawu przed usunięciem rekordów hello, ale go nie uniemożliwia jej jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="3da50-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="3da50-183">Dozwolone modyfikacje obejmują dodawanie i usuwanie rekordów z zestawu rekordów hello, łącznie z usunięciem wszystkich rekordów tooleave "empty" zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="3da50-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="3da50-184">To ustawienie hello sam efekt co usunięcie rekordu hello ustawić z punktu widzenia rozpoznawania DNS.</span><span class="sxs-lookup"><span data-stu-id="3da50-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="3da50-185">Zestaw rekordów zasobów na poziomie blokad można obecnie tylko skonfigurowany przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3da50-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="3da50-186">Nie są obsługiwane w portalu Azure hello lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3da50-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="3da50-187">Ochrona przed usunięciem strefy</span><span class="sxs-lookup"><span data-stu-id="3da50-187">Protecting against zone deletion</span></span>

<span data-ttu-id="3da50-188">Po usunięciu strefę w usłudze Azure DNS wszystkich zestawów rekordów w strefie hello również zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="3da50-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="3da50-189">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="3da50-189">This operation cannot be undone.</span></span>  <span data-ttu-id="3da50-190">Przypadkowego usunięcia strefy krytyczne ma wpływ firma toohave potencjalnych hello.</span><span class="sxs-lookup"><span data-stu-id="3da50-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="3da50-191">Dlatego jest bardzo ważne tooprotect przed usunięciem przypadkowemu strefy.</span><span class="sxs-lookup"><span data-stu-id="3da50-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="3da50-192">Zastosowanie strefy tooa blokady DoNotDelete zapobiega strefy hello przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="3da50-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="3da50-193">Jednak ponieważ blokady są dziedziczone przez zasoby podrzędne, uniemożliwia także żadnych zestawów rekordów w strefie hello przed usunięciem, który może być niepożądane.</span><span class="sxs-lookup"><span data-stu-id="3da50-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="3da50-194">Ponadto zgodnie z opisem w uwagi hello powyżej, jest również żadnego efektu, ponieważ nadal można usunąć rekordy z hello istniejące zestawy rekordów.</span><span class="sxs-lookup"><span data-stu-id="3da50-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="3da50-195">Alternatywnie należy rozważyć stosowanie rekord tooa blokady DoNotDelete ustawione w strefie hello, takiego jak zestaw rekordów SOA hello.</span><span class="sxs-lookup"><span data-stu-id="3da50-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="3da50-196">Ponieważ nie można usunąć strefy hello bez także usuwanie zestawów rekordów hello, chroni to przed usunięciem strefy, umożliwiając zestawów rekordów w ramach toobe strefy hello zmodyfikowany za darmo.</span><span class="sxs-lookup"><span data-stu-id="3da50-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="3da50-197">Jeśli strefa hello toodelete podejmowana jest próba, usługi Azure Resource Manager wykryje to spowoduje również usunięcie zestawu rekordów SOA hello i bloki hello wywołania, ponieważ hello SOA jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="3da50-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="3da50-198">Brak zestawów rekordów są usuwane.</span><span class="sxs-lookup"><span data-stu-id="3da50-198">No record sets are deleted.</span></span>

<span data-ttu-id="3da50-199">Witaj następującego polecenia programu PowerShell tworzy DoNotDelete blokadą rekord SOA hello hello podane strefy:</span><span class="sxs-lookup"><span data-stu-id="3da50-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="3da50-200">Innym sposobem jest tooprevent strefy przypadkowego usunięcia za pomocą operatora hello tooensure niestandardowej roli zabezpieczeń i toomanage konta używane usługi nie ma strefy stref usunąć uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3da50-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="3da50-201">Gdy potrzebne są toodelete strefy, można wymusić delete dwuetapową, pierwszy udzielającym strefy uprawnienia do usuwania (na zakres hello strefy tooprevent Usuwanie strefy niewłaściwy hello) i drugi toodelete hello strefy.</span><span class="sxs-lookup"><span data-stu-id="3da50-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="3da50-202">Tej metody drugi jest korzyść hello, która działa we wszystkich strefach dostępne przez te konta, bez konieczności tooremember toocreate wszystkie blokady.</span><span class="sxs-lookup"><span data-stu-id="3da50-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="3da50-203">Ma ona wadą hello czy kont z uprawnienia do usuwania strefy, takich jak hello właściciel subskrypcji, nadal przypadkowo można usunąć strefy krytyczne.</span><span class="sxs-lookup"><span data-stu-id="3da50-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="3da50-204">Jest to możliwe toouse obu podejść — blokowania zasobów i role niestandardowe — na powitania sam czas, jako ochrony strefy tooDNS podejście obrony zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3da50-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3da50-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3da50-205">Next steps</span></span>

* <span data-ttu-id="3da50-206">Aby uzyskać więcej informacji na temat pracy z RBAC, zobacz [wprowadzenie do zarządzania dostępem w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3da50-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="3da50-207">Aby uzyskać więcej informacji na temat pracy z blokowania zasobów, zobacz [blokowania zasobów z usługi Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="3da50-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

