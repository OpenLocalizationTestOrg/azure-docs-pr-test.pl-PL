---
title: "Równoważenie obciążenia Azure CLI przykładowym skrypcie — wiele witryn sieci Web z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Równoważenie obciążenia Azure CLI przykładowym skrypcie — wiele witryn sieci Web do tej samej maszyny wirtualnej"
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a>Równoważenie obciążenia wielu witryn sieci Web

Ten przykładowy skrypt tworzy sieć wirtualną z dwóch maszyn wirtualnych (VM), które są członkami zestawu dostępności. Moduł równoważenia obciążenia kieruje ruch dla dwóch osobnych adresów IP do dwóch maszyn wirtualnych. Po uruchomieniu skryptu, można wdrożyć oprogramowanie serwera sieci web do maszyn wirtualnych i hostów wiele witryn sieci web z własnego adresu IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt


[!code-azurecli-interactive[główne](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Równoważenie obciążenia wielu witryn sieci web")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieci wirtualnej, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Tworzenie sieci az publicznego ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS. |
| [Utwórz równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#create) | Tworzy moduł równoważenia obciążenia Azure. |
| [Utwórz sondowania równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Tworzy sondę modułu równoważenia obciążenia. Sondę modułu równoważenia obciążenia jest używany do monitorowania każdej maszyny Wirtualnej w zestawie usługi równoważenia obciążenia. Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany do maszyny Wirtualnej. |
| [Utwórz regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy regułę modułu równoważenia obciążenia. W tym przykładzie jest tworzona reguła dla portu 80. Jak ruchu HTTP dociera do usługi równoważenia obciążenia, jest kierowany do portu 80 jednej z maszyn wirtualnych w zestawie usługi równoważenia obciążenia. |
| [Utwórz az sieci lb-ip frontonu](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Utwórz adres IP frontonu dla usługi równoważenia obciążenia. |
| [AZ lb puli adresów sieciowych — tworzenie](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Tworzy puli adresów zaplecza. |
| [Utwórz az kart interfejsu sieciowego](https://docs.microsoft.com/cli/azure/network/nic#create) | Tworzy karty sieci wirtualnej i dołącza go do sieci wirtualnej i podsieci. |
| [Tworzenie maszyny wirtualnej az zestawu dostępności](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy zestaw dostępności. Zestawy dostępności upewnij się, czas działania aplikacji poprzez rozłożenie zasobów fizycznych maszyny wirtualnej tak, aby w przypadku niepowodzenia cały zestaw nie jest wykonywane. |
| [Tworzenie kart sieciowych az ip-config](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Tworzy confiuration IP. Musi być funkcja Microsoft.Network/AllowMultipleIpConfigurationsPerNic włączona dla Twojej subskrypcji. Tylko jedną konfigurację mogą być oznaczone jako podstawową konfigurację protokołu IP dla karty Sieciowej, za pomocą flagi — podstawowy upewnij. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG. To polecenie określa również obraz maszyny wirtualnej ma być używane i zapewnić poświadczenia administracyjne.  |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w [Azure Przegląd dokumentacji](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
