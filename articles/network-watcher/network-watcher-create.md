---
title: "aaaCreate wystąpienia obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera toocreate kroki hello wystąpienia obserwatora sieciowego przy użyciu portalu hello i interfejsu API REST Azure"
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="16cce-103">Utwórz wystąpienie obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="16cce-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="16cce-104">Obserwatora sieciowego jest usługą regionalnych, która umożliwia toomonitor możesz i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16cce-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="16cce-105">Scenariusz poziomu monitorowania umożliwia problemów toodiagnose na końcu tooend poziomu widok sieci.</span><span class="sxs-lookup"><span data-stu-id="16cce-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="16cce-106">Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="16cce-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="16cce-107">Obserwatora sieciowego aktualnie obsługuje tylko 1.0 interfejsu wiersza polecenia, toocreate instrukcje hello nowego wystąpienia obserwatora sieciowego jest dostępna dla interfejsu wiersza polecenia 1.0.</span><span class="sxs-lookup"><span data-stu-id="16cce-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="16cce-108">Utwórz w portalu hello obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="16cce-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="16cce-109">Przejdź za**więcej usług** > **sieci** > **obserwatora sieciowego**.</span><span class="sxs-lookup"><span data-stu-id="16cce-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="16cce-110">Możesz wybrać wszystkie subskrypcje hello ma tooenable obserwatora sieciowego dla.</span><span class="sxs-lookup"><span data-stu-id="16cce-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="16cce-111">Ta akcja tworzy obserwatora sieciowego w każdym regionie dostępnej.</span><span class="sxs-lookup"><span data-stu-id="16cce-111">This action creates a Network Watcher in every region that is available.</span></span>

![Utwórz obserwatora sieciowego][1]

<span data-ttu-id="16cce-113">Po włączeniu obserwatora sieciowego przy użyciu portalu hello hello nazwę wystąpienia obserwatora sieciowego hello zostanie automatycznie ustawiona tooNetworkWatcher_region_name gdzie region_name odpowiada toohello regionu Azure, gdy włączono hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="16cce-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="16cce-114">Na przykład będzie nazwę obserwatora sieciowego, włączona w regionie Zachód środkowe stany NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="16cce-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="16cce-115">Ponadto wystąpienia obserwatora sieciowego hello automatycznie zostanie dodany do grupy zasobów o nazwie NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="16cce-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="16cce-116">Ta grupa zasobów zostanie utworzony, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="16cce-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="16cce-117">Jeśli chcesz, aby nazwa hello toocustomize wystąpienia obserwatora sieciowego i hello grupy zasobów została umieszczona w, możesz użyć programu Powershell, interfejsu API REST hello lub ARMClient metod opisanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="16cce-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="16cce-118">W przypadku każdej opcji hello grupy zasobów musi istnieć przed umieszczeniem hello obserwatora sieciowego do niego.</span><span class="sxs-lookup"><span data-stu-id="16cce-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="16cce-119">Utwórz obserwatora sieciowego przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="16cce-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="16cce-120">toocreate wystąpienia obserwatora sieciowego, uruchom poniższy przykład hello:</span><span class="sxs-lookup"><span data-stu-id="16cce-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="16cce-121">Utwórz obserwatora sieciowego z hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="16cce-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="16cce-122">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16cce-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="16cce-123">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="16cce-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="16cce-124">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="16cce-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="16cce-125">Utwórz hello obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="16cce-125">Create hello network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="16cce-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16cce-126">Next steps</span></span>

<span data-ttu-id="16cce-127">Teraz, gdy masz wystąpienie obserwatora sieciowego Dowiedz się więcej o funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="16cce-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="16cce-128">Topologia</span><span class="sxs-lookup"><span data-stu-id="16cce-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="16cce-129">Przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="16cce-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="16cce-130">Weryfikowanie przepływu adresów IP</span><span class="sxs-lookup"><span data-stu-id="16cce-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="16cce-131">Następny przeskok</span><span class="sxs-lookup"><span data-stu-id="16cce-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="16cce-132">Widok grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="16cce-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="16cce-133">Rejestrowanie przepływu NSG</span><span class="sxs-lookup"><span data-stu-id="16cce-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="16cce-134">Rozwiązywanie problemów bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="16cce-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="16cce-135">Po utworzeniu wystąpienia obserwatora sieciowego przechwytywania pakietu można skonfigurować w następującym artykule hello: [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="16cce-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











