---
title: "aaaAdd właścicieli i użytkowników w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs przy użyciu hello portalu Azure lub programu PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Steruje dostępu w usłudze Azure DevTest Labs [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md). Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji do *ról* gdzie udzielić tylko hello ilość tooperform niezbędne toousers dostęp do swoich zadań. Są trzy te role RBAC *właściciela*, *DevTest Labs użytkownika*, i *współautora*. W tym artykule dowiesz się, jakie akcje można wykonać w każdym trzy główne role RBAC hello. Z tego miejsca, możesz dowiedzieć się, jak laboratorium tooa użytkowników tooadd — zarówno za pośrednictwem hello portalu i za pomocą skryptu programu PowerShell i jak użytkownicy tooadd hello poziomu subskrypcji.

## <a name="actions-that-can-be-performed-in-each-role"></a>Akcje, które mogą być wykonywane w każdej roli
Istnieją trzy główne role przypisanie użytkownika:

* Właściciel
* DevTest Labs użytkownika
* Współautor

Witaj poniższej tabeli przedstawiono akcje hello, które mogą być wykonywane przez użytkowników w każdej z tych ról:

| **Można wykonać akcje użytkowników w tej roli** | **DevTest Labs użytkownika** | **Właściciel** | **Współautora** |
| --- | --- | --- | --- |
| **Zadania laboratorium** | | | |
| Dodaj użytkowników tooa laboratorium |Nie |Tak |Nie |
| Aktualizowanie ustawień koszt |Nie |Tak |Tak |
| **Zadania podstawowej maszyny Wirtualnej** | | | |
| Dodawanie i usuwanie niestandardowych obrazów |Nie |Tak |Tak |
| Dodawanie, aktualizowanie i usuwanie formuły |Tak |Tak |Tak |
| Obrazy dozwolonych Azure Marketplace |Nie |Tak |Tak |
| **Zadania maszyny Wirtualnej** | | | |
| Tworzenie maszyn wirtualnych |Tak |Tak |Tak |
| Uruchamianie, zatrzymywanie i usuwanie maszyny wirtualne |Tylko maszyny wirtualne utworzone przez użytkownika hello |Tak |Tak |
| Aktualizowanie zasad maszyny Wirtualnej |Nie |Tak |Tak |
| Dodawanie/usuwanie dysków z danymi z maszyn wirtualnych |Tylko maszyny wirtualne utworzone przez użytkownika hello |Tak |Tak |
| **Zadania artefaktów** | | | |
| Dodawanie i usuwanie repozytoria artefaktów |Nie |Tak |Tak |
| Zastosuj artefaktów |Tak |Tak |Tak |

> [!NOTE]
> Gdy użytkownik tworzy Maszynę wirtualną, ten użytkownik zostanie automatycznie przypisany toohello **właściciela** roli hello utworzyć maszyny Wirtualnej.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Dodawanie właściciela lub użytkownika na poziomie laboratorium hello
Na poziomie laboratorium hello za pośrednictwem portalu Azure hello można dodać właścicieli i użytkowników. Dotyczy to również użytkowników zewnętrznych z prawidłowym [konta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).
następujące kroki Hello informacje pomocne przy hello proces dodawania laboratorium tooa właściciela lub użytkowników w usłudze Azure DevTest Labs:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello.
4. W bloku hello laboratorium, wybierz **konfiguracji**. 
5. Na powitania **konfiguracji** bloku, wybierz opcję **użytkowników**.
6. Na powitania **użytkowników** bloku, wybierz opcję **+ Dodaj**.
   
    ![Dodawanie użytkownika](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Na powitania **wybierz rolę** bloku, hello wybierz odpowiednią rolę. Witaj sekcji [akcje, które mogą być wykonywane w każdej roli](#actions-that-can-be-performed-in-each-role) list hello różne akcje, które mogą być wykonywane przez użytkowników pełniących role hello właściciela, DevTest użytkownika i współautor.
8. Na powitania **dodawania użytkowników** bloku, wprowadź adres e-mail hello lub nazwa użytkownika hello ma tooadd w określonej roli hello. Jeśli nie można odnaleźć użytkownika hello, komunikat o błędzie wyjaśniono hello problem. Jeśli użytkownik hello zostanie znaleziony, ten użytkownik jest na liście i wybrać. 
9. Wybierz **wybierz**.
10. Wybierz **OK** tooclose hello **Dodawanie dostępu** bloku.
11. Po powrocie toohello **użytkowników** bloku hello użytkownik został dodany.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Dodaj użytkownika zewnętrznego laboratorium tooa przy użyciu programu PowerShell
Ponadto tooadding użytkowników w portalu Azure hello, można dodać użytkownika zewnętrznego laboratorium tooyour za pomocą skryptu programu PowerShell. W hello poniższy przykład, wystarczy zmodyfikować hello wartości parametrów w obszarze hello **toochange wartości** komentarza.
Możesz pobrać hello `subscriptionId`, `labResourceGroup`, i `labName` wartości z bloku laboratorium hello w hello portalu Azure.

> [!NOTE]
> Witaj przykładowy skrypt przyjęto założenie, że tego hello określony użytkownik został dodany jako gość toohello usługi Active Directory i zakończy się niepowodzeniem, jeśli nie jest ona hello przypadku. tooadd użytkownik nie istnieje w hello laboratorium tooa usługi Active Directory, użyj roli użytkownika hello hello tooassign portalu Azure w tooa, jak pokazano w sekcji hello [dodać właściciela lub użytkownika na poziomie laboratorium hello](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Dodawanie właściciela lub użytkowników na poziomie subskrypcji hello
Azure uprawnienia zostały przeniesione z zakresu toochild zakresu nadrzędnego na platformie Azure. W związku z tym właściciele subskrypcji platformy Azure, która zawiera labs są automatycznie właścicieli tych labs. Właścicielem również hello maszyn wirtualnych i innych zasobów tworzone przez użytkowników hello laboratorium i hello Azure DevTest Labs usługi. 

Można dodać dodatkowe właścicieli laboratorium tooa za pomocą bloku laboratorium hello hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Jednak hello dodano zakres właściciela administracji jest coraz węższego niż właściciel subskrypcji hello zakresu. Na przykład hello dodać właścicieli nie mają pełny dostęp toosome hello zasobów, które są tworzone w ramach subskrypcji hello przez hello usługi DevTest Labs. 

tooadd tooan właściciela subskrypcji platformy Azure, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **subskrypcje** z listy hello.
3. Wybierz żądaną hello subskrypcję.
4. Wybierz **dostępu** ikony. 
   
    ![Dostęp do użytkowników](./media/devtest-lab-add-devtest-user/access-users.png)
5. Na powitania **użytkowników** bloku, wybierz opcję **Dodaj**.
   
    ![Dodawanie użytkownika](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Na powitania **wybierz rolę** bloku, wybierz **właściciela**.
7. Na powitania **dodawania użytkowników** bloku, wprowadź adres e-mail hello lub nazwa użytkownika hello ma tooadd jako właściciela. Jeśli nie można odnaleźć użytkownika hello, otrzymasz komunikat o błędzie wyjaśniający hello problem. Jeśli użytkownik hello zostanie znaleziony, ten użytkownik zostanie wyświetlony w obszarze hello **użytkownika** pola tekstowego.
8. Wybierz nazwę użytkownika znajduje się hello.
9. Wybierz **wybierz**.
10. Wybierz **OK** tooclose hello **Dodawanie dostępu** bloku.
11. Po powrocie toohello **użytkowników** bloku hello użytkownik został dodany jako właściciela. Ten użytkownik jest obecnie właścicielem żadnych labs utworzone w ramach tej subskrypcji, a w związku z tym być stanie tooperform właściciela zadania. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

