---
title: "zasady dotyczące aaaGrant użytkownika uprawnień toospecific laboratorium | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toogrant zasad laboratorium toospecific uprawnień użytkownika w usłudze DevTest Labs oparte na potrzeby każdego użytkownika"
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
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="6afe6-103">Przyznawanie uprawnień użytkownikom toospecific zasad laboratorium</span><span class="sxs-lookup"><span data-stu-id="6afe6-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="6afe6-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6afe6-104">Overview</span></span>
<span data-ttu-id="6afe6-105">W tym artykule przedstawiono sposób toouse PowerShell toogrant użytkownikom uprawnienia tooa laboratorium określonego zasad.</span><span class="sxs-lookup"><span data-stu-id="6afe6-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="6afe6-106">W ten sposób uprawnienia mogą być stosowane zgodnie z potrzebami każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6afe6-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="6afe6-107">Na przykład może być toogrant określonego hello możliwości toochange hello wirtualna ustawień zasad użytkownika, ale nie hello koszt zasad.</span><span class="sxs-lookup"><span data-stu-id="6afe6-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="6afe6-108">Zasady jako zasoby</span><span class="sxs-lookup"><span data-stu-id="6afe6-108">Policies as resources</span></span>
<span data-ttu-id="6afe6-109">Zgodnie z opisem w hello [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md) artykułu, RBAC umożliwia precyzyjne zarządzanie dostępem zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6afe6-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="6afe6-110">Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji DevOps i udzielić tylko hello ilość toousers dostępu do potrzebnych tooperform swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="6afe6-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="6afe6-111">W usłudze DevTest Labs zasady jest typ zasobu, który umożliwia działanie RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="6afe6-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="6afe6-112">Każda zasada laboratorium jest zasobem w hello typu zasobu zasad i można przypisać jako rola RBAC tooan zakresu.</span><span class="sxs-lookup"><span data-stu-id="6afe6-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="6afe6-113">Na przykład w kolejności toogrant użytkowników odczytu/zapisu uprawnienia toohello **dozwolone rozmiary maszyn wirtualnych** zasad, należy utworzyć niestandardową rolę, która współdziała z hello **Microsoft.DevTestLab/labs/policySets/policies/** * akcję, a następnie przypisz hello odpowiednich użytkowników toothis niestandardową rolę w zakresie hello **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="6afe6-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="6afe6-114">toolearn więcej informacji na temat ról niestandardowych w RBAC, zobacz hello [niestandardowych ról dla kontroli dostępu](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6afe6-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="6afe6-115">Tworzenie laboratorium niestandardowej roli zabezpieczeń przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6afe6-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="6afe6-116">W kolejności tooget uruchomiona, należy hello tooread poniższego artykułu, który objaśnia sposób tooinstall i skonfigurować poleceń cmdlet programu Azure PowerShell hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="6afe6-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="6afe6-117">Po skonfigurowaniu hello poleceń cmdlet programu Azure PowerShell, można wykonać hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="6afe6-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="6afe6-118">Lista wszystkich hello operacji akcji dla dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="6afe6-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="6afe6-119">Akcje listy z określoną rolą:</span><span class="sxs-lookup"><span data-stu-id="6afe6-119">List actions in a particular role:</span></span>
* <span data-ttu-id="6afe6-120">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="6afe6-120">Create a custom role</span></span>

<span data-ttu-id="6afe6-121">Witaj następującego skryptu programu PowerShell przedstawiono przykłady tooperform te zadania:</span><span class="sxs-lookup"><span data-stu-id="6afe6-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="6afe6-122">Przypisywanie uprawnień tooa użytkownika dla określonych zasad przy użyciu ról niestandardowych</span><span class="sxs-lookup"><span data-stu-id="6afe6-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="6afe6-123">Po zdefiniowaniu poszczególnych ról niestandardowych, można przypisać je toousers.</span><span class="sxs-lookup"><span data-stu-id="6afe6-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="6afe6-124">W kolejności tooassign użytkownika tooa niestandardowej roli zabezpieczeń, należy najpierw uzyskać hello **ObjectId** reprezentujący użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6afe6-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="6afe6-125">toodo, który Użyj hello **Get-AzureRmADUser** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6afe6-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="6afe6-126">W hello poniższy przykład, hello **ObjectId** z hello *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 jest użytkownik.</span><span class="sxs-lookup"><span data-stu-id="6afe6-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="6afe6-127">Po utworzeniu hello **ObjectId** hello użytkownika i nazwę niestandardowej roli zabezpieczeń, można przypisać tej roli użytkownika toohello z hello **AzureRmRoleAssignment nowy** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6afe6-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="6afe6-128">W poprzednim przykładzie hello hello **AllowedVmSizesInLab** zasady są używane.</span><span class="sxs-lookup"><span data-stu-id="6afe6-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="6afe6-129">Można użyć dowolnej z powitalne następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="6afe6-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="6afe6-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="6afe6-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="6afe6-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="6afe6-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="6afe6-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="6afe6-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="6afe6-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="6afe6-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6afe6-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6afe6-134">Next steps</span></span>
<span data-ttu-id="6afe6-135">Raz użytkownikowi nie zostały przyznane zasad laboratorium toospecific uprawnień użytkownika, poniżej przedstawiono niektóre dalej tooconsider kroki:</span><span class="sxs-lookup"><span data-stu-id="6afe6-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="6afe6-136">[Bezpieczny dostęp tooa laboratorium](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="6afe6-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="6afe6-137">[Set lab policies](devtest-lab-set-lab-policy.md) (Ustawianie zasad laboratorium).</span><span class="sxs-lookup"><span data-stu-id="6afe6-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="6afe6-138">[Create a lab template](devtest-lab-create-template.md) (Tworzenie szablonu laboratorium).</span><span class="sxs-lookup"><span data-stu-id="6afe6-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="6afe6-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md) (Tworzenie niestandardowych artefaktów dla maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="6afe6-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="6afe6-140">[Dodawanie maszyny Wirtualnej z laboratorium tooa artefakty](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6afe6-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

