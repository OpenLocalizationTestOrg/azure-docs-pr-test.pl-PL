---
title: "aaaAccess i zabezpieczeń w szablonach usługi Azure dla maszyn wirtualnych systemu Windows | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows

Aplikacje obsługiwane w dostępu toobe Azure prawdopodobnie konieczne za pośrednictwem hello, internet lub sieć VPN / połączenia usługi Express Route z platformy Azure. Z przykładowych aplikacji sklepu utworów muzycznych hello, hello witryny sieci web ma zostać udostępnione na hello internet z publicznym adresem IP. Dostęp nawiązane powinny być zabezpieczone połączenia toohello aplikacji i dostępu toohello zasobów maszyny wirtualnej samodzielnie. Zabezpieczeń dostępu jest dostarczany z grupy zabezpieczeń sieci. 

Ten dokument zawiera szczegóły dotyczące jak chronione są hello aplikację ze sklepu utworów muzycznych w hello przykładowy szablon usługi Azure Resource Manager. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager. Szablon pełną Hello można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Publiczny adres IP
można tooprovide dostępu publicznego tooan zasobów platformy Azure, zasób publicznego adresu IP. Publiczny adres IP można skonfigurować statyczny lub dynamiczny adres IP. W przypadku dynamicznego adresu jest używany, a hello maszyny wirtualnej zostanie zatrzymany i alokację, adresy hello zostanie usunięte. Po ponownym uruchomieniu komputera hello może można przypisać inny publiczny adres IP. tooprevent jako IP adresu z zmiana, zastrzeżonego adresu IP może być używany. 

Publiczny adres IP można dodać szablon usługi Azure Resource Manager tooan przy użyciu hello Visual Studio nowego Kreatora dodawania zasobów, lub przez wstawienie poprawne dane JSON do szablonu. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [publicznego adresu IP](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

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

Publiczny adres IP może być skojarzona z wirtualną kartę sieciową lub równoważenia obciążenia. W tym przykładzie ponieważ hello magazynu utworów muzycznych witryny sieci Web jest równoważone między kilka maszyn wirtualnych, hello publiczny adres IP jest dołączona toohello moduł równoważenia obciążenia.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenie publicznego adresu IP usługi równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

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

Witaj publicznego adresu IP jako odebrane przez hello portalu Azure. Zwróć uwagę, czy hello publicznego adresu IP usługi równoważenia obciążenia skojarzone tooa i nie maszyny wirtualnej. Moduły równoważenia obciążenia sieciowego są szczegółowo opisane w dokumencie dalej hello tej serii.

![Publiczny adres IP](./media/dotnet-core-3-access-security/pubip-win.png)

Aby uzyskać więcej informacji na publiczne adresy IP platformy Azure, zobacz [adresów IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Grupy zabezpieczeń sieci
Po dostępu do zasobów ustalonych tooAzure, ten dostęp powinien być ograniczony. Dla maszyn wirtualnych platformy Azure bezpieczny dostęp odbywa się za pomocą grupy zabezpieczeń sieci. Z przykładowych aplikacji sklepu utworów muzycznych hello wszystkie maszyny wirtualnej toohello dostęp jest ograniczony z wyjątkiem przez port 80 dla dostępu http i portu 3389 protokołu RDP dostępu. Szablon usługi Azure Resource Manager tooan przy użyciu hello Visual Studio Dodaj Kreatora nowego zasobu, można dodać sieciowej grupy zabezpieczeń lub przez wstawienie poprawne dane JSON do szablonu.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [sieciowej grupy zabezpieczeń](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

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

W tym przykładzie hello sieciowej grupy zabezpieczeń jest skojarzony z obiektem podsieci hello zadeklarowany w hello zasobów sieci wirtualnej. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenia sieciowej grupy zabezpieczeń z siecią wirtualną](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

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

Oto, jakie grupy zabezpieczeń sieci hello wygląda z hello portalu Azure. Należy zauważyć, że grupy NSG można skojarzyć z interfejsem podsieć i / lub sieci. W takim przypadku hello NSG jest skojarzona tooa podsieci. W tej konfiguracji hello reguł ruchu przychodzącego Zastosuj tooall maszyny wirtualne podłączone toohello podsieci.

![Grupy zabezpieczeń sieci](./media/dotnet-core-3-access-security/nsg-win.png)

Aby uzyskać szczegółowe informacje na temat grup zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Następny krok
<hr>

[Krok 3 — dostępności i skalowalności w szablonach usługi Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

