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
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="fe2d9-103">Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fe2d9-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="fe2d9-104">Aplikacje hostowane na platformie Azure mogą muszą być dostępu przez internet lub sieć VPN / połączenia usługi Express Route z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="fe2d9-105">Z magazynu utworów muzycznych przykładowej aplikacji witryny sieci web są udostępniane w Internecie z publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="fe2d9-106">Do których dostęp ustanowić połączenia do aplikacji i dostępu do zasobów maszyny wirtualnej, same powinny być zabezpieczone.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="fe2d9-107">Zabezpieczeń dostępu jest dostarczany z grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="fe2d9-108">Ten dokument zawiera szczegóły, jak aplikacji utworów muzycznych magazynu jest zabezpieczone w przykładowy szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="fe2d9-109">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="fe2d9-110">Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="fe2d9-111">Zakończenie szablonu można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="fe2d9-112">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="fe2d9-112">Public IP Address</span></span>
<span data-ttu-id="fe2d9-113">Aby zapewnić publiczny dostęp do zasobów platformy Azure, można użyć zasób publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="fe2d9-114">Publiczny adres IP można skonfigurować statyczny lub dynamiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="fe2d9-115">W przypadku dynamicznego adresu jest używany, a maszyna wirtualna zostanie zatrzymany i alokację, adresy zostanie usunięte.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="fe2d9-116">Po ponownym uruchomieniu komputera, może można przypisać inny publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="fe2d9-117">Aby uniemożliwić zmianę adresu IP, można użyć zastrzeżonego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="fe2d9-118">Publiczny adres IP można dodać do szablonu usługi Azure Resource Manager przy użyciu programu Visual Studio Kreatora dodawania nowych zasobów lub wstawiając poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="fe2d9-119">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [publicznego adresu IP](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

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

<span data-ttu-id="fe2d9-120">Publiczny adres IP może być skojarzona z wirtualną kartę sieciową lub równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="fe2d9-121">W tym przykładzie ponieważ magazynu utworów muzycznych witryny sieci Web jest równoważone między kilka maszyn wirtualnych, publiczny adres IP jest dołączony do usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="fe2d9-122">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [skojarzenie publicznego adresu IP usługi równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="fe2d9-123">Publiczny adres IP wyświetlanego w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="fe2d9-124">Zwróć uwagę, że publiczny adres IP jest skojarzony z modułem równoważenia obciążenia i nie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="fe2d9-125">Moduły równoważenia obciążenia sieciowego są szczegółowo opisane w dokumencie dalej w tej serii.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-125">Network load balancers are detailed in the next document of this series.</span></span>

![Publiczny adres IP](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="fe2d9-127">Aby uzyskać więcej informacji na publiczne adresy IP platformy Azure, zobacz [adresów IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="fe2d9-128">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="fe2d9-128">Network Security Group</span></span>
<span data-ttu-id="fe2d9-129">Po ustanowieniu dostępu do zasobów platformy Azure, ten dostęp powinien być ograniczony.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="fe2d9-130">Dla maszyn wirtualnych platformy Azure bezpieczny dostęp odbywa się za pomocą grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="fe2d9-131">Z magazynu utworów muzycznych przykładowej aplikacji dostęp do maszyny wirtualnej jest ograniczony z wyjątkiem przez port 80 dla dostępu http i portu 3389 dostępu RDP.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="fe2d9-132">Grupa zabezpieczeń sieci można dodać do szablonu usługi Azure Resource Manager przy użyciu programu Visual Studio Kreatora dodawania nowych zasobów lub wstawiając poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="fe2d9-133">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [sieciowej grupy zabezpieczeń](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

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

<span data-ttu-id="fe2d9-134">W tym przykładzie sieciowej grupy zabezpieczeń jest skojarzony z obiektem podsieci zadeklarowany w zasobie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="fe2d9-135">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [skojarzenia sieciowej grupy zabezpieczeń z siecią wirtualną](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

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

<span data-ttu-id="fe2d9-136">Oto, jak wygląda sieciowej grupy zabezpieczeń w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="fe2d9-137">Należy zauważyć, że grupy NSG można skojarzyć z interfejsem podsieć i / lub sieci.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="fe2d9-138">W takim przypadku grupa NSG jest skojarzona z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="fe2d9-139">W tej konfiguracji reguł ruchu przychodzącego dotyczą wszystkie maszyny wirtualne podłączone do podsieci.</span><span class="sxs-lookup"><span data-stu-id="fe2d9-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![Grupy zabezpieczeń sieci](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="fe2d9-141">Aby uzyskać szczegółowe informacje na temat grup zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="fe2d9-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="fe2d9-142">Następny krok</span><span class="sxs-lookup"><span data-stu-id="fe2d9-142">Next step</span></span>
<hr>

[<span data-ttu-id="fe2d9-143">Krok 3 — dostępności i skalowalności w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe2d9-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

