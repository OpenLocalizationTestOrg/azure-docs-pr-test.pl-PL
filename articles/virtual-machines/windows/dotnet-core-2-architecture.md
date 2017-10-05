---
title: "Wdrażanie systemu Windows obliczeniowe zasobów przy użyciu szablonów usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Architektura aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows

Podczas tworzenia wdrożenia usługi Azure Resource Manager, obliczeń wymagania muszą być mapowane do zasobów platformy Azure i usług. Jeśli aplikacja składa się z kilku punktów końcowych http, bazy danych i danych usługi buforowania, zasobów Azure hostujących każdego z tych składników musi być usprawnione. Na przykład przykładowej aplikacji sklepu utworów muzycznych obejmuje aplikacji sieci web, który znajduje się na maszynie wirtualnej, a baza danych SQL, który znajduje się w bazie danych Azure SQL. 

Ten dokument zawiera szczegóły dotyczące sposobu konfiguracji zasoby obliczeniowe magazynu utworów muzycznych w przykładowy szablon usługi Azure Resource Manager. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager. Zakończenie szablonu można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Maszyna wirtualna
Aplikacja utworów muzycznych magazynu zawiera aplikacji sieci web, w którym klienci mogą przeglądanie i kupowanie utworów muzycznych. Gdy istnieje kilka usług Azure, które można udostępniać aplikacji sieci web, na przykład maszyny wirtualnej jest używany. Przy użyciu przykładowego szablonu utworów muzycznych magazynu, wdrożono maszynę wirtualną, zainstalować serwer sieci web i witryny sieci Web sklep muzyczny zainstalowany i skonfigurowany. Dla tego artykułu została szczegółowo opisana tylko wdrożenia maszyny wirtualnej. Konfiguracji serwera sieci web i aplikacji została szczegółowo opisana w artykule nowsze.

Maszynę wirtualną można dodać do szablonu, za pomocą Kreatora programu Visual Studio Dodaj nowy zasób lub wstawiając poprawne dane JSON do szablonu wdrożenia. Podczas wdrażania maszyny wirtualnej, potrzebne są również kilka skojarzonych zasobów. Jeśli przy użyciu programu Visual Studio, aby utworzyć szablon, te zasoby są tworzone automatycznie. Jeśli ręcznie tworzenia szablonu, te zasoby muszą być wstawiane i skonfigurowana.

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [JSON maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

Po wdrożeniu właściwości maszyny wirtualnej są widoczne w portalu Azure.

![Maszyna wirtualna](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Konto magazynu
Konta magazynu mają wiele opcji magazynu i możliwości. Dla kontekstu maszyn wirtualnych Azure konta magazynu przechowuje wirtualnych dysków twardych maszyny wirtualnej i dowolnego dodatkowego dysku z danymi. Przykładowy sklep muzyczny zawiera jedno konto magazynu do przechowywania wirtualnych dysków twardych z każdej maszyny wirtualnej w ramach wdrożenia. 

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [konta magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Konto magazynu jest skojarzony z maszyną wirtualną wewnątrz deklaracji szablonu usługi Resource Manager maszyny wirtualnej. 

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [skojarzenie maszyny wirtualnej i konto magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Po wdrożeniu konta magazynu można wyświetlić w portalu Azure.

![Konto magazynu](./media/dotnet-core-2-architecture/storacct-win.png)

Kliknięcie przycisku do kontenera obiektów blob konta magazynu, można wyświetlić pliku wirtualnego dysku twardego dla każdej maszyny wirtualnej z szablonu.

![Wirtualne dyski twarde](./media/dotnet-core-2-architecture/vhd-win.png)

Aby uzyskać więcej informacji dotyczących usługi Azure Storage, zobacz [dokumentację usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Virtual Network
Jeśli maszyna wirtualna wymaga wewnętrznej sieci, takich jak możliwość komunikacji z innymi maszynami wirtualnymi i zasobów platformy Azure, sieci wirtualnej platformy Azure jest wymagany.  Sieć wirtualna nie udostępnić maszynie wirtualnej za pośrednictwem Internetu. Łączności publicznej w zakresie wymaga publicznego adresu IP, które szczegółowo w dalszej części tej serii.

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [sieci wirtualnej i podsieci](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

W portalu Azure sieci wirtualnej wygląda na poniższej ilustracji. Zwróć uwagę, że wszystkie maszyny wirtualne wdrażane z szablonem są prawidłowo podłączone do sieci wirtualnej.

![Virtual Network](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Interfejs sieciowy
 Interfejs sieciowy podłącza maszynę wirtualną do sieci wirtualnej, w szczególności do podsieci, która została zdefiniowana w sieci wirtualnej. 

 Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [interfejsu sieciowego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Każdy zasób maszyny wirtualnej zawiera profil sieciowy. Interfejs sieciowy jest skojarzony z maszyną wirtualną, w tym profilu.  

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [profilu sieciowego maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

W portalu Azure interfejsu sieciowego wygląda na poniższej ilustracji. Wewnętrzny adres IP i skojarzenie maszyny wirtualnej mogą być widoczne na zasobu interfejsu sieciowego.

![Interfejs sieciowy](./media/dotnet-core-2-architecture/nic-win.png)

Aby uzyskać więcej informacji o sieciach wirtualnych platformy Azure, zobacz [dokumentacji usługi Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Usługa Azure SQL Database
Oprócz maszyny wirtualnej hosting magazynu utworów muzycznych witryny sieci Web bazy danych SQL Azure jest wdrażana na bazę danych magazynu utworów muzycznych. Zaletą korzystania z bazy danych SQL Azure w tym miejscu jest drugi zestaw maszyn wirtualnych nie jest wymagane, czy skalowalność i dostępność jest wbudowana w usłudze.

Można dodać bazy danych Azure SQL za pomocą programu Visual Studio Dodaj nowy zasób kreatora lub przez wstawienie poprawne dane JSON do szablonu. Zasób programu SQL Server zawiera nazwę użytkownika i hasło, któremu udzielono prawa administracyjne w wystąpieniu programu SQL. Ponadto dodaniu zasobów zapory SQL. Domyślnie aplikacje hostowane na platformie Azure mogą nawiązać połączenia z wystąpieniem serwera SQL. Aby umożliwić aplikacji zewnętrznej takie programu SQL Server Management studio nawiązywania połączenia z wystąpieniem serwera SQL, zapory należy skonfigurować. Dla pokaz magazynu utworów muzycznych domyślna konfiguracja jest poprawnie. 

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [bazy danych SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Widok programu SQL server i MusicStore bazy danych, jak pokazano w portalu Azure.

![Oprogramowanie SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Aby uzyskać więcej informacji na temat wdrażania usługi Azure SQL Database, zobacz [dokumentacji usługi Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Następny krok
<hr>

[Krok 2 — dostępu i zabezpieczeń w szablonach usługi Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

