---
title: "-Maszyn wirtualnych platformy Azure — omówienie grup dostępności serwera SQL | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono grup dostępności programu SQL Server na maszynach wirtualnych Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="dbd44-103">Wprowadzenie do programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="dbd44-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="dbd44-104">W tym artykule przedstawiono grup dostępności programu SQL Server na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd44-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="dbd44-105">Zawsze włączone grupy dostępności na maszynach wirtualnych platformy Azure są podobne do zawsze włączonych grup dostępności lokalnie.</span><span class="sxs-lookup"><span data-stu-id="dbd44-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="dbd44-106">Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd44-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="dbd44-107">Diagram przedstawia części pełną grupy dostępności serwera SQL w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd44-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="dbd44-109">Najważniejsza różnica dla grupy dostępności w maszynach wirtualnych platformy Azure jest, że maszyn wirtualnych platformy Azure, wymaga [modułu równoważenia obciążenia](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbd44-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="dbd44-110">Moduł równoważenia obciążenia zawiera adresy IP dla odbiornika grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="dbd44-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="dbd44-111">Jeśli masz więcej niż jednej grupy dostępności w każdej grupie wymaga odbiornik.</span><span class="sxs-lookup"><span data-stu-id="dbd44-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="dbd44-112">Jeden moduł równoważenia obciążenia może obsługiwać wiele odbiorników.</span><span class="sxs-lookup"><span data-stu-id="dbd44-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="dbd44-113">Gdy wszystko będzie gotowe do tworzenia aroup dostępności programu SQL Server na maszynach wirtualnych platformy Azure można znaleźć samouczki.</span><span class="sxs-lookup"><span data-stu-id="dbd44-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="dbd44-114">Automatycznie utworzyć grupy dostępności na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="dbd44-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="dbd44-115">Konfigurowanie zawsze włączonej grupy dostępności w maszynie Wirtualnej platformy Azure automatycznie - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dbd44-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="dbd44-116">Ręcznie utwórz grupę dostępności w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dbd44-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="dbd44-117">Można również utworzyć maszyny wirtualne samodzielnie bez szablonu.</span><span class="sxs-lookup"><span data-stu-id="dbd44-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="dbd44-118">Najpierw spełnić wymagania wstępne, a następnie utworzyć grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="dbd44-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="dbd44-119">Zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="dbd44-119">See the following topics:</span></span> 

- [<span data-ttu-id="dbd44-120">Konfigurowanie wymagań wstępnych dla programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dbd44-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="dbd44-121">Utwórz zawsze włączonej grupy dostępności, aby zwiększyć dostępność i odzyskiwanie po awarii</span><span class="sxs-lookup"><span data-stu-id="dbd44-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="dbd44-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbd44-122">Next steps</span></span>

<span data-ttu-id="dbd44-123">[Konfigurowanie programu SQL Server, zawsze w grupie dostępności na maszynach wirtualnych Azure w różnych regionach](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="dbd44-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
