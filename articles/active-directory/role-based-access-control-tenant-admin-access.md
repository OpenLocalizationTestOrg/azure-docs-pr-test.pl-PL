---
title: "Administrator dzierżawy podniesienie uprawnień dostępu — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano wbudowanych ról dla kontroli dostępu opartej na rolach (RBAC)."
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
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="7b2fa-103">Podniesienie uprawnień dostępu jako Administrator dzierżawy przy użyciu kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="7b2fa-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="7b2fa-104">Oparta na rolach kontrola dostępu ułatwia administratorom dzierżawy uzyskiwania wybierającym tymczasowe w programie access, przyznają uprawnienia wyższe niż zwykle.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="7b2fa-105">Administrator dzierżawy może podnieść poziom siebie do roli Administrator dostępu użytkowników w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="7b2fa-106">Ta rola zapewnia dzierżawcy uprawnienia administratora, aby przydzielić sobie lub innych ról w zakresie "/".</span><span class="sxs-lookup"><span data-stu-id="7b2fa-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="7b2fa-107">Ta funkcja jest ważna, ponieważ zezwala ona na administratora dzierżawy wyświetlić wszystkie subskrypcje, które istnieją w organizacji.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="7b2fa-108">Umożliwia on również automatyzacji aplikacji (takich jak fakturowania i inspekcji) dostęp do wszystkich subskrypcji i podaj dokładnego widoku stanu zarządzania rozliczeń lub zasobów organizacji.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="7b2fa-109">Jak używać elevateAccess do udostępnienia dzierżawy</span><span class="sxs-lookup"><span data-stu-id="7b2fa-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="7b2fa-110">Podstawowy proces działa z następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="7b2fa-111">Za pomocą usługi REST, wywołaj *elevateAccess*, która udziela roli Administrator dostępu użytkowników na "/" zakres.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="7b2fa-112">Utwórz [przypisania roli](/rest/api/authorization/roleassignments) można przypisać żadnej roli w dowolnym zakresie.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="7b2fa-113">Poniższy przykład przedstawia właściwości przypisywanie roli czytnika w "/" zakres:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="7b2fa-114">Podczas administratorem dostępu użytkownika użytkownik może również usunąć przypisania roli w "/" zakres.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="7b2fa-115">Odwołaj Twoje uprawnienia administratora dostępu użytkownika, dopóki nie są potrzebne, ponownie.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="7b2fa-116">Jak cofnąć elevateAccess</span><span class="sxs-lookup"><span data-stu-id="7b2fa-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="7b2fa-117">Podczas wywoływania *elevateAccess* Tworzenie przypisania roli dla siebie, tak aby można było odwołać uprawnienia te należy usunąć przypisanie.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="7b2fa-118">Wywołanie [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) gdzie roleName = Administrator dostępu użytkowników można określić nazwy roli Administrator dostępu użytkowników identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="7b2fa-119">Odpowiedź powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
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

    <span data-ttu-id="7b2fa-120">Zapisz identyfikator GUID z *nazwa* parametru, w tym przypadku **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="7b2fa-121">Wywołanie [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) gdzie principalId = własne ObjectId.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="7b2fa-122">Ta lista zawiera wszystkie przypisaniami w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="7b2fa-123">Wyszukaj co gdzie jest zakresem "/" i RoleDefinitionId kończy nazwę roli GUID można znaleźć w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="7b2fa-124">Przypisanie roli powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-124">The role assignment should look like this:</span></span>

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

    <span data-ttu-id="7b2fa-125">Ponownie, Zapisz identyfikator GUID z *nazwa* parametru, w tym przypadku **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="7b2fa-126">Na koniec wywołania [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) gdzie roleAssignmentId = nazwa identyfikatora GUID można znaleźć w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b2fa-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b2fa-127">Next steps</span></span>

- <span data-ttu-id="7b2fa-128">Dowiedz się więcej o [zarządzania opartego na rolach kontrola dostępu przy użyciu REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="7b2fa-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="7b2fa-129">[Zarządzanie przypisaniami dostępu](role-based-access-control-manage-assignments.md) w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7b2fa-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
