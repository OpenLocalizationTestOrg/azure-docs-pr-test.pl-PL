---
title: "Konfigurowanie usługi równoważenia obciążenia dla bazy danych SQL zawsze na | Dokumentacja firmy Microsoft"
description: "Konfigurowanie równoważenia obciążenia do pracy z SQL zawsze na i sposób korzystania z programu powershell do utworzenia modułu równoważenia obciążenia dla wdrożenia SQL"
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
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="37078-103">Konfigurowanie usługi równoważenia obciążenia dla bazy danych SQL zawsze na</span><span class="sxs-lookup"><span data-stu-id="37078-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="37078-104">Obecnie można uruchomić z ILB grup dostępności AlwaysOn programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="37078-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="37078-105">Grupa dostępności jest rozwiązania najważniejszych programu SQL Server, aby uzyskać wysoką dostępność i odzyskiwanie po awarii.</span><span class="sxs-lookup"><span data-stu-id="37078-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="37078-106">Odbiornik grupy dostępności pozwala klienta aplikacjom bezproblemowo połączyć się repliką podstawową, niezależnie od liczby replik w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="37078-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="37078-107">Nazwa odbiornika (DNS) jest mapowany na adres IP z równoważeniem obciążenia i modułowi równoważenia obciążenia Azure kieruje ruch przychodzący do serwera podstawowego zestawu replik.</span><span class="sxs-lookup"><span data-stu-id="37078-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="37078-108">Obsługa ILB można użyć dla punktów końcowych AlwaysOn programu SQL Server (odbiornika).</span><span class="sxs-lookup"><span data-stu-id="37078-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="37078-109">Teraz kontrolują dostępność odbiornika i wybrać adres IP usługi równoważenia obciążenia z określonej podsieci w sieci wirtualnej (VNet).</span><span class="sxs-lookup"><span data-stu-id="37078-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="37078-110">Za pomocą ILB na obiektu nasłuchującego punktu końcowego serwera SQL (np. serwera = tcp:ListenerName, 1433; baza danych = DatabaseName) jest dostępny tylko dla:</span><span class="sxs-lookup"><span data-stu-id="37078-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="37078-111">Usług i maszyn wirtualnych w tej samej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="37078-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="37078-112">Usług i maszyn wirtualnych z sieci połączonych lokalnie</span><span class="sxs-lookup"><span data-stu-id="37078-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="37078-113">Usług i maszyn wirtualnych z połączonych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="37078-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="37078-115">Rysunek 1 — skonfigurowana z modułem równoważenia obciążenia internetowy funkcji SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="37078-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="37078-116">Dodawanie wewnętrznego modułu równoważenia obciążenia z usługą</span><span class="sxs-lookup"><span data-stu-id="37078-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="37078-117">W poniższym przykładzie mamy konfiguruje sieci wirtualnej, która zawiera podsieć o nazwie "Podsieć 1":</span><span class="sxs-lookup"><span data-stu-id="37078-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="37078-118">Dodawanie punktów końcowych ze zrównoważonym obciążeniem dla ILB na każdej maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="37078-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="37078-119">W powyższym przykładzie masz 2 maszyny Wirtualnej o nazwie "sqlsvc1" i "sqlsvc2" działa w chmurze usługi "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="37078-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="37078-120">Po utworzeniu ILB z `DirectServerReturn` przełącznika, można dodać punktów końcowych ze zrównoważonym obciążeniem do ILB, aby umożliwić SQL skonfigurować odbiorników dla grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="37078-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="37078-121">Aby uzyskać więcej informacji o funkcji SQL AlwaysOn, zobacz [skonfigurować wewnętrzny moduł równoważenia obciążenia dla grupy dostępności AlwaysOn w usłudze Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="37078-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="37078-122">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="37078-122">See Also</span></span>
[<span data-ttu-id="37078-123">Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="37078-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="37078-124">Przed rozpoczęciem konfigurowania wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="37078-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

<span data-ttu-id="37078-125">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="37078-125">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="37078-126">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="37078-126">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
