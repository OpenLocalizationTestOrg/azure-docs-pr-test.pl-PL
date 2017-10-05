---
title: "Wdrażanie zasoby obliczeniowe systemu Linux przy użyciu szablonów usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c3f9f98079e0c89d1231f9c3e62e82c33ad18236
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="d2ec6-103">Architektura aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="d2ec6-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="d2ec6-104">Podczas tworzenia wdrożenia usługi Azure Resource Manager, obliczeń wymagania muszą być mapowane do zasobów platformy Azure i usług.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="d2ec6-105">Jeśli aplikacja składa się z kilku punktów końcowych http, bazy danych i danych usługi buforowania, zasobów Azure hostujących każdego z tych składników musi być usprawnione.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="d2ec6-106">Na przykład przykładowej aplikacji sklepu utworów muzycznych obejmuje aplikacji sieci web, który znajduje się na maszynie wirtualnej, a baza danych SQL, który znajduje się w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="d2ec6-107">Ten dokument zawiera szczegóły dotyczące sposobu konfiguracji zasoby obliczeniowe magazynu utworów muzycznych w przykładowy szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="d2ec6-108">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="d2ec6-109">Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="d2ec6-110">Zakończenie szablonu można znaleźć tutaj — [wdrożenia magazynu utworów muzycznych na Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-110">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="d2ec6-111">Maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="d2ec6-111">Virtual Machine</span></span>
<span data-ttu-id="d2ec6-112">Aplikacja utworów muzycznych magazynu zawiera aplikacji sieci web, w którym klienci mogą przeglądanie i kupowanie utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="d2ec6-113">Gdy istnieje kilka usług Azure, które można udostępniać aplikacji sieci web, na przykład maszyny wirtualnej jest używany.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="d2ec6-114">Przy użyciu przykładowego szablonu utworów muzycznych magazynu, wdrożono maszynę wirtualną, zainstalować serwer sieci web i witryny sieci Web sklep muzyczny zainstalowany i skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="d2ec6-115">Dla tego artykułu została szczegółowo opisana tylko wdrożenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="d2ec6-116">Konfiguracji serwera sieci web i aplikacji została szczegółowo opisana w artykule nowsze.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="d2ec6-117">Maszynę wirtualną można dodać do szablonu, za pomocą Kreatora programu Visual Studio Dodaj nowy zasób lub wstawiając poprawne dane JSON do szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="d2ec6-118">Podczas wdrażania maszyny wirtualnej, potrzebne są również kilka skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="d2ec6-119">Jeśli przy użyciu programu Visual Studio, aby utworzyć szablon, te zasoby są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="d2ec6-120">Jeśli ręcznie tworzenia szablonu, te zasoby muszą być wstawiane i skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="d2ec6-121">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [JSON maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

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

<span data-ttu-id="d2ec6-122">Po wdrożeniu właściwości maszyny wirtualnej są widoczne w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Maszyna wirtualna](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="d2ec6-124">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="d2ec6-124">Storage Account</span></span>
<span data-ttu-id="d2ec6-125">Konta magazynu mają wiele opcji magazynu i możliwości.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="d2ec6-126">Dla kontekstu maszyn wirtualnych Azure konta magazynu przechowuje wirtualnych dysków twardych maszyny wirtualnej i dowolnego dodatkowego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="d2ec6-127">Przykładowy sklep muzyczny zawiera jedno konto magazynu do przechowywania wirtualnych dysków twardych z każdej maszyny wirtualnej w ramach wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="d2ec6-128">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [konta magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

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

<span data-ttu-id="d2ec6-129">Konto magazynu jest skojarzony z maszyną wirtualną wewnątrz deklaracji szablonu usługi Resource Manager maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="d2ec6-130">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [skojarzenie maszyny wirtualnej i konto magazynu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

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

<span data-ttu-id="d2ec6-131">Po wdrożeniu konta magazynu można wyświetlić w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Konto magazynu](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="d2ec6-133">Kliknięcie przycisku do kontenera obiektów blob konta magazynu, można wyświetlić pliku wirtualnego dysku twardego dla każdej maszyny wirtualnej z szablonu.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Wirtualne dyski twarde](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="d2ec6-135">Aby uzyskać więcej informacji dotyczących usługi Azure Storage, zobacz [dokumentację usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="d2ec6-136">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d2ec6-136">Virtual Network</span></span>
<span data-ttu-id="d2ec6-137">Jeśli maszyna wirtualna wymaga wewnętrznej sieci, takich jak możliwość komunikacji z innymi maszynami wirtualnymi i zasobów platformy Azure, sieci wirtualnej platformy Azure jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="d2ec6-138">Sieć wirtualna nie udostępnić maszynie wirtualnej za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="d2ec6-139">Łączności publicznej w zakresie wymaga publicznego adresu IP, które szczegółowo w dalszej części tej serii.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="d2ec6-140">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [sieci wirtualnej i podsieci](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

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

<span data-ttu-id="d2ec6-141">W portalu Azure sieci wirtualnej wygląda na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="d2ec6-142">Zwróć uwagę, że wszystkie maszyny wirtualne wdrażane z szablonem są prawidłowo podłączone do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Virtual Network](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="d2ec6-144">Interfejs sieciowy</span><span class="sxs-lookup"><span data-stu-id="d2ec6-144">Network Interface</span></span>
 <span data-ttu-id="d2ec6-145">Interfejs sieciowy podłącza maszynę wirtualną do sieci wirtualnej, w szczególności do podsieci, która została zdefiniowana w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="d2ec6-146">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [interfejsu sieciowego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

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

<span data-ttu-id="d2ec6-147">Każdy zasób maszyny wirtualnej zawiera profil sieciowy.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="d2ec6-148">Interfejs sieciowy jest skojarzony z maszyną wirtualną, w tym profilu.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="d2ec6-149">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [profilu sieciowego maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="d2ec6-150">W portalu Azure interfejsu sieciowego wygląda na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="d2ec6-151">Wewnętrzny adres IP i skojarzenie maszyny wirtualnej mogą być widoczne na zasobu interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Interfejs sieciowy](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="d2ec6-153">Aby uzyskać więcej informacji o sieciach wirtualnych platformy Azure, zobacz [dokumentacji usługi Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="d2ec6-154">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d2ec6-154">Azure SQL Database</span></span>
<span data-ttu-id="d2ec6-155">Oprócz maszyny wirtualnej hosting magazynu utworów muzycznych witryny sieci Web bazy danych SQL Azure jest wdrażana na bazę danych magazynu utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="d2ec6-156">Zaletą korzystania z bazy danych SQL Azure w tym miejscu jest drugi zestaw maszyn wirtualnych nie jest wymagane, czy skalowalność i dostępność jest wbudowana w usłudze.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="d2ec6-157">Można dodać bazy danych Azure SQL za pomocą programu Visual Studio Dodaj nowy zasób kreatora lub przez wstawienie poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="d2ec6-158">Zasób programu SQL Server zawiera nazwę użytkownika i hasło, któremu udzielono prawa administracyjne w wystąpieniu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="d2ec6-159">Ponadto dodaniu zasobów zapory SQL.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="d2ec6-160">Domyślnie aplikacje hostowane na platformie Azure mogą nawiązać połączenia z wystąpieniem serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="d2ec6-161">Aby umożliwić aplikacji zewnętrznej takie programu SQL Server Management studio nawiązywania połączenia z wystąpieniem serwera SQL, zapory należy skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="d2ec6-162">Dla pokaz magazynu utworów muzycznych domyślna konfiguracja jest poprawnie.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="d2ec6-163">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [bazy danych SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

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

<span data-ttu-id="d2ec6-164">Widok programu SQL server i MusicStore bazy danych, jak pokazano w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d2ec6-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![Oprogramowanie SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="d2ec6-166">Aby uzyskać więcej informacji na temat wdrażania usługi Azure SQL Database, zobacz [dokumentacji usługi Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="d2ec6-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="d2ec6-167">Następny krok</span><span class="sxs-lookup"><span data-stu-id="d2ec6-167">Next step</span></span>
<hr>

[<span data-ttu-id="d2ec6-168">Krok 2 — dostępu i zabezpieczeń w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d2ec6-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

