---
title: aaaSet zapasowej Key Vault dla maszyn wirtualnych systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Jak tooset się Key Vault do użycia z maszyny wirtualnej platformy Azure Resource Manager z hello Azure CLI w wersji 1.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager z hello Azure CLI w wersji 1.0
W stosie usługi Azure Resource Manager hello kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez dostawcę zasobów hello klucza magazynu. toolearn więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md) Aby używać z maszynami wirtualnymi Azure Resource Manager toobe Key Vault, hello *EnabledForDeployment* tootrue musi być ustawiona właściwość na magazyn kluczy. Można to zrobić w różnych klientów. W tym artykule opisano sposób tooset zapasowej Key Vault do użytku z maszyn wirtualnych platformy Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można wykonać zadania hello przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="use-cli-10-tooset-up-key-vault"></a>Użyj tooset 1.0 interfejsu wiersza polecenia w górę magazyn kluczy
toocreate magazynu kluczy przy użyciu hello interfejsu wiersza polecenia (CLI), zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

1.0 interfejsu wiersza polecenia masz magazynu kluczy hello toocreate przed przypisaniem hello wdrożenia zasad. Następnie można przypisać zasady hello przy użyciu hello następujące polecenie:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Użycie szablonów tooset zapasowej magazyn kluczy
W przypadku użycia szablonu należy tooset hello `enabledForDeployment` właściwości zbyt`true` dla hello zasobu magazynu kluczy.

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
