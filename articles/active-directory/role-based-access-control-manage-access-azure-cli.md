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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Zarządzanie oparte na rolach kontrola dostępu przy użyciu hello interfejsu wiersza polecenia platformy Azure
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md)
> * [Interfejs API REST](role-based-access-control-manage-access-rest.md)


Kontrola dostępu oparta na rolach (RBAC) służy w hello portalu Azure i interfejsu API usługi Azure Resource Manager toomanage dostępu tooyour subskrypcji i zasobów na poziomie szczegółowych. W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując toothem niektórych ról w określonym zakresie.

Przed użyciem hello Azure interfejsu wiersza polecenia (CLI) toomanage RBAC, musi mieć hello następujące wymagania wstępne:

* Azure CLI w wersji 0.8.8 lub nowszej. tooinstall hello najnowszej wersji i powiąż go z subskrypcją platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).
* Usługa Azure Resource Manager w interfejsu wiersza polecenia platformy Azure. Przejdź za[hello Using Azure CLI z hello Resource Manager](../xplat-cli-azure-resource-manager.md) więcej szczegółów.

## <a name="list-roles"></a>Lista ról
### <a name="list-all-available-roles"></a>Wyświetl listę wszystkich dostępnych ról
toolist wszystkie dostępne role, należy użyć:

        azure role list

Witaj poniższy przykład przedstawia listę hello *wszystkie dostępne role*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Zrzut ekranu wiersza polecenia — Lista roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Akcje listy roli
Akcje hello toolist roli, należy użyć:

    azure role show "<role name>"

Hello poniższy przykład przedstawia hello akcje hello *współautora* i *Współautor·maszyny·wirtualnej* ról.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Zrzut ekranu wiersza polecenia — Pokaż roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Dostęp do listy
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Lista przypisań ról skuteczne w grupie zasobów
przypisania ról hello toolist, które istnieją w grupie zasobów, użyj:

    azure role assignment list --resource-group <resource group name>

Witaj poniższy przykład przedstawia przypisań ról hello w hello *pharma sprzedaży projecforcast* grupy.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Zrzut ekranu wiersza polecenia — Lista przypisywanie roli azure przez grupę - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Lista przypisań ról dla użytkownika
przypisania ról hello toolist dla określonego użytkownika i hello przypisań grup tooa użytkowników, należy użyć:

    azure role assignment list --signInName <user email>

Możesz też sprawdzić przypisań ról, które są dziedziczone z grupy, modyfikując hello polecenia:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Witaj poniższy przykład przedstawia hello przypisań ról, którym udzielono toohello  *sameert@aaddemo.com*  użytkownika. W tym role, które są przypisywane bezpośrednio toohello użytkowników i role, które są dziedziczone z grupy.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Zrzut ekranu wiersza polecenia — Lista przypisywanie roli azure przez użytkownika - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Udzielanie dostępu
toogrant dostępu po zidentyfikowaniu hello roli, które mają tooassign za pomocą:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Przypisz toogroup roli, w zakresie subskrypcji hello
tooassign grupy tooa ról w zakresie subskrypcji hello, użyj:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Witaj w poniższym przykładzie przypisano hello *czytnika* roli zbyt*zespołu Christine Koch* na powitania *subskrypcji* zakresu.

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć grupy — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Przypisz aplikację tooan rola w zakresie subskrypcji hello
tooassign aplikacją tooan rola w zakresie subskrypcji hello, użyj:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Witaj w przykładzie poniżej zezwolenie hello *współautora* tooan roli *usługi Azure AD* wybrać aplikację na powitania subskrypcji.

 ![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć przez aplikację](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Przypisywanie roli użytkownika tooa w zakresie grupy zasobów hello
tooassign tooa roli użytkownika w zakresie hello do grupy zasobów, użyj:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Witaj poniższy przykład przyznaje hello *współautora maszyny wirtualnej* roli zbyt *samert@aaddemo.com*  użytkownika na powitania *Pharma-sprzedaży-ProjectForcast* zakres grupy zasobów.

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć przez użytkownika — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Przypisz grupę tooa rola w zakresie zasobów hello
tooassign grupy tooa ról w zakresie zasobów hello, użyj:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Witaj w przykładzie poniżej zezwolenie hello *współautora maszyny wirtualnej* tooan roli *usługi Azure AD* na *podsieci*.

![Wiersz poleceń Azure RBAC — przypisanie roli azure utworzyć grupy — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Usuń dostęp
Użyj tooremove przypisania roli:

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

Hello poniższy przykład umożliwia usunięcie hello *Współautor·maszyny·wirtualnej* przypisania roli z hello  *sammert@aaddemo.com*  użytkownika na powitania *Pharma-sprzedaży-ProjectForcast* grupy zasobów.
przykład Witaj następnie usuwa przypisanie roli hello grupy na powitania subskrypcji.

![Zrzut ekranu wiersza polecenia - usunięcia przypisania roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Tworzenie niestandardowej roli zabezpieczeń
toocreate niestandardowej roli zabezpieczeń, należy użyć:

    azure role create --inputfile <file path>

Witaj poniższy przykład powoduje utworzenie niestandardowej roli zabezpieczeń o nazwie *Operator maszyny wirtualnej*. Tę rolę niestandardową przyznaje tooall dostęp do odczytu dla operacji *Microsoft.Compute*, *Microsoft.Storage*, i *Microsoft.Network* dostęp do dostawcy i przyznaje zasobów toostart, ponownie uruchomić i monitorować maszyn wirtualnych. Tę rolę niestandardową można w dwóch subskrypcji. W tym przykładzie używany jest plik JSON jako danych wejściowych.

![JSON - niestandardową definicję roli — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Tworzenie roli azure wiersza poleceń Azure RBAC - — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Modyfikowanie niestandardowej roli zabezpieczeń
toomodify niestandardowej roli zabezpieczeń, należy najpierw użyć hello `azure role show` polecenia tooretrieve definicji roli. Po drugie upewnij się plik definicji roli hello żądane zmiany toohello. Na koniec użyj `azure role set` toosave hello zmodyfikował definicję roli.

    azure role set --inputfile <file path>

Witaj poniższy przykład umożliwia dodanie hello *Microsoft.Insights/diagnosticSettings/* toohello operacji **akcje**i toohello subskrypcji platformy Azure **AssignableScopes**roli niestandardowych hello Operator maszyny wirtualnej.

![JSON - zmodyfikować niestandardową definicję roli — zrzut ekranu](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Zrzut ekranu wiersza polecenia - azure roli set - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Usunięcia niestandardowej roli zabezpieczeń
toodelete niestandardowej roli zabezpieczeń, należy najpierw użyć hello `azure role show` hello toodetermine polecenia **identyfikator** hello roli. Następnie należy użyć hello `azure role delete` roli hello toodelete polecenie, określając hello **identyfikator**.

Witaj poniższy przykład umożliwia usunięcie hello *Operator maszyny wirtualnej* niestandardowej roli zabezpieczeń.

![Zrzut ekranu wiersza polecenia - usunięcia roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Lista ról niestandardowych
toolist hello ról, które są dostępne do przypisania w zakresie, użyj hello `azure role list` polecenia.

Witaj następujące polecenie wyświetla listę wszystkich ról, które są dostępne do przypisania w ramach subskrypcji hello wybrane.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Zrzut ekranu wiersza polecenia — Lista roli azure - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

W hello poniższy przykład, hello *Operator maszyny wirtualnej* rola niestandardowa nie jest dostępna w hello *Production4* subskrypcji, ponieważ nie ma subskrypcji hello  **AssignableScopes** hello roli.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Zrzut ekranu wiersza polecenia — Lista azure roli dla role niestandardowe - RBAC Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

