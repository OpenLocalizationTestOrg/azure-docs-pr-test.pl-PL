---
title: "aaaAvailability i skali w szablonach Menedżera zasobów Azure | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="cd116-103">Dostępności i skalowalności w szablonach usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cd116-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="cd116-104">Dostępności i skalowalności można znaleźć toouptime i hello żądanie toomeet możliwości.</span><span class="sxs-lookup"><span data-stu-id="cd116-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="cd116-105">Jeśli aplikacja musi być 99,9% czasu hello, musi on toohave architekturę, która zezwala na wiele zasobów obliczeniowych współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="cd116-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="cd116-106">Na przykład zamiast jedną witrynę sieci Web, konfiguracji na wyższym poziomie dostępności zawiera wiele wystąpień hello lokacji sam równoważenia technologii przed ich.</span><span class="sxs-lookup"><span data-stu-id="cd116-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="cd116-107">W tej konfiguracji jedno wystąpienie aplikacji hello może być przełączona w tryb konserwacji, hello pozostałych nadal toofunction.</span><span class="sxs-lookup"><span data-stu-id="cd116-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="cd116-108">Skala na powitania drugiej odwołuje się tooan aplikacji możliwość tooserve żądanie.</span><span class="sxs-lookup"><span data-stu-id="cd116-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="cd116-109">Z obciążeniem zrównoważonym aplikacji, dodawanie lub usuwanie wystąpienia z puli hello umożliwia żądanie toomeet tooscale aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd116-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="cd116-110">Ten dokument zawiera szczegóły dotyczące konfiguracji hello magazynu utworów muzycznych Przykładowe wdrożenie dla dostępności i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="cd116-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="cd116-111">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="cd116-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="cd116-112">Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd116-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="cd116-113">Szablon pełną Hello można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="cd116-113">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="cd116-114">Zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="cd116-114">Availability Set</span></span>
<span data-ttu-id="cd116-115">Logicznie zestawu dostępności obejmuje maszyny wirtualne Azure na hostach fizycznych i inne infrastrukturalne składniki, takie jak zasilacze i fizyczny sprzęt sieciowy.</span><span class="sxs-lookup"><span data-stu-id="cd116-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="cd116-116">Zestawy dostępności upewnij się, że podczas konserwacji, Niepowodzenie urządzenia lub innych czas przestoju, nie wszystkie maszyny wirtualne są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="cd116-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="cd116-117">Zestawu dostępności może zostać dodana szablonu usługi Azure Resource Manager tooan przy użyciu hello Visual Studio Kreatora dodawania nowych zasobów lub wstawianie poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="cd116-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="cd116-118">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [zestawu dostępności](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="cd116-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="cd116-119">Zestawu dostępności jest zadeklarowana jako właściwość zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd116-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="cd116-120">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [zestawu dostępności skojarzenia z maszyną wirtualną](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="cd116-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="cd116-121">dostępność Hello ustawione jako odebrane przez hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd116-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="cd116-122">Poszczególnych maszyn wirtualnych i szczegółowe informacje o konfiguracji hello są szczegółowo opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="cd116-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Zestaw dostępności](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="cd116-124">Aby uzyskać szczegółowe informacje na temat zestawów dostępności, zobacz [Zarządzanie dostępnością maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd116-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="cd116-125">Moduł równoważenia obciążenia sieciowego</span><span class="sxs-lookup"><span data-stu-id="cd116-125">Network Load Balancer</span></span>
<span data-ttu-id="cd116-126">Zestaw dostępności zapewnia odporność na uszkodzenia aplikacji, usługi równoważenia obciążenia udostępnia wiele wystąpień aplikacji hello na jednego adresu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="cd116-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="cd116-127">Wiele wystąpień aplikacji może być hostowana na wiele maszyn wirtualnych, każda z nich połączony tooa modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="cd116-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="cd116-128">Jak uzyskiwania dostępu do aplikacji hello trasy modułu równoważenia obciążenia hello hello przychodzące żądanie między hello dołączone elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="cd116-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="cd116-129">Usługi równoważenia obciążenia można dodać przy użyciu hello Visual Studio Kreatora dodawania nowych zasobów lub wstawiając prawidłowo sformatowane JSON zasobów do szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="cd116-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="cd116-130">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [Usługa równoważenia obciążenia sieciowego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="cd116-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="cd116-131">Ponieważ hello Przykładowa aplikacja jest narażonych toohello Internetu z publicznym adresem IP, ten adres jest skojarzony z usługą równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="cd116-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="cd116-132">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [skojarzenia Usługa równoważenia obciążenia sieciowego z publicznym adresem IP](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="cd116-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="cd116-133">Z hello portalu Azure hello usługi równoważenia obciążenia sieciowego — omówienie pokazuje hello skojarzenie z hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="cd116-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Moduł równoważenia obciążenia sieciowego](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="cd116-135">Reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="cd116-135">Load Balancer Rule</span></span>
<span data-ttu-id="cd116-136">Podczas korzystania z usługi równoważenia obciążenia, skonfigurowanych reguł kontrolujących sposób ruch jest równoważone między hello przeznaczone zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd116-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="cd116-137">Z aplikacją ze sklepu utworów muzycznych próbki hello ruch dociera na porcie 80 hello publicznego adresu IP i jest dystrybuowana do portu 80 wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cd116-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="cd116-138">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [reguły modułu równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="cd116-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

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

<span data-ttu-id="cd116-139">Widok sieci hello reguła modułu równoważenia obciążenia z hello portalu.</span><span class="sxs-lookup"><span data-stu-id="cd116-139">A view of hello network load balancer rule from hello portal.</span></span>

![Reguły modułu równoważenia obciążenia sieciowego](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="cd116-141">Sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="cd116-141">Load Balancer Probe</span></span>
<span data-ttu-id="cd116-142">usługi równoważenia obciążenia Hello musi także toomonitor każdej maszyny wirtualnej tak, aby żądania są obsługiwane tylko toorunning systemów.</span><span class="sxs-lookup"><span data-stu-id="cd116-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="cd116-143">Monitorowanie odbywa się przez sondowanie stałej wstępnie zdefiniowanego portu.</span><span class="sxs-lookup"><span data-stu-id="cd116-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="cd116-144">Wdrażanie magazynu utworów muzycznych Hello jest maszyn wirtualnych skonfigurowanych tooprobe port 80 na wszystkie zawarte.</span><span class="sxs-lookup"><span data-stu-id="cd116-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="cd116-145">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [sondy modułu równoważenia obciążenia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="cd116-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

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

<span data-ttu-id="cd116-146">Witaj odebrane przez hello portalu Azure sondę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="cd116-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Sondę modułu równoważenia obciążenia sieciowego](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="cd116-148">Reguły NAT dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="cd116-148">Inbound NAT Rules</span></span>
<span data-ttu-id="cd116-149">Podczas korzystania z usługi równoważenia obciążenia, zasady muszą toobe umieszczane w miejscu, które zapewniają dostęp równoważeniem obciążenia z systemem innym niż tooeach maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd116-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="cd116-150">Na przykład podczas tworzenia połączenia RDP z każdej maszyny wirtualnej, tego rodzaju ruch, nie powinien być równoważone, a nie powinno być konfigurowane wstępnie określoną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="cd116-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="cd116-151">wstępnie określoną ścieżki są skonfigurowane przy użyciu reguły NAT ruchu przychodzącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="cd116-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="cd116-152">Za pomocą tego zasobu, komunikacji przychodzącej mogą być mapowane tooindividual maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cd116-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="cd116-153">Z hello aplikację ze sklepu muzyki port, zaczynając od 5000 jest mapowanych tooport 3389 na każdej maszynie wirtualnej dostępu RDP.</span><span class="sxs-lookup"><span data-stu-id="cd116-153">With hello Music Store application, a port starting at 5000 is mapped tooport 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="cd116-154">Witaj `copyindex()` tooincrement używana jest funkcja hello przychodzący port, taki sposób, że hello drugiej maszyny wirtualnej odbiera przychodzący port 5001 hello trzeci 5002 i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="cd116-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span>

<span data-ttu-id="cd116-155">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [reguły NAT ruchu przychodzącego](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="cd116-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
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
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="cd116-156">Przykładem przychodzącej reguły NAT jako hello w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd116-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="cd116-157">Dla każdej maszyny wirtualnej we wdrożeniu hello tworzona jest reguła RDP NAT.</span><span class="sxs-lookup"><span data-stu-id="cd116-157">An RDP NAT rule is created for each virtual machine in hello deployment.</span></span>

![Reguły NAT ruchu przychodzącego](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="cd116-159">Aby uzyskać szczegółowe informacje na temat hello Azure Usługa równoważenia obciążenia sieciowego, zobacz [równoważenia obciążenia dla usług infrastruktury platformy Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd116-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="cd116-160">Wdrażanie wielu maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="cd116-160">Deploy multiple VMs</span></span>
<span data-ttu-id="cd116-161">Ponadto dla funkcję tooeffectively zestawu dostępności lub równoważenia obciążenia wielu maszyn wirtualnych są wymagane.</span><span class="sxs-lookup"><span data-stu-id="cd116-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="cd116-162">Wiele maszyn wirtualnych można wdrożyć przy użyciu funkcji kopiowania szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="cd116-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="cd116-163">Przy użyciu funkcji kopiowania hello, nie jest konieczne toodefine skończoną liczbę maszyn wirtualnych, zamiast tej wartości można dynamicznie udostępniać w czasie hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="cd116-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="cd116-164">Funkcja kopiowania Hello zużywa hello liczbę wystąpień toobe utworzone i uchwytów wdrażanie hello poprawną liczbę maszyn wirtualnych i skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd116-164">hello copy function consumes hello number of instances toobe created and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="cd116-165">W szablonie próbki magazynu utworów muzycznych hello parametr jest zdefiniowany przyjmującego liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="cd116-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="cd116-166">Numer ten jest używany w całym hello szablonu podczas tworzenia maszyn wirtualnych i powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd116-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

<span data-ttu-id="cd116-167">Na hello zasobu maszyny wirtualnej pętlę kopiowania hello podano nazwę i toocontrol hello liczbę kopii wynikowy używany numer hello wystąpienia parametru.</span><span class="sxs-lookup"><span data-stu-id="cd116-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="cd116-168">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [funkcji kopiowania maszyny wirtualnej](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="cd116-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="cd116-169">Hello bieżącą iterację funkcji kopiowania hello jest możliwy z hello `copyIndex()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd116-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="cd116-170">wartość Hello hello kopiowania indeksu funkcji może być używane tooname maszyn wirtualnych i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd116-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="cd116-171">Na przykład jeśli są wdrażane dwa wystąpienia maszyny wirtualnej, muszą różne nazwy.</span><span class="sxs-lookup"><span data-stu-id="cd116-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="cd116-172">Witaj `copyIndex()` funkcja może być używana jako część maszyny wirtualnej hello nazwa toocreate unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="cd116-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="cd116-173">Przykład Witaj `copyindex()` funkcja używany na potrzeby nazywania celów można wyświetlić w hello zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd116-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="cd116-174">W tym miejscu hello nazwa komputera jest złączeniem hello `vmName` parametr i hello `copyIndex()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd116-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="cd116-175">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [funkcji indeksu kopiowania](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="cd116-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="cd116-176">Witaj `copyIndex` funkcja jest używana wiele razy w hello magazynu utworów muzycznych przykładowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="cd116-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="cd116-177">Zasobów i funkcji przy użyciu `copyIndex` obejmują tooa cokolwiek określonego pojedynczego wystąpienia maszyny wirtualnej hello takie i interfejsu sieciowego, reguły modułu równoważenia obciążenia, oraz dowolne zależy od funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd116-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="cd116-178">Aby uzyskać więcej informacji o funkcji kopiowania hello, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cd116-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="cd116-179">Następny krok</span><span class="sxs-lookup"><span data-stu-id="cd116-179">Next step</span></span>
<hr>

[<span data-ttu-id="cd116-180">Krok 4. wdrożenie aplikacji z szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cd116-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

