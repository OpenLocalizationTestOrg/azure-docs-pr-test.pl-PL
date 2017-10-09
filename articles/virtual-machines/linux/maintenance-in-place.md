---
title: aaaVM zachowania konserwacji dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Migracja w miejscu maszyny Wirtualnej pamięci, zachowując aktualizacji."
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a><span data-ttu-id="2aafb-103">Maszyna wirtualna, zachowując konserwacji (migracja maszyny Wirtualnej w miejscu)</span><span class="sxs-lookup"><span data-stu-id="2aafb-103">VM preserving maintenance (In-place VM migration)</span></span>

<span data-ttu-id="2aafb-104">Podczas aktualizacji hello większość toohosted nie wpływu na maszynach wirtualnych, istnieją przypadki, w których toocomponents aktualizacji lub usług spowodować zakłócenia minimalnego toorunning maszyn wirtualnych (bez pełnego ponownego uruchomienia maszyny wirtualnej hello).</span><span class="sxs-lookup"><span data-stu-id="2aafb-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="2aafb-105">Te aktualizacje są realizowane za pomocą technologii, która umożliwia migrację na żywo w miejscu, nazywane również "zachowywania pamięci update".</span><span class="sxs-lookup"><span data-stu-id="2aafb-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="2aafb-106">Podczas aktualizowania hosta hello, hello maszyny wirtualnej jest umieszczany w "" wstrzymana, zachowując hello pamięci RAM, hello hosting środowiska (np. system operacyjny) dotyczy hello niezbędne aktualizacje i poprawki.</span><span class="sxs-lookup"><span data-stu-id="2aafb-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="2aafb-107">Maszyna wirtualna Hello następnie zostanie wznowione w ciągu 30 sekund wstrzymywane.</span><span class="sxs-lookup"><span data-stu-id="2aafb-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="2aafb-108">Po wznowieniu pracy, zostanie automatycznie zsynchronizowana zegara hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2aafb-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="2aafb-109">Nie wszystkie aktualizacje można wdrożyć przy użyciu ten mechanizm, ale podany okres krótkiej przerwie wdrażania aktualizacji w ten sposób znacznie zmniejsza wpływ toovirtual maszyny.</span><span class="sxs-lookup"><span data-stu-id="2aafb-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="2aafb-110">Mająca wiele wystąpień aktualizacje (maszyn wirtualnych w zestawie dostępności) są stosowane jednej domeny aktualizacji w czasie.</span><span class="sxs-lookup"><span data-stu-id="2aafb-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="2aafb-111">Niektóre aplikacje może mieć wpływ na więcej niż inne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="2aafb-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="2aafb-112">Aplikacje wykonujące przetwarzania zdarzeń w czasie rzeczywistym, przesyłania strumieniowego multimediów lub transkodowanie lub uzyskać wysoką przepustowość sieci scenariusze, na przykład nie można zaprojektowanego tootolerate 30 jednosekundową przerwę.</span><span class="sxs-lookup"><span data-stu-id="2aafb-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="2aafb-113">Aplikacje działające na maszynie wirtualnej dowiedzieć się o nadchodzących aktualizacji przez wywołanie hello [zaplanowane zdarzenia](../virtual-machines-scheduled-events.md) API hello [Azure metadanych usługi](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2aafb-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
