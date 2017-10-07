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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Przyznaj uprawnienie toomany aplikacji tooaccess magazyn kluczy

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>Pytanie: czy masz kilka aplikacji (ponad 16), które muszą tooaccess magazynu kluczy. Ponieważ magazyn kluczy umożliwia tylko 16 wpisów kontroli dostępu, jak można można osiągnąć?

Zasady kontroli dostępu do magazynu kluczy obsługuje tylko wpisy 16. Można jednak utworzyć grupy zabezpieczeń usługi Azure Active Directory. Dodaj wszystkie hello skojarzona grupa zabezpieczeń toothis podmiotów zabezpieczeń usługi, a następnie przyznać dostęp toothis zabezpieczeń grupy tooKey magazynu.

Poniżej przedstawiono wymagania wstępne hello:
* [Zainstaluj moduł programu PowerShell usługi Azure Active Directory w wersji 2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Zainstalowanie programu Azure PowerShell](/powershell/azure/overview).
* toorun hello następujące polecenia, należy grup toocreate/Edytuj uprawnienia w dzierżawie usługi Azure Active Directory hello. Jeśli nie masz uprawnień, może być konieczne toocontact administrator usługi Azure Active Directory.

Teraz uruchom następujące polecenia w programie PowerShell hello.

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

Jeśli potrzebujesz toogrant inny zestaw uprawnień tooa grupy aplikacji, należy utworzyć osobnej grupy zabezpieczeń usługi Azure Active Directory dla takich aplikacji.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o tym, jak za[bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).
