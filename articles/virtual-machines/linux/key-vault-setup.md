---
title: aaaSet zapasowej Azure Key Vault dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Jak tooset się Key Vault do użycia z maszyny wirtualnej platformy Azure Resource Manager z hello 2.0 interfejsu wiersza polecenia."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Jak tooset się Key Vault dla maszyn wirtualnych z hello Azure CLI 2.0

W stosie usługi Azure Resource Manager hello kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez usługi Key Vault. toolearn więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md) Aby używać z maszynami wirtualnymi Azure Resource Manager toobe Key Vault, hello *EnabledForDeployment* tootrue musi być ustawiona właściwość na magazyn kluczy. W tym artykule opisano sposób tooset zapasowej Key Vault do użycia z programem Azure maszynach wirtualnych (VM) przy użyciu hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform tych kroków, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy
Utwórz magazyn kluczy i przypisz hello zasady wdrażania z [az keyvault utworzyć](/cli/azure/keyvault#create). Witaj poniższy przykład tworzy magazyn kluczy o nazwie `myKeyVault` w hello `myResourceGroup` grupy zasobów:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Zaktualizuj magazyn kluczy do użytku z maszynami wirtualnymi
Ustaw zasady wdrażania hello na istniejący magazyn kluczy o [az keyvault aktualizacji](/cli/azure/keyvault#update). Witaj następujące aktualizacje hello magazyn kluczy o nazwie `myKeyVault` w hello `myResourceGroup` grupy zasobów:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Użycie szablonów tooset zapasowej magazyn kluczy
W przypadku użycia szablonu należy tooset hello `enabledForDeployment` właściwości zbyt`true` dla zasobu usługi Key Vault hello w następujący sposób:

```json
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
```

## <a name="next-steps"></a>Następne kroki
Inne opcje, które można skonfigurować podczas tworzenia usługi Key Vault przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
