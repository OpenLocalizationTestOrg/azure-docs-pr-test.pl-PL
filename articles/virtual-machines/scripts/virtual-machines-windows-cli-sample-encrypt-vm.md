---
title: "Azure CLI skrypt przykładowy — zaszyfrować maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — zaszyfrować maszyny Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9574d779982c939aa970cd4bdf7df6e66793e3b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>Szyfrowanie maszyny wirtualnej systemu Windows na platformie Azure

Ten skrypt tworzy bezpieczne usługi Azure Key Vault, klucze szyfrowania, nazwy głównej usługi Azure Active Directory i maszyny wirtualnej systemu Windows (VM). Maszyna wirtualna jest następnie szyfrowany przy użyciu klucza szyfrowania z magazynu kluczy i poświadczenia główne usługi.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "dysków szyfrowania maszyny Wirtualnej")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń w celu utworzenia grupy zasobów, usługi Azure Key Vault nazwy głównej usługi, maszyny wirtualnej i wszystkie powiązane zasoby. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Utwórz az keyvault](https://docs.microsoft.com/cli/azure/keyvault#create) | Tworzy magazynu kluczy Azure do przechowywania zabezpieczonych danych, takie jak klucze szyfrowania. |
| [Utwórz klucz keyvault az](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Tworzy klucz szyfrowania magazynu kluczy. |
| [ad az sp utworzyć do rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Tworzy nazwę główną usługi do bezpiecznego uwierzytelniania i kontroli dostępu do kluczy szyfrowania usługi Azure Active Directory. |
| [keyvault az set-policy.](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Ustawia uprawnienia Key Vault w celu udzielenia dostępu główną usługi do kluczy szyfrowania. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG. To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.  |
| [Włącz szyfrowanie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Włącza szyfrowanie na maszynie Wirtualnej przy użyciu poświadczeń głównej usługi i klucza szyfrowania. |
| [Pokaż szyfrowania maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Wyświetla stan procesu szyfrowania maszyny Wirtualnej. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).
