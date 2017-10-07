---
title: "aaaAvailability i skali w szablonach Menedżera zasobów Azure | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Dostępności i skalowalności w szablonach usługi Azure Resource Manager dla maszyn wirtualnych systemu Linux

Dostępności i skalowalności można znaleźć toouptime i hello żądanie toomeet możliwości. Jeśli aplikacja musi być 99,9% czasu hello, musi on toohave architekturę, która zezwala na wiele zasobów obliczeniowych współbieżnych. Na przykład zamiast jedną witrynę sieci Web, konfiguracji na wyższym poziomie dostępności zawiera wiele wystąpień hello lokacji sam równoważenia technologii przed ich. W tej konfiguracji jedno wystąpienie aplikacji hello może być przełączona w tryb konserwacji, hello pozostałych nadal toofunction. Skala na powitania drugiej odwołuje się tooan aplikacji możliwość tooserve żądanie. Z obciążeniem zrównoważonym aplikacji, dodawanie lub usuwanie wystąpienia z puli hello umożliwia żądanie toomeet tooscale aplikacji.

Ten dokument zawiera szczegóły dotyczące konfiguracji hello magazynu utworów muzycznych Przykładowe wdrożenie dla dostępności i skalowalności. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager. Szablon pełną Hello można znaleźć tutaj — [wdrożenia magazynu utworów muzycznych na Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Zestaw dostępności
Logicznie zestawu dostępności obejmuje maszyny wirtualne Azure na hostach fizycznych i inne infrastrukturalne składniki, takie jak zasilacze i fizyczny sprzęt sieciowy. Zestawy dostępności upewnij się, że podczas konserwacji, Niepowodzenie urządzenia lub innych czas przestoju, nie wszystkie maszyny wirtualne są wykonywane. Zestawu dostępności może zostać dodana szablonu usługi Azure Resource Manager tooan przy użyciu hello Visual Studio Kreatora dodawania nowych zasobów lub wstawianie poprawne dane JSON do szablonu.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [zestawu dostępności](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

Zestawu dostępności jest zadeklarowana jako właściwość zasobu maszyny wirtualnej. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [zestawu dostępności skojarzenia z maszyną wirtualną](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
dostępność Hello ustawione jako odebrane przez hello portalu Azure. Poszczególnych maszyn wirtualnych i szczegółowe informacje o konfiguracji hello są szczegółowo opisane w tym miejscu.

![Zestaw dostępności](./media/dotnet-core-4-availability-scale/aset.png)

Aby uzyskać szczegółowe informacje na temat zestawów dostępności, zobacz [Zarządzanie dostępnością maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Moduł równoważenia obciążenia sieciowego
Zestaw dostępności zapewnia odporność na uszkodzenia aplikacji, usługi równoważenia obciążenia udostępnia wiele wystąpień aplikacji hello na jednego adresu sieciowego. Wiele wystąpień aplikacji może być hostowana na wiele maszyn wirtualnych, każda z nich połączony tooa modułu równoważenia obciążenia. Jak uzyskiwania dostępu do aplikacji hello trasy modułu równoważenia obciążenia hello hello przychodzące żądanie między hello dołączone elementy członkowskie. Usługi równoważenia obciążenia można dodać przy użyciu hello Visual Studio Kreatora dodawania nowych zasobów lub wstawiając prawidłowo sformatowane JSON zasobów do szablonu usługi Azure Resource Manager hello.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [Usługa równoważenia obciążenia sieciowego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

Ponieważ hello Przykładowa aplikacja jest narażonych toohello Internetu z publicznym adresem IP, ten adres jest skojarzony z usługą równoważenia obciążenia hello. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenia Usługa równoważenia obciążenia sieciowego z publicznym adresem IP](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Z hello portalu Azure hello usługi równoważenia obciążenia sieciowego — omówienie pokazuje hello skojarzenie z hello publicznego adresu IP.

![Moduł równoważenia obciążenia sieciowego](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Reguły modułu równoważenia obciążenia
Podczas korzystania z usługi równoważenia obciążenia, skonfigurowanych reguł kontrolujących sposób ruch jest równoważone między hello przeznaczone zasobów. Z aplikacją ze sklepu utworów muzycznych próbki hello ruch dociera na porcie 80 hello publicznego adresu IP i jest dystrybuowana do portu 80 wszystkich maszyn wirtualnych. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [reguły modułu równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

Widok sieci hello reguła modułu równoważenia obciążenia z hello portalu.

![Reguły modułu równoważenia obciążenia sieciowego](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Sondę modułu równoważenia obciążenia
usługi równoważenia obciążenia Hello musi także toomonitor każdej maszyny wirtualnej tak, aby żądania są obsługiwane tylko toorunning systemów. Monitorowanie odbywa się przez sondowanie stałej wstępnie zdefiniowanego portu. Wdrażanie magazynu utworów muzycznych Hello jest maszyn wirtualnych skonfigurowanych tooprobe port 80 na wszystkie zawarte. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [sondy modułu równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

Witaj odebrane przez hello portalu Azure sondę modułu równoważenia obciążenia.

![Sondę modułu równoważenia obciążenia sieciowego](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Reguły NAT dla ruchu przychodzącego
Podczas korzystania z usługi równoważenia obciążenia, zasady muszą toobe umieszczane w miejscu, które zapewniają dostęp równoważeniem obciążenia z systemem innym niż tooeach maszyny wirtualnej. Na przykład podczas tworzenia połączenia SSH z każdej maszyny wirtualnej, tego rodzaju ruch, nie powinien być równoważone, a nie powinno być konfigurowane wstępnie określoną ścieżkę. wstępnie określoną ścieżki są skonfigurowane przy użyciu reguły NAT ruchu przychodzącego zasobu. Za pomocą tego zasobu, komunikacji przychodzącej mogą być mapowane tooindividual maszyn wirtualnych. 

Z hello aplikację ze sklepu muzyki port, zaczynając od 5000 jest mapowanych tooport 22 na każdej maszynie wirtualnej dostępu SSH. Witaj `copyindex()` tooincrement używana jest funkcja hello przychodzący port, taki sposób, że hello drugiej maszyny wirtualnej odbiera przychodzący port 5001 hello trzeci 5002 i tak dalej. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [reguły NAT ruchu przychodzącego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

Przykładem przychodzącej reguły NAT jako hello w portalu Azure. Dla każdej maszyny wirtualnej we wdrożeniu hello tworzona jest reguła SSH NAT.

![Reguły NAT ruchu przychodzącego](./media/dotnet-core-4-availability-scale/natrule.png)

Aby uzyskać szczegółowe informacje na temat hello Azure Usługa równoważenia obciążenia sieciowego, zobacz [równoważenia obciążenia dla usług infrastruktury platformy Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Wdrażanie wielu maszyn wirtualnych
Ponadto dla funkcję tooeffectively zestawu dostępności lub równoważenia obciążenia wielu maszyn wirtualnych są wymagane. Wiele maszyn wirtualnych można wdrożyć przy użyciu funkcji kopiowania szablonu usługi Azure Resource Manager hello. Przy użyciu funkcji kopiowania hello, nie jest konieczne toodefine skończoną liczbę maszyn wirtualnych, zamiast tej wartości można dynamicznie udostępniać w czasie hello wdrożenia. Funkcja kopiowania Hello zużywa hello liczbę wystąpień toocreated i uchwytów wdrażanie hello poprawną liczbę maszyn wirtualnych i skojarzonych zasobów.

W szablonie próbki magazynu utworów muzycznych hello parametr jest zdefiniowany przyjmującego liczba wystąpień. Numer ten jest używany w całym hello szablonu podczas tworzenia maszyn wirtualnych i powiązanych zasobów.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

Na hello zasobu maszyny wirtualnej pętlę kopiowania hello podano nazwę i toocontrol hello liczbę kopii wynikowy używany numer hello wystąpienia parametru.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [funkcji kopiowania maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

Hello bieżącą iterację funkcji kopiowania hello jest możliwy z hello `copyIndex()` funkcji. wartość Hello hello kopiowania indeksu funkcji może być używane tooname maszyn wirtualnych i innych zasobów. Na przykład jeśli są wdrażane dwa wystąpienia maszyny wirtualnej, muszą różne nazwy. Witaj `copyIndex()` funkcja może być używana jako część maszyny wirtualnej hello nazwa toocreate unikatową nazwę. Przykład Witaj `copyindex()` funkcja używany na potrzeby nazywania celów można wyświetlić w hello zasobu maszyny wirtualnej. W tym miejscu hello nazwa komputera jest złączeniem hello `vmName` parametr i hello `copyIndex()` funkcji. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [funkcji indeksu kopiowania](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

Witaj `copyIndex` funkcja jest używana wiele razy w hello magazynu utworów muzycznych przykładowego szablonu. Zasobów i funkcji przy użyciu `copyIndex` obejmują tooa cokolwiek określonego pojedynczego wystąpienia hello maszyny wirtualnej, takie jak interfejsu sieciowego, reguły modułu równoważenia obciążenia, oraz dowolne zależy od funkcji. 

Aby uzyskać więcej informacji o funkcji kopiowania hello, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Następny krok
<hr>

[Krok 4. wdrożenie aplikacji z szablonów usługi Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

