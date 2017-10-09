---
title: "Następny przeskok aaaFind z Azure sieci obserwatora następnego przeskoku - portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest adres ip przy użyciu następnego przeskoku hello portalu Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="86819-103">Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure za pomocą portalu hello</span><span class="sxs-lookup"><span data-stu-id="86819-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="86819-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="86819-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="86819-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86819-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="86819-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="86819-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="86819-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="86819-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="86819-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="86819-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="86819-109">Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86819-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="86819-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.</span><span class="sxs-lookup"><span data-stu-id="86819-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="86819-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="86819-111">Before you begin</span></span>

<span data-ttu-id="86819-112">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="86819-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="86819-113">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="86819-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="86819-114">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="86819-114">Scenario</span></span>

<span data-ttu-id="86819-115">Scenariusz Hello omówione w tym artykule używa następnego przeskoku toofind Typ następnego przeskoku hello i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="86819-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="86819-116">odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86819-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="86819-117">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="86819-117">In this scenario, you will:</span></span>

* <span data-ttu-id="86819-118">Pobrać hello następnego przeskoku z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86819-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="86819-119">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="86819-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="86819-120">Krok 1</span><span class="sxs-lookup"><span data-stu-id="86819-120">Step 1</span></span>

<span data-ttu-id="86819-121">Przejdź tooyour obserwatora sieciowego zasobu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="86819-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="86819-122">Krok 2</span><span class="sxs-lookup"><span data-stu-id="86819-122">Step 2</span></span>

<span data-ttu-id="86819-123">Kliknij przycisk **następnego przeskoku** w hello okienka nawigacji, wybierz hello maszyny wirtualnej i interfejsu sieciowego, wypełnij hello źródłowego i docelowego adresu IP, a następnie kliknij przycisk hello **następnego przeskoku** przycisku.</span><span class="sxs-lookup"><span data-stu-id="86819-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="86819-124">Następnego przeskoku wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.</span><span class="sxs-lookup"><span data-stu-id="86819-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![Pobierz następnego przeskoku — omówienie][1]

### <a name="step-3"></a><span data-ttu-id="86819-126">Krok 3</span><span class="sxs-lookup"><span data-stu-id="86819-126">Step 3</span></span>

<span data-ttu-id="86819-127">Po zakończeniu zadania hello hello wyniki są dostarczane.</span><span class="sxs-lookup"><span data-stu-id="86819-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="86819-128">Witaj, adres IP i typ następnego przeskoku hello urządzenia jest, zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="86819-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="86819-129">Witaj poniższej tabeli przedstawiono dostępne wartości zwracane hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="86819-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="86819-130">**Typ następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="86819-130">**Next Hop Type**</span></span>

* <span data-ttu-id="86819-131">Internet</span><span class="sxs-lookup"><span data-stu-id="86819-131">Internet</span></span>
* <span data-ttu-id="86819-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="86819-132">VirtualAppliance</span></span>
* <span data-ttu-id="86819-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="86819-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="86819-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="86819-134">VnetLocal</span></span>
* <span data-ttu-id="86819-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="86819-135">HyperNetGateway</span></span>
* <span data-ttu-id="86819-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="86819-136">VnetPeering</span></span>
* <span data-ttu-id="86819-137">Brak</span><span class="sxs-lookup"><span data-stu-id="86819-137">None</span></span>

<span data-ttu-id="86819-138">Jeśli niestandardowa trasa został użyty tooroute ten ruch trasy zdefiniowane przez użytkownika hello (przez) wyświetlany jest również z wynikami hello.</span><span class="sxs-lookup"><span data-stu-id="86819-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![Następny przeskok wyniki][2]

## <a name="next-steps"></a><span data-ttu-id="86819-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86819-140">Next steps</span></span>

<span data-ttu-id="86819-141">Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="86819-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














