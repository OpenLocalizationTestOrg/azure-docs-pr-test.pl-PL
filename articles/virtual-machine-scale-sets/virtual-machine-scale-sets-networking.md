---
title: "Obsługa sieci w kontekście zestawów skalowania maszyn wirtualnych platformy Azure | Microsoft Docs"
description: "Właściwości sieciowe konfiguracji dotyczące zestawów skalowania maszyn wirtualnych platformy Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Obsługa sieci w kontekście zestawów skalowania maszyn wirtualnych platformy Azure

W przypadku wdrażania zestawu skalowania maszyn wirtualnych platformy Azure za pośrednictwem portalu, niektóre właściwości sieciowe są konfigurowane domyślnie, na przykład usługa Azure Load Balancer z regułami NAT dla ruchu przychodzącego. W tym artykule opisano, jak korzystać z niektórych bardziej zaawansowanych funkcji sieciowych konfigurowalnych za pomocą zestawów skalowania.

Wszystkie funkcje omówione w tym artykule można skonfigurować za pomocą szablonów usługi Azure Resource Manager. Dla wybranych funkcji dołączono też przykłady związane z interfejsem wiersza polecenia platformy Azure i programem PowerShell. Użyj interfejsu wiersza polecenia w wersji 2.10 i programu PowerShell 4.2.0 lub nowszego.

## <a name="accelerated-networking"></a>Accelerated Networking
Usługa Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) zwiększa wydajność sieci, umożliwiając wirtualizację we/wy z jednym elementem głównym (SR-IOV) do maszyny wirtualnej. Aby korzystać z tej funkcji przyspieszania sieci wraz z zestawami skalowania, w ustawieniach networkInterfaceConfigurations zestawu skalowania ustaw dla właściwości enableAcceleratedNetworking wartość **true**. Na przykład:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Tworzenie zestawu skalowania odwołującego się do istniejącej usługi Azure Load Balancer
Podczas tworzenia zestawu skalowania przy użyciu witryny Azure Portal w przypadku większości opcji konfiguracji jest tworzony nowy moduł równoważenia obciążenia. W przypadku utworzenia zestawu skalowania, który musi odwoływać się do istniejącego modułu równoważenia obciążenia, można to zrobić przy użyciu interfejsu wiersza polecenia. Następujący skrypt przykładowy tworzy moduł równoważenia obciążenia, a następnie tworzy zestaw skalowania, który się do niego odwołuje:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Konfigurowalne ustawienia DNS
Domyślnie zestawy skalowania przyjmują konkretne ustawienia DNS sieci VNET i podsieci, w których je utworzono. Można jednak skonfigurować ustawienia DNS zestawu skalowania bezpośrednio.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Tworzenie zestawu skalowania z konfigurowalnymi serwerami DNS
Aby utworzyć zestaw skalowania z niestandardową konfiguracją DNS przy użyciu interfejsu wiersza polecenia w wersji 2.0, dodaj do polecenia **vmss create** argument **--dns-servers**, a po nim podaj oddzielane spacjami adresy IP serwerów. Na przykład:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
Aby skonfigurować niestandardowe serwery DNS w szablonie platformy Azure, do sekcji networkInterfaceConfigurations zestawu skalowania dodaj właściwość dnsSettings. Na przykład:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Tworzenie zestawu skalowania z konfigurowalnymi nazwami domen maszyn wirtualnych
Aby utworzyć zestaw skalowania z niestandardową nazwą DNS maszyn wirtualnych przy użyciu interfejsu wiersza polecenia w wersji 2.0, dodaj do polecenia **vmss create** argument **--vm-domain-name**, a po nim podaj ciąg reprezentujący nazwę domeny.

Aby ustawić nazwę domeny w szablonie platformy Azure, do sekcji **networkInterfaceConfigurations** zestawu skalowania dodaj właściwość **dnsSettings**. Na przykład:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

Dane wyjściowe dla nazwy DNS pojedynczej maszyny wirtualnej będą miały następującą formę: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Publiczny adres IPv4 dla każdej maszyny wirtualnej
Ogólnie maszyny wirtualne zestawu skalowania platformy Azure nie muszą mieć własnych publicznych adresów IP. W przypadku większości scenariuszy najekonomiczniejszym i najbezpieczniejszym rozwiązaniem jest skojarzenie publicznego adresu IP z modułem równoważenia obciążenia lub konkretną maszyną wirtualną, która kieruje połączenia przychodzące do maszyn wirtualnych zestawu skalowania zgodnie z potrzebami (na przykład za pomocą reguł NAT dla ruchu przychodzącego).

Jednak w niektórych scenariuszach maszyny wirtualne zestawu skalowania muszą mieć własne publiczne adresy IP. Przykładem są gry — gdy konsola musi nawiązać bezpośrednie połączenie z maszyną wirtualną w chmurze obsługującą przetwarzanie symulacji świata fizycznego w grze. Innym przykładem jest sytuacja, w której maszyny wirtualne muszą nawiązywać ze sobą połączenia zewnętrzne między regionami w rozproszonej bazie danych.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Tworzenie zestawu skalowania z publicznym adresem IP dla każdej maszyny wirtualnej
Aby utworzyć zestaw skalowania, w którym każdej maszynie wirtualnej zostanie przypisany publiczny adres IP, przy użyciu interfejsu wiersza polecenia w wersji 2.0, dodaj do polecenia **vmss create** parametr **--public-ip-per-vm**. 

Aby utworzyć zestaw skalowania przy użyciu szablonu platformy Azure, upewnij się, że interfejs API zasobu Microsoft.Compute/virtualMachineScaleSets ma wersję co najmniej **2017-03-30**, i dodaj właściwość JSON **publicIpAddressConfiguration** do sekcji ipConfigurations zestawu skalowania. Na przykład:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Przykład szablonu: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a>Badanie publicznych adresów IP maszyn wirtualnych w zestawie skalowania
Aby uzyskać listę publicznych adresów IP przypisanych do maszyn wirtualnych w zestawie skalowania przy użyciu interfejsu wiersza polecenia w wersji 2.0, użyj polecenia **az vmss list-instance-public-ips**.

Aby uzyskać listę publicznych adresów IP zestawu skalowania przy użyciu programu PowerShell, użyj polecenia _Get-AzureRmPublicIpAddress_. Na przykład:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Publiczne adresy IP można także badać, odwołując się bezpośrednio do identyfikatora zasobu konfiguracji adresów IP. Na przykład:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

Aby zbadać publiczne adresy IP przypisane do maszyn wirtualnych w zestawie skalowania, użyj witryny [Azure Resource Explorer](https://resources.azure.com) lub interfejsu Azure REST API w wersji co najmniej **2017-03-30**.

Aby sprawdzić publiczne adresy IP zestawu skalowania za pomocą witryny Resource Explorer, zajrzyj do sekcji **publicipaddresses** danego zestawu skalowania. Na przykład: https://resources.azure.com/subscriptions/_identyfikator_zasobu_/resourceGroups/_grupa_zasobów_/providers/Microsoft.Compute/virtualMachineScaleSets/_zestaw_skalowania_maszyn_wirtualnych_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Przykładowe dane wyjściowe:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Wiele adresów IP dla każdej karty sieciowej
Z każdą kartą sieciową dołączoną do maszyny wirtualnej w zestawie skalowania może być skojarzona co najmniej jedna konfiguracja adresu IP. Każdej konfiguracji jest przypisany jeden prywatny adres IP. Każda konfiguracja może mieć również skojarzony jeden zasób publicznego adresu IP. Aby zrozumieć, jak wiele adresów IP można przypisać do karty sieciowej i jak wielu publicznych adresów IP można używać w subskrypcji platformy Azure, zapoznaj się z [informacjami o limitach na platformie Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Wiele kart sieciowych dla każdej maszyny wirtualnej
Zależnie od rozmiaru maszyny wirtualnej każda z nich może mieć do 8 kart sieciowych. Maksymalna liczba kart sieciowych na maszynę jest podana w [artykule poświęconym rozmiarom maszyn wirtualnych](../virtual-machines/windows/sizes.md). Poniższej przedstawiono przykład profilu sieciowego zestawu skalowania z wieloma wpisami kart sieciowych oraz wieloma publicznymi adresami IP związanymi z poszczególnymi maszynami wirtualnymi:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>Sieciowa grupa zabezpieczeń dla zestawu skalowania
Grupy zabezpieczeń sieci można stosować bezpośrednio do zestawu skalowania przez dodanie odwołania w sekcji konfiguracji interfejsu sieciowego we właściwościach maszyn wirtualnych zestawu skalowania.

Na przykład: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o sieciach wirtualnych platformy Azure, zapoznaj się z [tą dokumentacją](../virtual-network/virtual-networks-overview.md).
