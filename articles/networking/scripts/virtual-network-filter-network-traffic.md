---
title: "Przykładowy skrypt interfejsu wiersza polecenia aaaAzure - ruchu sieciowego maszyn wirtualnych filtru | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — filtrowania ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej

Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza. Ruchu przychodzącego ruchu sieciowego podsieci frontonu toohello jest ograniczona tooHTTP, HTTPS i SSH, podczas gdy wychodzący ruch toohello Internet z podsieci wewnętrznej hello jest niedozwolone. Po uruchomieniu skryptu hello, będziesz mieć jedną maszynę wirtualną z dwiema kartami sieciowymi. Poszczególne karty Sieciowe są połączone tooa innej podsieci.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieci frontonu. |
| [Utwórz podsieć sieci az](/cli/azure/network/vnet/subnet#create) | Tworzy podsieć zaplecza. |
| [Aktualizacja podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) | Kojarzy toosubnets grup NSG. |
| [Tworzenie sieci az publicznego ip](/cli/azure/network/public-ip#create) | Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet. |
| [Utwórz az kart interfejsu sieciowego](/cli/azure/network/nic#create) | Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza. |
| [Tworzenie grupy nsg sieci az](/cli/azure/network/nsg#create) | Tworzy grupy zabezpieczeń sieci (NSG), które są skojarzone toohello podsieci frontonu i zaplecza. |
| [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) |Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci. |
| [Tworzenie maszyny wirtualnej az](/cli/azure/vm#create) | Tworzy maszyny wirtualne i dołącza tooeach karty Sieciowej maszyny Wirtualnej. To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne. |
| [Usuwanie grupy az](/cli/azure/group#delete) | Usuwa grupę zasobów i wszystkie zasoby, które zawiera. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).

Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md)
