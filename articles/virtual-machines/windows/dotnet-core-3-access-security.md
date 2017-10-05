---
title: "Dostęp i większe bezpieczeństwo w szablonów platformy Azure dla maszyn wirtualnych systemu Windows | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ad1b5c4763cf56f681a50bb1bccc825311bbfdf5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows

Aplikacje hostowane na platformie Azure mogą muszą być dostępu przez internet lub sieć VPN / połączenia usługi Express Route z platformy Azure. Z magazynu utworów muzycznych przykładowej aplikacji witryny sieci web są udostępniane w Internecie z publicznym adresem IP. Do których dostęp ustanowić połączenia do aplikacji i dostępu do zasobów maszyny wirtualnej, same powinny być zabezpieczone. Zabezpieczeń dostępu jest dostarczany z grupy zabezpieczeń sieci. 

Ten dokument zawiera szczegóły, jak aplikacji utworów muzycznych magazynu jest zabezpieczone w przykładowy szablon usługi Azure Resource Manager. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager. Zakończenie szablonu można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Publiczny adres IP
Aby zapewnić publiczny dostęp do zasobów platformy Azure, można użyć zasób publicznego adresu IP. Publiczny adres IP można skonfigurować statyczny lub dynamiczny adres IP. W przypadku dynamicznego adresu jest używany, a maszyna wirtualna zostanie zatrzymany i alokację, adresy zostanie usunięte. Po ponownym uruchomieniu komputera, może można przypisać inny publiczny adres IP. Aby uniemożliwić zmianę adresu IP, można użyć zastrzeżonego adresu IP. 

Publiczny adres IP można dodać do szablonu usługi Azure Resource Manager przy użyciu programu Visual Studio Kreatora dodawania nowych zasobów lub wstawiając poprawne dane JSON do szablonu. 

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [publicznego adresu IP](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Publiczny adres IP może być skojarzona z wirtualną kartę sieciową lub równoważenia obciążenia. W tym przykładzie ponieważ magazynu utworów muzycznych witryny sieci Web jest równoważone między kilka maszyn wirtualnych, publiczny adres IP jest dołączony do usługi równoważenia obciążenia.

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [skojarzenie publicznego adresu IP usługi równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Publiczny adres IP wyświetlanego w portalu Azure. Zwróć uwagę, że publiczny adres IP jest skojarzony z modułem równoważenia obciążenia i nie maszyny wirtualnej. Moduły równoważenia obciążenia sieciowego są szczegółowo opisane w dokumencie dalej w tej serii.

![Publiczny adres IP](./media/dotnet-core-3-access-security/pubip-win.png)

Aby uzyskać więcej informacji na publiczne adresy IP platformy Azure, zobacz [adresów IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Grupy zabezpieczeń sieci
Po ustanowieniu dostępu do zasobów platformy Azure, ten dostęp powinien być ograniczony. Dla maszyn wirtualnych platformy Azure bezpieczny dostęp odbywa się za pomocą grupy zabezpieczeń sieci. Z magazynu utworów muzycznych przykładowej aplikacji dostęp do maszyny wirtualnej jest ograniczony z wyjątkiem przez port 80 dla dostępu http i portu 3389 dostępu RDP. Grupa zabezpieczeń sieci można dodać do szablonu usługi Azure Resource Manager przy użyciu programu Visual Studio Kreatora dodawania nowych zasobów lub wstawiając poprawne dane JSON do szablonu.

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [sieciowej grupy zabezpieczeń](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

W tym przykładzie sieciowej grupy zabezpieczeń jest skojarzony z obiektem podsieci zadeklarowany w zasobie sieci wirtualnej. 

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [skojarzenia sieciowej grupy zabezpieczeń z siecią wirtualną](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

Oto, jak wygląda sieciowej grupy zabezpieczeń w portalu Azure. Należy zauważyć, że grupy NSG można skojarzyć z interfejsem podsieć i / lub sieci. W takim przypadku grupa NSG jest skojarzona z podsiecią. W tej konfiguracji reguł ruchu przychodzącego dotyczą wszystkie maszyny wirtualne podłączone do podsieci.

![Grupy zabezpieczeń sieci](./media/dotnet-core-3-access-security/nsg-win.png)

Aby uzyskać szczegółowe informacje na temat grup zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Następny krok
<hr>

[Krok 3 — dostępności i skalowalności w szablonach usługi Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

