---
title: "Przykładowy skrypt interfejsu wiersza polecenia aaaAzure — ruch sieciowy przez urządzenie wirtualne sieci | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt usługi Azure interfejsu wiersza polecenia — ruch trasy przez urządzenie wirtualne zapory w sieci."
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Kierować ruchem przez urządzenie wirtualne sieci

Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza. Tworzy również Maszynę wirtualną z tooroute włączone ruchu między dwiema podsieciami hello przekazywania pakietów IP. Po uruchomieniu skryptu hello można wdrażać oprogramowanie sieci, takie jak aplikacja zapory, toohello maszyny Wirtualnej.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Przykładowy skrypt


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

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
| [Utwórz podsieć sieci az](/cli/azure/network/vnet/subnet#create) | Tworzy zaplecza i strefą DMZ podsieci. |
| [Tworzenie sieci az publicznego ip](/cli/azure/network/public-ip#create) | Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet. |
| [Utwórz az kart interfejsu sieciowego](/cli/azure/network/nic#create) | Tworzy interfejs sieci wirtualnej i Włącz przesyłanie dalej IP dla niego. |
| [Tworzenie grupy nsg sieci az](/cli/azure/network/nsg#create) | Tworzy sieciową grupę zabezpieczeń (NSG). |
| [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) | Tworzy reguły NSG, które zezwala na portach HTTP i HTTPS ruchu przychodzącego toohello maszyny Wirtualnej. |
| [Aktualizacja podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update)| Grupy NSG hello stowarzyszonych i toosubnets tabele tras. |
| [Utwórz tabelę tras az sieci](/cli/azure/network/route-table#create)| Tworzy tabelę tras dla wszystkich tras. |
| [Utwórz trasę tabeli tras sieciowych az](/cli/azure/network/route-table/route#create)| Tworzy tras tooroute ruch między podsieciami i hello Internet za pośrednictwem hello maszyny Wirtualnej. |
| [Tworzenie maszyny wirtualnej az](/cli/azure/vm#create) | Tworzy maszynę wirtualną i dołącza hello tooit karty Sieciowej. To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne. |
| [Usuwanie grupy az](/cli/azure/group#delete) | Usuwa grupę zasobów i wszystkie zasoby, które zawiera. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).

Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md)
