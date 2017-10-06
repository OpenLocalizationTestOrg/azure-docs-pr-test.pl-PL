---
title: "Administrator aaaTenant podniesienie uprawnień dostępu — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano hello wbudowanych ról dla kontroli dostępu opartej na rolach (RBAC)."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Podniesienie uprawnień dostępu jako Administrator dzierżawy przy użyciu kontroli dostępu opartej na rolach

Oparta na rolach kontrola dostępu ułatwia administratorom dzierżawy uzyskiwania wybierającym tymczasowe w programie access, przyznają uprawnienia wyższe niż zwykle. Administrator dzierżawy podnieść poziom sobie toohello roli Administrator dostępu użytkowników, w razie potrzeby. Ta rola zapewnia hello toogrant uprawnień administratora dzierżawy, siebie lub innych ról na powitania zakresu "/".

Ta funkcja jest ważna, ponieważ umożliwia dzierżawy hello toosee admin hello wszystkie subskrypcje, które istnieją w organizacji. Również umożliwia automatyzacji aplikacji (takich jak fakturowania i inspekcji) tooaccess wszystkie subskrypcje hello i podaj dokładnego widoku stanu hello hello organizacji w celu zarządzania rozliczeń lub zasobów.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Jak toouse elevateAccess toogive dzierżawy dostępu

Witaj podstawowy proces działa z hello następujące kroki:

1. Za pomocą usługi REST, wywołaj *elevateAccess*, który przyznaje możesz hello roli Administrator dostępu użytkowników na "/" zakres.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Utwórz [przypisania roli](/rest/api/authorization/roleassignments) tooassign żadnej roli w dowolnym zakresie. Witaj poniższy przykład przedstawia właściwości hello przypisywania hello rolę czytelnika w "/" zakres:

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. Podczas administratorem dostępu użytkownika użytkownik może również usunąć przypisania roli w "/" zakres.

4. Odwołaj Twoje uprawnienia administratora dostępu użytkownika, dopóki nie są potrzebne, ponownie.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Jak tooundo hello elevateAccess akcji

Podczas wywoływania *elevateAccess* utworzyć przypisania roli dla siebie, więc toorevoke te uprawnienia możesz muszą toodelete hello przypisania.

1.  Wywołanie [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) gdzie roleName = nazwa hello Administrator dostępu użytkowników toodetermine identyfikator GUID hello roli Administrator dostępu użytkowników. odpowiedź Hello powinien wyglądać następująco:

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    Zapisz hello identyfikatora GUID z hello *nazwa* parametru, w tym przypadku **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Wywołanie [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) gdzie principalId = własne ObjectId. Ta lista zawiera wszystkie przypisaniami w dzierżawie powitalnych. Wyszukaj hello, co gdzie jest zakres hello "/" i kończy się RoleDefinitionId hello roli hello nazwy identyfikatora GUID można znaleźć w kroku 1. Przypisanie roli Hello powinien wyglądać następująco:

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    Ponownie zapisać hello identyfikatora GUID z hello *nazwa* parametru, w tym przypadku **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Na koniec wywołania [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) gdzie roleAssignmentId = nazwa hello GUID można znaleźć w kroku 2.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [zarządzania opartego na rolach kontrola dostępu przy użyciu REST](role-based-access-control-manage-access-rest.md)

- [Zarządzanie przypisaniami dostępu](role-based-access-control-manage-assignments.md) w hello portalu Azure
