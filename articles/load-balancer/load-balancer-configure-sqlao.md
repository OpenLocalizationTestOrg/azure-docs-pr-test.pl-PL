---
title: "dla bazy danych SQL zawsze włączone, usługi równoważenia obciążenia aaaConfigure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj toowork usługi równoważenia obciążenia z na zawsze SQL i jak Implementacja SQL hello usługę równoważenia obciążenia tooleverage toocreate programu powershell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="eb4c7-103">Konfigurowanie usługi równoważenia obciążenia dla bazy danych SQL zawsze na</span><span class="sxs-lookup"><span data-stu-id="eb4c7-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="eb4c7-104">Obecnie można uruchomić z ILB grup dostępności AlwaysOn programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eb4c7-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="eb4c7-105">Grupa dostępności jest rozwiązania najważniejszych programu SQL Server, aby uzyskać wysoką dostępność i odzyskiwanie po awarii.</span><span class="sxs-lookup"><span data-stu-id="eb4c7-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="eb4c7-106">Witaj odbiornika grupy dostępności zezwala aplikacjom klienckim tooseamlessly połączyć toohello repliki podstawowej, niezależnie od hello liczby replik hello w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="eb4c7-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="eb4c7-107">Hello nazwa odbiornika (DNS) jest adresem IP zamapowanych tooa równoważeniem obciążenia i modułowi równoważenia obciążenia Azure kieruje hello przychodzącego ruchu tooonly hello podstawowy serwer hello zestawu replik.</span><span class="sxs-lookup"><span data-stu-id="eb4c7-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="eb4c7-108">Obsługa ILB można użyć dla punktów końcowych AlwaysOn programu SQL Server (odbiornika).</span><span class="sxs-lookup"><span data-stu-id="eb4c7-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="eb4c7-109">Teraz kontrolują dostępność hello odbiornika hello i można wybrać adres IP z równoważeniem obciążenia hello określonej podsieci w sieci wirtualnej (VNet).</span><span class="sxs-lookup"><span data-stu-id="eb4c7-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="eb4c7-110">Przy użyciu ILB na powitania odbiornika, hello punkt końcowy serwera SQL (np. serwera = tcp:ListenerName, 1433; baza danych = DatabaseName) jest dostępny tylko dla:</span><span class="sxs-lookup"><span data-stu-id="eb4c7-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="eb4c7-111">Usług i maszyn wirtualnych w tej samej sieci wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="eb4c7-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="eb4c7-112">Usług i maszyn wirtualnych z sieci połączonych lokalnie</span><span class="sxs-lookup"><span data-stu-id="eb4c7-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="eb4c7-113">Usług i maszyn wirtualnych z połączonych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="eb4c7-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="eb4c7-115">Rysunek 1 — skonfigurowana z modułem równoważenia obciążenia internetowy funkcji SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="eb4c7-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="eb4c7-116">Dodawanie usługi toohello wewnętrzny moduł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="eb4c7-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="eb4c7-117">Poniższy przykład hello możemy konfigurowania w sieci wirtualnej, która zawiera podsieć o nazwie "Podsieć 1":</span><span class="sxs-lookup"><span data-stu-id="eb4c7-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="eb4c7-118">Dodawanie punktów końcowych ze zrównoważonym obciążeniem dla ILB na każdej maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="eb4c7-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="eb4c7-119">W powyższym przykładzie hello, masz 2 maszyny Wirtualnej o nazwie "sqlsvc1" i "sqlsvc2" działa w chmurze hello usługi "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="eb4c7-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="eb4c7-120">Po utworzeniu hello ILB z `DirectServerReturn` przełącznika, możesz dodać punktów końcowych ze zrównoważonym toohello ILB tooallow SQL tooconfigure hello odbiorników dla grup dostępności hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="eb4c7-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="eb4c7-121">Aby uzyskać więcej informacji o funkcji SQL AlwaysOn, zobacz [skonfigurować wewnętrzny moduł równoważenia obciążenia dla grupy dostępności AlwaysOn w usłudze Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="eb4c7-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="eb4c7-122">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="eb4c7-122">See Also</span></span>
[<span data-ttu-id="eb4c7-123">Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="eb4c7-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="eb4c7-124">Przed rozpoczęciem konfigurowania wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="eb4c7-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

<span data-ttu-id="eb4c7-125">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="eb4c7-125">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="eb4c7-126">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="eb4c7-126">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
