---
title: "aaaLoad równoważenia na wielu konfiguracji adresów IP przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszyny wirtualnej za pomocą wiersza polecenia platformy Azure | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="bf2e8-103">Obciążenia równoważenia na wielu konfiguracji adresów IP</span><span class="sxs-lookup"><span data-stu-id="bf2e8-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf2e8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bf2e8-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="bf2e8-105">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bf2e8-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="bf2e8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf2e8-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="bf2e8-107">W tym artykule opisano, jak toouse modułu równoważenia obciążenia Azure z adresem IP wielu adresów na pomocniczym interfejsie sieciowym (NIC).</span><span class="sxs-lookup"><span data-stu-id="bf2e8-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="bf2e8-108">W tym scenariuszu będziemy mieć dwie maszyny wirtualne z systemami Windows, każdy z podstawowym i pomocniczym karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="bf2e8-109">Każdy z hello dodatkowej karty sieciowe mają dwie konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="bf2e8-110">Każda maszyna wirtualna obsługuje zarówno contoso.com witryn sieci Web, jak i fabrikam.com. Każda witryna sieci Web jest powiązane tooone konfiguracji IP hello na powitania dodatkowej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="bf2e8-111">Używamy modułu równoważenia obciążenia Azure tooexpose dwa frontonu adresy IP, po jednej dla każdej witryny sieci Web, toodistribute ruchu toohello odpowiednich konfiguracji IP hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="bf2e8-112">W tym scenariuszu używa hello tego samego numeru portu między zarówno frontends, jak i oba adresy IP do puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="bf2e8-114">Saldo tooload czynności na wielu konfiguracji adresów IP</span><span class="sxs-lookup"><span data-stu-id="bf2e8-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="bf2e8-115">Wykonaj kroki hello poniżej scenariuszu hello tooachieve opisane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="bf2e8-116">[Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) hello wiersza polecenia platformy Azure, wykonując kroki hello w artykule połączonego hello i dziennika do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="bf2e8-117">[Utwórz grupę zasobów](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) o nazwie *contosofabrikam* zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="bf2e8-118">[Tworzenie zestawu dostępności](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor Witaj dwie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="bf2e8-119">W tym scenariuszu należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="bf2e8-120">[Tworzenie sieci wirtualnej](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) o nazwie *myVNet* i podsieć o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="bf2e8-121">[Tworzenie usługi równoważenia obciążenia hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o nazwie *mylb*:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="bf2e8-122">Utwórz dwa dynamiczne publiczne adresy IP, w przypadku konfiguracji IP frontonu hello z usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="bf2e8-123">Tworzenie frontonu Witaj dwie konfiguracje adresów IP *contosofe* i *fabrikamfe* odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="bf2e8-124">Tworzenie zaplecza pule adresów - *contosopool* i *fabrikampool*, [sondowania](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, i reguły - równoważenia obciążenia *HTTPc* i *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="bf2e8-125">Hello uruchom następujące polecenie poniżej, a następnie sprawdź dane wyjściowe hello zbyt[Sprawdź przez moduł równoważenia obciążenia](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) został utworzony prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="bf2e8-126">[Tworzenie publicznego adresu IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, i [konta magazynu](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* na pierwszej maszynie wirtualnej VM1, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="bf2e8-127">[Tworzenie interfejsów sieciowych hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) dla VM1 i dodać drugi konfiguracji adresów IP, *VM1 ipconfig2*, i [utworzyć hello maszyny Wirtualnej](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="bf2e8-128">Powtórz kroki od 10 11 dla drugiej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="bf2e8-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="bf2e8-129">Na koniec należy skonfigurować zasobów rekordów toopoint toohello odpowiednich frontonu adresu IP DNS hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="bf2e8-130">Może hostować domen w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="bf2e8-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="bf2e8-131">Aby uzyskać więcej informacji o korzystaniu z usługi Azure DNS z usługi równoważenia obciążenia, zobacz [przy użyciu usługi Azure DNS z innymi usługami Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="bf2e8-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf2e8-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf2e8-132">Next steps</span></span>
- <span data-ttu-id="bf2e8-133">Dowiedz się więcej na temat sposobu równoważenia obciążenia toocombine usługi na platformie Azure w [przy użyciu usługi równoważenia obciążenia w Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bf2e8-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="bf2e8-134">Dowiedz się, jak można używać różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługą równoważenia obciążenia w [dziennika analizy dla usługi równoważenia obciążenia Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="bf2e8-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
