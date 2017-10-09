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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Błąd RequestDisallowedByPolicy z zasadami zasobów platformy Azure

W tym artykule opisano hello Przyczyna błędu RequestDisallowedByPolicy hello, zapewnia także rozwiązania dla tego błędu.

## <a name="symptom"></a>Objaw

Podczas próby toodo akcji podczas wdrażania może odbierać **RequestDisallowedByPolicy** błąd uniemożliwiający hello akcję można wykonać. Hello poniżej przedstawiono przykładowe hello błędu:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Szczegóły tooretrieve hello zasad zablokowane wdrożenia, użyj powitania po jednej z metod hello:

### <a name="method-1"></a>1 — metoda

W programie PowerShell, podaj identyfikator zasad jako hello **identyfikator** parametru tooretrieve szczegóły hello zasad zablokowane wdrożenia.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>2 — metoda 

Azure CLI 2.0 Podaj nazwę hello hello definicji zasad: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Rozwiązanie

Zabezpieczeń i zgodności dział IT może wymusić zasady zasobów, które uniemożliwia tworzenie adresów publicznego adresu IP, grupy zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub tabele tras. W przykładowym hello hello komunikatu o błędzie opisany w sekcji "Symptomy" hello, nosi nazwę zasady hello **regionPolicyDefinition**, ale może się różnić.
tooresolve ten problem, pracy z zasadami IT działu tooreview hello zasobów i określają, jak tooperform hello Żądana akcja zgodnie z tymi zasadami.


Aby uzyskać więcej informacji zobacz następujące artykuły hello:

- [Przegląd zasad zasobów](resource-manager-policy.md)
- [Typowe błędy wdrożenia — RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


