---
title: aaaNetworking dla zestawy skalowania maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Obsługa sieci w kontekście zestawów skalowania maszyn wirtualnych platformy Azure

Podczas wdrażania zestaw za pośrednictwem portalu hello skalowania maszyny wirtualnej platformy Azure, jest konfigurowanych domyślnie niektóre właściwości sieci, na przykład modułu równoważenia obciążenia Azure z reguły dla ruchu przychodzącego translatora adresów Sieciowych. W tym artykule opisano sposób ustawiania toouse niektóre hello bardziej zaawansowane funkcje sieciowe, które można skonfigurować skali.

Można skonfigurować wszystkie funkcje hello omówione w tym artykule przy użyciu szablonów usługi Azure Resource Manager. Dla wybranych funkcji dołączono też przykłady związane z interfejsem wiersza polecenia platformy Azure i programem PowerShell. Użyj interfejsu wiersza polecenia w wersji 2.10 i programu PowerShell 4.2.0 lub nowszego.

## <a name="accelerated-networking"></a>Accelerated Networking
Azure [przyspieszony sieci](../virtual-network/virtual-network-create-vm-accelerated-networking.md) zwiększa wydajność sieci, umożliwiając maszyny wirtualnej tooa (SR-IOV) wirtualizacji we/wy pojedynczego elementu głównego. przyspieszony toouse sieć z zestawy skalowania, ustaw enableAcceleratedNetworking zbyt**true** w ustawieniach Networkinterfaceconfiguration zestawu skalowania. Na przykład:
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
Po utworzeniu zestawu skalowania za pomocą portalu Azure hello nowego modułu równoważenia obciążenia jest tworzony dla większości opcji konfiguracji. Jeśli utworzysz zestaw skali, którą należy tooreference istniejący moduł równoważenia obciążenia, można to zrobić przy użyciu interfejsu wiersza polecenia. powitania po przykładowy skrypt tworzy moduł równoważenia obciążenia, a następnie tworzy zestaw skali, który odwołuje się ona:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Konfigurowalne ustawienia DNS
Domyślnie zestawy skalowania przełączyć na powitania określonych ustawień DNS hello sieci Wirtualnej i podsieci, które zostały utworzone. Można jednak skonfigurować hello ustawień DNS na potrzeby skalowania ustawić bezpośrednio.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Tworzenie zestawu skalowania z konfigurowalnymi serwerami DNS
toocreate zestawu skalowania z niestandardowej konfiguracji DNS przy użyciu interfejsu wiersza polecenia 2.0, Dodaj hello **serwery dns —** argument toohello **vmss utworzyć** polecenia, a następnie miejsca oddzielone adresów ip serwerów. Na przykład:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
tooconfigure niestandardowych serwerów DNS w szablonu platformy Azure, Dodaj sekcji Networkinterfaceconfiguration zestawu skalowania toohello dnsSettings właściwości. Na przykład:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Tworzenie zestawu skalowania z konfigurowalnymi nazwami domen maszyn wirtualnych
toocreate zestawu skalowania z niestandardowej nazwy DNS dla maszyn wirtualnych przy użyciu interfejsu wiersza polecenia 2.0, Dodaj hello **nazwa domeny maszyny wirtualnej —** argument toohello **vmss utworzyć** polecenia następuje ciąg reprezentujący hello nazwy domeny.

Dodaj nazwę domeny hello tooset w szablonu Azure **dnsSettings** zestaw skali toohello właściwości **Networkinterfaceconfiguration** sekcji. Na przykład:

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

Hello danych wyjściowych dla poszczególnych maszyn wirtualnych nazwy dns, należy w hello następującej postaci: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Publiczny adres IPv4 dla każdej maszyny wirtualnej
Ogólnie maszyny wirtualne zestawu skalowania platformy Azure nie muszą mieć własnych publicznych adresów IP. W przypadku większości scenariuszy jest bardziej ekonomiczne i bezpieczne tooassociate publicznego adresu IP adres tooa obciążenia równoważenia lub tooan poszczególnych maszyn wirtualnych (alias jumpbox), który kieruje przychodzących połączeń tooscale zestaw maszyn wirtualnych, zgodnie z potrzebami (na przykład za pomocą reguły NAT ruchu przychodzącego).

Jednak w niektórych scenariuszach wymagane zestawu skalowania maszyn wirtualnych toohave własnych publicznego adresu IP adresów. Przykładem jest gry, gdy konsola musi toomake bezpośrednie połączenie tooa chmury maszynę wirtualną, która wykonuje przetwarzanie gier fizycznych. Innym przykładem jest, gdy maszyny wirtualne muszą tooone połączeń zewnętrznych toomake innego w regionach w rozproszoną bazę danych.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Tworzenie zestawu skalowania z publicznym adresem IP dla każdej maszyny wirtualnej
toocreate zestaw skali, który przypisuje publicznego adresu IP adres tooeach maszynę wirtualną z 2.0 interfejsu wiersza polecenia Dodaj hello **--publicznego adresu ip na wirtualna** toohello parametru **vmss utworzyć** polecenia. 

toocreate skali ustawiane przy użyciu szablonu platformy Azure, upewnij się, że wersja hello interfejsu API hello Microsoft.Compute/virtualMachineScaleSets zasobów jest co najmniej **2017-03-30**i Dodaj **publicIpAddressConfiguration**JSON właściwości toohello zestawu skalowania maszyny wirtualnej sekcji elementów Ipconfiguration. Na przykład:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Przykład szablonu: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Podczas badania hello publiczny adres IP zestawu adresów hello maszyn wirtualnych w skali
Witaj toolist publiczne adresy IP przypisane tooscale zestaw maszyn wirtualnych przy użyciu interfejsu wiersza polecenia 2.0, należy użyć hello **az vmss listy wystąpienie publicznego-adresy IP** polecenia.

zestaw skalowania toolist publicznych adresów IP przy użyciu programu PowerShell, użyj hello _Get-AzureRmPublicIpAddress_ polecenia. Na przykład:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Można również zapytania hello publicznych adresów IP za pomocą odwołań do identyfikatora zasobu hello hello publiczny adres IP bezpośrednio. Na przykład:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

Witaj tooquery publiczne adresy IP przypisane tooscale zestaw maszyn wirtualnych za pomocą hello [Eksploratora zasobów Azure](https://resources.azure.com), lub hello z wersją interfejsu API REST Azure **2017-03-30** lub nowszej.

tooview publicznych adresów IP dla skalowania ustawić za pomocą Eksploratora zasobów hello przyjrzeć się hello **elementów publicipaddress** w zestawie skali sekcji. Na przykład: https://resources.azure.com/subscriptions/_identyfikator_zasobu_/resourceGroups/_grupa_zasobów_/providers/Microsoft.Compute/virtualMachineScaleSets/_zestaw_skalowania_maszyn_wirtualnych_/publicipaddresses

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
Każdej karty Sieciowej podłączony tooa maszyny Wirtualnej w zestawie skalowania może mieć co najmniej jednej konfiguracji IP skojarzone z nim. Każdej konfiguracji jest przypisany jeden prywatny adres IP. Każda konfiguracja może mieć również skojarzony jeden zasób publicznego adresu IP. toounderstand liczbę adresów IP można przypisać tooa karty Sieciowej, i jak wiele publicznych adresów IP można używać w subskrypcji platformy Azure można znaleźć za[limity Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Wiele kart sieciowych dla każdej maszyny wirtualnej
Użytkownik może zawierać maksymalnie too8 kart interfejsu sieciowego na maszynę wirtualną, w zależności od rozmiaru maszyny. Witaj maksymalną liczbę kart sieciowych na komputerze jest dostępna w hello [artykułu rozmiar maszyny Wirtualnej](../virtual-machines/windows/sizes.md). Witaj poniższy przykład jest wyświetlane wiele wpisów karty Sieciowej i wiele publicznych adresów IP na maszynę wirtualną w profilu sieci zestawu skali:
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
Sieciowe grupy zabezpieczeń można stosować bezpośrednio tooa zestaw skali, dodając sekcję konfiguracji interfejsu sieci toohello odwołanie skali hello Ustaw właściwości maszyny wirtualnej.

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
Aby uzyskać więcej informacji na temat sieci wirtualnych platformy Azure można znaleźć zbyt[tej dokumentacji](../virtual-network/virtual-networks-overview.md).
