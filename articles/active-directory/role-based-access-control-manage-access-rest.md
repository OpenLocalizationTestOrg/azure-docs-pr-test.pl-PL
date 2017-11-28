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
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="4dbe3-103">Zarządzanie oparte na rolach kontrola dostępu przy użyciu hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="4dbe3-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4dbe3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dbe3-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="4dbe3-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4dbe3-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="4dbe3-106">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="4dbe3-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="4dbe3-107">Oparta na rolach kontroli dostępu (RBAC) w hello portalu Azure i interfejsu API usługi Azure Resource Manager ułatwia zarządzanie subskrypcji tooyour dostępu i zasobów na poziomie szczegółowych.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="4dbe3-108">W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując toothem niektórych ról w określonym zakresie.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="4dbe3-109">Wyświetl listę wszystkich przypisań ról</span><span class="sxs-lookup"><span data-stu-id="4dbe3-109">List all role assignments</span></span>
<span data-ttu-id="4dbe3-110">Wyświetla wszystkie przypisania roli hello na powitania określony zakres i subscopes.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="4dbe3-111">przypisania ról toolist, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleAssignments/read` operacji w zakresie hello.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="4dbe3-112">Wszystkie role wbudowane hello udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-113">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-114">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-114">Request</span></span>
<span data-ttu-id="4dbe3-115">Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="4dbe3-116">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-117">Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="4dbe3-118">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-119">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-120">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-121">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-122">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="4dbe3-123">Zastąp *{filtru}* z warunkiem hello, że chcesz Lista przypisywanie roli tooapply toofilter hello:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="4dbe3-124">Listę przypisań ról hello tylko określony zakres, nie włączając hello przypisania ról na subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="4dbe3-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="4dbe3-125">Utwórz listę przypisań ról dla określonego użytkownika, grupy lub aplikacji.`principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="4dbe3-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="4dbe3-126">Lista przypisań ról określonego użytkownika, między innymi dziedziczone z grup |`assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="4dbe3-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="4dbe3-127">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-127">Response</span></span>
<span data-ttu-id="4dbe3-128">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="4dbe3-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="4dbe3-129">Pobierz informacje o przypisaniu roli</span><span class="sxs-lookup"><span data-stu-id="4dbe3-129">Get information about a role assignment</span></span>
<span data-ttu-id="4dbe3-130">Pobiera informacje o przypisaniu roli jednej, określonej przez identyfikator przypisania roli hello.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="4dbe3-131">tooget informacje o przypisaniu roli, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleAssignments/read` operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="4dbe3-132">Wszystkie role wbudowane hello udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-133">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-134">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-134">Request</span></span>
<span data-ttu-id="4dbe3-135">Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="4dbe3-136">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-137">Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="4dbe3-138">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-139">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-140">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-141">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-142">Zastąp *{— identyfikator przypisania roli-}* o identyfikatorze GUID hello hello przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="4dbe3-143">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="4dbe3-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-144">Response</span></span>
<span data-ttu-id="4dbe3-145">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="4dbe3-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="4dbe3-146">Tworzy przypisanie roli</span><span class="sxs-lookup"><span data-stu-id="4dbe3-146">Create a Role Assignment</span></span>
<span data-ttu-id="4dbe3-147">Tworzenie roli przydziału na powitania określony zakres hello określić głównej udzielającym hello rolę określoną w programie.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="4dbe3-148">toocreate przypisania roli, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleAssignments/write` operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="4dbe3-149">Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-150">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-151">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-151">Request</span></span>
<span data-ttu-id="4dbe3-152">Użyj hello **PUT** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="4dbe3-153">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-154">Zastąp *{zakresu}* z zakresem hello, w którym chcesz toocreate hello przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="4dbe3-155">Po utworzeniu przypisanie roli w zakresie nadrzędnym, wszystkie zakresy podrzędne dziedziczą hello tego samego przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="4dbe3-156">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-157">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-158">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="4dbe3-159">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-160">Zastąp *{— identyfikator przypisania roli-}* za pomocą nowego identyfikatora GUID, który staje się identyfikator GUID hello hello nowe przypisanie roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="4dbe3-161">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="4dbe3-162">Treść żądania hello Podaj wartości hello w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="4dbe3-163">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="4dbe3-163">Element Name</span></span> | <span data-ttu-id="4dbe3-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4dbe3-164">Required</span></span> | <span data-ttu-id="4dbe3-165">Typ</span><span class="sxs-lookup"><span data-stu-id="4dbe3-165">Type</span></span> | <span data-ttu-id="4dbe3-166">Opis</span><span class="sxs-lookup"><span data-stu-id="4dbe3-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4dbe3-167">wartość roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="4dbe3-167">roleDefinitionId</span></span> |<span data-ttu-id="4dbe3-168">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-168">Yes</span></span> |<span data-ttu-id="4dbe3-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-169">String</span></span> |<span data-ttu-id="4dbe3-170">Identyfikator Hello hello roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-170">hello identifier of hello role.</span></span> <span data-ttu-id="4dbe3-171">format identyfikatora hello Hello jest:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="4dbe3-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="4dbe3-172">principalId</span><span class="sxs-lookup"><span data-stu-id="4dbe3-172">principalId</span></span> |<span data-ttu-id="4dbe3-173">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-173">Yes</span></span> |<span data-ttu-id="4dbe3-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-174">String</span></span> |<span data-ttu-id="4dbe3-175">Identyfikator obiektu podmiotu hello Azure AD (użytkownika, grupy lub nazwy głównej usługi) toowhich hello rola jest przypisywana.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="4dbe3-176">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-176">Response</span></span>
<span data-ttu-id="4dbe3-177">Kod stanu: 201</span><span class="sxs-lookup"><span data-stu-id="4dbe3-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="4dbe3-178">Usuwa przypisanie roli</span><span class="sxs-lookup"><span data-stu-id="4dbe3-178">Delete a Role Assignment</span></span>
<span data-ttu-id="4dbe3-179">Usuń przypisanie roli w hello określony zakres.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="4dbe3-180">toodelete przypisania roli musi mieć dostęp do toohello `Microsoft.Authorization/roleAssignments/delete` operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="4dbe3-181">Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-182">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-183">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-183">Request</span></span>
<span data-ttu-id="4dbe3-184">Użyj hello **usunąć** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="4dbe3-185">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-186">Zastąp *{zakresu}* z zakresem hello, w którym chcesz toocreate hello przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="4dbe3-187">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-188">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-189">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-190">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-191">Zastąp *{— identyfikator przypisania roli-}* z identyfikator przypisania roli hello identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="4dbe3-192">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="4dbe3-193">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-193">Response</span></span>
<span data-ttu-id="4dbe3-194">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="4dbe3-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="4dbe3-195">Wyświetl listę wszystkich ról</span><span class="sxs-lookup"><span data-stu-id="4dbe3-195">List all Roles</span></span>
<span data-ttu-id="4dbe3-196">Wyświetla wszystkie role hello, które są dostępne do przypisania w hello określony zakres.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="4dbe3-197">toolist ról, należy mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/read` operacji w zakresie hello.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="4dbe3-198">Wszystkie role wbudowane hello udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-199">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-200">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-200">Request</span></span>
<span data-ttu-id="4dbe3-201">Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="4dbe3-202">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-203">Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello ról.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="4dbe3-204">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-205">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-206">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-207">/Subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1 zasobów</span><span class="sxs-lookup"><span data-stu-id="4dbe3-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-208">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="4dbe3-209">Zastąp *{filtru}* z hello warunkiem, że chcesz tooapply toofilter hello lista ról:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="4dbe3-210">Lista ról dostępne do przypisania na powitania określony zakres oraz wszystkie jego zakresy podrzędne:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="4dbe3-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="4dbe3-211">Wyszukaj rolę przy użyciu nazwy wyświetlanej dokładne: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="4dbe3-212">Formularz hello zakodowane w adresie URL nazwy wyświetlanej dokładne hello hello roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="4dbe3-213">Na przykład`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="4dbe3-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="4dbe3-214">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-214">Response</span></span>
<span data-ttu-id="4dbe3-215">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="4dbe3-215">Status code: 200</span></span>

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

## <a name="get-information-about-a-role"></a><span data-ttu-id="4dbe3-216">Uzyskiwanie informacji o roli</span><span class="sxs-lookup"><span data-stu-id="4dbe3-216">Get information about a Role</span></span>
<span data-ttu-id="4dbe3-217">Pobiera informacje o określonej przez identyfikator definicji roli hello jedną rolę.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="4dbe3-218">tooget informacji o pojedynczej roli przy użyciu nazwy wyświetlanej, zobacz [listy wszystkich ról](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="4dbe3-219">tooget informacji na temat roli, trzeba mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/read` operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="4dbe3-220">Wszystkie role wbudowane hello udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-221">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-222">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-222">Request</span></span>
<span data-ttu-id="4dbe3-223">Użyj hello **UZYSKAĆ** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="4dbe3-224">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-225">Zastąp *{zakresu}* z zakresem hello, dla którego chcesz toolist hello przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="4dbe3-226">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-227">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-228">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-229">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-230">Zastąp *{— identyfikator definicji roli-}* o identyfikatorze GUID hello hello definicji roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="4dbe3-231">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="4dbe3-232">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-232">Response</span></span>
<span data-ttu-id="4dbe3-233">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="4dbe3-233">Status code: 200</span></span>

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

## <a name="create-a-custom-role"></a><span data-ttu-id="4dbe3-234">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="4dbe3-234">Create a Custom Role</span></span>
<span data-ttu-id="4dbe3-235">Tworzenie niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-235">Create a custom role.</span></span>

<span data-ttu-id="4dbe3-236">toocreate rolę niestandardową, musisz mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/write` operację na wszystkich hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="4dbe3-237">Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-238">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-239">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-239">Request</span></span>
<span data-ttu-id="4dbe3-240">Użyj hello **PUT** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="4dbe3-241">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-242">Zastąp *{zakresu}* z hello pierwszy *AssignableScope* hello niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="4dbe3-243">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="4dbe3-244">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-245">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-246">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-247">Zastąp *{— identyfikator definicji roli-}* za pomocą nowego identyfikatora GUID, który staje się identyfikator GUID hello hello nowej niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="4dbe3-248">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="4dbe3-249">Treść żądania hello Podaj wartości hello w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-249">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="4dbe3-250">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="4dbe3-250">Element Name</span></span> | <span data-ttu-id="4dbe3-251">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4dbe3-251">Required</span></span> | <span data-ttu-id="4dbe3-252">Typ</span><span class="sxs-lookup"><span data-stu-id="4dbe3-252">Type</span></span> | <span data-ttu-id="4dbe3-253">Opis</span><span class="sxs-lookup"><span data-stu-id="4dbe3-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4dbe3-254">name</span><span class="sxs-lookup"><span data-stu-id="4dbe3-254">name</span></span> |<span data-ttu-id="4dbe3-255">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-255">Yes</span></span> |<span data-ttu-id="4dbe3-256">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-256">String</span></span> |<span data-ttu-id="4dbe3-257">Identyfikator GUID hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="4dbe3-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="4dbe3-258">properties.roleName</span></span> |<span data-ttu-id="4dbe3-259">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-259">Yes</span></span> |<span data-ttu-id="4dbe3-260">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-260">String</span></span> |<span data-ttu-id="4dbe3-261">Nazwa wyświetlana hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-261">Display name of hello custom role.</span></span> <span data-ttu-id="4dbe3-262">Maksymalny rozmiar 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="4dbe3-263">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="4dbe3-263">properties.description</span></span> |<span data-ttu-id="4dbe3-264">Nie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-264">No</span></span> |<span data-ttu-id="4dbe3-265">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-265">String</span></span> |<span data-ttu-id="4dbe3-266">Opis roli niestandardowej hello.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-266">Description of hello custom role.</span></span> <span data-ttu-id="4dbe3-267">Maksymalny rozmiar 1024 znaki.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="4dbe3-268">Properties.Type</span><span class="sxs-lookup"><span data-stu-id="4dbe3-268">properties.type</span></span> |<span data-ttu-id="4dbe3-269">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-269">Yes</span></span> |<span data-ttu-id="4dbe3-270">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-270">String</span></span> |<span data-ttu-id="4dbe3-271">Ustaw zbyt "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="4dbe3-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="4dbe3-272">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="4dbe3-272">properties.permissions.actions</span></span> |<span data-ttu-id="4dbe3-273">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-273">Yes</span></span> |<span data-ttu-id="4dbe3-274">ciąg]</span><span class="sxs-lookup"><span data-stu-id="4dbe3-274">String[]</span></span> |<span data-ttu-id="4dbe3-275">Tablica akcji ciągi określania operacji hello przyznane przez hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="4dbe3-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="4dbe3-276">properties.permissions.notActions</span></span> |<span data-ttu-id="4dbe3-277">Nie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-277">No</span></span> |<span data-ttu-id="4dbe3-278">ciąg]</span><span class="sxs-lookup"><span data-stu-id="4dbe3-278">String[]</span></span> |<span data-ttu-id="4dbe3-279">Tablica ciągów akcji Określanie hello tooexclude operacje z operacji hello przyznane przez hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="4dbe3-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="4dbe3-280">properties.assignableScopes</span></span> |<span data-ttu-id="4dbe3-281">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-281">Yes</span></span> |<span data-ttu-id="4dbe3-282">ciąg]</span><span class="sxs-lookup"><span data-stu-id="4dbe3-282">String[]</span></span> |<span data-ttu-id="4dbe3-283">Tablica zakresów, w których hello można użyć niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="4dbe3-284">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-284">Response</span></span>
<span data-ttu-id="4dbe3-285">Kod stanu: 201</span><span class="sxs-lookup"><span data-stu-id="4dbe3-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="4dbe3-286">Aktualizacja niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="4dbe3-286">Update a Custom Role</span></span>
<span data-ttu-id="4dbe3-287">Zmodyfikuj niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-287">Modify a custom role.</span></span>

<span data-ttu-id="4dbe3-288">toomodify rolę niestandardową, musisz mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/write` operację na wszystkich hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="4dbe3-289">Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-290">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-291">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-291">Request</span></span>
<span data-ttu-id="4dbe3-292">Użyj hello **PUT** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="4dbe3-293">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-294">Zastąp *{zakresu}* z hello pierwszy *AssignableScope* hello niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="4dbe3-295">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-296">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-297">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-298">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-299">Zastąp *{— identyfikator definicji roli-}* z identyfikator GUID hello hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="4dbe3-300">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="4dbe3-301">Treść żądania hello Podaj wartości hello w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-301">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="4dbe3-302">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="4dbe3-302">Element Name</span></span> | <span data-ttu-id="4dbe3-303">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4dbe3-303">Required</span></span> | <span data-ttu-id="4dbe3-304">Typ</span><span class="sxs-lookup"><span data-stu-id="4dbe3-304">Type</span></span> | <span data-ttu-id="4dbe3-305">Opis</span><span class="sxs-lookup"><span data-stu-id="4dbe3-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4dbe3-306">name</span><span class="sxs-lookup"><span data-stu-id="4dbe3-306">name</span></span> |<span data-ttu-id="4dbe3-307">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-307">Yes</span></span> |<span data-ttu-id="4dbe3-308">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-308">String</span></span> |<span data-ttu-id="4dbe3-309">Identyfikator GUID hello niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="4dbe3-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="4dbe3-310">properties.roleName</span></span> |<span data-ttu-id="4dbe3-311">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-311">Yes</span></span> |<span data-ttu-id="4dbe3-312">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-312">String</span></span> |<span data-ttu-id="4dbe3-313">Nazwa wyświetlana hello zaktualizować niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="4dbe3-314">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="4dbe3-314">properties.description</span></span> |<span data-ttu-id="4dbe3-315">Nie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-315">No</span></span> |<span data-ttu-id="4dbe3-316">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-316">String</span></span> |<span data-ttu-id="4dbe3-317">Opis hello zaktualizować niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="4dbe3-318">Properties.Type</span><span class="sxs-lookup"><span data-stu-id="4dbe3-318">properties.type</span></span> |<span data-ttu-id="4dbe3-319">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-319">Yes</span></span> |<span data-ttu-id="4dbe3-320">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4dbe3-320">String</span></span> |<span data-ttu-id="4dbe3-321">Ustaw zbyt "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="4dbe3-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="4dbe3-322">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="4dbe3-322">properties.permissions.actions</span></span> |<span data-ttu-id="4dbe3-323">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-323">Yes</span></span> |<span data-ttu-id="4dbe3-324">ciąg]</span><span class="sxs-lookup"><span data-stu-id="4dbe3-324">String[]</span></span> |<span data-ttu-id="4dbe3-325">Tablica ciągów akcji Określanie hello operacji toowhich hello zaktualizować niestandardowej roli zabezpieczeń przyznaje dostęp.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="4dbe3-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="4dbe3-326">properties.permissions.notActions</span></span> |<span data-ttu-id="4dbe3-327">Nie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-327">No</span></span> |<span data-ttu-id="4dbe3-328">ciąg]</span><span class="sxs-lookup"><span data-stu-id="4dbe3-328">String[]</span></span> |<span data-ttu-id="4dbe3-329">Tablica akcji ciągi określania tooexclude operacji hello z operacji hello które hello zaktualizowane przyznaje niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="4dbe3-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="4dbe3-330">properties.assignableScopes</span></span> |<span data-ttu-id="4dbe3-331">Tak</span><span class="sxs-lookup"><span data-stu-id="4dbe3-331">Yes</span></span> |<span data-ttu-id="4dbe3-332">ciąg]</span><span class="sxs-lookup"><span data-stu-id="4dbe3-332">String[]</span></span> |<span data-ttu-id="4dbe3-333">Tablica zakresów, w których hello zaktualizowane niestandardowej roli zabezpieczeń mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="4dbe3-334">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-334">Response</span></span>
<span data-ttu-id="4dbe3-335">Kod stanu: 201</span><span class="sxs-lookup"><span data-stu-id="4dbe3-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="4dbe3-336">Usunięcia niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="4dbe3-336">Delete a Custom Role</span></span>
<span data-ttu-id="4dbe3-337">Usunięcia niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-337">Delete a custom role.</span></span>

<span data-ttu-id="4dbe3-338">toodelete rolę niestandardową, musisz mieć dostęp zbyt`Microsoft.Authorization/roleDefinitions/delete` operację na wszystkich hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="4dbe3-339">Witaj wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielono dostępu toothis operacji.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="4dbe3-340">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4dbe3-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="4dbe3-341">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4dbe3-341">Request</span></span>
<span data-ttu-id="4dbe3-342">Użyj hello **usunąć** metody z hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="4dbe3-343">W ramach hello identyfikatora URI należy powitania po toocustomize podstawień żądania:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="4dbe3-344">Zastąp *{zakresu}* z zakresem hello, w którym chcesz definicji roli hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="4dbe3-345">Hello następujące przykłady przedstawiają sposób toospecify hello zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="4dbe3-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="4dbe3-346">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="4dbe3-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="4dbe3-347">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="4dbe3-348">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="4dbe3-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="4dbe3-349">Zastąp *{— identyfikator definicji roli-}* z identyfikator definicji roli identyfikatora GUID hello hello niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="4dbe3-350">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="4dbe3-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="4dbe3-351">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4dbe3-351">Response</span></span>
<span data-ttu-id="4dbe3-352">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="4dbe3-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4dbe3-353">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4dbe3-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
