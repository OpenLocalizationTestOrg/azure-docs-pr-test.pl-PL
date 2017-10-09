---
title: aaaCreate konfiguracji wielu SID SAP na platformie Azure | Dokumentacja firmy Microsoft
description: "Przewodnik toohigh dostępności SAP NetWeaver identyfikatora SID wielu konfiguracji na maszynach wirtualnych systemu Windows"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="6f19a-103">Tworzenie konfiguracji wielu SID SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6f19a-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="6f19a-104">We wrześniu 2016 roku firma Microsoft opublikowała funkcja, której mogą zarządzać wielu wirtualnych adresów IP przy użyciu usługi Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6f19a-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="6f19a-105">Ta funkcja jest już istnieje w hello Azure zewnętrznej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6f19a-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="6f19a-106">W przypadku wdrożenia SAP, służy toocreate usługi równoważenia obciążenia wewnętrznego konfiguracji klastra systemu Windows dla programu SAP ASCS/SCS, zgodnie z opisem w hello [przewodnik wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="6f19a-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="6f19a-107">Ten artykuł skupia się na jak toomove z jednym ASCS/SCS instalacji tooan SAP identyfikatora SID wielu konfiguracji przez zainstalowanie dodatkowych SAP ASCS SCS klastrowanego wystąpienia do istniejącego klastra systemu Windows Server Failover Clustering (WSFC).</span><span class="sxs-lookup"><span data-stu-id="6f19a-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="6f19a-108">Po zakończeniu tego procesu został skonfigurowany klaster identyfikatora SID multi SAP.</span><span class="sxs-lookup"><span data-stu-id="6f19a-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6f19a-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6f19a-109">Prerequisites</span></span>
<span data-ttu-id="6f19a-110">Został już skonfigurowany klaster usługi WSFC, służący do jednego wystąpienia SAP ASCS/SCS, zgodnie z opisem w hello [przewodnik wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych Windows] [ sap-ha-guide] i jak pokazano na tym diagramie.</span><span class="sxs-lookup"><span data-stu-id="6f19a-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Wystąpienie programu SAP ASCS/SCS wysokiej dostępności][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="6f19a-112">Architektura docelowa</span><span class="sxs-lookup"><span data-stu-id="6f19a-112">Target architecture</span></span>

<span data-ttu-id="6f19a-113">Witaj celem jest tooinstall wielu SAP ABAP ASCS lub SAP Java SCS klastrowane wystąpienia w hello sam klaster usługi WSFC, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6f19a-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Wiele wystąpień programu SAP ASCS/SCS klastrowanego na platformie Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="6f19a-115">Brak limitu toohello liczba prywatnych adresów IP frontonu, dla każdej platformy Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6f19a-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="6f19a-116">Hello maksymalnej liczby wystąpień programu SAP ASCS/SCS w jednym klastrze usługi WSFC jest równy toohello maksymalna liczba prywatnych adresów IP frontonu, dla każdej platformy Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6f19a-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="6f19a-117">Aby uzyskać więcej informacji na temat limitów modułu równoważenia obciążenia, zobacz "frontonu prywatnego adresu IP dla modułu równoważenia obciążenia" w [limity sieci: usługi Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="6f19a-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="6f19a-118">Hello pełną w orientacji poziomej dwa systemy SAP wysokiej dostępności będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6f19a-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![SAP wysokiej dostępności multi-SID Instalatorowi systemu SAP identyfikatorów SID][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="6f19a-120">Instalator Hello musi spełniać hello następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="6f19a-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="6f19a-121">Witaj SAP ASCS/SCS muszą współużytkować wystąpień hello sam klaster usługi WSFC.</span><span class="sxs-lookup"><span data-stu-id="6f19a-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="6f19a-122">Każdy identyfikator SID systemu DBMS musi mieć własny dedykowany klaster usługi WSFC.</span><span class="sxs-lookup"><span data-stu-id="6f19a-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="6f19a-123">Serwery aplikacji SAP należą systemu SAP tooone identyfikatora SID musi mieć własne dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6f19a-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="6f19a-124">Przygotowanie infrastruktury hello</span><span class="sxs-lookup"><span data-stu-id="6f19a-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="6f19a-125">tooprepare infrastruktury, można zainstalować dodatkowe wystąpienia SAP ASCS/SCS z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6f19a-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="6f19a-126">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="6f19a-126">Parameter name</span></span> | <span data-ttu-id="6f19a-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="6f19a-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6f19a-128">SAP ASCS/SCS IDENTYFIKATORA SID</span><span class="sxs-lookup"><span data-stu-id="6f19a-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="6f19a-129">PR1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="6f19a-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="6f19a-130">System DBMS SAP wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6f19a-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="6f19a-131">PR5</span><span class="sxs-lookup"><span data-stu-id="6f19a-131">PR5</span></span> |
| <span data-ttu-id="6f19a-132">Nazwa hosta wirtualnego SAP</span><span class="sxs-lookup"><span data-stu-id="6f19a-132">SAP virtual host name</span></span> | <span data-ttu-id="6f19a-133">cl-pr5-sap</span><span class="sxs-lookup"><span data-stu-id="6f19a-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="6f19a-134">Adres IP hosta wirtualnego SAP ASCS/SCS (adres IP usługi równoważenia obciążenia Azure dodatkowe)</span><span class="sxs-lookup"><span data-stu-id="6f19a-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="6f19a-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="6f19a-135">10.0.0.50</span></span> |
| <span data-ttu-id="6f19a-136">SAP ASCS/SCS liczby wystąpień</span><span class="sxs-lookup"><span data-stu-id="6f19a-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="6f19a-137">50</span><span class="sxs-lookup"><span data-stu-id="6f19a-137">50</span></span> |
| <span data-ttu-id="6f19a-138">Port sondy ILB dodatkowe wystąpienia SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="6f19a-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="6f19a-139">62350</span><span class="sxs-lookup"><span data-stu-id="6f19a-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="6f19a-140">Każdy adres IP wystąpienia klastra programu SAP ASCS/SCS, wymaga port sondy unikatowy.</span><span class="sxs-lookup"><span data-stu-id="6f19a-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="6f19a-141">Na przykład jeśli jeden adres IP na Azure wewnętrznego modułu równoważenia obciążenia używa portu sondowania 62300, żaden adres IP w tej usługi równoważenia obciążenia można użyć portu sondowania 62300.</span><span class="sxs-lookup"><span data-stu-id="6f19a-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="6f19a-142">W naszym celów ponieważ port sondy 62300 jest już zarezerwowany, użyto port sondy 62350.</span><span class="sxs-lookup"><span data-stu-id="6f19a-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="6f19a-143">Można zainstalować dodatkowe wystąpienia SAP ASCS/SCS w istniejącym klastrze usługi WSFC hello z dwoma węzłami:</span><span class="sxs-lookup"><span data-stu-id="6f19a-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="6f19a-144">Roli maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f19a-144">Virtual machine role</span></span> | <span data-ttu-id="6f19a-145">Nazwa hosta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f19a-145">Virtual machine host name</span></span> | <span data-ttu-id="6f19a-146">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="6f19a-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6f19a-147">1. węzła klastra dla wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="6f19a-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="6f19a-148">PR1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="6f19a-148">pr1-ascs-0</span></span> |<span data-ttu-id="6f19a-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="6f19a-149">10.0.0.10</span></span> |
| <span data-ttu-id="6f19a-150">2 węzła klastra dla wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="6f19a-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="6f19a-151">PR1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="6f19a-151">pr1-ascs-1</span></span> |<span data-ttu-id="6f19a-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="6f19a-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="6f19a-153">Utwórz nazwę hosta wirtualnego wystąpienia programu SAP ASCS/SCS hello w klastrze na powitania serwera DNS</span><span class="sxs-lookup"><span data-stu-id="6f19a-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="6f19a-154">Można utworzyć wpis DNS dla nazwy hostów wirtualnych hello hello ASCS/SCS wystąpienia przy użyciu hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6f19a-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="6f19a-155">Nowa nazwa hosta wirtualnego SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="6f19a-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="6f19a-156">Skojarzony adres IP</span><span class="sxs-lookup"><span data-stu-id="6f19a-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="6f19a-157">cl-pr5-sap</span><span class="sxs-lookup"><span data-stu-id="6f19a-157">pr5-sap-cl</span></span> |<span data-ttu-id="6f19a-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="6f19a-158">10.0.0.50</span></span> |

<span data-ttu-id="6f19a-159">Hello nową nazwę hosta i adresu IP są wyświetlane w hello Menedżera DNS, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="6f19a-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Lista Menedżera DNS wyróżnianie hello zdefiniowano wpis DNS dla nazwy wirtualnego hello nowe SAP ASCS/SCS klastra i adres TCP/IP][sap-ha-guide-figure-6004]

<span data-ttu-id="6f19a-161">Hello procedurę tworzenia wpisu DNS jest również opisano szczegółowo w głównym hello [przewodnik wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="6f19a-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="6f19a-162">Witaj nowego adresu IP, aby przypisać nazwę hosta wirtualnego toohello hello dodatkowego wystąpienia ASCS/SCS musi być hello taki sam jak hello przypisania modułu równoważenia obciążenia SAP Azure toohello nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6f19a-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="6f19a-163">W naszym scenariuszu hello adres IP jest 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="6f19a-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="6f19a-164">Dodawanie adresu IP address tooan istniejących Azure wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f19a-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="6f19a-165">toocreate więcej niż jedno wystąpienie SAP ASCS/SCS w tej samej usługi WSFC hello klastra, użyj programu PowerShell tooadd tooan adresów IP istniejących Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6f19a-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="6f19a-166">Każdy adres IP wymaga własne reguły równoważenia obciążenia, port sondy frontonu puli adresów IP i puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6f19a-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="6f19a-167">Witaj poniższy skrypt dodaje nowe IP adres tooan istniejącej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6f19a-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="6f19a-168">Zaktualizuj hello zmiennych środowiska PowerShell dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="6f19a-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="6f19a-169">skrypt Hello utworzy wszystkie niezbędne reguły równoważenia obciążenia dla wszystkich portów SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="6f19a-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="6f19a-170">Po uruchomieniu skryptu hello, powitalne wyniki są wyświetlane w hello portalu Azure, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="6f19a-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Nowa pula IP frontonu, w portalu Azure hello][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="6f19a-172">Dodaj dyski toocluster maszyny i skonfiguruj hello SIOS klastra udziału dysku</span><span class="sxs-lookup"><span data-stu-id="6f19a-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="6f19a-173">Należy dodać nowy dysk udziału klastra dla każdego dodatkowego wystąpienia SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="6f19a-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="6f19a-174">Dla systemu Windows Server 2012 R2 hello SIOS DataKeeper oprogramowania rozwiązaniem jest dysk udziału klastra usługi WSFC hello obecnie w użyciu.</span><span class="sxs-lookup"><span data-stu-id="6f19a-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="6f19a-175">Witaj, po:</span><span class="sxs-lookup"><span data-stu-id="6f19a-175">Do hello following:</span></span>
1. <span data-ttu-id="6f19a-176">Dodanie dodatkowych dysk lub dyski hello tego samego rozmiaru (który jest wymagany toostripe) tooeach hello węzły klastra, a ich formatować.</span><span class="sxs-lookup"><span data-stu-id="6f19a-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="6f19a-177">Skonfigurować SIOS DataKeeper replikacji magazynu.</span><span class="sxs-lookup"><span data-stu-id="6f19a-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="6f19a-178">W tej procedurze przyjęto założenie, zainstalowano SIOS DataKeeper na komputerach klastra usługi WSFC hello.</span><span class="sxs-lookup"><span data-stu-id="6f19a-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="6f19a-179">Po zainstalowaniu go teraz należy skonfigurować replikację między hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="6f19a-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="6f19a-180">proces Hello jest szczegółowo opisane w głównym hello [przewodnik wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="6f19a-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![Synchroniczne dublowanie dla nowego dysku udziału SAP ASCS/SCS hello DataKeeper][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="6f19a-182">Wdrażanie maszyn wirtualnych dla serwerów aplikacji SAP i bazami danych klastra</span><span class="sxs-lookup"><span data-stu-id="6f19a-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="6f19a-183">Przygotowanie infrastruktury hello toocomplete hello drugiego systemu SAP, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6f19a-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="6f19a-184">Wdrażanie dedykowanych maszyn wirtualnych dla serwerów aplikacji SAP i umieść je w grupie własne dedykowane dostępności.</span><span class="sxs-lookup"><span data-stu-id="6f19a-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="6f19a-185">Wdrażanie dedykowanych maszyn wirtualnych klastra systemu DBMS i umieść je w grupie własne dedykowane dostępności.</span><span class="sxs-lookup"><span data-stu-id="6f19a-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="6f19a-186">Zainstaluj hello drugiego systemu SAP SID2 NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6f19a-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="6f19a-187">Hello Zakończ proces instalacji drugiego systemu SAP SID2 jest opisana w głównym hello [przewodnik wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="6f19a-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="6f19a-188">Procedura wysokiego poziomu Hello jest następująca:</span><span class="sxs-lookup"><span data-stu-id="6f19a-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="6f19a-189">[Zainstaluj pierwszym węźle klastra hello SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="6f19a-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="6f19a-190">W tym kroku jest instalowany SAP w wystąpieniach ASCS/SCS wysokiej dostępności na powitania **węzeł klastra usługi WSFC istniejących 1**.</span><span class="sxs-lookup"><span data-stu-id="6f19a-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="6f19a-191">[Modyfikowanie profilu SAP hello wystąpienia ASCS/SCS hello][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="6f19a-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="6f19a-192">[Skonfiguruj port sondy][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="6f19a-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="6f19a-193">W tym kroku konfigurowana jest zasób klastra SAP port sondy SAP SID2 IP przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f19a-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="6f19a-194">Tej konfiguracji należy wykonać na jednym z węzłów klastra SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="6f19a-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="6f19a-195">[Instaluj hello wystąpienie bazy danych] [sap-ha przewodnik-9.2].</span><span class="sxs-lookup"><span data-stu-id="6f19a-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="6f19a-196">W tym kroku jest instalowany system DBMS na dedykowany klaster usługi WSFC.</span><span class="sxs-lookup"><span data-stu-id="6f19a-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="6f19a-197">[Instaluj hello drugiego węzła klastra] [sap-ha przewodnik-9.3].</span><span class="sxs-lookup"><span data-stu-id="6f19a-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="6f19a-198">W tym kroku jest instalowany przy użyciu wystąpienia ASCS/SCS wysokiej dostępności na powitania istniejący WSFC węzeł klastra 2 SAP.</span><span class="sxs-lookup"><span data-stu-id="6f19a-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="6f19a-199">Otwórz porty zapory systemu Windows dla wystąpienia programu SAP ASCS/SCS hello i ProbePort.</span><span class="sxs-lookup"><span data-stu-id="6f19a-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="6f19a-200">Na obu węzłów klastra używane dla wystąpień SAP ASCS/SCS otwierasz wszystkie porty zapory systemu Windows, które są używane przez SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="6f19a-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="6f19a-201">Porty te są wymienione na powitania [przewodnik wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="6f19a-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="6f19a-202">Również otworzyć hello Azure obciążenia wewnętrznego modułu równoważenia sondowania portu, który jest 62350 w naszym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="6f19a-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="6f19a-203">[Zmień typ uruchomienia hello wystąpienie usługi SAP Wywołujących Windows hello][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="6f19a-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="6f19a-204">[Zainstaluj serwer aplikacji głównej SAP hello] [ sap-ha-guide-9.5] na powitania nowe dedykowane maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f19a-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="6f19a-205">[Instalowanie serwera aplikacji dodatkowe SAP hello] [ sap-ha-guide-9.6] na powitania nowe dedykowane maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f19a-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="6f19a-206">[Testowanie trybu failover wystąpienia programu SAP ASCS/SCS hello i replikacji SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="6f19a-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f19a-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f19a-207">Next steps</span></span>

- <span data-ttu-id="6f19a-208">[Ograniczenia sieciowe: Usługa Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="6f19a-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="6f19a-209">[Moduł równoważenia obciążenia z wieloma wirtualnymi adresami IP na platformie Azure][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="6f19a-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="6f19a-210">[Przewodnik dla wysokiej dostępności programu SAP NetWeaver na maszynach wirtualnych systemu Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="6f19a-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
