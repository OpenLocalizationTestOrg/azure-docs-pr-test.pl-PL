---
title: "aaaAzure przykładowym skrypcie programu PowerShell - tooVMs ruchu Równoważenie obciążenia wysokiej dostępności | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - tooVMs ruchu Równoważenie obciążenia wysokiej dostępności"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Ładowanie równowagi ruchu tooVMs wysokiej dostępności

Ten przykładowy skrypt tworzy wszystko, co jest potrzebne toorun kilka maszyn wirtualnych systemu Windows skonfigurowane w usłudze wysokiej dostępności oraz obciążenia zrównoważonym konfiguracji. Po uruchamianie skryptu hello, będzie mieć trzy maszyny wirtualne, połączone tooan zestawu dostępności Azure i jest dostępny za pośrednictwem usługi równoważenia obciążenia Azure.

W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Tworzy konfiguracji podsieci. Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej. |
| [Nowy AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Nowe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS. |
| [Nowe AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Tworzy moduł równoważenia obciążenia Azure. |
| [Nowe AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Tworzy sondę modułu równoważenia obciążenia. Sondę modułu równoważenia obciążenia jest używany toomonitor każdej maszyny Wirtualnej w zestawie usługi równoważenia obciążenia hello. Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany toohello maszyny Wirtualnej. |
| [Nowe AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Tworzy regułę modułu równoważenia obciążenia. W tym przykładzie jest tworzona reguła dla portu 80. Ruch HTTP dociera do usługi równoważenia obciążenia hello, jest kierowany tooport 80 jednej z maszyn wirtualnych hello w zestawie usługi równoważenia obciążenia hello. |
| [Nowe AzureRmLoadBalancerInboundNatRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Tworzy regułę translatora adresów sieciowych (NAT) usługi równoważenia obciążenia.  Reguły NAT mapować port portu programu tooa usługi równoważenia obciążenia w hello na maszynie Wirtualnej. W tym przykładzie tworzona jest reguła NAT dla tooeach ruchu SSH maszyny Wirtualnej w zestawie usługi równoważenia obciążenia hello.  |
| [Nowe AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Tworzy sieciową grupę zabezpieczeń (NSG), czyli granicę zabezpieczeń między hello internet i hello maszyny wirtualnej. |
| [Nowe AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Tworzy grupy NSG tooallow reguły ruchu przychodzącego. W tym przykładzie port 22 jest otwarty dla ruchu protokołu SSH. |
| [Nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Tworzy karty sieci wirtualnej i dołącza go w sieci wirtualnej toohello, podsieci i NSG. |
| [Nowe AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Tworzy zestaw dostępności. Zestawy dostępności upewnij się, czas działania aplikacji poprzez rozłożenie zasobów fizycznych hello maszyny wirtualnej tak, aby w przypadku niepowodzenia hello cały zestaw nie jest wykonywane. |
| [Nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Tworzy konfiguracji maszyny Wirtualnej. Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne. Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej. |
| [Nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
