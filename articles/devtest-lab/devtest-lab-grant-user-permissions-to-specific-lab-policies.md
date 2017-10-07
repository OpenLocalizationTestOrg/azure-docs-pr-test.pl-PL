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
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Przyznawanie uprawnień użytkownikom toospecific zasad laboratorium
## <a name="overview"></a>Omówienie
W tym artykule przedstawiono sposób toouse PowerShell toogrant użytkownikom uprawnienia tooa laboratorium określonego zasad. W ten sposób uprawnienia mogą być stosowane zgodnie z potrzebami każdego użytkownika. Na przykład może być toogrant określonego hello możliwości toochange hello wirtualna ustawień zasad użytkownika, ale nie hello koszt zasad.

## <a name="policies-as-resources"></a>Zasady jako zasoby
Zgodnie z opisem w hello [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md) artykułu, RBAC umożliwia precyzyjne zarządzanie dostępem zasobów platformy Azure. Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji DevOps i udzielić tylko hello ilość toousers dostępu do potrzebnych tooperform swoich zadań.

W usłudze DevTest Labs zasady jest typ zasobu, który umożliwia działanie RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**. Każda zasada laboratorium jest zasobem w hello typu zasobu zasad i można przypisać jako rola RBAC tooan zakresu.

Na przykład w kolejności toogrant użytkowników odczytu/zapisu uprawnienia toohello **dozwolone rozmiary maszyn wirtualnych** zasad, należy utworzyć niestandardową rolę, która współdziała z hello **Microsoft.DevTestLab/labs/policySets/policies/** * akcję, a następnie przypisz hello odpowiednich użytkowników toothis niestandardową rolę w zakresie hello **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn więcej informacji na temat ról niestandardowych w RBAC, zobacz hello [niestandardowych ról dla kontroli dostępu](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Tworzenie laboratorium niestandardowej roli zabezpieczeń przy użyciu programu PowerShell
W kolejności tooget uruchomiona, należy hello tooread poniższego artykułu, który objaśnia sposób tooinstall i skonfigurować poleceń cmdlet programu Azure PowerShell hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Po skonfigurowaniu hello poleceń cmdlet programu Azure PowerShell, można wykonać hello następujące zadania:

* Lista wszystkich hello operacji akcji dla dostawcy zasobów
* Akcje listy z określoną rolą:
* Tworzenie niestandardowej roli zabezpieczeń

Witaj następującego skryptu programu PowerShell przedstawiono przykłady tooperform te zadania:

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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Przypisywanie uprawnień tooa użytkownika dla określonych zasad przy użyciu ról niestandardowych
Po zdefiniowaniu poszczególnych ról niestandardowych, można przypisać je toousers. W kolejności tooassign użytkownika tooa niestandardowej roli zabezpieczeń, należy najpierw uzyskać hello **ObjectId** reprezentujący użytkownika. toodo, który Użyj hello **Get-AzureRmADUser** polecenia cmdlet.

W hello poniższy przykład, hello **ObjectId** z hello *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 jest użytkownik.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Po utworzeniu hello **ObjectId** hello użytkownika i nazwę niestandardowej roli zabezpieczeń, można przypisać tej roli użytkownika toohello z hello **AzureRmRoleAssignment nowy** polecenia cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

W poprzednim przykładzie hello hello **AllowedVmSizesInLab** zasady są używane. Można użyć dowolnej z powitalne następujące zasady:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
Raz użytkownikowi nie zostały przyznane zasad laboratorium toospecific uprawnień użytkownika, poniżej przedstawiono niektóre dalej tooconsider kroki:

* [Bezpieczny dostęp tooa laboratorium](devtest-lab-add-devtest-user.md).
* [Set lab policies](devtest-lab-set-lab-policy.md) (Ustawianie zasad laboratorium).
* [Create a lab template](devtest-lab-create-template.md) (Tworzenie szablonu laboratorium).
* [Create custom artifacts for your VMs](devtest-lab-artifact-author.md) (Tworzenie niestandardowych artefaktów dla maszyn wirtualnych).
* [Dodawanie maszyny Wirtualnej z laboratorium tooa artefakty](devtest-lab-add-vm-with-artifacts.md).

