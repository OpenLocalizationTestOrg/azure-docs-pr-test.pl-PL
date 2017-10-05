---
title: "Błąd RequestDisallowedByPolicy z zasadami zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano przyczyny tego błędu RequestDisallowedByPolicy."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 182a27e444c2f5db66d518a1a0c608d3e319d553
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="44371-103">Błąd RequestDisallowedByPolicy z zasadami zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="44371-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="44371-104">W tym artykule opisano przyczyny tego błędu RequestDisallowedByPolicy, umożliwia także rozwiązania dla tego błędu.</span><span class="sxs-lookup"><span data-stu-id="44371-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="44371-105">Objaw</span><span class="sxs-lookup"><span data-stu-id="44371-105">Symptom</span></span>

<span data-ttu-id="44371-106">Podczas próby wykonania akcji podczas wdrażania, może zostać wyświetlony **RequestDisallowedByPolicy** błąd uniemożliwiający akcję można wykonać.</span><span class="sxs-lookup"><span data-stu-id="44371-106">When you try to do an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents the action be performed.</span></span> <span data-ttu-id="44371-107">Poniżej przedstawiono przykładowe błędu:</span><span class="sxs-lookup"><span data-stu-id="44371-107">The following is a sample of the error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="44371-108">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="44371-108">Troubleshooting</span></span>

<span data-ttu-id="44371-109">Aby uzyskać szczegółowe informacje dotyczące zasad zablokowane wdrożenia, użyj następujących metod:</span><span class="sxs-lookup"><span data-stu-id="44371-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="44371-110">1 — metoda</span><span class="sxs-lookup"><span data-stu-id="44371-110">Method 1</span></span>

<span data-ttu-id="44371-111">W programie PowerShell, podaj identyfikator zasad jako **identyfikator** parametr, aby pobrać szczegółowe informacje dotyczące zasad zablokowane wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="44371-111">In PowerShell, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="44371-112">2 — metoda</span><span class="sxs-lookup"><span data-stu-id="44371-112">Method 2</span></span> 

<span data-ttu-id="44371-113">W programie Azure CLI 2.0 należy podać nazwę definicji zasad:</span><span class="sxs-lookup"><span data-stu-id="44371-113">In Azure CLI 2.0, provide the name of the policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="44371-114">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="44371-114">Solution</span></span>

<span data-ttu-id="44371-115">Zabezpieczeń i zgodności dział IT może wymusić zasady zasobów, które uniemożliwia tworzenie adresów publicznego adresu IP, grupy zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub tabele tras.</span><span class="sxs-lookup"><span data-stu-id="44371-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="44371-116">W przykładowym komunikat o błędzie opisany w sekcji "Symptomy" nosi nazwę zasady **regionPolicyDefinition**, ale może się różnić.</span><span class="sxs-lookup"><span data-stu-id="44371-116">In the sample of the error message that is described in the "Symptoms" section, the policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="44371-117">Aby rozwiązać ten problem, pracować ze swoim działem IT, aby przejrzeć zasad zasobów i określić, w jaki można wykonać żądanej akcji zgodnie z tymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="44371-117">To resolve this problem, work with your IT department to review the resource policies, and determine how to perform the requested action in compliance with those policies.</span></span>


<span data-ttu-id="44371-118">Aby uzyskać więcej informacji zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="44371-118">For more information, see the following articles:</span></span>

- [<span data-ttu-id="44371-119">Przegląd zasad zasobów</span><span class="sxs-lookup"><span data-stu-id="44371-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="44371-120">Typowe błędy wdrożenia — RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="44371-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


