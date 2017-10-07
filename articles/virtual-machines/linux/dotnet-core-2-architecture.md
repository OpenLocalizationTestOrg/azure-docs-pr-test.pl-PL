---
title: "aaaDeploying zasoby obliczeniowe systemu Linux przy użyciu usługi Azure Resource Manager szablonów | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a>Architektura aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Linux

Podczas tworzenia wdrożenia usługi Azure Resource Manager, wymagania obliczeniowe wymagają toobe mapowane tooAzure zasobów i usług. Jeśli aplikacja składa się z kilku punktów końcowych http, bazy danych i danych usługi buforowania, hello zasobów platformy Azure obsługujące każdy z tych składników musi toobe usprawnione. Na przykład hello przykładowej aplikacji sklepu utworów muzycznych obejmuje aplikacji sieci web, który znajduje się na maszynie wirtualnej, a baza danych SQL, który znajduje się w bazie danych Azure SQL. 

Ten dokument zawiera szczegóły dotyczące sposobu konfiguracji zasoby obliczeniowe magazynu utworów muzycznych hello w hello przykładowy szablon usługi Azure Resource Manager. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager. Szablon pełną Hello można znaleźć tutaj — [wdrożenia magazynu utworów muzycznych na Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="virtual-machine"></a>Maszyna wirtualna
Hello aplikacji utworów muzycznych magazynu zawiera aplikacji sieci web, w którym klienci mogą przeglądanie i kupowanie utworów muzycznych. Gdy istnieje kilka usług Azure, które można udostępniać aplikacji sieci web, na przykład maszyny wirtualnej jest używany. Przy użyciu szablonu magazynu utworów muzycznych próbki hello, wdrożono maszynę wirtualną, zainstalować serwer sieci web i hello magazynu utworów muzycznych witryny sieci Web zainstalowany i skonfigurowany. Dla zapewnienia hello w tym artykule została szczegółowo opisana tylko hello wdrożenia maszyny wirtualnej. Konfiguracja Hello powitania serwera sieci web i aplikacji hello została szczegółowo opisana w artykule nowsze.

Maszyny wirtualne można dodać szablon tooa przy użyciu hello Visual Studio Dodaj nowy zasób kreatora, lub wstawiając poprawne dane JSON do hello Szablon wdrożenia. Podczas wdrażania maszyny wirtualnej, potrzebne są również kilka skojarzonych zasobów. Przy użyciu programu Visual Studio toocreate hello szablonu, te zasoby są tworzone automatycznie. Jeśli ręcznie konstruowania hello szablonu, te zasoby muszą toobe wstawiony i skonfigurowane.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [JSON maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).

```json
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

Po wdrożeniu hello właściwości maszyny wirtualnej można znaleźć w portalu Azure hello.

![Maszyna wirtualna](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a>Konto magazynu
Konta magazynu mają wiele opcji magazynu i możliwości. Dla kontekstu hello maszyn wirtualnych Azure konto magazynu zawiera hello wirtualnych dysków twardych maszyny wirtualnej hello i dowolnego dodatkowego dysku z danymi. Przykładowy sklep muzyczny Hello zawiera jeden magazyn konta toohold hello wirtualnych dysków twardych poszczególnych maszyn wirtualnych w hello wdrożenia. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [konta magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).

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

Konto magazynu jest skojarzony z maszyną wirtualną wewnątrz deklaracji szablonu usługi Resource Manager hello hello maszyny wirtualnej. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenie maszyny wirtualnej i konto magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).

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

Po wdrożeniu hello konta magazynu można wyświetlić w portalu Azure hello.

![Konto magazynu](./media/dotnet-core-2-architecture/storacct.png)

Kliknięcie przycisku do kontenera obiektów blob konta magazynu hello, hello pliku wirtualnego dysku twardego dla każdej maszyny wirtualnej z szablonu hello są widoczne.

![Wirtualne dyski twarde](./media/dotnet-core-2-architecture/vhd.png)

Aby uzyskać więcej informacji dotyczących usługi Azure Storage, zobacz [dokumentację usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Virtual Network
Jeśli maszyna wirtualna wymaga wewnętrzny sieci, takich jak toocommunicate możliwości hello z innymi maszynami wirtualnymi i zasobów platformy Azure, sieci wirtualnej platformy Azure jest wymagany.  Sieć wirtualna nie udostępnić hello maszyny wirtualnej za pośrednictwem hello internet. Łączności publicznej w zakresie wymaga publicznego adresu IP, które szczegółowo w dalszej części tej serii.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [sieci wirtualnej i podsieci](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).

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

Z hello portalu Azure sieci wirtualnej hello wygląda na powitania po obrazu. Zauważyć, że wszystkie maszyny wirtualne wdrażane z szablonu hello są dołączone toohello sieci wirtualnej.

![Virtual Network](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a>Interfejs sieciowy
 Interfejs sieciowy łączy sieci wirtualnej tooa maszyny wirtualnej, w szczególności podsieci tooa, która została zdefiniowana w sieci wirtualnej hello. 

 Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [interfejsu sieciowego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
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
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
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
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Każdy zasób maszyny wirtualnej zawiera profil sieciowy. Interfejs sieciowy Hello jest skojarzony z maszyną wirtualną hello w tym profilu.  

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [profilu sieciowego maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

Z hello portalu Azure interfejsu sieciowego hello wygląda na powitania po obrazu. wewnętrzny adres IP Hello i hello skojarzenie maszyny wirtualnej mogą być widoczne na zasobu interfejsu sieciowego hello.

![Interfejs sieciowy](./media/dotnet-core-2-architecture/nic.png)

Aby uzyskać więcej informacji o sieciach wirtualnych platformy Azure, zobacz [dokumentacji usługi Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Usługa Azure SQL Database
Ponadto maszyna wirtualna tooa hosting hello magazynu utworów muzycznych witryny sieci Web, bazy danych SQL Azure jest bazy danych magazynu utworów muzycznych hello toohost wdrożone. Zaletą Hello tutaj przy użyciu bazy danych SQL Azure jest drugi zestaw maszyn wirtualnych nie jest wymagane, czy skalowalność i dostępność wbudowaną hello usługi.

Można dodać bazy danych Azure SQL przy użyciu hello Visual Studio Dodaj nowy zasób kreatora lub przez wstawienie poprawne dane JSON do szablonu. Hello zasobów programu SQL Server zawiera nazwę użytkownika i hasło, któremu udzielono prawa administracyjne na powitania wystąpienia serwera SQL. Ponadto dodaniu zasobów zapory SQL. Domyślnie aplikacje hostowane na platformie Azure są stanie tooconnect z hello wystąpienia serwera SQL. tooallow zewnętrznej aplikacji takich programu SQL Server Management studio tooconnect toohello wystąpienie serwera SQL, zapory hello musi toobe skonfigurowany. Dla zapewnienia hello hello magazynu utworów muzycznych demonstracyjnej hello domyślnej konfiguracji jest poprawnie. 

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [bazy danych SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Widok hello programu SQL server i MusicStore bazy danych, jak pokazano w hello portalu Azure.

![Oprogramowanie SQL Server](./media/dotnet-core-2-architecture/sql.png)

Aby uzyskać więcej informacji na temat wdrażania usługi Azure SQL Database, zobacz [dokumentacji usługi Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Następny krok
<hr>

[Krok 2 — dostępu i zabezpieczeń w szablonach usługi Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

