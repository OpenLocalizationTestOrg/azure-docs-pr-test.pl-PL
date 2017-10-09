---
title: "Równoważenie obciążenia aaaAzure przykładowy skrypt programu PowerShell — wiele witryn sieci Web przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - wiele witryn sieci Web toohello Równoważenie obciążenia tej samej maszyny wirtualnej"
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
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Równoważenie obciążenia wielu witryn sieci Web

Ten przykładowy skrypt tworzy sieć wirtualną z dwóch maszyn wirtualnych (VM), które są członkami zestawu dostępności. Moduł równoważenia obciążenia kieruje ruch na dwa oddzielne toohello dwóch maszyn wirtualnych adresów IP. Po uruchamianie skryptu hello można wdrożyć toohello oprogramowania serwera sieci web maszyn wirtualnych i obsługiwać wiele witryn sieci web z własnego adresu IP.

W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów sieci wirtualnej obciążenia równoważenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Tworzy Azure dostępność zestawu tooprovide wysokiej dostępności. |
| [Nowe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Tworzy konfiguracji podsieci. Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej. |
| [Nowy AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Tworzy sieć wirtualną. |
| [Nowe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Tworzy publiczny adres IP. |
| [Nowe AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | Tworzy konfiguracji IP frontonu modułu równoważenia obciążenia. |
| [Nowe AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | Tworzy Konfiguracja puli adresów zaplecza, usługi równoważenia obciążenia. |
| [Nowe AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Tworzy badanie równoważenia obciążenia Sieciowego. Sonda równoważenia obciążenia Sieciowego jest używane toomonitor każdej maszyny Wirtualnej w zestawie równoważenia obciążenia Sieciowego hello. Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany toohello maszyny Wirtualnej. |
| [Nowe AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Tworzy regułę równoważenia obciążenia Sieciowego. W tym przykładzie jest tworzona reguła dla portu 80. Ruch HTTP dociera hello równoważenia obciążenia Sieciowego, jest kierowany tooport 80 jednej z maszyn wirtualnych hello hello zestawu równoważenia obciążenia Sieciowego. |
| [Nowe AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) | Tworzy moduł równoważenia obciążenia. |
| [Nowe AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | Definiuje zaawansowane funkcje dla interfejsu sieci wirtualnej. |
| [Nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Tworzy interfejs sieciowy. |
| [Nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Tworzy konfiguracji maszyny Wirtualnej. Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne. Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej. |
| [Nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Utwórz maszynę wirtualną. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
