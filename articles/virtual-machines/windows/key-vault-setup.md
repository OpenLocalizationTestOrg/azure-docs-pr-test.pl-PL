---
title: "aaaSet się klucz magazynu dla maszyn wirtualnych systemu Windows w usłudze Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Jak tooset się Key Vault do użycia z maszyny wirtualnej platformy Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

W stosie usługi Azure Resource Manager kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez dostawcę zasobów hello klucza magazynu. toolearn więcej informacji na temat usługi Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Aby używać z maszynami wirtualnymi Azure Resource Manager toobe Key Vault, hello **EnabledForDeployment** tootrue musi być ustawiona właściwość na magazyn kluczy. Można to zrobić w różnych klientów.
> 2. Hello magazynu kluczy musi toobe utworzone w hello tej samej subskrypcji i lokalizacji jako hello maszyny wirtualnej.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Użyj programu PowerShell tooset zapasowej magazyn kluczy
toocreate magazynu kluczy przy użyciu programu PowerShell, zobacz [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).

Dla nowych magazynów kluczy można użyć tego polecenia cmdlet programu PowerShell:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Dla istniejących magazynów kluczy można użyć tego polecenia cmdlet programu PowerShell:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Nam CLI tooset zapasowej magazyn kluczy
toocreate magazynu kluczy przy użyciu hello interfejsu wiersza polecenia (CLI), zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Dla interfejsu wiersza polecenia masz magazynu kluczy hello toocreate przed przypisaniem hello wdrożenia zasad. Można to zrobić za pomocą hello następujące polecenie:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Użycie szablonów tooset zapasowej magazyn kluczy
Gdy używasz szablonu należy tooset hello `enabledForDeployment` właściwości zbyt`true` dla hello zasobu magazynu kluczy.

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

Inne opcje, które można skonfigurować podczas tworzenia magazynu kluczy przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
