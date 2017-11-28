---
title: tootopology aaaIntroduction w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie funkcji topologii hello obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="dde61-103">Wprowadzenie tootopology w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="dde61-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="dde61-104">Topologia zwraca wykres zasobów sieciowych w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dde61-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="dde61-105">Witaj wykres przedstawia hello połączenia między łączności sieciowej tooend hello zasobów toorepresent hello zakończenia.</span><span class="sxs-lookup"><span data-stu-id="dde61-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![Omówienie topologii][1]

<span data-ttu-id="dde61-107">W portalu hello topologii zwraca obiekty zasobów hello na poszczególnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dde61-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="dde61-108">Relacje Hello są określone przez linie między zasobami hello zasobów poza region obserwatora sieciowego hello, nawet jeśli w zasobie hello grupy nie zostaną wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="dde61-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="dde61-109">zasoby Hello zwracane w widoku portalu hello są podzbiorem hello składników sieciowych, które są wyświetlone na wykresie.</span><span class="sxs-lookup"><span data-stu-id="dde61-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="dde61-110">toosee hello pełną listę zasobów sieciowych można użyć [PowerShell](network-watcher-topology-powershell.md) lub [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="dde61-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="dde61-111">Wystąpienie Monitora sieci jest wymagana w każdym regionie, który ma być toorun topologii.</span><span class="sxs-lookup"><span data-stu-id="dde61-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="dde61-112">Ponieważ zasoby są zwracane hello połączenia między nimi są modelowane w obszarze dwie relacje.</span><span class="sxs-lookup"><span data-stu-id="dde61-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="dde61-113">**Zawieranie** — przykład: sieć wirtualna zawiera podsieci, która zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="dde61-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="dde61-114">**Skojarzone** — przykład: A kart interfejsu Sieciowego jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="dde61-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="dde61-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dde61-115">Next steps</span></span>

<span data-ttu-id="dde61-116">Dowiedz się, jak wyświetlić toouse PowerShell tooretrieve hello topologii odwiedzając [topologii obserwatora sieciowego przy użyciu programu PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="dde61-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
