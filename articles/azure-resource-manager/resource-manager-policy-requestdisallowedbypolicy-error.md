---
title: "Błąd aaaRequestDisallowedByPolicy z zasadami zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje przyczynę hello hello RequestDisallowedByPolicy błędu."
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
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="90c77-103">Błąd RequestDisallowedByPolicy z zasadami zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="90c77-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="90c77-104">W tym artykule opisano hello Przyczyna błędu RequestDisallowedByPolicy hello, zapewnia także rozwiązania dla tego błędu.</span><span class="sxs-lookup"><span data-stu-id="90c77-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="90c77-105">Objaw</span><span class="sxs-lookup"><span data-stu-id="90c77-105">Symptom</span></span>

<span data-ttu-id="90c77-106">Podczas próby toodo akcji podczas wdrażania może odbierać **RequestDisallowedByPolicy** błąd uniemożliwiający hello akcję można wykonać.</span><span class="sxs-lookup"><span data-stu-id="90c77-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="90c77-107">Hello poniżej przedstawiono przykładowe hello błędu:</span><span class="sxs-lookup"><span data-stu-id="90c77-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="90c77-108">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="90c77-108">Troubleshooting</span></span>

<span data-ttu-id="90c77-109">Szczegóły tooretrieve hello zasad zablokowane wdrożenia, użyj powitania po jednej z metod hello:</span><span class="sxs-lookup"><span data-stu-id="90c77-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="90c77-110">1 — metoda</span><span class="sxs-lookup"><span data-stu-id="90c77-110">Method 1</span></span>

<span data-ttu-id="90c77-111">W programie PowerShell, podaj identyfikator zasad jako hello **identyfikator** parametru tooretrieve szczegóły hello zasad zablokowane wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="90c77-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="90c77-112">2 — metoda</span><span class="sxs-lookup"><span data-stu-id="90c77-112">Method 2</span></span> 

<span data-ttu-id="90c77-113">Azure CLI 2.0 Podaj nazwę hello hello definicji zasad:</span><span class="sxs-lookup"><span data-stu-id="90c77-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="90c77-114">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="90c77-114">Solution</span></span>

<span data-ttu-id="90c77-115">Zabezpieczeń i zgodności dział IT może wymusić zasady zasobów, które uniemożliwia tworzenie adresów publicznego adresu IP, grupy zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub tabele tras.</span><span class="sxs-lookup"><span data-stu-id="90c77-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="90c77-116">W przykładowym hello hello komunikatu o błędzie opisany w sekcji "Symptomy" hello, nosi nazwę zasady hello **regionPolicyDefinition**, ale może się różnić.</span><span class="sxs-lookup"><span data-stu-id="90c77-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="90c77-117">tooresolve ten problem, pracy z zasadami IT działu tooreview hello zasobów i określają, jak tooperform hello Żądana akcja zgodnie z tymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="90c77-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="90c77-118">Aby uzyskać więcej informacji zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="90c77-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="90c77-119">Przegląd zasad zasobów</span><span class="sxs-lookup"><span data-stu-id="90c77-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="90c77-120">Typowe błędy wdrożenia — RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="90c77-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


