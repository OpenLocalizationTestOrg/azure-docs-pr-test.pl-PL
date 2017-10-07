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
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Zarządzanie kontrolą dostępu opartą na rolach za pomocą programu Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md)
> * [Interfejs API REST](role-based-access-control-manage-access-rest.md)

Kontrola dostępu oparta na rolach (RBAC) służy w hello portalu Azure i interfejs API zarządzania zasobów Azure toomanage dostępu tooyour subskrypcji na poziomie szczegółowych. W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując toothem niektórych ról w określonym zakresie.

Przed użyciem programu PowerShell toomanage RBAC, należy hello następujące wymagania wstępne:

* Program Azure PowerShell w wersji 0.8.8 lub nowszej. tooinstall hello najnowszej wersji i powiąż go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Polecenia cmdlet Menedżera zasobów systemu Azure. Zainstaluj hello [poleceń cmdlet usługi Azure Resource Manager](/powershell/azure/overview) w programie PowerShell.

## <a name="list-roles"></a>Lista ról
### <a name="list-all-available-roles"></a>Wyświetl listę wszystkich dostępnych ról
role RBAC toolist, które są dostępne do przypisania i toowhich operacji hello tooinspect przyznają dostęp, użyj `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Akcje listy roli
działania hello toolist dla konkretnej roli przy użyciu `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition dla konkretnej roli - RBAC](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Zobacz, kto ma dostęp
przydziały dostępu RBAC toolist, użyj `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Lista przypisań ról w określonym zakresie
Znajduje wszystkie przypisania dostępu powitania dla określonej subskrypcji, grupy zasobów lub zasobów. Na przykład toosee hello wszystkich hello active przydziałów dla grupy zasobów, użyj `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![Zrzut ekranu PowerShell-Get AzureRmRoleAssignment dla grupy zasobów - RBAC](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Lista ról przypisany użytkownik tooa
wszystkie role hello przypisanych tooa określony użytkownika i przypisanych grup toohello toowhich hello użytkownika, należy ról hello toolist użyj `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![Zrzut ekranu PowerShell-Get AzureRmRoleAssignment dla użytkownika — RBAC](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Wyświetl listę przypisań ról administratora i coadmin klasycznym usługi
toolist dostępu przydziały hello subskrypcji klasycznego administratora i coadministrators, należy użyć:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Udzielanie dostępu
### <a name="search-for-object-ids"></a>Wyszukaj identyfikatory obiektów
tooassign roli należy tooidentify zarówno hello obiektów (użytkowników, grupy lub aplikacji), jak i zakres hello.

Jeśli nie znasz hello identyfikator subskrypcji można znaleźć je w hello **subskrypcje** bloku na powitania portalu Azure. toolearn tooquery hello subskrypcji o identyfikatorze, zobacz temat [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) w witrynie MSDN.

Użyj Identyfikatora obiektu hello tooget dla grupy usługi Azure AD:

    Get-AzureRmADGroup -SearchString <group name in quotes>

Identyfikator obiektu hello tooget nazwy głównej usługi Azure AD lub aplikacji, należy użyć:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Przypisz aplikację tooan rola w zakresie subskrypcji hello
toogrant aplikacji tooan dostępu w zakresie subskrypcji hello, użyj:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![Zrzut ekranu PowerShell — nowy AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Przypisywanie roli użytkownika tooa w zakresie grupy zasobów hello
toogrant dostęp tooa użytkownika w zakresie hello do grupy zasobów, użyj:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![Zrzut ekranu PowerShell — nowy AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Przypisz grupę tooa rola w zakresie zasobów hello
toogrant grupy tooa dostępu w zakresie zasobów hello, użyj:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![Zrzut ekranu PowerShell — nowy AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Usuń dostęp
tooremove dostęp dla użytkowników, grup i aplikacji, użyj:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![Zrzut ekranu PowerShell-Remove AzureRmRoleAssignment - RBAC](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Tworzenie niestandardowej roli zabezpieczeń
toocreate niestandardowej roli zabezpieczeń, użyj hello ```New-AzureRmRoleDefinition``` polecenia. Istnieją dwie metody struktury hello rolę, za pomocą PSRoleDefinitionObject lub szablonu JSON. 

## <a name="get-actions-for-a-resource-provider"></a>Pobierz akcji dla dostawcy zasobów
Tworząc role niestandardowe od początku, jest ważne tooknow hello wszystkie możliwe operacje z hello dostawców zasobów.
Użyj hello ```Get-AzureRMProviderOperation``` polecenia tooget te informacje.
Na przykład jeśli chcesz toocheck wszystkie hello operacje dostępne dla maszyny wirtualnej, użyj tego polecenia:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Tworzenie roli z PSRoleDefinitionObject
Korzystając z programu PowerShell toocreate niestandardowej roli zabezpieczeń, możesz rozpocząć od początku lub użyj jednej z hello [wbudowane role](role-based-access-built-in-roles.md) jako punktu wyjścia. przykład Witaj w tej sekcji rozpoczyna się od wbudowanej roli i dostosowuje go z wyższego poziomu uprawnień. Edytuj hello atrybuty tooadd hello *akcje*, *notActions*, lub *zakresy* , a następnie zapisz zmiany hello jako nową rolę.

Hello poniższy przykład rozpoczyna się od hello *Współautor·maszyny·wirtualnej* roli i używa tego toocreate niestandardowej roli zabezpieczeń o nazwie *Operator maszyny wirtualnej*. Witaj nowa rola przyznaje tooall dostęp do odczytu dla operacji *Microsoft.Compute*, *Microsoft.Storage*, i *Microsoft.Network* dostęp do dostawcy i przyznaje zasobów toostart, ponownie uruchomić i monitorować maszyn wirtualnych. Rola niestandardowa Hello może służyć w dwóch subskrypcji.

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

### <a name="create-role-with-json-template"></a>Tworzenie roli przy użyciu szablonu JSON
Szablon JSON można jako definicji źródła hello hello niestandardowej roli zabezpieczeń. Witaj poniższy przykład tworzy niestandardową rolę, która umożliwia dostęp do odczytu toostorage i zasoby obliczeniowe, dostęp do toosupport i dodaje tej roli tootwo subskrypcji. Utwórz nowy plik `C:\CustomRoles\customrole1.json` z hello poniższy przykład. Witaj Id powinna być ustawiona zbyt`null` na tworzenie początkowej roli jako nowy identyfikator jest generowany automatycznie. 

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
tooadd hello roli toohello subskrypcje, uruchom następujące polecenia programu PowerShell hello:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Modyfikowanie niestandardowej roli zabezpieczeń
Podobne toocreating niestandardowej roli zabezpieczeń, można zmodyfikować istniejącą rolę niestandardowych za pomocą hello PSRoleDefinitionObject lub szablonu JSON.

### <a name="modify-role-with-psroledefinitionobject"></a>Modyfikuj rolę z PSRoleDefinitionObject
toomodify niestandardowej roli zabezpieczeń, najpierw użyj hello `Get-AzureRmRoleDefinition` definicji roli hello tooretrieve poleceń. Po drugie zmiany hello potrzeby toohello definicji roli. Na koniec użyj hello `Set-AzureRmRoleDefinition` hello toosave polecenia zmodyfikować definicji roli.

Witaj poniższy przykład umożliwia dodanie hello `Microsoft.Insights/diagnosticSettings/*` toohello operacji *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![Zrzut ekranu PowerShell-Set AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Witaj poniższy przykład umożliwia dodanie zakresy możliwe do przypisania toohello subskrypcji platformy Azure z hello *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![Zrzut ekranu PowerShell-Set AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Modyfikuj rolę przy użyciu szablonu JSON
Przy użyciu szablonu JSON w poprzednim hello, można łatwo zmodyfikować istniejący tooadd niestandardowej roli zabezpieczeń lub usunąć akcje. Aktualizowanie hello JSON szablonu, a następnie dodaj hello odczytu działania dotyczące sieci, jak pokazano w hello poniższy przykład. definicje Hello hello szablonu na liście są zbiorczo zastosowane tooan istniejącej definicji, co oznacza, że ta rola hello pojawi się dokładnie, jak określone w szablonie hello. Należy również pole identyfikatora hello tooupdate o identyfikatorze hello hello roli. Jeśli nie masz pewności, ta wartość jest, możesz użyć hello `Get-AzureRmRoleDefinition` tooget polecenia cmdlet te informacje.

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

tooupdate hello istniejącą rolę, uruchom następujące polecenia programu PowerShell hello:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Usunięcia niestandardowej roli zabezpieczeń
toodelete niestandardowej roli zabezpieczeń, użyj hello `Remove-AzureRmRoleDefinition` polecenia.

Witaj poniższy przykład umożliwia usunięcie hello *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![Zrzut ekranu PowerShell-Remove AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Lista ról niestandardowych
toolist hello ról, które są dostępne do przypisania w zakresie, użyj hello `Get-AzureRmRoleDefinition` polecenia.

Poniższy przykład Hello zawiera listę wszystkich ról, które są dostępne do przypisania w ramach subskrypcji hello wybrane.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

W hello poniższy przykład, hello *Operator maszyny wirtualnej* rola niestandardowa nie jest dostępna w hello *Production4* subskrypcji, ponieważ nie ma subskrypcji hello  **AssignableScopes** hello roli.

![Zrzut ekranu PowerShell-Get AzureRmRoleDefinition - RBAC](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Zobacz też
* [Używanie programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

