---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - zaszyfrować Maszynę wirtualną systemu Linux | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — zaszyfrować Maszynę wirtualną systemu Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a>Szyfrowanie maszyny wirtualnej systemu Linux na platformie Azure

Ten skrypt tworzy bezpieczne usługi Azure Key Vault, klucze szyfrowania, nazwy głównej usługi Azure Active Directory i maszyny wirtualnej systemu Linux (VM). Hello maszyny Wirtualnej jest następnie szyfrowany przy użyciu klucza szyfrowania hello z magazynu kluczy i poświadczenia główne.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate zasobów grupy usługi Azure Key Vault usługi głównej, maszyny wirtualnej, i wszystkich powiązanych zasobów. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Utwórz az keyvault](https://docs.microsoft.com/cli/azure/keyvault#create) | Tworzy usługi Azure Key Vault toostore bezpiecznego dane, takie jak klucze szyfrowania. |
| [Utwórz klucz keyvault az](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Tworzy klucz szyfrowania magazynu kluczy. |
| [ad az sp utworzyć do rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Tworzy usługę Azure Active Directory główna toosecurely uwierzytelniania i kontroli dostępu tooencryption kluczy. |
| [keyvault az set-policy.](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Ustawia uprawnienia na powitania Key Vault toogrant hello usługi głównej dostępu tooencryption kluczy. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [Włącz szyfrowanie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Włącza szyfrowanie na maszynie Wirtualnej za pomocą poświadczenia główne hello usługi i klucza szyfrowania. |
| [Pokaż szyfrowania maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Wyświetla stan hello hello proces szyfrowania maszyny Wirtualnej. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
