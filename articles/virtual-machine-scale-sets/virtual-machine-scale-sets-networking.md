---
title: "Obsługa sieci w kontekście zestawów skalowania maszyn wirtualnych platformy Azure | Microsoft Docs"
description: "Właściwości sieciowe konfiguracji dotyczące zestawów skalowania maszyn wirtualnych platformy Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="e39ec-103">Obsługa sieci w kontekście zestawów skalowania maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e39ec-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="e39ec-104">W przypadku wdrażania zestawu skalowania maszyn wirtualnych platformy Azure za pośrednictwem portalu, niektóre właściwości sieciowe są konfigurowane domyślnie, na przykład usługa Azure Load Balancer z regułami NAT dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="e39ec-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="e39ec-105">W tym artykule opisano, jak korzystać z niektórych bardziej zaawansowanych funkcji sieciowych konfigurowalnych za pomocą zestawów skalowania.</span><span class="sxs-lookup"><span data-stu-id="e39ec-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="e39ec-106">Wszystkie funkcje omówione w tym artykule można skonfigurować za pomocą szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e39ec-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="e39ec-107">Dla wybranych funkcji dołączono też przykłady związane z interfejsem wiersza polecenia platformy Azure i programem PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e39ec-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="e39ec-108">Użyj interfejsu wiersza polecenia w wersji 2.10 i programu PowerShell 4.2.0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="e39ec-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="e39ec-109">Accelerated Networking</span><span class="sxs-lookup"><span data-stu-id="e39ec-109">Accelerated Networking</span></span>
<span data-ttu-id="e39ec-110">Usługa Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) zwiększa wydajność sieci, umożliwiając wirtualizację we/wy z jednym elementem głównym (SR-IOV) do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e39ec-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="e39ec-111">Aby korzystać z tej funkcji przyspieszania sieci wraz z zestawami skalowania, w ustawieniach networkInterfaceConfigurations zestawu skalowania ustaw dla właściwości enableAcceleratedNetworking wartość **true**.</span><span class="sxs-lookup"><span data-stu-id="e39ec-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="e39ec-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="e39ec-113">Tworzenie zestawu skalowania odwołującego się do istniejącej usługi Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e39ec-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="e39ec-114">Podczas tworzenia zestawu skalowania przy użyciu witryny Azure Portal w przypadku większości opcji konfiguracji jest tworzony nowy moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e39ec-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="e39ec-115">W przypadku utworzenia zestawu skalowania, który musi odwoływać się do istniejącego modułu równoważenia obciążenia, można to zrobić przy użyciu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e39ec-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="e39ec-116">Następujący skrypt przykładowy tworzy moduł równoważenia obciążenia, a następnie tworzy zestaw skalowania, który się do niego odwołuje:</span><span class="sxs-lookup"><span data-stu-id="e39ec-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="e39ec-117">Konfigurowalne ustawienia DNS</span><span class="sxs-lookup"><span data-stu-id="e39ec-117">Configurable DNS Settings</span></span>
<span data-ttu-id="e39ec-118">Domyślnie zestawy skalowania przyjmują konkretne ustawienia DNS sieci VNET i podsieci, w których je utworzono.</span><span class="sxs-lookup"><span data-stu-id="e39ec-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="e39ec-119">Można jednak skonfigurować ustawienia DNS zestawu skalowania bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e39ec-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="e39ec-120">Tworzenie zestawu skalowania z konfigurowalnymi serwerami DNS</span><span class="sxs-lookup"><span data-stu-id="e39ec-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="e39ec-121">Aby utworzyć zestaw skalowania z niestandardową konfiguracją DNS przy użyciu interfejsu wiersza polecenia w wersji 2.0, dodaj do polecenia **vmss create** argument **--dns-servers**, a po nim podaj oddzielane spacjami adresy IP serwerów.</span><span class="sxs-lookup"><span data-stu-id="e39ec-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="e39ec-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="e39ec-123">Aby skonfigurować niestandardowe serwery DNS w szablonie platformy Azure, do sekcji networkInterfaceConfigurations zestawu skalowania dodaj właściwość dnsSettings.</span><span class="sxs-lookup"><span data-stu-id="e39ec-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="e39ec-124">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="e39ec-125">Tworzenie zestawu skalowania z konfigurowalnymi nazwami domen maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="e39ec-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="e39ec-126">Aby utworzyć zestaw skalowania z niestandardową nazwą DNS maszyn wirtualnych przy użyciu interfejsu wiersza polecenia w wersji 2.0, dodaj do polecenia **vmss create** argument **--vm-domain-name**, a po nim podaj ciąg reprezentujący nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="e39ec-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="e39ec-127">Aby ustawić nazwę domeny w szablonie platformy Azure, do sekcji **networkInterfaceConfigurations** zestawu skalowania dodaj właściwość **dnsSettings**.</span><span class="sxs-lookup"><span data-stu-id="e39ec-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="e39ec-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="e39ec-129">Dane wyjściowe dla nazwy DNS pojedynczej maszyny wirtualnej będą miały następującą formę:</span><span class="sxs-lookup"><span data-stu-id="e39ec-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="e39ec-130">Publiczny adres IPv4 dla każdej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e39ec-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="e39ec-131">Ogólnie maszyny wirtualne zestawu skalowania platformy Azure nie muszą mieć własnych publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e39ec-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="e39ec-132">W przypadku większości scenariuszy najekonomiczniejszym i najbezpieczniejszym rozwiązaniem jest skojarzenie publicznego adresu IP z modułem równoważenia obciążenia lub konkretną maszyną wirtualną, która kieruje połączenia przychodzące do maszyn wirtualnych zestawu skalowania zgodnie z potrzebami (na przykład za pomocą reguł NAT dla ruchu przychodzącego).</span><span class="sxs-lookup"><span data-stu-id="e39ec-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="e39ec-133">Jednak w niektórych scenariuszach maszyny wirtualne zestawu skalowania muszą mieć własne publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="e39ec-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="e39ec-134">Przykładem są gry — gdy konsola musi nawiązać bezpośrednie połączenie z maszyną wirtualną w chmurze obsługującą przetwarzanie symulacji świata fizycznego w grze.</span><span class="sxs-lookup"><span data-stu-id="e39ec-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="e39ec-135">Innym przykładem jest sytuacja, w której maszyny wirtualne muszą nawiązywać ze sobą połączenia zewnętrzne między regionami w rozproszonej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e39ec-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="e39ec-136">Tworzenie zestawu skalowania z publicznym adresem IP dla każdej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e39ec-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="e39ec-137">Aby utworzyć zestaw skalowania, w którym każdej maszynie wirtualnej zostanie przypisany publiczny adres IP, przy użyciu interfejsu wiersza polecenia w wersji 2.0, dodaj do polecenia **vmss create** parametr **--public-ip-per-vm**.</span><span class="sxs-lookup"><span data-stu-id="e39ec-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="e39ec-138">Aby utworzyć zestaw skalowania przy użyciu szablonu platformy Azure, upewnij się, że interfejs API zasobu Microsoft.Compute/virtualMachineScaleSets ma wersję co najmniej **2017-03-30**, i dodaj właściwość JSON **publicIpAddressConfiguration** do sekcji ipConfigurations zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="e39ec-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="e39ec-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="e39ec-140">Przykład szablonu: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="e39ec-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="e39ec-141">Badanie publicznych adresów IP maszyn wirtualnych w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="e39ec-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="e39ec-142">Aby uzyskać listę publicznych adresów IP przypisanych do maszyn wirtualnych w zestawie skalowania przy użyciu interfejsu wiersza polecenia w wersji 2.0, użyj polecenia **az vmss list-instance-public-ips**.</span><span class="sxs-lookup"><span data-stu-id="e39ec-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="e39ec-143">Aby uzyskać listę publicznych adresów IP zestawu skalowania przy użyciu programu PowerShell, użyj polecenia _Get-AzureRmPublicIpAddress_.</span><span class="sxs-lookup"><span data-stu-id="e39ec-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="e39ec-144">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="e39ec-145">Publiczne adresy IP można także badać, odwołując się bezpośrednio do identyfikatora zasobu konfiguracji adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e39ec-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="e39ec-146">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="e39ec-147">Aby zbadać publiczne adresy IP przypisane do maszyn wirtualnych w zestawie skalowania, użyj witryny [Azure Resource Explorer](https://resources.azure.com) lub interfejsu Azure REST API w wersji co najmniej **2017-03-30**.</span><span class="sxs-lookup"><span data-stu-id="e39ec-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="e39ec-148">Aby sprawdzić publiczne adresy IP zestawu skalowania za pomocą witryny Resource Explorer, zajrzyj do sekcji **publicipaddresses** danego zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="e39ec-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="e39ec-149">Na przykład: https://resources.azure.com/subscriptions/_identyfikator_zasobu_/resourceGroups/_grupa_zasobów_/providers/Microsoft.Compute/virtualMachineScaleSets/_zestaw_skalowania_maszyn_wirtualnych_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="e39ec-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="e39ec-150">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e39ec-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="e39ec-151">Wiele adresów IP dla każdej karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="e39ec-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="e39ec-152">Z każdą kartą sieciową dołączoną do maszyny wirtualnej w zestawie skalowania może być skojarzona co najmniej jedna konfiguracja adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e39ec-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="e39ec-153">Każdej konfiguracji jest przypisany jeden prywatny adres IP.</span><span class="sxs-lookup"><span data-stu-id="e39ec-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="e39ec-154">Każda konfiguracja może mieć również skojarzony jeden zasób publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e39ec-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="e39ec-155">Aby zrozumieć, jak wiele adresów IP można przypisać do karty sieciowej i jak wielu publicznych adresów IP można używać w subskrypcji platformy Azure, zapoznaj się z [informacjami o limitach na platformie Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="e39ec-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="e39ec-156">Wiele kart sieciowych dla każdej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e39ec-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="e39ec-157">Zależnie od rozmiaru maszyny wirtualnej każda z nich może mieć do 8 kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="e39ec-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="e39ec-158">Maksymalna liczba kart sieciowych na maszynę jest podana w [artykule poświęconym rozmiarom maszyn wirtualnych](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e39ec-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="e39ec-159">Poniższej przedstawiono przykład profilu sieciowego zestawu skalowania z wieloma wpisami kart sieciowych oraz wieloma publicznymi adresami IP związanymi z poszczególnymi maszynami wirtualnymi:</span><span class="sxs-lookup"><span data-stu-id="e39ec-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="e39ec-160">Sieciowa grupa zabezpieczeń dla zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="e39ec-160">NSG per scale set</span></span>
<span data-ttu-id="e39ec-161">Grupy zabezpieczeń sieci można stosować bezpośrednio do zestawu skalowania przez dodanie odwołania w sekcji konfiguracji interfejsu sieciowego we właściwościach maszyn wirtualnych zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="e39ec-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="e39ec-162">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e39ec-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="e39ec-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e39ec-163">Next steps</span></span>
<span data-ttu-id="e39ec-164">Aby uzyskać więcej informacji o sieciach wirtualnych platformy Azure, zapoznaj się z [tą dokumentacją](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e39ec-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
