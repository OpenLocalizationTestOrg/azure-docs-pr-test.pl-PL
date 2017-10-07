---
title: przeskoku toonext aaaIntroduction obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello obserwatora sieciowego następnego przeskoku możliwości"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="03e1a-103">Wprowadzenie przeskoku toonext obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="03e1a-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="03e1a-104">Ruch z maszyny Wirtualnej jest wysyłany tooa docelowym oparte na trasach efektywne hello skojarzony z jedną kartą sieciową.</span><span class="sxs-lookup"><span data-stu-id="03e1a-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="03e1a-105">Następny przeskok pobiera typ następnego przeskoku hello i adres IP pakietu z określonej maszyny wirtualnej i karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="03e1a-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="03e1a-106">Dzięki temu toodetermine hello pakietów jest docelowy skierowanego toohello lub jest holed ruchu hello jest czarny.</span><span class="sxs-lookup"><span data-stu-id="03e1a-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="03e1a-107">Niepoprawna konfiguracja tras przez użytkownika hello, w których ruch jest ukierunkowanej tooan lokalnej lokalizacji lub urządzenie wirtualne, może spowodować problemy tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="03e1a-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="03e1a-108">Następny przeskok zwraca również wartość tabeli tras hello skojarzone z następnego przeskoku hello.</span><span class="sxs-lookup"><span data-stu-id="03e1a-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="03e1a-109">Podczas wykonywania zapytania następnego przeskoku, jeśli trasa hello jest zdefiniowana jako trasy zdefiniowane przez użytkownika, zostanie zwrócony tej trasy.</span><span class="sxs-lookup"><span data-stu-id="03e1a-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="03e1a-110">W przeciwnym razie wartość następnego skoku zwraca "Trasa systemowa".</span><span class="sxs-lookup"><span data-stu-id="03e1a-110">Otherwise Next hop returns "System Route".</span></span>

![następnego przeskoku — omówienie][1]

<span data-ttu-id="03e1a-112">Witaj poniżej znajduje się lista hello następnego przeskoku typów, które mogą być zwrócone podczas wykonywania zapytania w następnym przeskoku.</span><span class="sxs-lookup"><span data-stu-id="03e1a-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="03e1a-113">Internet</span><span class="sxs-lookup"><span data-stu-id="03e1a-113">Internet</span></span>
* <span data-ttu-id="03e1a-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="03e1a-114">VirtualAppliance</span></span>
* <span data-ttu-id="03e1a-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="03e1a-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="03e1a-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="03e1a-116">VnetLocal</span></span>
* <span data-ttu-id="03e1a-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="03e1a-117">HyperNetGateway</span></span>
* <span data-ttu-id="03e1a-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="03e1a-118">VnetPeering</span></span>
* <span data-ttu-id="03e1a-119">Brak</span><span class="sxs-lookup"><span data-stu-id="03e1a-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="03e1a-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03e1a-120">Next steps</span></span>

<span data-ttu-id="03e1a-121">Dowiedz się, jak toouse następnego przeskoku toofind problemy z połączeniem sieciowym, odwiedzając [wyboru hello następnego przeskoku na maszynie Wirtualnej](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="03e1a-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













