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
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="2e256-103">Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="2e256-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="2e256-104">Aplikacje obsługiwane w dostępu toobe Azure prawdopodobnie konieczne za pośrednictwem hello, internet lub sieć VPN / połączenia usługi Express Route z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2e256-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="2e256-105">Z przykładowych aplikacji sklepu utworów muzycznych hello, hello witryny sieci web ma zostać udostępnione na hello internet z publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="2e256-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="2e256-106">Dostęp nawiązane powinny być zabezpieczone połączenia toohello aplikacji i dostępu toohello zasobów maszyny wirtualnej samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="2e256-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="2e256-107">Zabezpieczeń dostępu jest dostarczany z grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="2e256-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="2e256-108">Ten dokument zawiera szczegóły dotyczące jak chronione są hello aplikację ze sklepu utworów muzycznych w hello przykładowy szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2e256-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="2e256-109">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="2e256-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="2e256-110">Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2e256-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="2e256-111">Szablon pełną Hello można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="2e256-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="2e256-112">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="2e256-112">Public IP Address</span></span>
<span data-ttu-id="2e256-113">można tooprovide dostępu publicznego tooan zasobów platformy Azure, zasób publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="2e256-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="2e256-114">Publiczny adres IP można skonfigurować statyczny lub dynamiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="2e256-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="2e256-115">W przypadku dynamicznego adresu jest używany, a hello maszyny wirtualnej zostanie zatrzymany i alokację, adresy hello zostanie usunięte.</span><span class="sxs-lookup"><span data-stu-id="2e256-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="2e256-116">Po ponownym uruchomieniu komputera hello może można przypisać inny publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="2e256-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="2e256-117">tooprevent jako IP adresu z zmiana, zastrzeżonego adresu IP może być używany.</span><span class="sxs-lookup"><span data-stu-id="2e256-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="2e256-118">Publiczny adres IP można dodać szablon usługi Azure Resource Manager tooan przy użyciu hello Visual Studio nowego Kreatora dodawania zasobów, lub przez wstawienie poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="2e256-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="2e256-119">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [publicznego adresu IP](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="2e256-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

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

<span data-ttu-id="2e256-120">Publiczny adres IP może być skojarzona z wirtualną kartę sieciową lub równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2e256-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="2e256-121">W tym przykładzie ponieważ hello magazynu utworów muzycznych witryny sieci Web jest równoważone między kilka maszyn wirtualnych, hello publiczny adres IP jest dołączona toohello moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2e256-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="2e256-122">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenie publicznego adresu IP usługi równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="2e256-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="2e256-123">Witaj publicznego adresu IP jako odebrane przez hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2e256-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="2e256-124">Zwróć uwagę, czy hello publicznego adresu IP usługi równoważenia obciążenia skojarzone tooa i nie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e256-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="2e256-125">Moduły równoważenia obciążenia sieciowego są szczegółowo opisane w dokumencie dalej hello tej serii.</span><span class="sxs-lookup"><span data-stu-id="2e256-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Publiczny adres IP](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="2e256-127">Aby uzyskać więcej informacji na publiczne adresy IP platformy Azure, zobacz [adresów IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2e256-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="2e256-128">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="2e256-128">Network Security Group</span></span>
<span data-ttu-id="2e256-129">Po dostępu do zasobów ustalonych tooAzure, ten dostęp powinien być ograniczony.</span><span class="sxs-lookup"><span data-stu-id="2e256-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="2e256-130">Dla maszyn wirtualnych platformy Azure bezpieczny dostęp odbywa się za pomocą grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="2e256-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="2e256-131">Z przykładowych aplikacji sklepu utworów muzycznych hello wszystkie maszyny wirtualnej toohello dostęp jest ograniczony z wyjątkiem przez port 80 dla dostępu http i portu 3389 protokołu RDP dostępu.</span><span class="sxs-lookup"><span data-stu-id="2e256-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="2e256-132">Szablon usługi Azure Resource Manager tooan przy użyciu hello Visual Studio Dodaj Kreatora nowego zasobu, można dodać sieciowej grupy zabezpieczeń lub przez wstawienie poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="2e256-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="2e256-133">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [sieciowej grupy zabezpieczeń](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="2e256-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

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

<span data-ttu-id="2e256-134">W tym przykładzie hello sieciowej grupy zabezpieczeń jest skojarzony z obiektem podsieci hello zadeklarowany w hello zasobów sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e256-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="2e256-135">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenia sieciowej grupy zabezpieczeń z siecią wirtualną](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="2e256-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

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

<span data-ttu-id="2e256-136">Oto, jakie grupy zabezpieczeń sieci hello wygląda z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2e256-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="2e256-137">Należy zauważyć, że grupy NSG można skojarzyć z interfejsem podsieć i / lub sieci.</span><span class="sxs-lookup"><span data-stu-id="2e256-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="2e256-138">W takim przypadku hello NSG jest skojarzona tooa podsieci.</span><span class="sxs-lookup"><span data-stu-id="2e256-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="2e256-139">W tej konfiguracji hello reguł ruchu przychodzącego Zastosuj tooall maszyny wirtualne podłączone toohello podsieci.</span><span class="sxs-lookup"><span data-stu-id="2e256-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Grupy zabezpieczeń sieci](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="2e256-141">Aby uzyskać szczegółowe informacje na temat grup zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="2e256-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="2e256-142">Następny krok</span><span class="sxs-lookup"><span data-stu-id="2e256-142">Next step</span></span>
<hr>

[<span data-ttu-id="2e256-143">Krok 3 — dostępności i skalowalności w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e256-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

