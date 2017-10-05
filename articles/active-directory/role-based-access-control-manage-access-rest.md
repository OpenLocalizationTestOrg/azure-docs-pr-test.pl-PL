---
title: "Kontrola dostępu oparta na rolach przy użyciu REST - usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zarządzanie kontrolą dostępu opartej na rolach przy użyciu interfejsu API REST"
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
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="e5f5c-103">Zarządzanie kontrolą dostępu opartej na rolach przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="e5f5c-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5f5c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5f5c-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="e5f5c-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5f5c-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="e5f5c-106">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="e5f5c-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="e5f5c-107">Opartej na rolach kontroli dostępu (RBAC) w portalu Azure i interfejsu API usługi Azure Resource Manager ułatwia zarządzanie dostępem do Twojej subskrypcji i zasobów na poziomie szczegółowych.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="e5f5c-108">W przypadku tej funkcji mogą udzielać dostępu dla użytkowników, grupy lub podmiotów zabezpieczeń usługi Active Directory, przypisując niektóre role do ich w określonym zakresie.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="e5f5c-109">Wyświetl listę wszystkich przypisań ról</span><span class="sxs-lookup"><span data-stu-id="e5f5c-109">List all role assignments</span></span>
<span data-ttu-id="e5f5c-110">Wyświetla listę wszystkich przypisań ról w określonym zakresie i subscopes.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="e5f5c-111">Na liście przypisań ról musi mieć dostęp do `Microsoft.Authorization/roleAssignments/read` operacji w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="e5f5c-112">Wbudowane role mają dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-113">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-114">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-114">Request</span></span>
<span data-ttu-id="e5f5c-115">Użyj **UZYSKAĆ** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="e5f5c-116">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-117">Zastąp *{zakresu}* z zakresem, dla którego chcesz wyświetlić listę przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="e5f5c-118">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-119">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-120">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-121">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-122">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="e5f5c-123">Zastąp *{filtru}* warunek, który chcesz zastosować, aby filtrować listę przypisania roli:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="e5f5c-124">Wyświetl listę przypisań ról tylko określony zakres, z wyłączeniem przypisania ról na subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="e5f5c-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="e5f5c-125">Utwórz listę przypisań ról dla określonego użytkownika, grupy lub aplikacji.`principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="e5f5c-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="e5f5c-126">Lista przypisań ról określonego użytkownika, między innymi dziedziczone z grup |`assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="e5f5c-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="e5f5c-127">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-127">Response</span></span>
<span data-ttu-id="e5f5c-128">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="e5f5c-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="e5f5c-129">Pobierz informacje o przypisaniu roli</span><span class="sxs-lookup"><span data-stu-id="e5f5c-129">Get information about a role assignment</span></span>
<span data-ttu-id="e5f5c-130">Pobiera informacje o przypisaniu roli jednej, określonej przez identyfikator przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="e5f5c-131">Aby uzyskać informacje o przypisaniu roli, musi mieć dostęp do `Microsoft.Authorization/roleAssignments/read` operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="e5f5c-132">Wbudowane role mają dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-133">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-134">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-134">Request</span></span>
<span data-ttu-id="e5f5c-135">Użyj **UZYSKAĆ** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="e5f5c-136">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-137">Zastąp *{zakresu}* z zakresem, dla którego chcesz wyświetlić listę przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="e5f5c-138">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-139">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-140">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-141">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-142">Zastąp *{— identyfikator przypisania roli-}* o identyfikatorze GUID przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="e5f5c-143">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e5f5c-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-144">Response</span></span>
<span data-ttu-id="e5f5c-145">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="e5f5c-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="e5f5c-146">Tworzy przypisanie roli</span><span class="sxs-lookup"><span data-stu-id="e5f5c-146">Create a Role Assignment</span></span>
<span data-ttu-id="e5f5c-147">Tworzy przypisanie roli w podanym zakresie dla określonego podmiotu zabezpieczeń udzielanie określonej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="e5f5c-148">Aby utworzyć przypisanie roli, musi mieć dostęp do `Microsoft.Authorization/roleAssignments/write` operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="e5f5c-149">Wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielany jest dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-150">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-151">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-151">Request</span></span>
<span data-ttu-id="e5f5c-152">Użyj **PUT** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="e5f5c-153">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-154">Zastąp *{zakresu}* w zakresie, w którym chcesz utworzyć przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="e5f5c-155">Po utworzeniu przypisanie roli w zakresie nadrzędnym, wszystkie zakresy podrzędne dziedziczą tego samego przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="e5f5c-156">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-157">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-158">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="e5f5c-159">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-160">Zastąp *{— identyfikator przypisania roli-}* za pomocą nowego identyfikatora GUID, który staje się identyfikator GUID nowe przypisanie roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="e5f5c-161">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="e5f5c-162">Treść żądania Podaj wartości w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="e5f5c-163">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="e5f5c-163">Element Name</span></span> | <span data-ttu-id="e5f5c-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5f5c-164">Required</span></span> | <span data-ttu-id="e5f5c-165">Typ</span><span class="sxs-lookup"><span data-stu-id="e5f5c-165">Type</span></span> | <span data-ttu-id="e5f5c-166">Opis</span><span class="sxs-lookup"><span data-stu-id="e5f5c-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5f5c-167">wartość roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="e5f5c-167">roleDefinitionId</span></span> |<span data-ttu-id="e5f5c-168">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-168">Yes</span></span> |<span data-ttu-id="e5f5c-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-169">String</span></span> |<span data-ttu-id="e5f5c-170">Identyfikator roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-170">The identifier of the role.</span></span> <span data-ttu-id="e5f5c-171">Format identyfikatora jest:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="e5f5c-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="e5f5c-172">principalId</span><span class="sxs-lookup"><span data-stu-id="e5f5c-172">principalId</span></span> |<span data-ttu-id="e5f5c-173">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-173">Yes</span></span> |<span data-ttu-id="e5f5c-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-174">String</span></span> |<span data-ttu-id="e5f5c-175">Identyfikator obiektu głównego usługi Azure AD (użytkownika, grupy lub nazwy głównej usługi), do której przypisano rolę.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="e5f5c-176">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-176">Response</span></span>
<span data-ttu-id="e5f5c-177">Kod stanu: 201</span><span class="sxs-lookup"><span data-stu-id="e5f5c-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="e5f5c-178">Usuwa przypisanie roli</span><span class="sxs-lookup"><span data-stu-id="e5f5c-178">Delete a Role Assignment</span></span>
<span data-ttu-id="e5f5c-179">Usuwa przypisanie roli w podanym zakresie.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="e5f5c-180">Aby usunąć przypisanie roli, musi mieć dostęp do `Microsoft.Authorization/roleAssignments/delete` operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="e5f5c-181">Wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielany jest dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-182">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-183">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-183">Request</span></span>
<span data-ttu-id="e5f5c-184">Użyj **usunąć** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="e5f5c-185">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-186">Zastąp *{zakresu}* w zakresie, w którym chcesz utworzyć przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="e5f5c-187">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-188">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-189">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-190">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-191">Zastąp *{— identyfikator przypisania roli-}* o identyfikatorze GUID przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="e5f5c-192">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e5f5c-193">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-193">Response</span></span>
<span data-ttu-id="e5f5c-194">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="e5f5c-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="e5f5c-195">Wyświetl listę wszystkich ról</span><span class="sxs-lookup"><span data-stu-id="e5f5c-195">List all Roles</span></span>
<span data-ttu-id="e5f5c-196">Wyświetla wszystkie role, które są dostępne do przypisania w podanym zakresie.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="e5f5c-197">Do listy ról musi mieć dostęp do `Microsoft.Authorization/roleDefinitions/read` operacji w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="e5f5c-198">Wbudowane role mają dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-199">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-200">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-200">Request</span></span>
<span data-ttu-id="e5f5c-201">Użyj **UZYSKAĆ** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="e5f5c-202">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-203">Zastąp *{zakresu}* z zakresem, dla którego chcesz wyświetlić listę ról.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="e5f5c-204">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-205">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-206">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-207">/Subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1 zasobów</span><span class="sxs-lookup"><span data-stu-id="e5f5c-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-208">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="e5f5c-209">Zastąp *{filtru}* warunek, który chcesz zastosować, aby filtrować listę ról:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="e5f5c-210">Lista ról dostępne do przypisania w określonym zakresie i w żadnym z jego zakresy podrzędne:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="e5f5c-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="e5f5c-211">Wyszukaj rolę przy użyciu nazwy wyświetlanej dokładne: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="e5f5c-212">Formularz zakodowane w adresie URL nazwę wyświetlaną dokładne roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="e5f5c-213">Na przykład`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="e5f5c-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="e5f5c-214">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-214">Response</span></span>
<span data-ttu-id="e5f5c-215">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="e5f5c-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="e5f5c-216">Uzyskiwanie informacji o roli</span><span class="sxs-lookup"><span data-stu-id="e5f5c-216">Get information about a Role</span></span>
<span data-ttu-id="e5f5c-217">Pobiera informacje o pojedynczej roli określonej przez identyfikator definicji roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="e5f5c-218">Aby uzyskać informacje o pojedynczej roli przy użyciu nazwy wyświetlanej, zobacz [listy wszystkich ról](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="e5f5c-219">Aby uzyskać informacje o roli, musi mieć dostęp do `Microsoft.Authorization/roleDefinitions/read` operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="e5f5c-220">Wbudowane role mają dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-221">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-222">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-222">Request</span></span>
<span data-ttu-id="e5f5c-223">Użyj **UZYSKAĆ** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e5f5c-224">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-225">Zastąp *{zakresu}* z zakresem, dla którego chcesz wyświetlić listę przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="e5f5c-226">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-227">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-228">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-229">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-230">Zastąp *{— identyfikator definicji roli-}* o identyfikatorze GUID definicji roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="e5f5c-231">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e5f5c-232">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-232">Response</span></span>
<span data-ttu-id="e5f5c-233">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="e5f5c-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="e5f5c-234">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e5f5c-234">Create a Custom Role</span></span>
<span data-ttu-id="e5f5c-235">Tworzenie niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-235">Create a custom role.</span></span>

<span data-ttu-id="e5f5c-236">Aby utworzyć niestandardową rolę, musi mieć dostęp do `Microsoft.Authorization/roleDefinitions/write` operację na wszystkich `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="e5f5c-237">Wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielany jest dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-238">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-239">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-239">Request</span></span>
<span data-ttu-id="e5f5c-240">Użyj **PUT** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e5f5c-241">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-242">Zastąp *{zakresu}* przy pierwszym *AssignableScope* niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="e5f5c-243">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="e5f5c-244">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-245">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-246">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-247">Zastąp *{— identyfikator definicji roli-}* za pomocą nowego identyfikatora GUID, który staje się identyfikator GUID nowej niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="e5f5c-248">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="e5f5c-249">Treść żądania Podaj wartości w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-249">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="e5f5c-250">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="e5f5c-250">Element Name</span></span> | <span data-ttu-id="e5f5c-251">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5f5c-251">Required</span></span> | <span data-ttu-id="e5f5c-252">Typ</span><span class="sxs-lookup"><span data-stu-id="e5f5c-252">Type</span></span> | <span data-ttu-id="e5f5c-253">Opis</span><span class="sxs-lookup"><span data-stu-id="e5f5c-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5f5c-254">name</span><span class="sxs-lookup"><span data-stu-id="e5f5c-254">name</span></span> |<span data-ttu-id="e5f5c-255">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-255">Yes</span></span> |<span data-ttu-id="e5f5c-256">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-256">String</span></span> |<span data-ttu-id="e5f5c-257">Identyfikator GUID tworzona rola niestandardowa.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="e5f5c-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="e5f5c-258">properties.roleName</span></span> |<span data-ttu-id="e5f5c-259">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-259">Yes</span></span> |<span data-ttu-id="e5f5c-260">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-260">String</span></span> |<span data-ttu-id="e5f5c-261">Tworzona rola niestandardowa nazwa wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-261">Display name of the custom role.</span></span> <span data-ttu-id="e5f5c-262">Maksymalny rozmiar 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="e5f5c-263">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="e5f5c-263">properties.description</span></span> |<span data-ttu-id="e5f5c-264">Nie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-264">No</span></span> |<span data-ttu-id="e5f5c-265">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-265">String</span></span> |<span data-ttu-id="e5f5c-266">Opis roli niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-266">Description of the custom role.</span></span> <span data-ttu-id="e5f5c-267">Maksymalny rozmiar 1024 znaki.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="e5f5c-268">Properties.Type</span><span class="sxs-lookup"><span data-stu-id="e5f5c-268">properties.type</span></span> |<span data-ttu-id="e5f5c-269">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-269">Yes</span></span> |<span data-ttu-id="e5f5c-270">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-270">String</span></span> |<span data-ttu-id="e5f5c-271">Wartość "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="e5f5c-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="e5f5c-272">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="e5f5c-272">properties.permissions.actions</span></span> |<span data-ttu-id="e5f5c-273">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-273">Yes</span></span> |<span data-ttu-id="e5f5c-274">ciąg]</span><span class="sxs-lookup"><span data-stu-id="e5f5c-274">String[]</span></span> |<span data-ttu-id="e5f5c-275">Tablica ciągów akcji określenie operacji przyznanych przez rolę niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="e5f5c-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="e5f5c-276">properties.permissions.notActions</span></span> |<span data-ttu-id="e5f5c-277">Nie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-277">No</span></span> |<span data-ttu-id="e5f5c-278">ciąg]</span><span class="sxs-lookup"><span data-stu-id="e5f5c-278">String[]</span></span> |<span data-ttu-id="e5f5c-279">Tablica ciągów akcji określenie operacji do wykluczenia z operacji przyznanych przez rolę niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="e5f5c-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="e5f5c-280">properties.assignableScopes</span></span> |<span data-ttu-id="e5f5c-281">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-281">Yes</span></span> |<span data-ttu-id="e5f5c-282">ciąg]</span><span class="sxs-lookup"><span data-stu-id="e5f5c-282">String[]</span></span> |<span data-ttu-id="e5f5c-283">Tablica zakresów, w których można użyć niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="e5f5c-284">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-284">Response</span></span>
<span data-ttu-id="e5f5c-285">Kod stanu: 201</span><span class="sxs-lookup"><span data-stu-id="e5f5c-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="e5f5c-286">Aktualizacja niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e5f5c-286">Update a Custom Role</span></span>
<span data-ttu-id="e5f5c-287">Zmodyfikuj niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-287">Modify a custom role.</span></span>

<span data-ttu-id="e5f5c-288">Aby zmodyfikować niestandardową rolę, musi mieć dostęp do `Microsoft.Authorization/roleDefinitions/write` operację na wszystkich `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="e5f5c-289">Wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielany jest dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-290">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-291">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-291">Request</span></span>
<span data-ttu-id="e5f5c-292">Użyj **PUT** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e5f5c-293">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-294">Zastąp *{zakresu}* przy pierwszym *AssignableScope* niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="e5f5c-295">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-296">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-297">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-298">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-299">Zastąp *{— identyfikator definicji roli-}* o identyfikatorze GUID niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="e5f5c-300">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="e5f5c-301">Treść żądania Podaj wartości w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-301">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="e5f5c-302">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="e5f5c-302">Element Name</span></span> | <span data-ttu-id="e5f5c-303">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5f5c-303">Required</span></span> | <span data-ttu-id="e5f5c-304">Typ</span><span class="sxs-lookup"><span data-stu-id="e5f5c-304">Type</span></span> | <span data-ttu-id="e5f5c-305">Opis</span><span class="sxs-lookup"><span data-stu-id="e5f5c-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5f5c-306">name</span><span class="sxs-lookup"><span data-stu-id="e5f5c-306">name</span></span> |<span data-ttu-id="e5f5c-307">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-307">Yes</span></span> |<span data-ttu-id="e5f5c-308">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-308">String</span></span> |<span data-ttu-id="e5f5c-309">Identyfikator GUID tworzona rola niestandardowa.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="e5f5c-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="e5f5c-310">properties.roleName</span></span> |<span data-ttu-id="e5f5c-311">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-311">Yes</span></span> |<span data-ttu-id="e5f5c-312">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-312">String</span></span> |<span data-ttu-id="e5f5c-313">Nazwa wyświetlana zaktualizowane rola niestandardowa.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="e5f5c-314">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="e5f5c-314">properties.description</span></span> |<span data-ttu-id="e5f5c-315">Nie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-315">No</span></span> |<span data-ttu-id="e5f5c-316">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-316">String</span></span> |<span data-ttu-id="e5f5c-317">Opis roli niestandardowej zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="e5f5c-318">Properties.Type</span><span class="sxs-lookup"><span data-stu-id="e5f5c-318">properties.type</span></span> |<span data-ttu-id="e5f5c-319">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-319">Yes</span></span> |<span data-ttu-id="e5f5c-320">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5f5c-320">String</span></span> |<span data-ttu-id="e5f5c-321">Wartość "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="e5f5c-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="e5f5c-322">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="e5f5c-322">properties.permissions.actions</span></span> |<span data-ttu-id="e5f5c-323">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-323">Yes</span></span> |<span data-ttu-id="e5f5c-324">ciąg]</span><span class="sxs-lookup"><span data-stu-id="e5f5c-324">String[]</span></span> |<span data-ttu-id="e5f5c-325">Tablica ciągów akcji Określanie operacje, do których tworzona rola niestandardowa zaktualizowane udziela dostępu.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="e5f5c-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="e5f5c-326">properties.permissions.notActions</span></span> |<span data-ttu-id="e5f5c-327">Nie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-327">No</span></span> |<span data-ttu-id="e5f5c-328">ciąg]</span><span class="sxs-lookup"><span data-stu-id="e5f5c-328">String[]</span></span> |<span data-ttu-id="e5f5c-329">Tablica ciągów akcji określenie operacji do wykluczenia z działań, które zaktualizowane niestandardowe rola przyznaje.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="e5f5c-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="e5f5c-330">properties.assignableScopes</span></span> |<span data-ttu-id="e5f5c-331">Tak</span><span class="sxs-lookup"><span data-stu-id="e5f5c-331">Yes</span></span> |<span data-ttu-id="e5f5c-332">ciąg]</span><span class="sxs-lookup"><span data-stu-id="e5f5c-332">String[]</span></span> |<span data-ttu-id="e5f5c-333">Tablica zakresów, w których można użyć roli zaktualizowane niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="e5f5c-334">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-334">Response</span></span>
<span data-ttu-id="e5f5c-335">Kod stanu: 201</span><span class="sxs-lookup"><span data-stu-id="e5f5c-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="e5f5c-336">Usunięcia niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e5f5c-336">Delete a Custom Role</span></span>
<span data-ttu-id="e5f5c-337">Usunięcia niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-337">Delete a custom role.</span></span>

<span data-ttu-id="e5f5c-338">Aby usunąć rolę niestandardową, należy mieć dostęp do `Microsoft.Authorization/roleDefinitions/delete` operację na wszystkich `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="e5f5c-339">Wbudowanych ról, tylko *właściciela* i *Administrator dostępu użytkowników* udzielany jest dostęp do tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e5f5c-340">Aby uzyskać więcej informacji na temat przypisania ról i zarządzanie dostęp do zasobów platformy Azure, zobacz [kontroli dostępu](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e5f5c-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e5f5c-341">Żądanie</span><span class="sxs-lookup"><span data-stu-id="e5f5c-341">Request</span></span>
<span data-ttu-id="e5f5c-342">Użyj **usunąć** metody za pomocą następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e5f5c-343">W identyfikatorze URI wprowadź następujące elementy zastępcze, aby dostosować żądania:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e5f5c-344">Zastąp *{zakresu}* w zakresie, w którym chcesz usunąć definicji roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="e5f5c-345">Poniższe przykłady przedstawiają sposób określania zakresu dla różnych poziomów:</span><span class="sxs-lookup"><span data-stu-id="e5f5c-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e5f5c-346">Subskrypcja: /subscriptions/ {identyfikator subskrypcji}</span><span class="sxs-lookup"><span data-stu-id="e5f5c-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e5f5c-347">Grupa zasobów: /subscriptions/ {identyfikator subskrypcji} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e5f5c-348">Zasób: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e5f5c-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e5f5c-349">Zastąp *{— identyfikator definicji roli-}* z identyfikatorem GUID identyfikator definicji roli niestandardowej roli.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="e5f5c-350">Zastąp *{wersja interfejsu api}* z 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e5f5c-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e5f5c-351">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e5f5c-351">Response</span></span>
<span data-ttu-id="e5f5c-352">Kod stanu: 200</span><span class="sxs-lookup"><span data-stu-id="e5f5c-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e5f5c-353">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5f5c-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
