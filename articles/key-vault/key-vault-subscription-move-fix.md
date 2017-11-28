---
title: "Zmiana identyfikatora dzierżawy magazynu kluczy po przeniesieniu subskrypcji | Microsoft Docs"
description: "Dowiedz się, jak przełączyć identyfikator dzierżawy magazynu kluczy po przeniesieniu subskrypcji do innej dzierżawy"
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
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="ca476-103">Zmiana identyfikatora dzierżawy magazynu kluczy po przeniesieniu subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ca476-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="ca476-104">Pytanie: Moja subskrypcja została przeniesiona z dzierżawy A do dzierżawy B. Jak zmienić identyfikator dzierżawy dla istniejącego magazynu kluczy i ustawić prawidłowe listy ACL dla nazw głównych w dzierżawie B?</span><span class="sxs-lookup"><span data-stu-id="ca476-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="ca476-105">Po utworzeniu nowego magazynu kluczy w subskrypcji zostaje on automatycznie powiązany z domyślnym identyfikatorem dzierżawy usługi Azure Active Directory dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ca476-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="ca476-106">Wszystkie wpisy zasad dostępu również zostają powiązane z tym identyfikatorem dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ca476-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="ca476-107">Po przeniesieniu subskrypcji platformy Azure z dzierżawy A do dzierżawy B istniejące magazyny kluczy są niedostępne za pomocą nazw głównych (użytkowników i aplikacji) w dzierżawie B. Aby rozwiązać ten problem, należy:</span><span class="sxs-lookup"><span data-stu-id="ca476-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="ca476-108">zmienić identyfikator dzierżawy skojarzony ze wszystkimi istniejącymi magazynami kluczy w tej subskrypcji na dzierżawę B,</span><span class="sxs-lookup"><span data-stu-id="ca476-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="ca476-109">usunąć wszystkie istniejące wpisy zasad dostępu,</span><span class="sxs-lookup"><span data-stu-id="ca476-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="ca476-110">dodać nowe wpisy zasad dostępu skojarzone z dzierżawą B.</span><span class="sxs-lookup"><span data-stu-id="ca476-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="ca476-111">Jeśli na przykład masz magazyn kluczy „myvault” w subskrypcji przeniesionej z dzierżawy a do dzierżawy B, oto jak zmienić identyfikator dzierżawy dla tego magazynu kluczy i usunąć stare zasady dostępu.</span><span class="sxs-lookup"><span data-stu-id="ca476-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="ca476-112">Ponieważ ten magazyn przed przeniesieniem był w dzierżawie A, pierwotna wartość właściwości **$vault.Properties.TenantId** to dzierżawa A, podczas gdy wartość właściwości **(Get-AzureRmContext).Tenant.TenantId** to dzierżawa B.</span><span class="sxs-lookup"><span data-stu-id="ca476-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="ca476-113">Po skojarzeniu magazynu z poprawnym identyfikatorem dzierżawy i usunięciu starych wpisów zasad dostępu ustaw nowe wpisy zasad dostępu za pomocą polecenia [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca476-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca476-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca476-114">Next steps</span></span>
<span data-ttu-id="ca476-115">Jeśli masz pytania dotyczące usługi Azure Key Vault, odwiedź [forum usługi Azure Key Vault](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="ca476-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

