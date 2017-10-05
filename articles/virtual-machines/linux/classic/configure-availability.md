---
title: "Zestawy dostępności dla maszyn wirtualnych systemu Linux klasycznego | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zbiór dostępności dla maszyny wirtualnej systemu Linux nowego lub istniejącego w klasycznym modelu wdrażania przy użyciu portalu Azure i programu Azure PowerShell."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 41d427862150d17e1ad726afc51114d6f62f5a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-linux-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="4c487-103">Jak skonfigurować zbiór dostępności dla maszyn wirtualnych systemu Linux w klasycznym modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="4c487-103">How to configure an availability set for Linux virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4c487-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4c487-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c487-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4c487-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4c487-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c487-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4c487-107">Możesz również [skonfigurować zestawy dostępności](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) w przypadku wdrożeń usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c487-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]