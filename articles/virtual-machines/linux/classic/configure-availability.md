---
title: Ustawia aaaAvailability klasycznych maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Skonfiguruj zbiór dostępności dla maszyny wirtualnej systemu Linux nowego lub istniejącego w hello klasycznego modelu wdrażania przy użyciu hello portalu Azure i programu Azure PowerShell."
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
ms.openlocfilehash: 8d8d041e3540e42a1921f5665469a2fdcaa30a29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-linux-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="75d9a-103">Jak tooconfigure, zbiór dostępności, dla maszyn wirtualnych systemu Linux w hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="75d9a-103">How tooconfigure an availability set for Linux virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="75d9a-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="75d9a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="75d9a-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="75d9a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="75d9a-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="75d9a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="75d9a-107">Możesz również [skonfigurować zestawy dostępności](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) w przypadku wdrożeń usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="75d9a-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]