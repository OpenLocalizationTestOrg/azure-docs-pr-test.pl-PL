---
title: "Utwórz wystąpienie obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona przedstawia kroki tworzenia wystąpienia obserwatora sieciowego przy użyciu portalu i interfejsu API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="1e2c4-103">Utwórz wystąpienie obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="1e2c4-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="1e2c4-104">Monitor sieci jest regionalnych usługa, która umożliwia monitorowanie i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="1e2c4-105">Scenariusz poziomu monitorowania umożliwia diagnozowanie problemów w sieci pełnego widoku poziomu.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="1e2c4-106">Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i Uzyskaj wgląd do sieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1e2c4-107">Obserwatora sieciowego aktualnie obsługuje tylko 1.0 interfejsu wiersza polecenia, z instrukcjami, aby utworzyć nowe wystąpienie obserwatora sieciowego jest dostępna dla interfejsu wiersza polecenia 1.0.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="1e2c4-108">Utwórz obserwatora sieciowego w portalu</span><span class="sxs-lookup"><span data-stu-id="1e2c4-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="1e2c4-109">Przejdź do **więcej usług** > **sieci** > **sieci obserwatora**.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="1e2c4-110">Możesz wybrać wszystkie subskrypcje, które chcesz włączyć Monitor sieci.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="1e2c4-111">Ta akcja tworzy obserwatora sieciowego w każdym regionie dostępnej.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-111">This action creates a Network Watcher in every region that is available.</span></span>

![Utwórz obserwatora sieciowego][1]

<span data-ttu-id="1e2c4-113">Po włączeniu obserwatora sieciowego przy użyciu portalu automatycznie można ustawić nazwę wystąpienia obserwatora sieciowego do NetworkWatcher_region_name gdzie region_name odpowiada regionu Azure, gdy wystąpienie zostało włączone.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-113">When you enable Network Watcher using the Portal, the name of the Network Watcher instance will automatically be set to NetworkWatcher_region_name where region_name corresponds to the Azure Region where the instance was enabled.</span></span>  <span data-ttu-id="1e2c4-114">Na przykład będzie nazwę obserwatora sieciowego, włączona w regionie Zachód środkowe stany NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="1e2c4-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="1e2c4-115">Ponadto wystąpienia obserwatora sieciowego automatycznie zostanie dodany do grupy zasobów o nazwie NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-115">Additionally, the Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="1e2c4-116">Ta grupa zasobów zostanie utworzony, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="1e2c4-117">Jeśli chcesz dostosować nazwę wystąpienia obserwatora sieciowego i grupy zasobów jest umieszczany w, możesz użyć programu Powershell, interfejsu API REST lub ARMClient metod opisanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-117">If you wish to customize the name of a Network Watcher instance and the Resource Group it's placed into, you can use Powershell, the REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="1e2c4-118">W każdej opcji grupy zasobów musi istnieć przed umieszczeniem obserwatora sieciowego do niego.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-118">In each option, the Resource Group must exist before you place the Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="1e2c4-119">Utwórz obserwatora sieciowego przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e2c4-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="1e2c4-120">Aby utworzyć wystąpienie obserwatora sieciowego, należy uruchomić poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="1e2c4-120">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="1e2c4-121">Utwórz obserwatora sieciowego przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="1e2c4-121">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="1e2c4-122">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e2c4-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="1e2c4-123">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="1e2c4-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="1e2c4-124">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="1e2c4-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="1e2c4-125">Utwórz obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="1e2c4-125">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="1e2c4-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e2c4-126">Next steps</span></span>

<span data-ttu-id="1e2c4-127">Teraz, gdy masz wystąpienie obserwatora sieciowego Dowiedz się więcej o funkcjach dostępnych:</span><span class="sxs-lookup"><span data-stu-id="1e2c4-127">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="1e2c4-128">Topologia</span><span class="sxs-lookup"><span data-stu-id="1e2c4-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="1e2c4-129">Przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="1e2c4-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="1e2c4-130">Weryfikowanie przepływu adresów IP</span><span class="sxs-lookup"><span data-stu-id="1e2c4-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="1e2c4-131">Następny przeskok</span><span class="sxs-lookup"><span data-stu-id="1e2c4-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="1e2c4-132">Widok grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="1e2c4-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="1e2c4-133">Rejestrowanie przepływu NSG</span><span class="sxs-lookup"><span data-stu-id="1e2c4-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="1e2c4-134">Rozwiązywanie problemów bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1e2c4-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="1e2c4-135">Po utworzeniu wystąpienia obserwatora sieciowego przechwytywania pakietu można skonfigurować, postępując w artykule: [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="1e2c4-135">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











