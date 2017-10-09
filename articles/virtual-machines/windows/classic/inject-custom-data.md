---
title: dane aaaInject do maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "W tym temacie opisano, jak tooinject niestandardowe dane do wirtualnej Azure komputera, gdy jest tworzone wystąpienie hello i jak toolocate hello niestandardowe dane w systemie Windows lub Linux."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 48759f76-eaa0-4202-ada0-706d3f9a9467
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 2b2a12e5d0942fa957387ace7e38a353dbf27197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="ed623-103">Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ed623-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ed623-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed623-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ed623-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ed623-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ed623-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed623-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ed623-107">Aby uzyskać informacji o korzystaniu z modelu Resource Manager hello hello niestandardowe rozszerzenie skryptu, zobacz [tutaj](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed623-107">For information about using hello Custom Script Extension with hello Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

