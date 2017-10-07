---
title: "Następny przeskok aaaFind z Azure sieci obserwatora następnego przeskoku - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest przy użyciu adresu ip następnego przeskoku przy użyciu wiersza polecenia platformy Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="a86a9-103">Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a86a9-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a86a9-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a86a9-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="a86a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a86a9-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="a86a9-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="a86a9-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="a86a9-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="a86a9-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="a86a9-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="a86a9-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="a86a9-109">Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a86a9-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="a86a9-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.</span><span class="sxs-lookup"><span data-stu-id="a86a9-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="a86a9-111">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="a86a9-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a86a9-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a86a9-112">Before you begin</span></span>

<span data-ttu-id="a86a9-113">W tym scenariuszu użyje hello Azure CLI toofind hello Typ następnego przeskoku i adres IP.</span><span class="sxs-lookup"><span data-stu-id="a86a9-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="a86a9-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a86a9-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a86a9-115">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="a86a9-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a86a9-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="a86a9-116">Scenario</span></span>

<span data-ttu-id="a86a9-117">Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a86a9-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="a86a9-118">odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a86a9-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="a86a9-119">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="a86a9-119">Get Next Hop</span></span>

<span data-ttu-id="a86a9-120">tooget hello następnego przeskoku nazywamy hello `azure netowrk watcher next-hop` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a86a9-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="a86a9-121">Grupa zasobów hello polecenia cmdlet hello obserwatora sieciowego, hello NetworkWatcher maszynę wirtualną identyfikator, źródłowego adresu IP i docelowy adres IP jest przekazywana.</span><span class="sxs-lookup"><span data-stu-id="a86a9-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="a86a9-122">W tym przykładzie hello docelowy adres IP jest tooa maszyny Wirtualnej w innej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a86a9-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="a86a9-123">Między dwiema sieciami wirtualnymi hello jest bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a86a9-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="a86a9-124">Jeśli hello maszyna wirtualna ma wiele kart sieciowych i przesyłanie dalej IP jest włączona na żadnym z hello kart sieciowych, hello parametru karty Sieciowej (-i identyfikator karty sieciowej) musi być określona.</span><span class="sxs-lookup"><span data-stu-id="a86a9-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="a86a9-125">W przeciwnym razie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a86a9-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="a86a9-126">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="a86a9-126">Review results</span></span>

<span data-ttu-id="a86a9-127">Po zakończeniu hello wyniki są dostarczane.</span><span class="sxs-lookup"><span data-stu-id="a86a9-127">When complete, hello results are provided.</span></span> <span data-ttu-id="a86a9-128">oraz hello typ zasobu, który jest zwracany jest adres IP następnego przeskoku Hello.</span><span class="sxs-lookup"><span data-stu-id="a86a9-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="a86a9-129">Witaj Poniższa lista zawiera aktualnie dostępne wartości Typ następnego przeskoku hello:</span><span class="sxs-lookup"><span data-stu-id="a86a9-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="a86a9-130">**Typ następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="a86a9-130">**Next Hop Type**</span></span>

* <span data-ttu-id="a86a9-131">Internet</span><span class="sxs-lookup"><span data-stu-id="a86a9-131">Internet</span></span>
* <span data-ttu-id="a86a9-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="a86a9-132">VirtualAppliance</span></span>
* <span data-ttu-id="a86a9-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="a86a9-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="a86a9-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="a86a9-134">VnetLocal</span></span>
* <span data-ttu-id="a86a9-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="a86a9-135">HyperNetGateway</span></span>
* <span data-ttu-id="a86a9-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="a86a9-136">VnetPeering</span></span>
* <span data-ttu-id="a86a9-137">Brak</span><span class="sxs-lookup"><span data-stu-id="a86a9-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86a9-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a86a9-138">Next steps</span></span>

<span data-ttu-id="a86a9-139">Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a86a9-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
