---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - tooVMs ruchu Równoważenie obciążenia wysokiej dostępności | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - tooVMs ruchu Równoważenie obciążenia wysokiej dostępności"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Ładowanie równowagi ruchu tooVMs wysokiej dostępności

Ten przykładowy skrypt tworzy wszystko, co jest potrzebne toorun kilka maszyny wirtualnej systemu Ubuntu skonfigurowany w wysokiej dostępności i załadować zrównoważonym konfiguracji. Po uruchamianie skryptu hello, będzie mieć trzy maszyny wirtualne, połączone tooan zestawu dostępności Azure i jest dostępny za pośrednictwem usługi równoważenia obciążenia Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Tworzenie sieci az publicznego ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS. |
| [Utwórz równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#create) | Tworzy moduł równoważenia obciążenia Azure. |
| [Utwórz sondowania równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Tworzy sondę modułu równoważenia obciążenia. Sondę modułu równoważenia obciążenia jest używany toomonitor każdej maszyny Wirtualnej w zestawie usługi równoważenia obciążenia hello. Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany toohello maszyny Wirtualnej. |
| [Utwórz regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy regułę modułu równoważenia obciążenia. W tym przykładzie jest tworzona reguła dla portu 80. Ruch HTTP dociera do usługi równoważenia obciążenia hello, jest kierowany tooport 80 jednej z maszyn wirtualnych hello w zestawie hello LB. |
| [Utwórz az sieci lb ruchu przychodzącego translatora adresów sieciowych — reguł](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Tworzy regułę translatora adresów sieciowych (NAT) usługi równoważenia obciążenia.  Reguły NAT mapować port portu programu tooa usługi równoważenia obciążenia w hello na maszynie Wirtualnej. W tym przykładzie tworzona jest reguła NAT dla tooeach ruchu SSH maszyny Wirtualnej w zestawie usługi równoważenia obciążenia hello.  |
| [Tworzenie grupy nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg#create) | Tworzy sieciową grupę zabezpieczeń (NSG), czyli granicę zabezpieczeń między hello internet i hello maszyny wirtualnej. |
| [Tworzenie reguły nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Tworzy grupy NSG tooallow reguły ruchu przychodzącego. W tym przykładzie port 22 jest otwarty dla ruchu protokołu SSH. |
| [Utwórz az kart interfejsu sieciowego](https://docs.microsoft.com/cli/azure/network/nic#create) | Tworzy karty sieci wirtualnej i dołącza go w sieci wirtualnej toohello, podsieci i NSG. |
| [Tworzenie maszyny wirtualnej az zestawu dostępności](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy zestaw dostępności. Zestawy dostępności upewnij się, czas działania aplikacji poprzez rozłożenie zasobów fizycznych hello maszyny wirtualnej tak, aby w przypadku niepowodzenia hello cały zestaw nie jest wykonywane. |
| [Tworzenie maszyny wirtualnej az](/cli/azure/vm#create) | Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów wiersza polecenia platformy Azure sieci można znaleźć w hello [Azure Networking dokumentacji](../cli-samples.md).
