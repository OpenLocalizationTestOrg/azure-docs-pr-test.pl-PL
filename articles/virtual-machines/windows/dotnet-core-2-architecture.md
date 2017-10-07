---
title: "aaaDeploying zasoby obliczeniowe systemu Windows przy użyciu usługi Azure Resource Manager szablonów | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="0415a-103">Architektura aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="0415a-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="0415a-104">Podczas tworzenia wdrożenia usługi Azure Resource Manager, wymagania obliczeniowe wymagają toobe mapowane tooAzure zasobów i usług.</span><span class="sxs-lookup"><span data-stu-id="0415a-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="0415a-105">Jeśli aplikacja składa się z kilku punktów końcowych http, bazy danych i danych usługi buforowania, hello zasobów platformy Azure obsługujące każdy z tych składników musi toobe usprawnione.</span><span class="sxs-lookup"><span data-stu-id="0415a-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="0415a-106">Na przykład hello przykładowej aplikacji sklepu utworów muzycznych obejmuje aplikacji sieci web, który znajduje się na maszynie wirtualnej, a baza danych SQL, który znajduje się w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0415a-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="0415a-107">Ten dokument zawiera szczegóły dotyczące sposobu konfiguracji zasoby obliczeniowe magazynu utworów muzycznych hello w hello przykładowy szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0415a-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="0415a-108">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="0415a-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="0415a-109">Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0415a-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="0415a-110">Szablon pełną Hello można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="0415a-110">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="0415a-111">Maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="0415a-111">Virtual Machine</span></span>
<span data-ttu-id="0415a-112">Hello aplikacji utworów muzycznych magazynu zawiera aplikacji sieci web, w którym klienci mogą przeglądanie i kupowanie utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="0415a-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="0415a-113">Gdy istnieje kilka usług Azure, które można udostępniać aplikacji sieci web, na przykład maszyny wirtualnej jest używany.</span><span class="sxs-lookup"><span data-stu-id="0415a-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="0415a-114">Przy użyciu szablonu magazynu utworów muzycznych próbki hello, wdrożono maszynę wirtualną, zainstalować serwer sieci web i hello magazynu utworów muzycznych witryny sieci Web zainstalowany i skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="0415a-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="0415a-115">Dla zapewnienia hello w tym artykule została szczegółowo opisana tylko hello wdrożenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0415a-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="0415a-116">Konfiguracja Hello powitania serwera sieci web i aplikacji hello została szczegółowo opisana w artykule nowsze.</span><span class="sxs-lookup"><span data-stu-id="0415a-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="0415a-117">Maszyny wirtualne można dodać szablon tooa przy użyciu hello Visual Studio Dodaj nowy zasób kreatora, lub wstawiając poprawne dane JSON do hello Szablon wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0415a-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="0415a-118">Podczas wdrażania maszyny wirtualnej, potrzebne są również kilka skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0415a-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="0415a-119">Przy użyciu programu Visual Studio toocreate hello szablonu, te zasoby są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0415a-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="0415a-120">Jeśli ręcznie konstruowania hello szablonu, te zasoby muszą toobe wstawiony i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="0415a-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="0415a-121">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [JSON maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="0415a-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

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

<span data-ttu-id="0415a-122">Po wdrożeniu hello właściwości maszyny wirtualnej można znaleźć w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0415a-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Maszyna wirtualna](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="0415a-124">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="0415a-124">Storage Account</span></span>
<span data-ttu-id="0415a-125">Konta magazynu mają wiele opcji magazynu i możliwości.</span><span class="sxs-lookup"><span data-stu-id="0415a-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="0415a-126">Dla kontekstu hello maszyn wirtualnych Azure konto magazynu zawiera hello wirtualnych dysków twardych maszyny wirtualnej hello i dowolnego dodatkowego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="0415a-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="0415a-127">Przykładowy sklep muzyczny Hello zawiera jeden magazyn konta toohold hello wirtualnych dysków twardych poszczególnych maszyn wirtualnych w hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0415a-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="0415a-128">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [konta magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="0415a-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

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

<span data-ttu-id="0415a-129">Konto magazynu jest skojarzony z maszyną wirtualną wewnątrz deklaracji szablonu usługi Resource Manager hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0415a-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="0415a-130">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenie maszyny wirtualnej i konto magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="0415a-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

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

<span data-ttu-id="0415a-131">Po wdrożeniu hello konta magazynu można wyświetlić w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0415a-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Konto magazynu](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="0415a-133">Kliknięcie przycisku do kontenera obiektów blob konta magazynu hello, hello pliku wirtualnego dysku twardego dla każdej maszyny wirtualnej z szablonu hello są widoczne.</span><span class="sxs-lookup"><span data-stu-id="0415a-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Wirtualne dyski twarde](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="0415a-135">Aby uzyskać więcej informacji dotyczących usługi Azure Storage, zobacz [dokumentację usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="0415a-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="0415a-136">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0415a-136">Virtual Network</span></span>
<span data-ttu-id="0415a-137">Jeśli maszyna wirtualna wymaga wewnętrzny sieci, takich jak toocommunicate możliwości hello z innymi maszynami wirtualnymi i zasobów platformy Azure, sieci wirtualnej platformy Azure jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="0415a-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="0415a-138">Sieć wirtualna nie udostępnić hello maszyny wirtualnej za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="0415a-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="0415a-139">Łączności publicznej w zakresie wymaga publicznego adresu IP, które szczegółowo w dalszej części tej serii.</span><span class="sxs-lookup"><span data-stu-id="0415a-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="0415a-140">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [sieci wirtualnej i podsieci](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="0415a-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

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

<span data-ttu-id="0415a-141">Z hello portalu Azure sieci wirtualnej hello wygląda na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="0415a-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="0415a-142">Zauważyć, że wszystkie maszyny wirtualne wdrażane z szablonu hello są dołączone toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0415a-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Virtual Network](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="0415a-144">Interfejs sieciowy</span><span class="sxs-lookup"><span data-stu-id="0415a-144">Network Interface</span></span>
 <span data-ttu-id="0415a-145">Interfejs sieciowy łączy sieci wirtualnej tooa maszyny wirtualnej, w szczególności podsieci tooa, która została zdefiniowana w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="0415a-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="0415a-146">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [interfejsu sieciowego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="0415a-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

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

<span data-ttu-id="0415a-147">Każdy zasób maszyny wirtualnej zawiera profil sieciowy.</span><span class="sxs-lookup"><span data-stu-id="0415a-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="0415a-148">Interfejs sieciowy Hello jest skojarzony z maszyną wirtualną hello w tym profilu.</span><span class="sxs-lookup"><span data-stu-id="0415a-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="0415a-149">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [profilu sieciowego maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="0415a-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="0415a-150">Z hello portalu Azure interfejsu sieciowego hello wygląda na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="0415a-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="0415a-151">wewnętrzny adres IP Hello i hello skojarzenie maszyny wirtualnej mogą być widoczne na zasobu interfejsu sieciowego hello.</span><span class="sxs-lookup"><span data-stu-id="0415a-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Interfejs sieciowy](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="0415a-153">Aby uzyskać więcej informacji o sieciach wirtualnych platformy Azure, zobacz [dokumentacji usługi Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="0415a-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="0415a-154">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0415a-154">Azure SQL Database</span></span>
<span data-ttu-id="0415a-155">Ponadto maszyna wirtualna tooa hosting hello magazynu utworów muzycznych witryny sieci Web, bazy danych SQL Azure jest bazy danych magazynu utworów muzycznych hello toohost wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0415a-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="0415a-156">Zaletą Hello tutaj przy użyciu bazy danych SQL Azure jest drugi zestaw maszyn wirtualnych nie jest wymagane, czy skalowalność i dostępność wbudowaną hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0415a-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="0415a-157">Można dodać bazy danych Azure SQL przy użyciu hello Visual Studio Dodaj nowy zasób kreatora lub przez wstawienie poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="0415a-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="0415a-158">Hello zasobów programu SQL Server zawiera nazwę użytkownika i hasło, któremu udzielono prawa administracyjne na powitania wystąpienia serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="0415a-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="0415a-159">Ponadto dodaniu zasobów zapory SQL.</span><span class="sxs-lookup"><span data-stu-id="0415a-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="0415a-160">Domyślnie aplikacje hostowane na platformie Azure są stanie tooconnect z hello wystąpienia serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="0415a-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="0415a-161">tooallow zewnętrznej aplikacji takich programu SQL Server Management studio tooconnect toohello wystąpienie serwera SQL, zapory hello musi toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="0415a-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="0415a-162">Dla zapewnienia hello hello magazynu utworów muzycznych demonstracyjnej hello domyślnej konfiguracji jest poprawnie.</span><span class="sxs-lookup"><span data-stu-id="0415a-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="0415a-163">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [bazy danych SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="0415a-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

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

<span data-ttu-id="0415a-164">Widok hello programu SQL server i MusicStore bazy danych, jak pokazano w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0415a-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![Oprogramowanie SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="0415a-166">Aby uzyskać więcej informacji na temat wdrażania usługi Azure SQL Database, zobacz [dokumentacji usługi Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0415a-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="0415a-167">Następny krok</span><span class="sxs-lookup"><span data-stu-id="0415a-167">Next step</span></span>
<hr>

[<span data-ttu-id="0415a-168">Krok 2 — dostępu i zabezpieczeń w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0415a-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

