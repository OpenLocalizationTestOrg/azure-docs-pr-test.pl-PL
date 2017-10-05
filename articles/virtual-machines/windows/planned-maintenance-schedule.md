---
title: "Sposób tworzenia harmonogramu konserwacji dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zaplanować zaplanowanej konserwacji na maszynach wirtualnych Azure."
services: virtual-machines-windows
documentationcenter: 
author: igalf
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ab33e5da-6bb6-4e95-a7a6-a6303d21b15c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: igalf
ms.openlocfilehash: 7c137d6709ec246fd93e70dd46eed78b4288d05a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-schedule-planned-maintenance-on-azure-vms"></a><span data-ttu-id="bf967-103">Sposób tworzenia harmonogramu zaplanowanej konserwacji na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="bf967-103">How to Schedule Planned Maintenance on Azure VMs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bf967-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf967-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf967-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="bf967-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bf967-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bf967-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="bf967-107">Informacje o zaplanowanej konserwacji w modelu usługi Resource Manager, zobacz [tutaj](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf967-107">For information about planned maintenance in the Resource Manager model, see [here](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-planned-maintenance-schedule](../../../includes/virtual-machines-common-planned-maintenance-schedule.md)]
