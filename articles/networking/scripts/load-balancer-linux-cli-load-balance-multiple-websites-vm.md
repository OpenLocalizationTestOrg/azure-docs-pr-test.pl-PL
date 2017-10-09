---
title: "Równoważenie obciążenia aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — wiele witryn sieci Web z wiersza polecenia platformy Azure hello | Dokumentacja firmy Microsoft"
description: "Równoważenie obciążenia Azure CLI przykładowym skrypcie — wiele witryn sieci Web toohello tej samej maszyny wirtualnej"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Równoważenie obciążenia wielu witryn sieci Web

Ten przykładowy skrypt tworzy sieć wirtualną z dwóch maszyn wirtualnych (VM), które są członkami zestawu dostępności. Moduł równoważenia obciążenia kieruje ruch na dwa oddzielne toohello dwóch maszyn wirtualnych adresów IP. Po uruchamianie skryptu hello można wdrożyć toohello oprogramowania serwera sieci web maszyn wirtualnych i obsługiwać wiele witryn sieci web z własnego adresu IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów sieci wirtualnej obciążenia równoważenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Tworzenie sieci az publicznego ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS. |
| [Utwórz równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#create) | Tworzy moduł równoważenia obciążenia Azure. |
| [Utwórz sondowania równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Tworzy sondę modułu równoważenia obciążenia. Sondę modułu równoważenia obciążenia jest używany toomonitor każdej maszyny Wirtualnej w zestawie usługi równoważenia obciążenia hello. Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany toohello maszyny Wirtualnej. |
| [Utwórz regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy regułę modułu równoważenia obciążenia. W tym przykładzie jest tworzona reguła dla portu 80. Ruch HTTP dociera do usługi równoważenia obciążenia hello, jest kierowany tooport 80 jednej z maszyn wirtualnych hello w zestawie usługi równoważenia obciążenia hello. |
| [Utwórz az sieci lb-ip frontonu](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Utwórz adres IP frontonu w hello modułu równoważenia obciążenia. |
| [AZ lb puli adresów sieciowych — tworzenie](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Tworzy puli adresów zaplecza. |
| [Utwórz az kart interfejsu sieciowego](https://docs.microsoft.com/cli/azure/network/nic#create) | Tworzy karty sieci wirtualnej i dołącza go toohello sieci wirtualnej i podsieci. |
| [Tworzenie maszyny wirtualnej az zestawu dostępności](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy zestaw dostępności. Zestawy dostępności upewnij się, czas działania aplikacji poprzez rozłożenie zasobów fizycznych hello maszyny wirtualnej tak, aby w przypadku niepowodzenia hello cały zestaw nie jest wykonywane. |
| [Tworzenie kart sieciowych az ip-config](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Tworzy confiuration IP. Musi mieć hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic funkcja jest włączona dla Twojej subskrypcji. Tylko jedną konfigurację mogą być oznaczone jako hello podstawową konfigurację protokołu IP dla karty Sieciowej, za pomocą hello — flagi podstawowej upewnij. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
