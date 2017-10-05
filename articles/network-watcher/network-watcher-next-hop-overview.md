---
title: "Wprowadzenie do następnego przeskoku obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie obserwatora sieciowego następnego przeskoku możliwości"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="2a04d-103">Wprowadzenie do następnego przeskoku obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="2a04d-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="2a04d-104">Ruch z maszyny Wirtualnej są wysyłane do lokalizacji docelowej, na podstawie tras skuteczne skojarzony z jedną kartą sieciową.</span><span class="sxs-lookup"><span data-stu-id="2a04d-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="2a04d-105">Następny przeskok pobiera typ następnego przeskoku i adres IP pakietu z określonej maszyny wirtualnej i karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="2a04d-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="2a04d-106">Dzięki temu do określenia, czy pakiet jest być kierowany do lokalizacji docelowej i jest holed ruchu jest czarny.</span><span class="sxs-lookup"><span data-stu-id="2a04d-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="2a04d-107">Niepoprawna konfiguracja tras przez użytkownika, których ruch jest kierowany do lokalizacji lokalnej lub urządzenie wirtualne, może prowadzić do problemów z łącznością.</span><span class="sxs-lookup"><span data-stu-id="2a04d-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="2a04d-108">Następny przeskok zwraca również wartość tabeli tras skojarzone z następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="2a04d-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="2a04d-109">Podczas wykonywania zapytania następnego przeskoku, jeśli trasa jest zdefiniowana jako trasy zdefiniowane przez użytkownika, zostanie zwrócony tej trasy.</span><span class="sxs-lookup"><span data-stu-id="2a04d-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="2a04d-110">W przeciwnym razie wartość następnego skoku zwraca "Trasa systemowa".</span><span class="sxs-lookup"><span data-stu-id="2a04d-110">Otherwise Next hop returns "System Route".</span></span>

![następnego przeskoku — omówienie][1]

<span data-ttu-id="2a04d-112">Poniżej znajduje się lista typów następnego przeskoku, które mogą być zwrócone podczas wykonywania zapytania w następnym przeskoku.</span><span class="sxs-lookup"><span data-stu-id="2a04d-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="2a04d-113">Internet</span><span class="sxs-lookup"><span data-stu-id="2a04d-113">Internet</span></span>
* <span data-ttu-id="2a04d-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="2a04d-114">VirtualAppliance</span></span>
* <span data-ttu-id="2a04d-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="2a04d-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="2a04d-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="2a04d-116">VnetLocal</span></span>
* <span data-ttu-id="2a04d-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="2a04d-117">HyperNetGateway</span></span>
* <span data-ttu-id="2a04d-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="2a04d-118">VnetPeering</span></span>
* <span data-ttu-id="2a04d-119">Brak</span><span class="sxs-lookup"><span data-stu-id="2a04d-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="2a04d-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2a04d-120">Next steps</span></span>

<span data-ttu-id="2a04d-121">Dowiedz się, jak znaleźć problemy z połączeniem sieciowym, odwiedzając za pomocą następnego przeskoku [Sprawdź następnego przeskoku na maszynie Wirtualnej](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2a04d-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













