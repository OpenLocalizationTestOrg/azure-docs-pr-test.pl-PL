---
title: "Azure CLI skrypt przykładowy — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych grupy NSG | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych NSG"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7bd8c315ab0b7b3bcbbd9ebc8f17728079611f9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Bezpieczny ruch sieciowy między maszynami wirtualnymi

Ten skrypt tworzy dwie maszyny wirtualne i zabezpiecza ruch przychodzący do obu. Jednej maszyny wirtualnej jest dostępny w Internecie i skonfigurował grupy zabezpieczeń sieci (NSG) tak, aby zezwolić na ruch na port 22 i portu 80. Drugiej maszyny wirtualnej nie jest dostępny w Internecie, i ma skonfigurowane grupy NSG tylko zezwalająca na ruch z pierwszej maszynie wirtualnej. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Utwórz maszynę Wirtualną z grupy NSG")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Utwórz az podsieci sieci wirtualnej](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Tworzy podsieć. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG. To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.  |
| [Lista reguł nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Zwraca informacje dotyczące reguły grupy zabezpieczeń sieci. W tym przykładzie nazwa reguły jest przechowywana w zmiennej do użycia później w skrypcie. |
| [Aktualizacja reguły nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Aktualizuje reguły NSG. W tym przykładzie jest aktualizowana reguła zaplecza, aby przekazywać ruch tylko z podsieci frontonu. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
