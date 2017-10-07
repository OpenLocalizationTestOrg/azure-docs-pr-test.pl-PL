---
title: polecenia aaaCommon programu PowerShell dla sieci wirtualnych Azure | Dokumentacja firmy Microsoft
description: "Rozpoczęto tworzenie sieci wirtualnej i jej skojarzonych zasobów dla maszyn wirtualnych wspólnej tooget poleceń programu PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Typowe polecenia programu PowerShell dla sieci wirtualnych Azure

Jeśli chcesz toocreate maszyny wirtualnej, należy toocreate [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md) lub wiedzieć o istniejącej sieci wirtualnej, w których hello można dodać maszyny Wirtualnej. Zazwyczaj podczas tworzenia maszyny Wirtualnej, należy również tooconsider tworzenia zasobów hello opisane w tym artykule.

Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.

Niektóre zmienne może być dla Ciebie przydatne, jeśli więcej niż jedno z poleceń hello uruchomione w tym artykule:

- $location - lokalizacji hello hello zasobów sieciowych. Można użyć [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind [regionu geograficznego](https://azure.microsoft.com/regions/) działający za Ciebie.
- $myResourceGroup - hello nazwę grupy zasobów hello, gdzie znajdują się hello zasobów sieciowych.

## <a name="create-network-resources"></a>Utwórz zasoby sieciowe

| Zadanie | Polecenie |
| ---- | ------- |
| Tworzenie konfiguracji podsieci |$podsieć1 = [nowe AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" - AddressPrefix XX. X.X.X/XX<BR>$podsieć2 = nowe AzureRmVirtualNetworkSubnetConfig-Name "mySubnet2" - AddressPrefix XX. X.X.X/XX<BR><BR>Typowej sieci może być podsieć [internetowy modułu równoważenia obciążenia](../../load-balancer/load-balancer-internet-overview.md) i oddzielne podsieci dla [wewnętrznego modułu równoważenia obciążenia](../../load-balancer/load-balancer-internal-overview.md). |
| Tworzenie sieci wirtualnej |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" - ResourceGroupName $myResourceGroup-lokalizacji $location - AddressPrefix XX. X.X.X/XX-podsieci $podsieć1, podsieć2 $ |
| Testowanie dla nazwy domeny unikatowy |[Test AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) - DomainNameLabel "myDNS"-lokalizacji $location<BR><BR>Można określić nazwę domeny DNS [publicznego adresu IP zasobu](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), która tworzy mapowanie domainname.location.cloudapp.azure.com toohello publicznego adresu IP w hello serwery zarządzane Azure DNS. Nazwa Hello może zawierać tylko litery, cyfry i łączniki. Witaj pierwszy i ostatni znak musi być literą lub cyfrą i hello nazwy domeny muszą być unikatowe w lokalizacji platformy Azure. Jeśli **True** jest zwracany, proponowana nazwa jest globalnie unikatowa. |
| Tworzenie publicznego adresu IP |$pip = [AzureRmPublicIpAddress nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" - ResourceGroupName $myResourceGroup - DomainNameLabel "myDNS"-lokalizacji $location - AllocationMethod dynamiczne<BR><BR>publiczny adres IP Hello używa nazwy domeny hello wcześniej przetestowane i jest używany przez hello frontonu konfiguracji usługi równoważenia obciążenia hello. |
| Tworzenie konfiguracji IP frontonu |$frontendIP = [AzureRmLoadBalancerFrontendIpConfig nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" - PublicIpAddress $pip<BR><BR>Konfiguracja frontonu Hello obejmuje hello publicznego adresu IP wcześniej utworzony dla przychodzącego ruchu sieciowego. |
| Utwórz pulę adresów zaplecza |$beAddressPool = [AzureRmLoadBalancerBackendAddressPoolConfig nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Zapewnia możliwość wewnętrznych adresów zaplecza hello z hello załadować równoważenia, które są dostępne za pośrednictwem karty sieciowej. |
| Utworzyć sondy |$healthProbe = [AzureRmLoadBalancerProbeConfig nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" - RequestPath "HealthProbe.aspx"-protokołu http — Port 80 - element IntervalInSeconds 15 - ProbeCount 2<BR><BR>Zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello. |
| Utwórz regułę równoważenia obciążenia |$lbRule = [AzureRmLoadBalancerRuleConfig nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) — Name HTTP — element FrontendIpConfiguration $frontendIP - BackendAddressPool $beAddressPool-sondowania $healthProbe — Protokół Tcp - elementu FrontendPort 80 - BackendPort 80<BR><BR>Zawiera reguły, które przypisać port publiczny w usłudze równoważenia obciążenia hello portu tooa w puli adresów zaplecza hello. |
| Utwórz regułę ruchu przychodzącego translatora adresów Sieciowych |$inboundNATRule = [AzureRmLoadBalancerInboundNatRuleConfig nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" - elementu FrontendIpConfiguration $frontendIP-protokołu TCP - elementu FrontendPort 3441 - BackendPort 3389<BR><BR>Zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello. |
| Tworzenie modułu równoważenia obciążenia |$loadBalancer = [AzureRmLoadBalancer nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) - ResourceGroupName $myResourceGroup-Name "myLoadBalancer"-lokalizacji $location - elementu FrontendIpConfiguration $frontendIP - InboundNatRule $inboundNATRule - LoadBalancingRule $ lbRule - BackendAddressPool $beAddressPool-sondowania $healthProbe |
| Tworzenie interfejsu sieciowego |$nic1 = [AzureRmNetworkInterface nowy](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) - ResourceGroupName $myResourceGroup-Name "myNIC" - lokalizacji $location - elementu PrivateIpAddress XX. X.X.X-$loadBalancer.BackendAddressPools[0 - LoadBalancerBackendAddressPool podsieci $podsieć2] - LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Tworzenie interfejsu sieciowego przy użyciu hello publicznego adresu IP i podsieć sieci wirtualnej, która została wcześniej utworzona. |

## <a name="get-information-about-network-resources"></a>Pobierz informacje o zasoby sieciowe

| Zadanie | Polecenie |
| ---- | ------- |
| Listy sieci wirtualnych |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) - ResourceGroupName $myResourceGroup<BR><BR>Wyświetla listę wszystkich hello sieci wirtualne w grupie zasobów hello. |
| Pobierz informacje o sieci wirtualnej |Get-AzureRmVirtualNetwork-Name "myVNet" - ResourceGroupName $myResourceGroup |
| Lista podsieci w sieci wirtualnej |Get-AzureRmVirtualNetwork-Name "myVNet" - ResourceGroupName $myResourceGroup &#124; Wybierz podsieci |
| Uzyskiwanie informacji o podsieci |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" - VirtualNetwork $vnet<BR><BR>Pobiera informacje o podsieci hello w hello określonej sieci wirtualnej. wartość Hello $vnet reprezentuje hello obiektu zwróconego przez Get-AzureRmVirtualNetwork. |
| Adresy IP |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) - ResourceGroupName $myResourceGroup<BR><BR>Wyświetla listę hello publicznych adresów IP w grupie zasobów hello. |
| Lista modułów równoważenia obciążenia |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) - ResourceGroupName $myResourceGroup<BR><BR>Wyświetla listę wszystkich usług równoważenia obciążenia hello w grupie zasobów hello. |
| Lista interfejsów sieciowych |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) - ResourceGroupName $myResourceGroup<BR><BR>Wyświetla listę wszystkich interfejsów sieciowych hello w grupie zasobów hello. |
| Uzyskiwanie informacji na temat interfejsu sieciowego |Get-AzureRmNetworkInterface-Name "myNIC" - ResourceGroupName $myResourceGroup<BR><BR>Pobiera informacje o w konkretnym interfejsie sieciowym. |
| Pobierz hello Konfiguracja IP interfejsu sieciowego |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" - interfejsu sieciowego $nic<BR><BR>Pobiera informacje o konfiguracji IP hello hello określonej sieci interfejsu. wartość Hello $nic reprezentuje hello obiektu zwróconego przez Get AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Zarządzanie zasobami sieciowymi

| Zadanie | Polecenie |
| ---- | ------- |
| Dodaj podsieć sieci wirtualnej tooa |[Dodaj AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) - AddressPrefix XX. X.X.X/XX-Name "mySubnet1" - VirtualNetwork $vnet<BR><BR>Dodaje podsieci tooan istniejącej sieci wirtualnej. wartość Hello $vnet reprezentuje hello obiektu zwróconego przez Get-AzureRmVirtualNetwork. |
| Usunąć sieci wirtualnej |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" - ResourceGroupName $myResourceGroup<BR><BR>Usuwa hello określonej sieci wirtualnej z grupy zasobów hello. |
| Usunąć interfejsu sieciowego |[Usuń AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" - ResourceGroupName $myResourceGroup<BR><BR>Usuwa interfejs sieciowy określony hello z hello grupy zasobów. |
| Usuwanie modułu równoważenia obciążenia |[Usuń AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" - ResourceGroupName $myResourceGroup<BR><BR>Usuwa hello określony moduł równoważenia obciążenia z hello grupy zasobów. |
| Usuwanie publicznego adresu IP |[Usuń AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" - ResourceGroupName $myResourceGroup<BR><BR>Usuwa hello określony publiczny adres IP z hello grupy zasobów. |

## <a name="next-steps"></a>Następne kroki
* Interfejs sieciowy hello Użyj właśnie tworzone, gdy użytkownik [tworzenie maszyny Wirtualnej](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Poznaj sposoby [tworzenia maszyn wirtualnych z wieloma interfejsami sieciowymi](../../virtual-network/virtual-networks-multiple-nics.md).

