---
title: Wprowadzenie do topologii w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera przegląd możliwości topologii obserwatora sieciowego"
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
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="237b7-103">Wprowadzenie do topologii w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="237b7-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="237b7-104">Topologia zwraca wykres zasobów sieciowych w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="237b7-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="237b7-105">Wykres przedstawia połączenia między zasobami do reprezentowania łączność sieciową pełnego.</span><span class="sxs-lookup"><span data-stu-id="237b7-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![Omówienie topologii][1]

<span data-ttu-id="237b7-107">W portalu topologii zwraca obiekty zasobów na poszczególnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="237b7-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="237b7-108">Relacje są określone przez linie między zasobami zasobów poza region obserwatora sieciowego, nawet jeśli w zasobie grupy nie zostaną wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="237b7-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="237b7-109">Zasoby zwracane w widoku portalu są podzbiorem składników sieciowych, które są wyświetlone na wykresie.</span><span class="sxs-lookup"><span data-stu-id="237b7-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="237b7-110">Aby wyświetlić pełną listę zasobów sieciowych, można użyć [PowerShell](network-watcher-topology-powershell.md) lub [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="237b7-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="237b7-111">Wystąpienie Monitora sieci jest wymagana w każdym regionie, który chcesz uruchomić topologii.</span><span class="sxs-lookup"><span data-stu-id="237b7-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="237b7-112">Ponieważ zasoby są zwracane połączenia między nimi są modelowane w obszarze dwie relacje.</span><span class="sxs-lookup"><span data-stu-id="237b7-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="237b7-113">**Zawieranie** — przykład: sieć wirtualna zawiera podsieci, która zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="237b7-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="237b7-114">**Skojarzone** — przykład: A kart interfejsu Sieciowego jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="237b7-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="237b7-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="237b7-115">Next steps</span></span>

<span data-ttu-id="237b7-116">Dowiedz się, jak za pomocą programu PowerShell można pobrać widoku topologii odwiedzając [topologii obserwatora sieciowego przy użyciu programu PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="237b7-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
