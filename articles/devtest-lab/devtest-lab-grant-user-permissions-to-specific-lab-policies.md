---
title: "Przyznawanie uprawnień użytkownikom laboratorium określonych zasad | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można udzielić użytkownikowi uprawnień do zasad określonych laboratorium w usłudze DevTest Labs na podstawie potrzeb każdego użytkownika"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="b03d8-103">Przyznawanie uprawnień użytkownikom zasad określonych laboratorium</span><span class="sxs-lookup"><span data-stu-id="b03d8-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="b03d8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b03d8-104">Overview</span></span>
<span data-ttu-id="b03d8-105">W tym artykule przedstawiono sposób udzielić uprawnień użytkowników do zasad laboratorium określonego za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b03d8-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="b03d8-106">W ten sposób uprawnienia mogą być stosowane zgodnie z potrzebami każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b03d8-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="b03d8-107">Na przykład można przyznać określonemu użytkownikowi możliwość zmiany ustawień zasad maszyny Wirtualnej, ale nie zasady kosztów.</span><span class="sxs-lookup"><span data-stu-id="b03d8-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="b03d8-108">Zasady jako zasoby</span><span class="sxs-lookup"><span data-stu-id="b03d8-108">Policies as resources</span></span>
<span data-ttu-id="b03d8-109">Zgodnie z opisem w [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md) artykułu, RBAC umożliwia precyzyjne zarządzanie dostępem zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b03d8-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="b03d8-110">Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji DevOps i udzielić tylko takiego dostępu dla użytkowników, które są niezbędne do wykonywania swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="b03d8-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="b03d8-111">W usłudze DevTest Labs zasady jest typ zasobu, który umożliwia działanie RBAC **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="b03d8-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="b03d8-112">Każda zasada laboratorium jest zasobem w typie zasobów zasad i można przypisać zasięgu roli RBAC.</span><span class="sxs-lookup"><span data-stu-id="b03d8-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="b03d8-113">Na przykład, aby przyznać użytkownikom uprawnienia odczytu/zapisu do **dozwolone rozmiary maszyn wirtualnych** zasad, należy utworzyć niestandardową rolę, która współdziała z **Microsoft.DevTestLab/labs/policySets/policies/*** akcji i Przypisz tę rolę niestandardową, w zakresie odpowiednich użytkowników **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="b03d8-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="b03d8-114">Aby dowiedzieć się więcej na temat ról niestandardowych w RBAC, zobacz [niestandardowych ról dla kontroli dostępu](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b03d8-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="b03d8-115">Tworzenie laboratorium niestandardowej roli zabezpieczeń przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b03d8-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="b03d8-116">Aby rozpocząć pracę, należy przeczytać artykuł następujące, które wyjaśniają, jak zainstalować i skonfigurować poleceń cmdlet programu PowerShell usługi Azure: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="b03d8-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="b03d8-117">Po skonfigurowaniu poleceń cmdlet programu Azure PowerShell, można wykonywać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="b03d8-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="b03d8-118">Lista wszystkich operacji/akcje dla dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="b03d8-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="b03d8-119">Akcje listy z określoną rolą:</span><span class="sxs-lookup"><span data-stu-id="b03d8-119">List actions in a particular role:</span></span>
* <span data-ttu-id="b03d8-120">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="b03d8-120">Create a custom role</span></span>

<span data-ttu-id="b03d8-121">Poniższy skrypt programu PowerShell przedstawiono przykłady sposobu wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="b03d8-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="b03d8-122">Przypisywanie uprawnień do użytkownika dla określonych zasad przy użyciu ról niestandardowych</span><span class="sxs-lookup"><span data-stu-id="b03d8-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="b03d8-123">Po zdefiniowaniu poszczególnych ról niestandardowych, można przypisać je do użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b03d8-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="b03d8-124">Aby można było przypisać niestandardową rolę dla użytkownika, należy najpierw uzyskać **ObjectId** reprezentujący użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b03d8-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="b03d8-125">Aby to zrobić, użyj **Get-AzureRmADUser** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b03d8-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="b03d8-126">W poniższym przykładzie **ObjectId** z *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 jest użytkownik.</span><span class="sxs-lookup"><span data-stu-id="b03d8-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="b03d8-127">Po utworzeniu **ObjectId** dla użytkownika i nazwy niestandardowej roli zabezpieczeń, można przypisać tej roli użytkownika z **AzureRmRoleAssignment nowy** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b03d8-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="b03d8-128">W poprzednim przykładzie **AllowedVmSizesInLab** zasady są używane.</span><span class="sxs-lookup"><span data-stu-id="b03d8-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="b03d8-129">Można użyć dowolnego z następujących zasad:</span><span class="sxs-lookup"><span data-stu-id="b03d8-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="b03d8-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="b03d8-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="b03d8-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="b03d8-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="b03d8-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="b03d8-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="b03d8-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="b03d8-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="b03d8-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b03d8-134">Next steps</span></span>
<span data-ttu-id="b03d8-135">Raz użytkownikowi nie zostały przyznane użytkownikowi uprawnień do laboratorium określone zasady, poniżej przedstawiono niektóre warto rozważyć poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="b03d8-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="b03d8-136">[Secure access to a lab](devtest-lab-add-devtest-user.md) (Zabezpieczanie dostępu do laboratorium).</span><span class="sxs-lookup"><span data-stu-id="b03d8-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="b03d8-137">[Set lab policies](devtest-lab-set-lab-policy.md) (Ustawianie zasad laboratorium).</span><span class="sxs-lookup"><span data-stu-id="b03d8-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="b03d8-138">[Create a lab template](devtest-lab-create-template.md) (Tworzenie szablonu laboratorium).</span><span class="sxs-lookup"><span data-stu-id="b03d8-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="b03d8-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md) (Tworzenie niestandardowych artefaktów dla maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="b03d8-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="b03d8-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md) (Dodawanie maszyny wirtualnej z artefaktami do laboratorium).</span><span class="sxs-lookup"><span data-stu-id="b03d8-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

