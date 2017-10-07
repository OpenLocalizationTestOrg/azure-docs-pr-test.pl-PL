---
title: "Omówienie grup dostępności serwera — maszyny wirtualne Azure - aaaSQL | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="00e48-103">Wprowadzenie do programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="00e48-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="00e48-104">W tym artykule przedstawiono grup dostępności programu SQL Server na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="00e48-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="00e48-105">Zawsze włączone grupy dostępności na maszynach wirtualnych platformy Azure są podobne tooAlways dotyczących grup dostępności lokalnie.</span><span class="sxs-lookup"><span data-stu-id="00e48-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="00e48-106">Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="00e48-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="00e48-107">Witaj diagram przedstawia hello części pełną grupy dostępności serwera SQL w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="00e48-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="00e48-109">Witaj Najważniejsza różnica dla grupy dostępności w maszynach wirtualnych platformy Azure jest, który hello maszyn wirtualnych platformy Azure, wymagają [modułu równoważenia obciążenia](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00e48-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="00e48-110">Moduł równoważenia obciążenia Hello przechowuje hello adresów IP dla odbiornika grupy dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="00e48-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="00e48-111">Jeśli masz więcej niż jednej grupy dostępności w każdej grupie wymaga odbiornik.</span><span class="sxs-lookup"><span data-stu-id="00e48-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="00e48-112">Jeden moduł równoważenia obciążenia może obsługiwać wiele odbiorników.</span><span class="sxs-lookup"><span data-stu-id="00e48-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="00e48-113">Gdy wszystko jest gotowe toobuild aroup dostępności programu SQL Server na maszynach wirtualnych platformy Azure, można znaleźć samouczki toothese.</span><span class="sxs-lookup"><span data-stu-id="00e48-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="00e48-114">Automatycznie utworzyć grupy dostępności na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="00e48-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="00e48-115">Konfigurowanie zawsze włączonej grupy dostępności w maszynie Wirtualnej platformy Azure automatycznie - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="00e48-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="00e48-116">Ręcznie utwórz grupę dostępności w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="00e48-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="00e48-117">Można również utworzyć maszyny wirtualne hello samodzielnie bez hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="00e48-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="00e48-118">Najpierw należy ukończyć powitalnych wymagania wstępne, a następnie utworzyć grupy dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="00e48-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="00e48-119">Zobacz hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="00e48-119">See hello following topics:</span></span> 

- [<span data-ttu-id="00e48-120">Konfigurowanie wymagań wstępnych dla programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="00e48-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="00e48-121">Utwórz zawsze włączonej grupy dostępności tooimprove dostępności i odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="00e48-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="00e48-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="00e48-122">Next steps</span></span>

<span data-ttu-id="00e48-123">[Konfigurowanie programu SQL Server, zawsze w grupie dostępności na maszynach wirtualnych Azure w różnych regionach](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="00e48-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
