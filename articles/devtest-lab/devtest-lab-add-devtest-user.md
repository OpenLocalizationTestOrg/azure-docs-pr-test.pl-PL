---
title: "Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs za pomocą portalu Azure lub programu PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-craic
ms.openlocfilehash: 2921356f848739d602807236006f9867eaa2a4e4
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2018
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Steruje dostępu w usłudze Azure DevTest Labs [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md). Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji do *ról* gdzie udzielić tylko takiego dostępu niezbędne użytkownikom do wykonywania swoich zadań. Są trzy te role RBAC *właściciela*, *DevTest Labs użytkownika*, i *współautora*. W tym artykule dowiesz się, jakie akcje można wykonać w każdym trzy główne role RBAC. Z tego miejsca możesz dowiedzieć się, jak dodać użytkowników do laboratorium — zarówno w portalu, jak i za pomocą skryptu programu PowerShell i jak dodać użytkowników na poziomie subskrypcji.

## <a name="actions-that-can-be-performed-in-each-role"></a>Akcje, które mogą być wykonywane w każdej roli
Istnieją trzy główne role przypisanie użytkownika:

* Właściciel
* Użytkownik usługi DevTest Labs
* Współautor

W poniższej tabeli przedstawiono akcje, które mogą być wykonywane przez użytkowników w każdej z tych ról:

| **Można wykonać akcje użytkowników w tej roli** | **DevTest Labs użytkownika** | **Właściciel** | **Współautora** |
| --- | --- | --- | --- |
| **Zadania laboratorium** | | | |
| Dodawanie użytkowników do laboratorium |Nie |Yes |Nie |
| Aktualizowanie ustawień koszt |Nie |Yes |Yes |
| **Zadania podstawowej maszyny Wirtualnej** | | | |
| Dodawanie i usuwanie niestandardowych obrazów |Nie |Yes |Yes |
| Dodawanie, aktualizowanie i usuwanie formuły |Yes |Yes |Yes |
| Obrazy dozwolonych Azure Marketplace |Nie |Yes |Yes |
| **Zadania maszyny Wirtualnej** | | | |
| Tworzenie maszyn wirtualnych |Yes |Yes |Yes |
| Uruchamianie, zatrzymywanie i usuwanie maszyny wirtualne |Tylko maszyny wirtualne utworzone przez użytkownika |Yes |Yes |
| Aktualizowanie zasad maszyny Wirtualnej |Nie |Yes |Yes |
| Dodawanie/usuwanie dysków z danymi z maszyn wirtualnych |Tylko maszyny wirtualne utworzone przez użytkownika |Yes |Yes |
| **Zadania artefaktów** | | | |
| Dodawanie i usuwanie repozytoria artefaktów |Nie |Yes |Yes |
| Zastosuj artefaktów |Yes |Yes |Yes |

> [!NOTE]
> Gdy użytkownik tworzy Maszynę wirtualną, ten użytkownik zostanie automatycznie przypisany do **właściciela** roli maszyny wirtualnej utworzone.
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a>Dodawanie właściciela lub użytkownika na poziomie laboratorium
Właściciele i użytkowników można dodać na poziomie laboratorium za pośrednictwem portalu Azure. Dotyczy to również użytkowników zewnętrznych z prawidłowym [konta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).
Poniższe kroki ułatwiają dodawanie właściciela lub użytkowników do laboratorium w usłudze Azure DevTest Labs:

1. Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz pozycję **Więcej usług**, a następnie z listy wybierz pozycję **DevTest Labs**.
3. Z listy labs wybierz żądany laboratorium.
4. W bloku laboratorium, wybierz **konfiguracji**. 
5. Na **konfiguracji** bloku, wybierz opcję **użytkowników**.
6. Na **użytkowników** bloku, wybierz opcję **+ Dodaj**.
   
    ![Dodawanie użytkownika](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Na **wybierz rolę** bloku, wybierz odpowiednią rolę. Sekcja [akcje, które mogą być wykonywane w każdej roli](#actions-that-can-be-performed-in-each-role) wymieniono różne akcje, które mogą być wykonywane przez użytkowników w roli właściciela, DevTest użytkownika i współautor.
8. Na **dodawania użytkowników** bloku, wprowadź adres e-mail lub nazwa użytkownika mają zostać dodane w określonej roli. Jeśli nie można odnaleźć użytkownika, komunikat o błędzie opisano problem. Jeśli użytkownik zostanie znaleziony, ten użytkownik jest na liście i wybrane. 
9. Wybierz **wybierz**.
10. Wybierz **OK** zamknąć **Dodawanie dostępu** bloku.
11. Po powrocie do **użytkowników** bloku użytkownik został dodany.  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a>Dodaj użytkownika zewnętrznego w laboratorium przy użyciu programu PowerShell
Oprócz dodawania użytkowników w portalu Azure, można dodać użytkownika zewnętrznego do laboratorium za pomocą skryptu programu PowerShell. W poniższym przykładzie, po prostu zmodyfikuj wartości parametrów w obszarze **wartości w celu zmiany** komentarza.
Możesz pobrać `subscriptionId`, `labResourceGroup`, i `labName` wartości z bloku laboratorium w portalu Azure.

> [!NOTE]
> Przykładowy skrypt założono, że podany użytkownik został dodany jako gość w usłudze Active Directory i zakończy się niepowodzeniem, jeśli nie jest to. Aby dodać użytkownika nie w usłudze Active Directory w laboratorium, użyj portalu Azure można przypisać do roli użytkownika, jak pokazano w sekcji [dodać właściciela lub użytkownika na poziomie laboratorium](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a>Dodawanie właściciela lub użytkowników na poziomie subskrypcji
Azure uprawnienia są propagowane z zakresu nadrzędnego do zakresie podrzędnym na platformie Azure. W związku z tym właściciele subskrypcji platformy Azure, która zawiera labs są automatycznie właścicieli tych labs. Właścicielem również maszyn wirtualnych i innych zasobów utworzone przez użytkowników lab i usługa Azure DevTest Labs. 

Możesz dodać dodatkowe właścicieli do laboratorium za pomocą bloku laboratorium należy utworzyć w [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Jednak zakres właściciela dodano administracji jest coraz węższego niż zakresu właściciela subskrypcji. Na przykład dodano właścicieli nie masz pełny dostęp do niektórych zasobów, które są tworzone w subskrypcji przez usługę DevTest Labs. 

Aby dodać właściciela subskrypcji platformy Azure, wykonaj następujące kroki:

1. Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **subskrypcje** z listy.
3. Wybierz odpowiednią subskrypcję.
4. Wybierz **dostępu** ikony. 
   
    ![Dostęp do użytkowników](./media/devtest-lab-add-devtest-user/access-users.png)
5. Na **użytkowników** bloku, wybierz opcję **Dodaj**.
   
    ![Dodawanie użytkownika](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Na **wybierz rolę** bloku, wybierz **właściciela**.
7. Na **dodawania użytkowników** bloku, wprowadź adres e-mail lub nazwę użytkownika, które chcesz dodać jako właściciela. Jeśli nie można odnaleźć użytkownika, zostanie wyświetlony komunikat o błędzie, wyjaśniający problem. Jeśli użytkownik zostanie znaleziony, ten użytkownik zostanie wyświetlony w obszarze **użytkownika** pola tekstowego.
8. Wybierz nazwę użytkownika znajduje się.
9. Wybierz **wybierz**.
10. Wybierz **OK** zamknąć **Dodawanie dostępu** bloku.
11. Po powrocie do **użytkowników** bloku użytkownik został dodany jako właściciela. Ten użytkownik jest obecnie właścicielem żadnych labs utworzone w ramach tej subskrypcji i w związku z tym można wykonywać zadania właściciela. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

