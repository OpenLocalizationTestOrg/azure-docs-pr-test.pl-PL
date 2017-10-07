---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych grupy NSG | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych NSG"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Bezpieczny ruch sieciowy między maszynami wirtualnymi

Ten skrypt tworzy dwie maszyny wirtualne i zabezpiecza tooboth ruchu przychodzącego. Witaj jednej maszyny wirtualnej jest dostępny z Internetu i grupy zabezpieczeń sieci (NSG) skonfigurował tooallow ruchu na portu 3389 i portu 80. Witaj drugiej maszyny wirtualnej nie jest dostępny na hello internet i tooonly NSG skonfigurowane ma zezwalać na ruch z hello na pierwszej maszynie wirtualnej. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Utwórz az podsieci sieci wirtualnej](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Tworzy podsieć. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [Aktualizacja reguły nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Aktualizuje reguły NSG. W tym przykładzie reguła zaplecza hello jest zaktualizowane toopass ruch tylko z podsieci frontonu hello. |
| [Lista reguł nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Zwraca informacje dotyczące reguły grupy zabezpieczeń sieci. W tym przykładzie nazwa reguły hello jest przechowywana w zmiennej do użycia później w skrypcie hello. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
