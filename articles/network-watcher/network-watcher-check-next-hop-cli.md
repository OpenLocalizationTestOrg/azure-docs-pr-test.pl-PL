---
title: "Następny przeskok aaaFind z Azure sieci obserwatora następnego przeskoku - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="8c38c-103">Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="8c38c-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8c38c-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8c38c-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="8c38c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c38c-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="8c38c-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="8c38c-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="8c38c-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="8c38c-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="8c38c-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="8c38c-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="8c38c-109">Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c38c-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="8c38c-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.</span><span class="sxs-lookup"><span data-stu-id="8c38c-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="8c38c-111">W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="8c38c-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8c38c-112">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8c38c-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8c38c-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8c38c-113">Before you begin</span></span>

<span data-ttu-id="8c38c-114">W tym scenariuszu użyje hello Azure CLI toofind hello Typ następnego przeskoku i adres IP.</span><span class="sxs-lookup"><span data-stu-id="8c38c-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="8c38c-115">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="8c38c-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="8c38c-116">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="8c38c-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="8c38c-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="8c38c-117">Scenario</span></span>

<span data-ttu-id="8c38c-118">Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="8c38c-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="8c38c-119">odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c38c-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="8c38c-120">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="8c38c-120">Get Next Hop</span></span>

<span data-ttu-id="8c38c-121">tooget hello następnego przeskoku nazywamy hello `az network watcher show-next-hop` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c38c-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="8c38c-122">Grupa zasobów hello polecenia cmdlet hello obserwatora sieciowego, hello NetworkWatcher maszynę wirtualną identyfikator, źródłowego adresu IP i docelowy adres IP jest przekazywana.</span><span class="sxs-lookup"><span data-stu-id="8c38c-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="8c38c-123">W tym przykładzie hello docelowy adres IP jest tooa maszyny Wirtualnej w innej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c38c-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="8c38c-124">Między dwiema sieciami wirtualnymi hello jest bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c38c-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="8c38c-125">Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8c38c-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="8c38c-126">Następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8c38c-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="8c38c-127">Jeśli hello maszyna wirtualna ma wiele kart sieciowych i przesyłanie dalej IP jest włączona na żadnym z hello kart sieciowych, hello parametru karty Sieciowej (-i identyfikator karty sieciowej) musi być określona.</span><span class="sxs-lookup"><span data-stu-id="8c38c-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="8c38c-128">W przeciwnym razie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="8c38c-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="8c38c-129">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="8c38c-129">Review results</span></span>

<span data-ttu-id="8c38c-130">Po zakończeniu hello wyniki są dostarczane.</span><span class="sxs-lookup"><span data-stu-id="8c38c-130">When complete, hello results are provided.</span></span> <span data-ttu-id="8c38c-131">oraz hello typ zasobu, który jest zwracany jest adres IP następnego przeskoku Hello.</span><span class="sxs-lookup"><span data-stu-id="8c38c-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="8c38c-132">Witaj Poniższa lista zawiera aktualnie dostępne wartości Typ następnego przeskoku hello:</span><span class="sxs-lookup"><span data-stu-id="8c38c-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="8c38c-133">**Typ następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="8c38c-133">**Next Hop Type**</span></span>

* <span data-ttu-id="8c38c-134">Internet</span><span class="sxs-lookup"><span data-stu-id="8c38c-134">Internet</span></span>
* <span data-ttu-id="8c38c-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="8c38c-135">VirtualAppliance</span></span>
* <span data-ttu-id="8c38c-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="8c38c-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="8c38c-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="8c38c-137">VnetLocal</span></span>
* <span data-ttu-id="8c38c-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="8c38c-138">HyperNetGateway</span></span>
* <span data-ttu-id="8c38c-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="8c38c-139">VnetPeering</span></span>
* <span data-ttu-id="8c38c-140">Brak</span><span class="sxs-lookup"><span data-stu-id="8c38c-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c38c-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c38c-141">Next steps</span></span>

<span data-ttu-id="8c38c-142">Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8c38c-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
