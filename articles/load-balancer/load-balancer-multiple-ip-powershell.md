---
title: "aaaLoad równoważenia na wielu konfiguracji adresów IP na platformie Azure | Dokumentacja firmy Microsoft"
description: "Równoważenie obciążenia w konfiguracji adresu IP podstawowego i pomocniczego."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="1fa20-103">Obciążenia równoważenia na wielu konfiguracji adresów IP przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fa20-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fa20-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1fa20-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="1fa20-105">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="1fa20-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="1fa20-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fa20-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="1fa20-107">W tym artykule opisano, jak toouse modułu równoważenia obciążenia Azure z adresem IP wielu adresów na pomocniczym interfejsie sieciowym (NIC).</span><span class="sxs-lookup"><span data-stu-id="1fa20-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="1fa20-108">W tym scenariuszu będziemy mieć dwie maszyny wirtualne z systemami Windows, każdy z podstawowym i pomocniczym karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="1fa20-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="1fa20-109">Każdy z hello dodatkowej karty sieciowe mają dwie konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="1fa20-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="1fa20-110">Każda maszyna wirtualna obsługuje zarówno contoso.com witryn sieci Web, jak i fabrikam.com. Każda witryna sieci Web jest powiązane tooone konfiguracji IP hello na powitania dodatkowej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="1fa20-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="1fa20-111">Używamy modułu równoważenia obciążenia Azure tooexpose dwa frontonu adresy IP, po jednej dla każdej witryny sieci Web, toodistribute ruchu toohello odpowiednich konfiguracji IP hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1fa20-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="1fa20-112">W tym scenariuszu używa hello tego samego numeru portu między zarówno frontends, jak i oba adresy IP do puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1fa20-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="1fa20-114">Saldo tooload czynności na wielu konfiguracji adresów IP</span><span class="sxs-lookup"><span data-stu-id="1fa20-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="1fa20-115">Wykonaj kroki hello poniżej scenariuszu hello tooachieve opisane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="1fa20-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="1fa20-116">Zainstaluj program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fa20-116">Install Azure PowerShell.</span></span> <span data-ttu-id="1fa20-117">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="1fa20-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="1fa20-118">Utwórz grupę zasobów, przy użyciu hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="1fa20-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="1fa20-119">Aby uzyskać więcej informacji, zobacz krok 2 [Utwórz grupę zasobów](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fa20-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="1fa20-120">[Utwórz zbiór dostępności](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1fa20-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="1fa20-121">W tym scenariuszu należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1fa20-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="1fa20-122">Postępuj zgodnie z instrukcjami kroki od 3 do 5 w [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artykuł tooprepare hello tworzenia maszyny wirtualnej z jednej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="1fa20-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="1fa20-123">Wykonaj krok 6.1 i użyć następujących hello zamiast krok 6.2:</span><span class="sxs-lookup"><span data-stu-id="1fa20-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="1fa20-124">Następnie wykonaj [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) kroki 6.3 za pośrednictwem 6.8.</span><span class="sxs-lookup"><span data-stu-id="1fa20-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="1fa20-125">Dodaj drugi tooeach konfiguracji adresu IP z hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1fa20-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="1fa20-126">Postępuj zgodnie z instrukcjami hello [przypisać wiele adresów IP maszyny toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artykułu.</span><span class="sxs-lookup"><span data-stu-id="1fa20-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="1fa20-127">Użyj hello następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="1fa20-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="1fa20-128">Nie trzeba tooassociate hello dodatkowej konfiguracji adresów IP z publicznych adresów IP w celu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1fa20-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="1fa20-129">Edytuj hello polecenia tooremove hello publicznego adresu IP skojarzenia części.</span><span class="sxs-lookup"><span data-stu-id="1fa20-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="1fa20-130">Wykonaj kroki od 4 do 6 w tym artykule ponownie dla maszyny VM2.</span><span class="sxs-lookup"><span data-stu-id="1fa20-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="1fa20-131">Być tooVM2 nazwę maszyny Wirtualnej hello tooreplace się w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="1fa20-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="1fa20-132">Uwaga niepotrzebne toocreate sieci wirtualnej dla hello drugie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fa20-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="1fa20-133">Może lub nie można utworzyć nową podsieć oparte na sieci przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="1fa20-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="1fa20-134">Utwórz dwa publiczne adresy IP i przechowywać je w odpowiednich zmiennych hello, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="1fa20-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="1fa20-135">Utwórz dwie konfiguracje adresów IP frontonu:</span><span class="sxs-lookup"><span data-stu-id="1fa20-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="1fa20-136">Utwórz użytkownika pul adresów zaplecza, badanie i reguły równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="1fa20-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="1fa20-137">Po utworzeniu te zasoby utworzone, Utwórz moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="1fa20-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="1fa20-138">Dodaj hello drugi wewnętrznej bazy danych adresów puli i frontonu IP konfiguracji tooyour nowo utworzony moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="1fa20-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="1fa20-139">Poniższe polecenia Hello uzyskać hello kart sieciowych, a następnie dodaj usługi równoważenia obciążenia dla obu konfiguracji IP każdej dodatkowej kart toohello puli adresów zaplecza programu hello:</span><span class="sxs-lookup"><span data-stu-id="1fa20-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="1fa20-140">Na koniec należy skonfigurować zasobów rekordów toopoint toohello odpowiednich frontonu adresu IP DNS hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1fa20-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="1fa20-141">Może hostować domen w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1fa20-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="1fa20-142">Aby uzyskać więcej informacji o korzystaniu z usługi Azure DNS z usługi równoważenia obciążenia, zobacz [przy użyciu usługi Azure DNS z innymi usługami Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1fa20-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fa20-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1fa20-143">Next steps</span></span>
- <span data-ttu-id="1fa20-144">Dowiedz się więcej na temat sposobu równoważenia obciążenia toocombine usługi na platformie Azure w [przy użyciu usługi równoważenia obciążenia w Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1fa20-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="1fa20-145">Dowiedz się, jak można używać różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługą równoważenia obciążenia w [dziennika analizy dla usługi równoważenia obciążenia Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="1fa20-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
