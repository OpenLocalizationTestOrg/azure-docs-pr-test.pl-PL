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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="83788-103">Zmiana identyfikatora dzierżawy magazynu kluczy po przeniesieniu subskrypcji</span><span class="sxs-lookup"><span data-stu-id="83788-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="83788-104">Pytanie: mojej subskrypcji został przeniesiony z dzierżawy A tootenant B. Jak zmienić identyfikator dzierżawcy hello Mój istniejący magazyn kluczy i ustawić odpowiednich list ACL dla podmiotów zabezpieczeń w dzierżawie B?</span><span class="sxs-lookup"><span data-stu-id="83788-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="83788-105">Po utworzeniu nowego magazynu kluczy w subskrypcji jest identyfikator dzierżawy usługi Azure Active Directory automatycznie wiązanej toohello domyślny dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="83788-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="83788-106">Wszystkie wpisy zasady dostępu są również identyfikator wiązanej toothis dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="83788-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="83788-107">Po przeniesieniu subskrypcji platformy Azure z dzierżawy tootenant B, magazynów są niedostępne dla istniejącego klucza hello podmiotów zabezpieczeń (Użytkownicy i aplikacje) w toofix dzierżawy B. ten problem, musisz:</span><span class="sxs-lookup"><span data-stu-id="83788-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="83788-108">Zmień hello Identyfikatora dzierżawy skojarzonego z istniejącą wszystkich magazynów kluczy w tej subskrypcji tootenant B.</span><span class="sxs-lookup"><span data-stu-id="83788-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="83788-109">usunąć wszystkie istniejące wpisy zasad dostępu,</span><span class="sxs-lookup"><span data-stu-id="83788-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="83788-110">dodać nowe wpisy zasad dostępu skojarzone z dzierżawą B.</span><span class="sxs-lookup"><span data-stu-id="83788-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="83788-111">Na przykład, jeśli masz magazynu kluczy "myvault" w ramach subskrypcji, która została przeniesiona z dzierżawy A tootenant B, tutaj w sposób toochange hello Identyfikatorem dzierżawy dla tego magazynu kluczy i Usuń stare zasad dostępu.</span><span class="sxs-lookup"><span data-stu-id="83788-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="83788-112">Ponieważ ten magazyn został w dzierżawie A przed przesunięciem hello, hello oryginalna wartość **$vault. Properties.TenantId** a dzierżawy podczas **(Get-AzureRmContext). Tenant.TenantId** jest dzierżawy B.</span><span class="sxs-lookup"><span data-stu-id="83788-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="83788-113">Magazyn jest skojarzony z Identyfikatorem dzierżawy poprawne hello i są usuwane stare wpisy zasad dostępu, ustaw nowy dostęp wpisy zasad z [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="83788-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83788-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83788-114">Next steps</span></span>
<span data-ttu-id="83788-115">Jeśli masz pytania dotyczące usługi Azure Key Vault, odwiedź stronę hello [fora magazynu kluczy Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="83788-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

