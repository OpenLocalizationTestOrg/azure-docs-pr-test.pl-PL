---
title: "na podstawie aaaRole kontroli dostępu z POZOSTAŁĄ — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zarządzanie kontrolą dostępu na podstawie ról z hello interfejsu API REST"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Zarządzanie oparte na rolach kontrola dostępu przy użyciu hello interfejsu API REST
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md)
> * [Interfejs API REST](role-based-access-control-manage-access-rest.md)

Oparta na rolach kontroli dostępu (RBAC) w hello portalu Azure i interfejsu API usługi Azure Resource Manager ułatwia zarządzanie subskrypcji tooyour dostępu i zasobów na poziomie szczegółowych. W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując toothem niektórych ról w określonym zakresie.

## <a name="list-all-role-assignments"></a>Wyświetl listę wszystkich przypisań ról
Wyświetla wszystkie przypisania roli hello na powitania określony zakres i subscopes.

przypisania ról toolist, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleAssignments/read` operacji w zakresie hello. Wszystkie role wbudowane hello udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello przypisań ról. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{wersja interfejsu api}* z 2015-07-01.
3. Zastąp *{filtru}* z warunkiem hello, że chcesz Lista przypisywanie roli tooapply toofilter hello:

   * Listę przypisań ról hello tylko określony zakres, nie włączając hello przypisania ról na subscopes:`atScope()`    
   * Utwórz listę przypisań ról dla określonego użytkownika, grupy lub aplikacji.`principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Lista przypisań ról określonego użytkownika, między innymi dziedziczone z grup |`assignedTo('{objectId of user}')`

### <a name="response"></a>Odpowiedź
Kod stanu: 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>Pobierz informacje o przypisaniu roli
Pobiera informacje o przypisaniu roli jednej, określonej przez identyfikator przypisania roli hello.

tooget informacje o przypisaniu roli, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleAssignments/read` operacji. Wszystkie role wbudowane hello udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello przypisań ról. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator przypisania roli-}* o identyfikatorze GUID hello hello przypisania roli.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

### <a name="response"></a>Odpowiedź
Kod stanu: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>Tworzy przypisanie roli
Tworzenie roli przydziału na powitania określony zakres hello określić głównej udzielającym hello rolę określoną w programie.

toocreate przypisania roli, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleAssignments/write` operacji. Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **PUT** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, w którym chcesz toocreate hello przypisań ról. Po utworzeniu przypisanie roli w zakresie nadrzędnym, wszystkie zakresy podrzędne dziedziczą hello tego samego przypisania roli. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1   
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator przypisania roli-}* za pomocą nowego identyfikatora GUID, który staje się identyfikator GUID hello hello nowe przypisanie roli.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

Treść żądania hello Podaj wartości hello w hello następującego formatu:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Nazwa elementu | Wymagane | Typ | Opis |
| --- | --- | --- | --- |
| wartość roleDefinitionId |Tak |Ciąg |Identyfikator Hello hello roli. format identyfikatora hello Hello jest:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Tak |Ciąg |Identyfikator obiektu podmiotu hello Azure AD (użytkownika, grupy lub nazwy głównej usługi) toowhich hello rola jest przypisywana. |

### <a name="response"></a>Odpowiedź
Kod stanu: 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>Usuwa przypisanie roli
Usuń przypisanie roli w hello określony zakres.

toodelete przypisania roli musi mieć dostęp do toohello `Microsoft.Authorization/roleAssignments/delete` operacji. Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **usunąć** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, w którym chcesz toocreate hello przypisań ról. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator przypisania roli-}* z identyfikator przypisania roli hello identyfikatora GUID.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

### <a name="response"></a>Odpowiedź
Kod stanu: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>Wyświetl listę wszystkich ról
Wyświetla wszystkie role hello, które są dostępne do przypisania w hello określony zakres.

toolist ról, należy mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/read` operacji w zakresie hello. Wszystkie role wbudowane hello udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello ról. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * /Subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1 zasobów  
2. Zastąp *{wersja interfejsu api}* z 2015-07-01.
3. Zastąp *{filtru}* z hello warunkiem, że chcesz tooapply toofilter hello lista ról:

   * Lista ról dostępne do przypisania na powitania określony zakres oraz wszystkie jego zakresy podrzędne:`atScopeAndBelow()`
   * Wyszukaj rolę przy użyciu nazwy wyświetlanej dokładne: `roleName%20eq%20'{role-display-name}'`. Formularz hello zakodowane w adresie URL nazwy wyświetlanej dokładne hello hello roli. Na przykład`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Odpowiedź
Kod stanu: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>Uzyskiwanie informacji o roli
Pobiera informacje o określonej przez identyfikator definicji roli hello jedną rolę. tooget informacji o pojedynczej roli przy użyciu nazwy wyświetlanej, zobacz [listy wszystkich ról](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget informacji na temat roli, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/read` operacji. Wszystkie role wbudowane hello udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello przypisań ról. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator definicji roli-}* o identyfikatorze GUID hello hello definicji roli.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

### <a name="response"></a>Odpowiedź
Kod stanu: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>Tworzenie niestandardowej roli zabezpieczeń
Tworzenie niestandardowej roli zabezpieczeń.

toocreate rolę niestandardową, musisz mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/write` operację na wszystkich hello `AssignableScopes`. Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **PUT** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z hello pierwszy *AssignableScope* hello niestandardowej roli. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów.

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator definicji roli-}* za pomocą nowego identyfikatora GUID, który staje się identyfikator GUID hello hello nowej niestandardowej roli.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

Treść żądania hello Podaj wartości hello w hello następującego formatu:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nazwa elementu | Wymagane | Typ | Opis |
| --- | --- | --- | --- |
| name |Tak |Ciąg |Identyfikator GUID hello niestandardowej roli zabezpieczeń. |
| properties.roleName |Tak |Ciąg |Nazwa wyświetlana hello niestandardowej roli zabezpieczeń. Maksymalny rozmiar 128 znaków. |
| Properties.Description |Nie |Ciąg |Opis roli niestandardowej hello. Maksymalny rozmiar 1024 znaki. |
| Properties.Type |Tak |Ciąg |Ustaw zbyt "CustomRole." |
| Properties.permissions.Actions |Tak |ciąg] |Tablica akcji ciągi określania operacji hello przyznane przez hello niestandardowej roli zabezpieczeń. |
| properties.permissions.notActions |Nie |ciąg] |Tablica ciągów akcji Określanie hello tooexclude operacje z operacji hello przyznane przez hello niestandardowej roli zabezpieczeń. |
| properties.assignableScopes |Tak |ciąg] |Tablica zakresów, w których hello można użyć niestandardowej roli zabezpieczeń. |

### <a name="response"></a>Odpowiedź
Kod stanu: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>Aktualizacja niestandardowej roli zabezpieczeń
Zmodyfikuj niestandardowej roli zabezpieczeń.

toomodify rolę niestandardową, musisz mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/write` operację na wszystkich hello `AssignableScopes`. Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **PUT** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z hello pierwszy *AssignableScope* hello niestandardowej roli. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator definicji roli-}* z identyfikator GUID hello hello niestandardowej roli zabezpieczeń.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

Treść żądania hello Podaj wartości hello w hello następującego formatu:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nazwa elementu | Wymagane | Typ | Opis |
| --- | --- | --- | --- |
| name |Tak |Ciąg |Identyfikator GUID hello niestandardowej roli zabezpieczeń. |
| properties.roleName |Tak |Ciąg |Nazwa wyświetlana hello zaktualizować niestandardowej roli zabezpieczeń. |
| Properties.Description |Nie |Ciąg |Opis hello zaktualizować niestandardowej roli zabezpieczeń. |
| Properties.Type |Tak |Ciąg |Ustaw zbyt "CustomRole." |
| Properties.permissions.Actions |Tak |ciąg] |Tablica ciągów akcji Określanie hello operacji toowhich hello zaktualizować niestandardowej roli zabezpieczeń przyznaje dostęp. |
| properties.permissions.notActions |Nie |ciąg] |Tablica akcji ciągi określania tooexclude operacji hello z operacji hello które hello zaktualizowane przyznaje niestandardowej roli zabezpieczeń. |
| properties.assignableScopes |Tak |ciąg] |Tablica zakresów, w których hello zaktualizowane niestandardowej roli zabezpieczeń mogą być używane. |

### <a name="response"></a>Odpowiedź
Kod stanu: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>Usunięcia niestandardowej roli zabezpieczeń
Usunięcia niestandardowej roli zabezpieczeń.

toodelete rolę niestandardową, musisz mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/delete` operację na wszystkich hello `AssignableScopes`. Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji. Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).

### <a name="request"></a>Żądanie
Użyj hello **usunąć** metody z hello następującego identyfikatora URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:

1. Zastąp *{zakresu}* z zakresem hello, w którym chcesz definicji roli hello toodelete. Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:

   * Subskrypcja: /subscriptions/ {identyfikator subskrypcji}  
   * Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1  
   * Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Zastąp *{— identyfikator definicji roli-}* z identyfikator definicji roli identyfikatora GUID hello hello niestandardowej roli.
3. Zastąp *{wersja interfejsu api}* z 2015-07-01.

### <a name="response"></a>Odpowiedź
Kod stanu: 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
