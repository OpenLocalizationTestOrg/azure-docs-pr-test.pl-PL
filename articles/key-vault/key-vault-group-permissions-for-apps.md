---
title: "Przyznanie uprawnień do wielu aplikacjom dostęp do usługi Azure key vault | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można udzielić uprawnienia do wielu aplikacjom dostęp do magazynu kluczy"
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
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="33e2d-103">Udziel uprawnień do wielu aplikacjom dostęp do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="33e2d-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="33e2d-104">Pytanie: czy masz kilka aplikacji (ponad 16), które trzeba uzyskać dostępu do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="33e2d-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="33e2d-105">Ponieważ magazyn kluczy umożliwia tylko 16 wpisów kontroli dostępu, jak można można osiągnąć?</span><span class="sxs-lookup"><span data-stu-id="33e2d-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="33e2d-106">Zasady kontroli dostępu do magazynu kluczy obsługuje tylko wpisy 16.</span><span class="sxs-lookup"><span data-stu-id="33e2d-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="33e2d-107">Można jednak utworzyć grupy zabezpieczeń usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33e2d-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="33e2d-108">Dodaj do tej grupy zabezpieczeń wszystkich podmiotów zabezpieczeń skojarzona usługa, a następnie przyznać dostęp do tej grupy zabezpieczeń do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="33e2d-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="33e2d-109">Poniżej przedstawiono wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="33e2d-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="33e2d-110">[Zainstaluj moduł programu PowerShell usługi Azure Active Directory w wersji 2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="33e2d-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="33e2d-111">[Zainstalowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="33e2d-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="33e2d-112">Aby uruchomić następujące polecenia, musisz mieć uprawnienia Utwórz/Edytuj grup w dzierżawie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33e2d-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="33e2d-113">Jeśli nie masz uprawnień, może być konieczne skontaktuj się z administratorem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33e2d-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="33e2d-114">Teraz uruchom następujące polecenia w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33e2d-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="33e2d-115">Jeśli musisz przyznać inny zestaw uprawnień do grupy aplikacji, należy utworzyć osobnej grupy zabezpieczeń usługi Azure Active Directory dla takich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33e2d-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33e2d-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33e2d-116">Next steps</span></span>

<span data-ttu-id="33e2d-117">Dowiedz się więcej o sposobie [bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="33e2d-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
