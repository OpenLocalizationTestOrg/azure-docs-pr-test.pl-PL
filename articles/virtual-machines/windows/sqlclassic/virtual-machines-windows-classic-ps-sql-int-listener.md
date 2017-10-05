---
title: "Skonfiguruj odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek używa zasobów utworzone za pomocą klasycznym modelu wdrożenia, i tworzy zawsze na odbiornik grupy dostępności na platformie Azure, która używa wewnętrznego modułu równoważenia obciążenia."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: fea70b389b1f1d6af963e3f14fdc48e8d857dd53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="7cd26-103">Skonfiguruj odbiornik ILB dla zawsze włączonych grup dostępności w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="7cd26-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7cd26-104">Odbiornik wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="7cd26-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="7cd26-105">Odbiornik zewnętrzny</span><span class="sxs-lookup"><span data-stu-id="7cd26-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="7cd26-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7cd26-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7cd26-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7cd26-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7cd26-108">W tym artykule omówiono korzystanie z klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7cd26-108">This article covers the use of the classic deployment model.</span></span> <span data-ttu-id="7cd26-109">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7cd26-109">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="7cd26-110">Aby skonfigurować odbiornik grupy dostępności AlwaysOn w modelu usługi Resource Manager, zobacz [skonfigurowania funkcji równoważenia obciążenia dla grupy dostępności AlwaysOn w Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="7cd26-110">To configure a listener for an Always On availability group in the Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="7cd26-111">Grupy dostępności może zawierać replik z lokalnymi tylko lub tylko Azure lub który obejmować zarówno lokalnych, jak i Azure dla hybrydowych konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="7cd26-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="7cd26-112">Azure replik może się znajdować w tym samym regionie lub w wielu regionach, które używają wielu sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7cd26-112">Azure replicas can reside within the same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="7cd26-113">Procedury przedstawione w tym artykule założono, że istnieje już [skonfigurowane grupy dostępności](../classic/portal-sql-alwayson-availability-groups.md) , ale nie ma jeszcze skonfigurowany odbiornik.</span><span class="sxs-lookup"><span data-stu-id="7cd26-113">The procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="7cd26-114">Zasady i ograniczenia dotyczące odbiorników wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="7cd26-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="7cd26-115">Użycie wewnętrznego modułu równoważenia obciążenia (ILB) z odbiornika grupy dostępności na platformie Azure podlega następujących wytycznych:</span><span class="sxs-lookup"><span data-stu-id="7cd26-115">The use of an internal load balancer (ILB) with an availability group listener in Azure is subject to the following guidelines:</span></span>

* <span data-ttu-id="7cd26-116">Odbiornik grupy dostępności jest obsługiwana w systemie Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="7cd26-116">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="7cd26-117">Tylko jeden odbiornik grupy dostępności wewnętrznego jest obsługiwana dla każdej usługi w chmurze, ponieważ odbiornika jest skonfigurowany do ILB, a istnieje tylko jeden ILB dla każdej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7cd26-117">Only one internal availability group listener is supported for each cloud service, because the listener is configured to the ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="7cd26-118">Istnieje możliwość utworzenia wielu odbiorników zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="7cd26-118">However, it is possible to create multiple external listeners.</span></span> <span data-ttu-id="7cd26-119">Aby uzyskać więcej informacji, zobacz [skonfigurować odbiornik zewnętrzny dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="7cd26-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="7cd26-120">Ustalić dostępność odbiornika</span><span class="sxs-lookup"><span data-stu-id="7cd26-120">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="7cd26-121">Ten artykuł skupia się na utworzenie odbiornika, który używa ILB.</span><span class="sxs-lookup"><span data-stu-id="7cd26-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="7cd26-122">Odbiornik publiczny lub zewnętrzne, należy wyświetlić wersję tego artykułu, w którym omówiono ustawienia zapasowej [zewnętrznych odbiornika](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cd26-122">If you need an public or external listener, see the version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="7cd26-123">Tworzyć równoważeniem obciążenia punkty końcowe maszyny Wirtualnej z serwerem bezpośredniego zwrotu</span><span class="sxs-lookup"><span data-stu-id="7cd26-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="7cd26-124">Należy najpierw utworzyć ILB, uruchamiając skrypt później w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7cd26-124">You first create an ILB by running the script later in this section.</span></span>

<span data-ttu-id="7cd26-125">Tworzenie punktu końcowego z równoważeniem obciążenia dla każdej maszyny Wirtualnej, który obsługuje replikę Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd26-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="7cd26-126">Jeśli masz repliki w wielu regionach, każdej repliki dla tego regionu musi być w tej samej usługi w chmurze w tej samej sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd26-126">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same Azure virtual network.</span></span> <span data-ttu-id="7cd26-127">Tworzenie dostępności replik grupy, obejmujące wiele regionów platformy Azure wymaga konfigurowania wielu sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7cd26-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="7cd26-128">Aby uzyskać więcej informacji na temat konfigurowania granic łączność sieci wirtualnej, zobacz [Konfigurowanie sieci wirtualnej do sieci wirtualnej łączności](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7cd26-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network to virtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="7cd26-129">W portalu Azure przejdź do każdej maszyny Wirtualnej, który obsługuje replikę, aby wyświetlić szczegóły.</span><span class="sxs-lookup"><span data-stu-id="7cd26-129">In the Azure portal, go to each VM that hosts a replica to view the details.</span></span>

2. <span data-ttu-id="7cd26-130">Kliknij przycisk **punkty końcowe** kartę dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7cd26-130">Click the **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="7cd26-131">Sprawdź, czy **nazwa** i **Port publiczny** nasłuchującego punktu końcowego, który chcesz użyć nie są już używane.</span><span class="sxs-lookup"><span data-stu-id="7cd26-131">Verify that the **Name** and **Public Port** of the listener endpoint that you want to use are not already in use.</span></span> <span data-ttu-id="7cd26-132">W tym przykładzie w tej sekcji jest nazwa *MyEndpoint*, a numer portu to *1433*.</span><span class="sxs-lookup"><span data-stu-id="7cd26-132">In the example in this section, the name is *MyEndpoint*, and the port is *1433*.</span></span>

4. <span data-ttu-id="7cd26-133">Na kliencie lokalnym, Pobierz i zainstaluj najnowszą [modułu PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7cd26-133">On your local client, download and install the latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="7cd26-134">Uruchom program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cd26-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="7cd26-135">Umożliwia otwarcie nowej sesji programu PowerShell z Azure załadowanych modułów administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="7cd26-135">A new PowerShell session opens, with the Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="7cd26-136">Uruchom polecenie `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="7cd26-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="7cd26-137">To polecenie cmdlet kieruje do przeglądarki, aby pobrać plik ustawień publikowania do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="7cd26-137">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="7cd26-138">Użytkownik może zostać poproszony o podanie poświadczeń logowania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd26-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="7cd26-139">Uruchom następujące polecenie `Import-AzurePublishSettingsFile` polecenia ze ścieżką pobrany plik ustawień publikowania:</span><span class="sxs-lookup"><span data-stu-id="7cd26-139">Run the following `Import-AzurePublishSettingsFile` command with the path of the publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="7cd26-140">Po zaimportowaniu ustawień publikowania, można zarządzać subskrypcją platformy Azure w sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cd26-140">After the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>

8. <span data-ttu-id="7cd26-141">Aby uzyskać *ILB*, Przypisz statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="7cd26-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="7cd26-142">Sprawdź bieżącą konfigurację sieci wirtualnej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7cd26-142">Examine the current virtual network configuration by running the following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="7cd26-143">Uwaga *podsieci* nazwy podsieci, która zawiera maszyny wirtualnej tego hosta repliki.</span><span class="sxs-lookup"><span data-stu-id="7cd26-143">Note the *Subnet* name for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="7cd26-144">Ta nazwa jest używana w parametrze $SubnetName w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="7cd26-144">This name is used in the $SubnetName parameter in the script.</span></span>

10. <span data-ttu-id="7cd26-145">Uwaga *VirtualNetworkSite* nazwy i początkowe *prefiks adresu* dla podsieci, która zawiera maszyny wirtualne, które hosta repliki.</span><span class="sxs-lookup"><span data-stu-id="7cd26-145">Note the *VirtualNetworkSite* name and the starting *AddressPrefix* for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="7cd26-146">Wyszukaj dostępnego adresu IP przez przekazanie obie wartości `Test-AzureStaticVNetIP` polecenia i po sprawdzeniu *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="7cd26-146">Look for an available IP address by passing both values to the `Test-AzureStaticVNetIP` command and by examining the *AvailableAddresses*.</span></span> <span data-ttu-id="7cd26-147">Na przykład, jeśli sieć wirtualną o nazwie *MyVNet* i ma zakres adresów podsieci, która rozpoczyna się od *172.16.0.128*, polecenie pojawi się lista dostępnych adresów:</span><span class="sxs-lookup"><span data-stu-id="7cd26-147">For example, if the virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, the following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="7cd26-148">Wybierz jedną z dostępnych adresów, a następnie użyć jej w parametrze $ILBStaticIP skryptu w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="7cd26-148">Select one of the available addresses, and use it in the $ILBStaticIP parameter of the script in the next step.</span></span>

12. <span data-ttu-id="7cd26-149">Skopiuj poniższy skrypt programu PowerShell do edytora tekstu, a następnie ustaw wartości zmiennych do potrzeb środowiska.</span><span class="sxs-lookup"><span data-stu-id="7cd26-149">Copy the following PowerShell script to a text editor, and set the variable values to suit your environment.</span></span> <span data-ttu-id="7cd26-150">Wartości domyślne zostały dołączone niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="7cd26-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="7cd26-151">Istniejące wdrożenia, które korzysta z grup koligacji nie można dodać ILB.</span><span class="sxs-lookup"><span data-stu-id="7cd26-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="7cd26-152">Aby uzyskać więcej informacji na temat wymagań dotyczących ILB, zobacz [Omówienie usługi równoważenia obciążenia wewnętrznego](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cd26-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="7cd26-153">Ponadto jeśli grupy dostępności obejmuje regiony platformy Azure, musi uruchamiania skryptu raz w każdym centrum danych do usługi w chmurze i węzły, które znajdują się w tym centrum danych.</span><span class="sxs-lookup"><span data-stu-id="7cd26-153">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that the replicas use in the virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for the ILB in the subnet
        $ILBName = "AGListenerLB" # customize the ILB name or use this default value

        # Create the ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="7cd26-154">Po ustawieniu zmienne, skopiuj skrypt w edytorze tekstu do sesji programu PowerShell, aby go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="7cd26-154">After you have set the variables, copy the script from the text editor to your PowerShell session to run it.</span></span> <span data-ttu-id="7cd26-155">Jeśli nadal wyświetlany jest monit  **>>** , naciśnij klawisz Enter ponownie, aby upewnić się, uruchomienie skryptu.</span><span class="sxs-lookup"><span data-stu-id="7cd26-155">If the prompt still shows **>>**, press Enter again to make sure the script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="7cd26-156">Sprawdź, czy KB2854082 jest zainstalowana w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="7cd26-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="7cd26-157">Otworzyć porty zapory w węzłach grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="7cd26-157">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="7cd26-158">Tworzenie odbiornika grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="7cd26-158">Create the availability group listener</span></span>

<span data-ttu-id="7cd26-159">Tworzenie odbiornika grupy dostępności w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="7cd26-159">Create the availability group listener in two steps.</span></span> <span data-ttu-id="7cd26-160">Najpierw należy utworzyć zasobu klastra punkt dostępu klienta i skonfigurować zależności.</span><span class="sxs-lookup"><span data-stu-id="7cd26-160">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="7cd26-161">Po drugie Skonfiguruj zasoby klastra w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cd26-161">Second, configure the cluster resources in PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="7cd26-162">Utwórz punkt dostępu klienta i skonfiguruj zależności klastra</span><span class="sxs-lookup"><span data-stu-id="7cd26-162">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="7cd26-163">Konfigurowanie zasobów klastra w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cd26-163">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="7cd26-164">ILB należy użyć adresu IP ILB, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7cd26-164">For ILB, you must use the IP address of the ILB that was created earlier.</span></span> <span data-ttu-id="7cd26-165">Aby uzyskać ten adres IP w programie PowerShell, użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="7cd26-165">To obtain this IP address in PowerShell, use the following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # the name of the cloud service that contains the AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="7cd26-166">Na jednym z maszyn wirtualnych Skopiuj skrypt programu PowerShell dla systemu operacyjnego do edytora tekstu, a następnie ustaw zmienne do wartości, które wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="7cd26-166">On one of the VMs, copy the PowerShell script for your operating system to a text editor, and then set the variables to the values you noted earlier.</span></span>

    <span data-ttu-id="7cd26-167">Dla systemu Windows Server 2012 lub nowszym Użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="7cd26-167">For Windows Server 2012 or later, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="7cd26-168">Dla systemu Windows Server 2008 R2 Użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="7cd26-168">For Windows Server 2008 R2, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="7cd26-169">Po ustawieniu zmienne, Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień, wklej skrypt w edytorze tekstowym w sesji programu PowerShell, aby go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="7cd26-169">After you have set the variables, open an elevated Windows PowerShell window, paste the script from the text editor into your PowerShell session to run it.</span></span> <span data-ttu-id="7cd26-170">Jeśli nadal wyświetlany jest monit  **>>** , naciśnij klawisz Enter, ponownie, aby upewnić się, że skrypt zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="7cd26-170">If the prompt still shows **>>**, Press Enter again to make sure that the script starts running.</span></span>

4. <span data-ttu-id="7cd26-171">Powtórz te czynności dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7cd26-171">Repeat the preceding steps for each VM.</span></span>  
    <span data-ttu-id="7cd26-172">Ten skrypt konfiguruje zasobu adresów IP przy użyciu adresu IP usługi w chmurze i ustawia innych parametrów, takich jak port sondy.</span><span class="sxs-lookup"><span data-stu-id="7cd26-172">This script configures the IP address resource with the IP address of the cloud service and sets other parameters, such as the probe port.</span></span> <span data-ttu-id="7cd26-173">Gdy zasób adresu IP w tryb online, mogą odpowiadać na sondowanie na port sondy z równoważeniem obciążenia punktu końcowego, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7cd26-173">When the IP address resource is brought online, it can respond to the polling on the probe port from the load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="7cd26-174">Przełącz odbiornika w trybie online</span><span class="sxs-lookup"><span data-stu-id="7cd26-174">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="7cd26-175">Elementy monitowania</span><span class="sxs-lookup"><span data-stu-id="7cd26-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-virtual-network"></a><span data-ttu-id="7cd26-176">Testowanie odbiornika grupy dostępności (w ramach tej samej sieci wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="7cd26-176">Test the availability group listener (within the same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="7cd26-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7cd26-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
