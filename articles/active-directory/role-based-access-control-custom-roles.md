---
title: role niestandardowe aaaCreate dla Azure RBAC | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak role niestandardowe toodefine z kontroli dostępu dla bardziej precyzyjne zarządzanie tożsamościami w ramach subskrypcji platformy Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Tworzenie niestandardowych ról dla kontroli dostępu
Utwórz niestandardową rolę based kontroli dostępu (RBAC), jeśli żadna hello wbudowanych ról nie spełnia Twoje potrzeby określonym dostępu. Role niestandardowe można tworzyć przy użyciu [programu Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfejsu wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) i hello [interfejsu API REST](role-based-access-control-manage-access-rest.md). Podobnie jak wbudowane role można przypisać role niestandardowe toousers, grup i aplikacji w subskrypcji, grupy zasobów i zakresy zasobów. Role niestandardowe są przechowywane w dzierżawie usługi Azure AD i mogą być udostępniane między subskrypcjami.

Poszczególni dzierżawcy można utworzyć zapasowej too2000 role niestandardowe. 

Witaj poniższy przykład przedstawia niestandardowej roli zabezpieczeń dotyczące monitorowania i ponowne uruchamianie maszyn wirtualnych:

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>Akcje
Witaj **akcje** określa właściwości niestandardowej roli zabezpieczeń hello Azure operacji toowhich hello rola przyznaje dostęp. Jest kolekcją operacji ciągów, które identyfikują zabezpieczanego operacje dostawców zasobów platformy Azure. Operacja ciągów wykonaj hello format `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Ciągi operacji, które zawierają symbole wieloznaczne (\*) udzielić dostępu tooall operacje, które odpowiada hello operacji ciągu. Na wystąpienie:

* `*/read`udziela dostępu do operacji tooread dla wszystkich typów zasobów wszystkich dostawców zasobów platformy Azure.
* `Microsoft.Compute/*`udziela dostępu do operacji tooall dla wszystkich typów zasobów dostawcy zasobów Microsoft.Compute hello.
* `Microsoft.Network/*/read`udziela dostępu do operacji tooread dla wszystkich typów zasobów w dostawcę zasobów Microsoft.Network hello Azure.
* `Microsoft.Compute/virtualMachines/*`udziela dostępu do operacji tooall maszyn wirtualnych i jego typów zasobów podrzędnych.
* `Microsoft.Web/sites/restart/Action`udziela dostępu do witryn sieci Web toorestart.

Użyj `Get-AzureRmProviderOperation` (w programie PowerShell) lub `azure provider operations show` (w Azure CLI) operacji toolist dostawców zasobów platformy Azure. Można także użyć tych poleceń tooverify, czy parametry operacji są prawidłowe i tooexpand symbolu wieloznacznego operacji ciągów.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Zrzut ekranu PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Azure CLI zrzut ekranu - azure dostawcy operacji Pokaż "Microsoft.Compute/virtualMachines/\*Action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Użyj hello **NotActions** właściwość, o ile hello zestaw operacji, że chcesz tooallow łatwiej jest definiowana za pomocą z wyjątkiem operacji ograniczone. Witaj dostępu przyznane przez niestandardowej roli zabezpieczeń jest obliczana przez odjęcie hello **NotActions** operacji hello **akcje** operacji.

> [!NOTE]
> Jeśli użytkownik ma przypisaną rolę, który wyklucza operacji w **NotActions**i ma przypisaną rolę drugiego, która udziela dostępu toohello tej samej operacji, hello użytkownika jest dozwolone tooperform tej operacji. **NotActions** nie jest odmowy reguły — jest po prostu wygodny sposób toocreate zestaw dozwolonych operacji określonych operacji należy toobe wykluczone.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Witaj **AssignableScopes** właściwości niestandardowej roli zabezpieczeń hello Określa zakresy hello (subskrypcji, grupy zasobów lub zasobów) w ramach których hello niestandardowej roli zabezpieczeń jest dostępne do przypisania. Można udostępnić hello niestandardowej roli zabezpieczeń do przypisywania w tylko hello subskrypcji lub grupy zasobów, które wymagają, a nie użytkownika bałaganu środowisko reszty hello hello subskrypcji lub grupy zasobów.

Prawidłowe zakresy można przypisać należą:

* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - sprawia, że rola hello jest dostępne do przypisania w dwóch subskrypcji.
* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - sprawia, że rola hello jest dostępne do przypisania w ramach jednej subskrypcji.
* "/ subskrypcji i c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/sieci" - sprawia, że hello dostępne do przypisania tylko w grupie zasobów sieciowych hello roli.

> [!NOTE]
> Należy użyć co najmniej jednego subskrypcji, grupy zasobów lub identyfikator zasobu.
>
>

## <a name="custom-roles-access-control"></a>Kontrola dostępu role niestandardowe
Witaj **AssignableScopes** właściwości niestandardowej roli zabezpieczeń hello również określać, kto może wyświetlać, modyfikowanie i usuwanie roli hello.

* Który można utworzyć niestandardową rolę?
    Właściciele (i administratorów dostępu użytkownika) subskrypcji, grupy zasobów i zasoby można tworzyć role niestandardowe do użycia w tych zakresów.
    Hello tworzenie hello roli użytkownika musi tooperform stanie toobe `Microsoft.Authorization/roleDefinition/write` operację na wszystkich hello **AssignableScopes** hello roli.
* Kto może zmodyfikować niestandardową rolę?
    Właściciele (i administratorów dostępu użytkowników) z subskrypcji, grupy zasobów i zasoby można zmodyfikować role niestandardowe w tych zakresów. Użytkownicy muszą hello stanie tooperform toobe `Microsoft.Authorization/roleDefinition/write` operację na wszystkich hello **AssignableScopes** z niestandardowej roli zabezpieczeń.
* Kto może wyświetlać role niestandardowe?
    Wszystkie role wbudowane w Azure RBAC umożliwiają wyświetlanie ról, które są dostępne do przypisania. Użytkownicy, którzy mogą wykonywać hello `Microsoft.Authorization/roleDefinition/read` operacji w zakresie mogą wyświetlać role RBAC hello, które są dostępne do przypisania w tym zakresie.

## <a name="see-also"></a>Zobacz też
* [Kontroli dostępu opartej na rolach](role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w hello portalu Azure.
* Dowiedz się, jak toomanage do uzyskiwania dostępu do:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Interfejs wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md)
  * [Interfejs API REST](role-based-access-control-manage-access-rest.md)
* [Wbudowane role](role-based-access-built-in-roles.md): uzyskiwanie szczegółowych informacji o rolach hello, które standardowo w RBAC.
