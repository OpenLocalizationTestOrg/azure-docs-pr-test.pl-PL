---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz Maszynę wirtualną systemu Linux z NGINX | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>Utwórz maszynę Wirtualną z NGINX

Ten skrypt tworzy maszynę wirtualną platformy Azure i używa hello Azure maszyny wirtualnej niestandardowe rozszerzenie skryptu tooinstall NGINX. Po uruchomieniu skryptu hello, można uzyskać dostępu do pokaz witryny sieci Web na publiczny adres IP hello hello maszyny wirtualnej.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Rozszerzenie niestandardowego skryptu

Witaj niestandardowe rozszerzenie skryptu kopiuje ten skrypt na powitania maszyny wirtualnej. skrypt Hello jest następnie uruchom tooinstall i skonfigurować serwer sieci web NGINX. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy hello maszyny wirtualnej. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [open — port az maszyny wirtualnej](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Tworzy sieci zabezpieczeń grupy reguł tooallow ruchu przychodzącego. W tym przykładzie port 80 jest otwarty dla ruchu HTTP. |
| [zestaw rozszerzeń maszyny wirtualnej platformy Azure](https://docs.microsoft.com/cli/azure/vm/extension#set) | Dodaje i uruchamia tooa rozszerzenia maszyny wirtualnej maszyny Wirtualnej. W tym przykładzie hello niestandardowe rozszerzenie skryptu jest używany tooinstall NGINX.|
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
