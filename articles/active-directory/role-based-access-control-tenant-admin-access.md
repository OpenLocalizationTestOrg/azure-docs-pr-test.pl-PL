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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="4d9b2-103">Podniesienie uprawnień dostępu jako Administrator dzierżawy przy użyciu kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="4d9b2-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="4d9b2-104">Oparta na rolach kontrola dostępu ułatwia administratorom dzierżawy uzyskiwania wybierającym tymczasowe w programie access, przyznają uprawnienia wyższe niż zwykle.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="4d9b2-105">Administrator dzierżawy podnieść poziom sobie toohello roli Administrator dostępu użytkowników, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="4d9b2-106">Ta rola zapewnia hello toogrant uprawnień administratora dzierżawy, siebie lub innych ról na powitania zakresu "/".</span><span class="sxs-lookup"><span data-stu-id="4d9b2-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="4d9b2-107">Ta funkcja jest ważna, ponieważ umożliwia dzierżawy hello toosee admin hello wszystkie subskrypcje, które istnieją w organizacji.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="4d9b2-108">Również umożliwia automatyzacji aplikacji (takich jak fakturowania i inspekcji) tooaccess wszystkie subskrypcje hello i podaj dokładnego widoku stanu hello hello organizacji w celu zarządzania rozliczeń lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="4d9b2-109">Jak toouse elevateAccess toogive dzierżawy dostępu</span><span class="sxs-lookup"><span data-stu-id="4d9b2-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="4d9b2-110">Witaj podstawowy proces działa z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4d9b2-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="4d9b2-111">Za pomocą usługi REST, wywołaj *elevateAccess*, który przyznaje możesz hello roli Administrator dostępu użytkowników na "/" zakres.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="4d9b2-112">Utwórz [przypisania roli](/rest/api/authorization/roleassignments) tooassign żadnej roli w dowolnym zakresie.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="4d9b2-113">Witaj poniższy przykład przedstawia właściwości hello przypisywania hello rolę czytelnika w "/" zakres:</span><span class="sxs-lookup"><span data-stu-id="4d9b2-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="4d9b2-114">Podczas administratorem dostępu użytkownika użytkownik może również usunąć przypisania roli w "/" zakres.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="4d9b2-115">Odwołaj Twoje uprawnienia administratora dostępu użytkownika, dopóki nie są potrzebne, ponownie.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="4d9b2-116">Jak tooundo hello elevateAccess akcji</span><span class="sxs-lookup"><span data-stu-id="4d9b2-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="4d9b2-117">Podczas wywoływania *elevateAccess* utworzyć przypisania roli dla siebie, więc toorevoke te uprawnienia możesz muszą toodelete hello przypisania.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="4d9b2-118">Wywołanie [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) gdzie roleName = nazwa hello Administrator dostępu użytkowników toodetermine identyfikator GUID hello roli Administrator dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="4d9b2-119">odpowiedź Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4d9b2-119">hello response should look like this:</span></span>

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

    <span data-ttu-id="4d9b2-120">Zapisz hello identyfikatora GUID z hello *nazwa* parametru, w tym przypadku **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="4d9b2-121">Wywołanie [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) gdzie principalId = własne ObjectId.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="4d9b2-122">Ta lista zawiera wszystkie przypisaniami w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="4d9b2-123">Wyszukaj hello, co gdzie jest zakres hello "/" i kończy się RoleDefinitionId hello roli hello nazwy identyfikatora GUID można znaleźć w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="4d9b2-124">Przypisanie roli Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4d9b2-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="4d9b2-125">Ponownie zapisać hello identyfikatora GUID z hello *nazwa* parametru, w tym przypadku **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="4d9b2-126">Na koniec wywołania [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) gdzie roleAssignmentId = nazwa hello GUID można znaleźć w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="4d9b2-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d9b2-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d9b2-127">Next steps</span></span>

- <span data-ttu-id="4d9b2-128">Dowiedz się więcej o [zarządzania opartego na rolach kontrola dostępu przy użyciu REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="4d9b2-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="4d9b2-129">[Zarządzanie przypisaniami dostępu](role-based-access-control-manage-assignments.md) w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4d9b2-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
