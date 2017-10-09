---
title: "aaaChange hello magazynu kluczy identyfikator dzierżawcy po przenieść subskrypcję | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak identyfikator dzierżawcy hello tooswitch dla magazynu kluczy, gdy subskrypcja jest przenoszone tooa innej dzierżawy"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Zmiana identyfikatora dzierżawy magazynu kluczy po przeniesieniu subskrypcji
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>Pytanie: mojej subskrypcji został przeniesiony z dzierżawy A tootenant B. Jak zmienić identyfikator dzierżawcy hello Mój istniejący magazyn kluczy i ustawić odpowiednich list ACL dla podmiotów zabezpieczeń w dzierżawie B?
Po utworzeniu nowego magazynu kluczy w subskrypcji jest identyfikator dzierżawy usługi Azure Active Directory automatycznie wiązanej toohello domyślny dla tej subskrypcji. Wszystkie wpisy zasady dostępu są również identyfikator wiązanej toothis dzierżawcy. Po przeniesieniu subskrypcji platformy Azure z dzierżawy tootenant B, magazynów są niedostępne dla istniejącego klucza hello podmiotów zabezpieczeń (Użytkownicy i aplikacje) w toofix dzierżawy B. ten problem, musisz:

* Zmień hello Identyfikatora dzierżawy skojarzonego z istniejącą wszystkich magazynów kluczy w tej subskrypcji tootenant B.
* usunąć wszystkie istniejące wpisy zasad dostępu,
* dodać nowe wpisy zasad dostępu skojarzone z dzierżawą B.

Na przykład, jeśli masz magazynu kluczy "myvault" w ramach subskrypcji, która została przeniesiona z dzierżawy A tootenant B, tutaj w sposób toochange hello Identyfikatorem dzierżawy dla tego magazynu kluczy i Usuń stare zasad dostępu.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Ponieważ ten magazyn został w dzierżawie A przed przesunięciem hello, hello oryginalna wartość **$vault. Properties.TenantId** a dzierżawy podczas **(Get-AzureRmContext). Tenant.TenantId** jest dzierżawy B.

Magazyn jest skojarzony z Identyfikatorem dzierżawy poprawne hello i są usuwane stare wpisy zasad dostępu, ustaw nowy dostęp wpisy zasad z [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Następne kroki
Jeśli masz pytania dotyczące usługi Azure Key Vault, odwiedź stronę hello [fora magazynu kluczy Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

