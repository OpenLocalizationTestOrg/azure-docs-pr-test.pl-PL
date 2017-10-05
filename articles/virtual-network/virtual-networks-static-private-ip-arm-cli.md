---
title: "Konfigurowanie prywatnych adresów IP dla maszyn wirtualnych - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować prywatnych adresów IP maszyn wirtualnych za pomocą interfejsu wiersza polecenia platformy Azure (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="bbdc4-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej z wykorzystaniem 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bbdc4-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bbdc4-104">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="bbdc4-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="bbdc4-105">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="bbdc4-106">[Interfejs wiersza polecenia platformy Azure w wersji 1.0](virtual-networks-static-private-ip-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="bbdc4-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="bbdc4-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -naszej nowej generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="bbdc4-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bbdc4-108">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="bbdc4-109">Możesz również [Zarządzanie statycznego prywatnego adresu IP w klasycznym modelu wdrażania](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bbdc4-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="bbdc4-110">Poniższe przykładowe polecenia Azure CLI 2.0 oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="bbdc4-111">Aby uruchomić polecenia wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bbdc4-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="bbdc4-112">Określanie statycznego prywatnego adresu IP podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bbdc4-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="bbdc4-113">Aby utworzyć Maszynę wirtualną o nazwie *DNS01* w *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="bbdc4-114">Jeśli nie zostało jeszcze, instalowania i konfigurowania najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się do platformy Azure konta przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bbdc4-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="bbdc4-115">Tworzenie publicznego adresu IP dla maszyny Wirtualnej z [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="bbdc4-116">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bbdc4-117">Może być lub muszą używać różnych wartości argumentów w tej i kolejnych krokach, w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="bbdc4-118">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="bbdc4-119">`--resource-group`: Nazwa grupy zasobów, w której chcesz utworzyć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="bbdc4-120">`--name`: Nazwa publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="bbdc4-121">`--location`: Region platformy azure, w której chcesz utworzyć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="bbdc4-122">Uruchom [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create) polecenie, aby utworzyć z kartą Sieciową za pomocą statycznego prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="bbdc4-123">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="bbdc4-124">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="bbdc4-125">Parametry:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-125">Parameters:</span></span>

    * <span data-ttu-id="bbdc4-126">`--private-ip-address`: Statycznego prywatnego adresu IP dla karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="bbdc4-127">`--vnet-name`: Nazwa sieci wirtualnej, w której chcesz utworzyć karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="bbdc4-128">`--subnet`: Nazwa podsieci, w której chcesz utworzyć karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="bbdc4-129">Uruchom [tworzenia maszyny wirtualnej azure](/cli/azure/vm/nic#create) polecenie, aby utworzyć maszynę Wirtualną za pomocą publicznego adresu IP i NIC utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="bbdc4-130">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-130">The list shown after the output explains the parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="bbdc4-131">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="bbdc4-132">Parametrów innych niż podstawowe [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) parametrów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="bbdc4-133">`--nics`: Nazwa karty Sieciowej, do której jest dołączona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="bbdc4-134">Pobrać statycznych prywatne informacje o adresie IP dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bbdc4-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="bbdc4-135">Aby wyświetlić statycznego prywatnego adresu IP, który został utworzony, uruchom następujące polecenie z wiersza polecenia platformy Azure i sprawdź wartości *metody alokacji prywatnego adresu IP* i *prywatny adres IP*:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="bbdc4-136">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="bbdc4-137">Aby wyświetlić określone informacje IP karty interfejsu sieciowego dla tej maszyny Wirtualnej, w szczególności kwerendy karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="bbdc4-138">Dane wyjściowe wyglądają mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="bbdc4-139">Usuń statycznego prywatnego adresu IP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bbdc4-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="bbdc4-140">Nie można usunąć statycznego prywatnego adresu IP z karty Sieciowej w wiersza polecenia platformy Azure dla wdrożenia Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="bbdc4-141">Należy:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-141">You must:</span></span>
- <span data-ttu-id="bbdc4-142">Utwórz nowy kartę Sieciową, która korzysta z dynamicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="bbdc4-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="bbdc4-143">Ustawić karty Sieciowej dla maszyny Wirtualnej nowo utworzonej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="bbdc4-144">Aby zmienić karty Sieciowej dla maszyny Wirtualnej, używany w powyższych poleceń, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="bbdc4-145">Uruchom **tworzenie kart interfejsu sieciowego azure** polecenie, aby utworzyć nowe przy użyciu alokacji dynamicznego adresu IP za pomocą nowego adresu IP karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="bbdc4-146">Należy pamiętać, że żaden adres IP, ponieważ określono metodę alokacji **dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="bbdc4-147">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="bbdc4-148">Uruchom **zestawu azure vm** polecenie, aby zmienić używane przez maszynę Wirtualną kartę Sieciową.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="bbdc4-149">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bbdc4-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="bbdc4-150">Jeśli maszyna wirtualna jest wystarczająco duży, aby mieć więcej niż jedną kartę Sieciową, uruchom **usunąć kart interfejsu sieciowego azure** polecenie, aby usunąć stare karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="bbdc4-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbdc4-151">Next steps</span></span>
* <span data-ttu-id="bbdc4-152">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bbdc4-153">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="bbdc4-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bbdc4-154">Zapoznaj się [zastrzeżone interfejsów API REST IP](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbdc4-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

