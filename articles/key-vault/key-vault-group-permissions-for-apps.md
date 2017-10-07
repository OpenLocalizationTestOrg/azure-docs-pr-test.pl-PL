---
title: "aaaGrant uprawnienia toomany aplikacji tooaccess usługi Azure key vault | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toogrant uprawnienia toomany aplikacji tooaccess klucza magazynu"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="23f77-103">Przyznaj uprawnienie toomany aplikacji tooaccess magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="23f77-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="23f77-104">Pytanie: czy masz kilka aplikacji (ponad 16), które muszą tooaccess magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="23f77-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="23f77-105">Ponieważ magazyn kluczy umożliwia tylko 16 wpisów kontroli dostępu, jak można można osiągnąć?</span><span class="sxs-lookup"><span data-stu-id="23f77-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="23f77-106">Zasady kontroli dostępu do magazynu kluczy obsługuje tylko wpisy 16.</span><span class="sxs-lookup"><span data-stu-id="23f77-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="23f77-107">Można jednak utworzyć grupy zabezpieczeń usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="23f77-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="23f77-108">Dodaj wszystkie hello skojarzona grupa zabezpieczeń toothis podmiotów zabezpieczeń usługi, a następnie przyznać dostęp toothis zabezpieczeń grupy tooKey magazynu.</span><span class="sxs-lookup"><span data-stu-id="23f77-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="23f77-109">Poniżej przedstawiono wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="23f77-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="23f77-110">[Zainstaluj moduł programu PowerShell usługi Azure Active Directory w wersji 2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="23f77-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="23f77-111">[Zainstalowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="23f77-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="23f77-112">toorun hello następujące polecenia, należy grup toocreate/Edytuj uprawnienia w dzierżawie usługi Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="23f77-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="23f77-113">Jeśli nie masz uprawnień, może być konieczne toocontact administrator usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="23f77-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="23f77-114">Teraz uruchom następujące polecenia w programie PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="23f77-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="23f77-115">Jeśli potrzebujesz toogrant inny zestaw uprawnień tooa grupy aplikacji, należy utworzyć osobnej grupy zabezpieczeń usługi Azure Active Directory dla takich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23f77-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23f77-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23f77-116">Next steps</span></span>

<span data-ttu-id="23f77-117">Dowiedz się więcej o tym, jak za[bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="23f77-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
