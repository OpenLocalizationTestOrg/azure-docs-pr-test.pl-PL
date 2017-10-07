---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych za pomocą hello Azure interfejsu wiersza polecenia (CLI) 2.0."
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
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="27eca-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej z wykorzystaniem hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="27eca-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="27eca-104">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="27eca-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="27eca-105">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="27eca-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="27eca-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="27eca-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="27eca-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="27eca-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="27eca-108">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="27eca-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="27eca-109">Możesz również [Zarządzanie statycznego prywatnego adresu IP w hello klasycznego modelu wdrażania](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="27eca-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="27eca-110">Poniższe polecenia Azure CLI 2.0 próbki Hello oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="27eca-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="27eca-111">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="27eca-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="27eca-112">Określanie statycznego prywatnego adresu IP podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="27eca-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="27eca-113">toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="27eca-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="27eca-114">Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27eca-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="27eca-115">Utwórz publiczny adres IP dla hello maszyny Wirtualnej z hello [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="27eca-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="27eca-116">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="27eca-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27eca-117">Może dokonać lub wymagane toouse różne wartości dla argumentów w tej i kolejnych krokach, w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="27eca-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="27eca-118">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="27eca-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="27eca-119">`--resource-group`: Nazwa grupy zasobów hello, w których toocreate hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="27eca-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="27eca-120">`--name`: Nazwa hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="27eca-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="27eca-121">`--location`: Region platformy azure, w których toocreate hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="27eca-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="27eca-122">Uruchom hello [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create) toocreate polecenia ze statycznego prywatnego adresu IP karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="27eca-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="27eca-123">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="27eca-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="27eca-124">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="27eca-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="27eca-125">Parametry:</span><span class="sxs-lookup"><span data-stu-id="27eca-125">Parameters:</span></span>

    * <span data-ttu-id="27eca-126">`--private-ip-address`: Statycznego prywatnego adresu IP dla hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="27eca-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="27eca-127">`--vnet-name`: Name hello sieci wirtualnej, w których toocreate hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="27eca-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="27eca-128">`--subnet`: Name hello podsieci, w których hello toocreate karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="27eca-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="27eca-129">Uruchom hello [tworzenia maszyny wirtualnej azure](/cli/azure/vm/nic#create) hello toocreate polecenia przy użyciu hello publicznego adresu IP i karty Sieciowej maszyny Wirtualnej utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="27eca-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="27eca-130">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="27eca-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="27eca-131">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="27eca-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="27eca-132">Parametrów innych niż podstawowe hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) parametrów.</span><span class="sxs-lookup"><span data-stu-id="27eca-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="27eca-133">`--nics`: Nazwa hello kart toowhich hello maszyny Wirtualnej jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="27eca-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="27eca-134">Pobrać statycznych prywatne informacje o adresie IP dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="27eca-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="27eca-135">tooview hello statycznego prywatnego adresu IP, który został utworzony, uruchom następujące polecenie z wiersza polecenia platformy Azure hello i sprawdź wartości hello *metody alokacji prywatnego adresu IP* i *prywatny adres IP*:</span><span class="sxs-lookup"><span data-stu-id="27eca-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="27eca-136">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="27eca-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="27eca-137">toodisplay hello określone informacje IP hello karty Sieciowej dla tej maszyny Wirtualnej, zapytania hello karty Sieciowej, w szczególności:</span><span class="sxs-lookup"><span data-stu-id="27eca-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="27eca-138">dane wyjściowe Hello to wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="27eca-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="27eca-139">Usuń statycznego prywatnego adresu IP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="27eca-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="27eca-140">Nie można usunąć statycznego prywatnego adresu IP z karty Sieciowej w wiersza polecenia platformy Azure dla wdrożenia Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="27eca-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="27eca-141">Należy:</span><span class="sxs-lookup"><span data-stu-id="27eca-141">You must:</span></span>
- <span data-ttu-id="27eca-142">Utwórz nowy kartę Sieciową, która korzysta z dynamicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="27eca-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="27eca-143">Hello karty Sieciowej na powitania hello maszyny Wirtualnej nowo utworzony zestaw kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="27eca-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="27eca-144">toochange hello kart interfejsu Sieciowego dla powitalne wirtualna używana w hello poleceń powyżej, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="27eca-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="27eca-145">Uruchom hello **tworzenie kart interfejsu sieciowego azure** polecenia toocreate nowej karty Sieciowej, za pomocą alokacji dynamicznego adresu IP za pomocą nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="27eca-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="27eca-146">Należy pamiętać, że żaden adres IP, ponieważ określono metodę alokacji hello **dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="27eca-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="27eca-147">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="27eca-147">Expected output:</span></span>

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

2. <span data-ttu-id="27eca-148">Uruchom hello **zestawu azure vm** hello toochange polecenia używane przez hello maszyny Wirtualnej karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="27eca-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="27eca-149">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="27eca-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="27eca-150">Jeśli hello maszyna wirtualna jest wystarczająco duży toohave więcej niż jedną kartę Sieciową, uruchom hello **usunąć kart interfejsu sieciowego azure** polecenia toodelete hello starego karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="27eca-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="27eca-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="27eca-151">Next steps</span></span>
* <span data-ttu-id="27eca-152">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="27eca-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="27eca-153">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="27eca-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="27eca-154">Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="27eca-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

