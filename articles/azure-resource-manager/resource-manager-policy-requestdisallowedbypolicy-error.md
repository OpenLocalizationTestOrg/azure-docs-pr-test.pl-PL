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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Błąd RequestDisallowedByPolicy z zasadami zasobów platformy Azure

W tym artykule opisano przyczyny tego błędu RequestDisallowedByPolicy, umożliwia także rozwiązania dla tego błędu.

## <a name="symptom"></a>Objaw

Podczas próby wykonania akcji podczas wdrażania, może zostać wyświetlony **RequestDisallowedByPolicy** błąd uniemożliwiający akcję można wykonać. Poniżej przedstawiono przykładowe błędu:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Aby uzyskać szczegółowe informacje dotyczące zasad zablokowane wdrożenia, użyj następujących metod:

### <a name="method-1"></a>1 — metoda

W programie PowerShell, podaj identyfikator zasad jako **identyfikator** parametr, aby pobrać szczegółowe informacje dotyczące zasad zablokowane wdrożenia.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>2 — metoda 

W programie Azure CLI 2.0 należy podać nazwę definicji zasad: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Rozwiązanie

Zabezpieczeń i zgodności dział IT może wymusić zasady zasobów, które uniemożliwia tworzenie adresów publicznego adresu IP, grupy zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub tabele tras. W przykładowym komunikat o błędzie opisany w sekcji "Symptomy" nosi nazwę zasady **regionPolicyDefinition**, ale może się różnić.
Aby rozwiązać ten problem, pracować ze swoim działem IT, aby przejrzeć zasad zasobów i określić, w jaki można wykonać żądanej akcji zgodnie z tymi zasadami.


Aby uzyskać więcej informacji zobacz następujące artykuły:

- [Przegląd zasad zasobów](resource-manager-policy.md)
- [Typowe błędy wdrożenia — RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


