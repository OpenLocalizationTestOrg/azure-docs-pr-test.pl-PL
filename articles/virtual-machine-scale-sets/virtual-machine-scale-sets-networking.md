---
title: aaaNetworking dla zestawy skalowania maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="5e650-103">Obsługa sieci w kontekście zestawów skalowania maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5e650-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="5e650-104">Podczas wdrażania zestaw za pośrednictwem portalu hello skalowania maszyny wirtualnej platformy Azure, jest konfigurowanych domyślnie niektóre właściwości sieci, na przykład modułu równoważenia obciążenia Azure z reguły dla ruchu przychodzącego translatora adresów Sieciowych.</span><span class="sxs-lookup"><span data-stu-id="5e650-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="5e650-105">W tym artykule opisano sposób ustawiania toouse niektóre hello bardziej zaawansowane funkcje sieciowe, które można skonfigurować skali.</span><span class="sxs-lookup"><span data-stu-id="5e650-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="5e650-106">Można skonfigurować wszystkie funkcje hello omówione w tym artykule przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5e650-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="5e650-107">Dla wybranych funkcji dołączono też przykłady związane z interfejsem wiersza polecenia platformy Azure i programem PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e650-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="5e650-108">Użyj interfejsu wiersza polecenia w wersji 2.10 i programu PowerShell 4.2.0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="5e650-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="5e650-109">Accelerated Networking</span><span class="sxs-lookup"><span data-stu-id="5e650-109">Accelerated Networking</span></span>
<span data-ttu-id="5e650-110">Azure [przyspieszony sieci](../virtual-network/virtual-network-create-vm-accelerated-networking.md) zwiększa wydajność sieci, umożliwiając maszyny wirtualnej tooa (SR-IOV) wirtualizacji we/wy pojedynczego elementu głównego.</span><span class="sxs-lookup"><span data-stu-id="5e650-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="5e650-111">przyspieszony toouse sieć z zestawy skalowania, ustaw enableAcceleratedNetworking zbyt**true** w ustawieniach Networkinterfaceconfiguration zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="5e650-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="5e650-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="5e650-113">Tworzenie zestawu skalowania odwołującego się do istniejącej usługi Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5e650-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="5e650-114">Po utworzeniu zestawu skalowania za pomocą portalu Azure hello nowego modułu równoważenia obciążenia jest tworzony dla większości opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5e650-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="5e650-115">Jeśli utworzysz zestaw skali, którą należy tooreference istniejący moduł równoważenia obciążenia, można to zrobić przy użyciu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e650-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="5e650-116">powitania po przykładowy skrypt tworzy moduł równoważenia obciążenia, a następnie tworzy zestaw skali, który odwołuje się ona:</span><span class="sxs-lookup"><span data-stu-id="5e650-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="5e650-117">Konfigurowalne ustawienia DNS</span><span class="sxs-lookup"><span data-stu-id="5e650-117">Configurable DNS Settings</span></span>
<span data-ttu-id="5e650-118">Domyślnie zestawy skalowania przełączyć na powitania określonych ustawień DNS hello sieci Wirtualnej i podsieci, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="5e650-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="5e650-119">Można jednak skonfigurować hello ustawień DNS na potrzeby skalowania ustawić bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="5e650-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="5e650-120">Tworzenie zestawu skalowania z konfigurowalnymi serwerami DNS</span><span class="sxs-lookup"><span data-stu-id="5e650-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="5e650-121">toocreate zestawu skalowania z niestandardowej konfiguracji DNS przy użyciu interfejsu wiersza polecenia 2.0, Dodaj hello **serwery dns —** argument toohello **vmss utworzyć** polecenia, a następnie miejsca oddzielone adresów ip serwerów.</span><span class="sxs-lookup"><span data-stu-id="5e650-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="5e650-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="5e650-123">tooconfigure niestandardowych serwerów DNS w szablonu platformy Azure, Dodaj sekcji Networkinterfaceconfiguration zestawu skalowania toohello dnsSettings właściwości.</span><span class="sxs-lookup"><span data-stu-id="5e650-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="5e650-124">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="5e650-125">Tworzenie zestawu skalowania z konfigurowalnymi nazwami domen maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="5e650-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="5e650-126">toocreate zestawu skalowania z niestandardowej nazwy DNS dla maszyn wirtualnych przy użyciu interfejsu wiersza polecenia 2.0, Dodaj hello **nazwa domeny maszyny wirtualnej —** argument toohello **vmss utworzyć** polecenia następuje ciąg reprezentujący hello nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="5e650-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="5e650-127">Dodaj nazwę domeny hello tooset w szablonu Azure **dnsSettings** zestaw skali toohello właściwości **Networkinterfaceconfiguration** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5e650-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="5e650-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-128">For example:</span></span>

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

<span data-ttu-id="5e650-129">Hello danych wyjściowych dla poszczególnych maszyn wirtualnych nazwy dns, należy w hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="5e650-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="5e650-130">Publiczny adres IPv4 dla każdej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5e650-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="5e650-131">Ogólnie maszyny wirtualne zestawu skalowania platformy Azure nie muszą mieć własnych publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="5e650-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="5e650-132">W przypadku większości scenariuszy jest bardziej ekonomiczne i bezpieczne tooassociate publicznego adresu IP adres tooa obciążenia równoważenia lub tooan poszczególnych maszyn wirtualnych (alias jumpbox), który kieruje przychodzących połączeń tooscale zestaw maszyn wirtualnych, zgodnie z potrzebami (na przykład za pomocą reguły NAT ruchu przychodzącego).</span><span class="sxs-lookup"><span data-stu-id="5e650-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="5e650-133">Jednak w niektórych scenariuszach wymagane zestawu skalowania maszyn wirtualnych toohave własnych publicznego adresu IP adresów.</span><span class="sxs-lookup"><span data-stu-id="5e650-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="5e650-134">Przykładem jest gry, gdy konsola musi toomake bezpośrednie połączenie tooa chmury maszynę wirtualną, która wykonuje przetwarzanie gier fizycznych.</span><span class="sxs-lookup"><span data-stu-id="5e650-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="5e650-135">Innym przykładem jest, gdy maszyny wirtualne muszą tooone połączeń zewnętrznych toomake innego w regionach w rozproszoną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="5e650-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="5e650-136">Tworzenie zestawu skalowania z publicznym adresem IP dla każdej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5e650-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="5e650-137">toocreate zestaw skali, który przypisuje publicznego adresu IP adres tooeach maszynę wirtualną z 2.0 interfejsu wiersza polecenia Dodaj hello **--publicznego adresu ip na wirtualna** toohello parametru **vmss utworzyć** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e650-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="5e650-138">toocreate skali ustawiane przy użyciu szablonu platformy Azure, upewnij się, że wersja hello interfejsu API hello Microsoft.Compute/virtualMachineScaleSets zasobów jest co najmniej **2017-03-30**i Dodaj **publicIpAddressConfiguration**JSON właściwości toohello zestawu skalowania maszyny wirtualnej sekcji elementów Ipconfiguration.</span><span class="sxs-lookup"><span data-stu-id="5e650-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="5e650-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="5e650-140">Przykład szablonu: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="5e650-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="5e650-141">Podczas badania hello publiczny adres IP zestawu adresów hello maszyn wirtualnych w skali</span><span class="sxs-lookup"><span data-stu-id="5e650-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="5e650-142">Witaj toolist publiczne adresy IP przypisane tooscale zestaw maszyn wirtualnych przy użyciu interfejsu wiersza polecenia 2.0, należy użyć hello **az vmss listy wystąpienie publicznego-adresy IP** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e650-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="5e650-143">zestaw skalowania toolist publicznych adresów IP przy użyciu programu PowerShell, użyj hello _Get-AzureRmPublicIpAddress_ polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e650-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="5e650-144">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="5e650-145">Można również zapytania hello publicznych adresów IP za pomocą odwołań do identyfikatora zasobu hello hello publiczny adres IP bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="5e650-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="5e650-146">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="5e650-147">Witaj tooquery publiczne adresy IP przypisane tooscale zestaw maszyn wirtualnych za pomocą hello [Eksploratora zasobów Azure](https://resources.azure.com), lub hello z wersją interfejsu API REST Azure **2017-03-30** lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5e650-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="5e650-148">tooview publicznych adresów IP dla skalowania ustawić za pomocą Eksploratora zasobów hello przyjrzeć się hello **elementów publicipaddress** w zestawie skali sekcji.</span><span class="sxs-lookup"><span data-stu-id="5e650-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="5e650-149">Na przykład: https://resources.azure.com/subscriptions/_identyfikator_zasobu_/resourceGroups/_grupa_zasobów_/providers/Microsoft.Compute/virtualMachineScaleSets/_zestaw_skalowania_maszyn_wirtualnych_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="5e650-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="5e650-150">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5e650-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="5e650-151">Wiele adresów IP dla każdej karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="5e650-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="5e650-152">Każdej karty Sieciowej podłączony tooa maszyny Wirtualnej w zestawie skalowania może mieć co najmniej jednej konfiguracji IP skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="5e650-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="5e650-153">Każdej konfiguracji jest przypisany jeden prywatny adres IP.</span><span class="sxs-lookup"><span data-stu-id="5e650-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="5e650-154">Każda konfiguracja może mieć również skojarzony jeden zasób publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5e650-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="5e650-155">toounderstand liczbę adresów IP można przypisać tooa karty Sieciowej, i jak wiele publicznych adresów IP można używać w subskrypcji platformy Azure można znaleźć za[limity Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="5e650-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="5e650-156">Wiele kart sieciowych dla każdej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5e650-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="5e650-157">Użytkownik może zawierać maksymalnie too8 kart interfejsu sieciowego na maszynę wirtualną, w zależności od rozmiaru maszyny.</span><span class="sxs-lookup"><span data-stu-id="5e650-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="5e650-158">Witaj maksymalną liczbę kart sieciowych na komputerze jest dostępna w hello [artykułu rozmiar maszyny Wirtualnej](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="5e650-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="5e650-159">Witaj poniższy przykład jest wyświetlane wiele wpisów karty Sieciowej i wiele publicznych adresów IP na maszynę wirtualną w profilu sieci zestawu skali:</span><span class="sxs-lookup"><span data-stu-id="5e650-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="5e650-160">Sieciowa grupa zabezpieczeń dla zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="5e650-160">NSG per scale set</span></span>
<span data-ttu-id="5e650-161">Sieciowe grupy zabezpieczeń można stosować bezpośrednio tooa zestaw skali, dodając sekcję konfiguracji interfejsu sieci toohello odwołanie skali hello Ustaw właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e650-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="5e650-162">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5e650-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="5e650-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e650-163">Next steps</span></span>
<span data-ttu-id="5e650-164">Aby uzyskać więcej informacji na temat sieci wirtualnych platformy Azure można znaleźć zbyt[tej dokumentacji](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e650-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
