---
title: "aaaConfigure odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania i tworzy zawsze na odbiornik grupy dostępności na platformie Azure, która używa wewnętrznego modułu równoważenia obciążenia."
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
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="53b3c-103">Skonfiguruj odbiornik ILB dla zawsze włączonych grup dostępności w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="53b3c-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="53b3c-104">Odbiornik wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="53b3c-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="53b3c-105">Odbiornik zewnętrzny</span><span class="sxs-lookup"><span data-stu-id="53b3c-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="53b3c-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="53b3c-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53b3c-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="53b3c-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="53b3c-108">W tym artykule omówiono używanie hello hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="53b3c-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="53b3c-109">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="53b3c-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="53b3c-110">Zobacz tooconfigure odbiornika dla zawsze włączone grupy dostępności w modelu Resource Manager hello [skonfigurowania funkcji równoważenia obciążenia dla grupy dostępności AlwaysOn w Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="53b3c-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="53b3c-111">Grupy dostępności może zawierać replik z lokalnymi tylko lub tylko Azure lub który obejmować zarówno lokalnych, jak i Azure dla hybrydowych konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="53b3c-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="53b3c-112">Azure replik może znajdować się w obrębie hello sam region lub w wielu regionach, które używają wielu sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="53b3c-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="53b3c-113">Witaj procedury przedstawione w tym artykule założono, że istnieje już [skonfigurowane grupy dostępności](../classic/portal-sql-alwayson-availability-groups.md) , ale nie ma jeszcze skonfigurowany odbiornik.</span><span class="sxs-lookup"><span data-stu-id="53b3c-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="53b3c-114">Zasady i ograniczenia dotyczące odbiorników wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="53b3c-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="53b3c-115">Użycie Hello wewnętrznego modułu równoważenia obciążenia (ILB) z odbiornika grupy dostępności na platformie Azure jest toohello podmiotu następujące wytyczne:</span><span class="sxs-lookup"><span data-stu-id="53b3c-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="53b3c-116">odbiornik grupy dostępności Hello jest obsługiwana w systemie Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="53b3c-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="53b3c-117">Tylko jeden odbiornik grupy dostępności wewnętrzny jest obsługiwana dla każdej usługi w chmurze, ponieważ odbiornik hello jest skonfigurowany toohello ILB, a istnieje tylko jeden ILB dla każdej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="53b3c-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="53b3c-118">Jest jednak możliwe toocreate wiele odbiorników zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="53b3c-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="53b3c-119">Aby uzyskać więcej informacji, zobacz [skonfigurować odbiornik zewnętrzny dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="53b3c-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="53b3c-120">Ustalić dostępność hello hello odbiornika</span><span class="sxs-lookup"><span data-stu-id="53b3c-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="53b3c-121">Ten artykuł skupia się na utworzenie odbiornika, który używa ILB.</span><span class="sxs-lookup"><span data-stu-id="53b3c-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="53b3c-122">Odbiornik publiczny lub zewnętrzne, należy wyświetlić wersję hello tego artykułu, w którym omówiono ustawienia zapasowej [zewnętrznych odbiornika](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53b3c-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="53b3c-123">Tworzyć równoważeniem obciążenia punkty końcowe maszyny Wirtualnej z serwerem bezpośredniego zwrotu</span><span class="sxs-lookup"><span data-stu-id="53b3c-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="53b3c-124">Należy najpierw utworzyć ILB, uruchamiając skrypt hello później w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="53b3c-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="53b3c-125">Tworzenie punktu końcowego z równoważeniem obciążenia dla każdej maszyny Wirtualnej, który obsługuje replikę Azure.</span><span class="sxs-lookup"><span data-stu-id="53b3c-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="53b3c-126">Jeśli masz repliki w wielu regionach, każdej repliki dla tego regionu musi być w hello takie same usługi w chmurze hello sama sieć wirtualna platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53b3c-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="53b3c-127">Tworzenie dostępności replik grupy, obejmujące wiele regionów platformy Azure wymaga konfigurowania wielu sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="53b3c-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="53b3c-128">Aby uzyskać więcej informacji na temat konfigurowania granic łączność sieci wirtualnej, zobacz [skonfigurować łączność sieciową toovirtual sieci wirtualnej](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="53b3c-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="53b3c-129">W hello portalu Azure Przejdź tooeach maszynę Wirtualną, która obsługuje szczegóły hello tooview repliki.</span><span class="sxs-lookup"><span data-stu-id="53b3c-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="53b3c-130">Kliknij przycisk hello **punkty końcowe** kartę dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53b3c-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="53b3c-131">Sprawdź, że hello **nazwa** i **Port publiczny** punktu końcowego odbiornika hello, który ma być toouse nie są już używane.</span><span class="sxs-lookup"><span data-stu-id="53b3c-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="53b3c-132">Na przykład Witaj w tej sekcji, nazwa hello to *MyEndpoint*, a hello port jest *1433*.</span><span class="sxs-lookup"><span data-stu-id="53b3c-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="53b3c-133">Na kliencie lokalnym, należy pobrać i zainstalować najnowsze hello [modułu PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="53b3c-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="53b3c-134">Uruchom program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53b3c-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="53b3c-135">Otwiera nową sesję programu PowerShell, z hello Azure administracyjne załadowanych modułów.</span><span class="sxs-lookup"><span data-stu-id="53b3c-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="53b3c-136">Uruchom polecenie `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="53b3c-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="53b3c-137">To polecenie cmdlet kieruje tooa przeglądarki toodownload publikowania ustawienia pliku tooa katalogiem lokalnym.</span><span class="sxs-lookup"><span data-stu-id="53b3c-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="53b3c-138">Użytkownik może zostać poproszony o podanie poświadczeń logowania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53b3c-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="53b3c-139">Uruchom następujące hello `Import-AzurePublishSettingsFile` pobranego pliku ustawień publikowania polecenie z hello ścieżka hello:</span><span class="sxs-lookup"><span data-stu-id="53b3c-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="53b3c-140">Po publikowania hello jest importowany plik ustawień, można zarządzać subskrypcją platformy Azure w sesji programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="53b3c-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="53b3c-141">Aby uzyskać *ILB*, Przypisz statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="53b3c-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="53b3c-142">Sprawdź hello bieżącą konfigurację sieci wirtualnej, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="53b3c-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="53b3c-143">Uwaga hello *podsieci* nazwę podsieci hello, która zawiera hello maszyn wirtualnych, które hosta replik hello.</span><span class="sxs-lookup"><span data-stu-id="53b3c-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="53b3c-144">Ta nazwa jest używana w parametrze hello $SubnetName w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="53b3c-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="53b3c-145">Uwaga hello *VirtualNetworkSite* nazwy i hello uruchamianie *prefiks adresu* dla podsieci hello, który zawiera hello maszyn wirtualnych, które hosta replik hello.</span><span class="sxs-lookup"><span data-stu-id="53b3c-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="53b3c-146">Wyszukaj dostępnego adresu IP przez przekazanie toohello obie wartości `Test-AzureStaticVNetIP` polecenia i sprawdzając hello *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="53b3c-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="53b3c-147">Na przykład, jeśli hello sieci wirtualnej nosi nazwę *MyVNet* i ma zakres adresów podsieci, która rozpoczyna się od *172.16.0.128*, hello następujące polecenie, pojawi się lista dostępnych adresów:</span><span class="sxs-lookup"><span data-stu-id="53b3c-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="53b3c-148">Wybierz jedną z dostępnych adresów hello i użyć go w parametrze hello $ILBStaticIP skryptu hello na powitania następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="53b3c-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="53b3c-149">Skopiuj powitania po Edytor tekstu tooa skrypt programu PowerShell i ustaw hello toosuit wartości zmiennych środowiska.</span><span class="sxs-lookup"><span data-stu-id="53b3c-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="53b3c-150">Wartości domyślne zostały dołączone niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="53b3c-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="53b3c-151">Istniejące wdrożenia, które korzysta z grup koligacji nie można dodać ILB.</span><span class="sxs-lookup"><span data-stu-id="53b3c-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="53b3c-152">Aby uzyskać więcej informacji na temat wymagań dotyczących ILB, zobacz [Omówienie usługi równoważenia obciążenia wewnętrznego](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53b3c-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="53b3c-153">Ponadto jeśli grupy dostępności obejmuje regiony platformy Azure, należy uruchomić skrypt hello raz w centrum danych z każdej usługi w chmurze hello i węzły, które znajdują się w tym centrum danych.</span><span class="sxs-lookup"><span data-stu-id="53b3c-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="53b3c-154">Po ustawieniu zmienne hello hello Kopiuj skrypt z hello tekstu Edytor tooyour PowerShell sesji toorun go.</span><span class="sxs-lookup"><span data-stu-id="53b3c-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="53b3c-155">Jeśli nadal wyświetlany jest monit hello  **>>** , naciśnij klawisz Enter ponownie toomake się, że skrypt hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="53b3c-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="53b3c-156">Sprawdź, czy KB2854082 jest zainstalowana w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="53b3c-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="53b3c-157">Otworzyć porty zapory hello w węzłach grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="53b3c-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="53b3c-158">Tworzenie odbiornika grupy dostępności hello</span><span class="sxs-lookup"><span data-stu-id="53b3c-158">Create hello availability group listener</span></span>

<span data-ttu-id="53b3c-159">Tworzenie odbiornika grupy dostępności hello w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="53b3c-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="53b3c-160">Najpierw należy utworzyć zasobu klastra punktu dostępu klienta hello i skonfigurować zależności.</span><span class="sxs-lookup"><span data-stu-id="53b3c-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="53b3c-161">Po drugie skonfiguruj hello zasoby klastra w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53b3c-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="53b3c-162">Tworzenie punktu dostępu klienta hello i konfigurowanie hello zależności klastra</span><span class="sxs-lookup"><span data-stu-id="53b3c-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="53b3c-163">Konfigurowanie zasobów klastra hello w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="53b3c-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="53b3c-164">ILB należy użyć adresu IP hello hello ILB, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53b3c-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="53b3c-165">tooobtain adresów IP to w programie PowerShell hello Użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="53b3c-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="53b3c-166">Na jednym z hello maszyn wirtualnych Skopiuj skrypt programu PowerShell hello do edytora tekstu tooa systemu operacyjnego, a następnie ustaw zmienne hello toohello wartości, które wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="53b3c-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="53b3c-167">Dla systemu Windows Server 2012 lub nowszym Użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="53b3c-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="53b3c-168">Dla systemu Windows Server 2008 R2 Użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="53b3c-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="53b3c-169">Po utworzeniu zestawu hello zmiennych, Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień, Wklej hello skrypt z edytora tekstów hello do toorun sesji programu PowerShell go.</span><span class="sxs-lookup"><span data-stu-id="53b3c-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="53b3c-170">Jeśli nadal wyświetlany jest monit hello  **>>** , naciśnij klawisz Enter, ponownie toomake się upewnić, że skrypt hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="53b3c-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="53b3c-171">Powtórz hello w poprzednich krokach dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53b3c-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="53b3c-172">Ten skrypt konfiguruje zasobu adresu IP hello o adresie IP hello hello usługi w chmurze i ustawia innych parametrów, takich jak port sondy hello.</span><span class="sxs-lookup"><span data-stu-id="53b3c-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="53b3c-173">Gdy zasób adresu IP hello w tryb online, jego odpowiadają toohello sondowania na porcie sondowania powitania od hello równoważeniem obciążenia punktu końcowego, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53b3c-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="53b3c-174">Przełącz odbiornika hello w trybie online</span><span class="sxs-lookup"><span data-stu-id="53b3c-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="53b3c-175">Elementy monitowania</span><span class="sxs-lookup"><span data-stu-id="53b3c-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="53b3c-176">Odbiornik grupy dostępności hello testu (poziomu hello sam sieci wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="53b3c-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="53b3c-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53b3c-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
