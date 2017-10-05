---
title: "Znajdź następny przeskok z sieci platformy Azure obserwatora następnego przeskoku - REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak znaleźć, co to jest typ następnego przeskoku i adres ip za pomocą następnego przeskoku przy użyciu interfejsu API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="1b4f5-103">Sprawdź, jaki typ następnego przeskoku jest przy użyciu funkcji w następnym przeskoku w obserwatora sieciowego Azure przy użyciu interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="1b4f5-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1b4f5-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b4f5-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="1b4f5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b4f5-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="1b4f5-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="1b4f5-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="1b4f5-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="1b4f5-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="1b4f5-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="1b4f5-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="1b4f5-109">Następny przeskok jest funkcją obserwatora sieciowego, który zapewnia możliwość get Typ następnego przeskoku i adres IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="1b4f5-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne na uzyskanie dostępu do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1b4f5-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1b4f5-111">Before you begin</span></span>

<span data-ttu-id="1b4f5-112">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="1b4f5-113">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="1b4f5-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="1b4f5-114">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="1b4f5-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="1b4f5-115">Scenario</span></span>

<span data-ttu-id="1b4f5-116">Scenariusz omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="1b4f5-117">Aby dowiedzieć się więcej na temat następnego przeskoku, odwiedź stronę [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b4f5-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="1b4f5-118">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="1b4f5-118">In this scenario, you will:</span></span>

* <span data-ttu-id="1b4f5-119">Pobrać następnego skoku dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="1b4f5-120">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="1b4f5-120">Log in with ARMClient</span></span>

<span data-ttu-id="1b4f5-121">Zaloguj się do armclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="1b4f5-122">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1b4f5-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="1b4f5-123">Uruchom następujący skrypt, aby wrócić do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="1b4f5-124">Te informacje są potrzebne do uruchomienia następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="1b4f5-125">Poniższy kod wymaga wartości dla następujących zmiennych:</span><span class="sxs-lookup"><span data-stu-id="1b4f5-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="1b4f5-126">**Identyfikator subskrypcji** — identyfikator do użycia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="1b4f5-127">**resourceGroupName** — Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="1b4f5-128">Z następujących danych wyjściowych identyfikator maszyny wirtualnej jest używany w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1b4f5-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="1b4f5-129">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="1b4f5-129">Get Next Hop</span></span>

<span data-ttu-id="1b4f5-130">Po utworzeniu nagłówek autoryzacji można pobrać następnego przeskoku z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="1b4f5-131">Następujące wartości należy zastąpić, na przykład kodu do pracy.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="1b4f5-132">Dla wywołań interfejsu API REST obserwatora sieciowego się, że nazwa grupy zasobów w identyfikatorze URI żądania jest grupę zasobów, która zawiera obserwatora sieciowego nie zasoby są wykonywane czynności diagnostyczne na.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="1b4f5-133">Następnego przeskoku wymaga, aby zasobu maszyny Wirtualnej jest przydzielona do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="1b4f5-134">Wyniki</span><span class="sxs-lookup"><span data-stu-id="1b4f5-134">Results</span></span>

<span data-ttu-id="1b4f5-135">Poniższy fragment jest przykładem otrzymane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="1b4f5-136">Wyniki zawierają następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="1b4f5-136">The results contain the following values:</span></span>

* <span data-ttu-id="1b4f5-137">**Typ następnego przeskoku** — ta wartość jest jednym z następujących wartości: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway lub None.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="1b4f5-138">**adres IP następnego przeskoku** -adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="1b4f5-139">**routeTableId** — wartość jest albo identyfikatorem uri dla tabeli tras skojarzone z trasą lub jeśli zdefiniowane przez użytkownika nie zdefiniowano trasy wartość *trasa systemowa* jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="1b4f5-140">Poniżej przedstawiono wyniki w formacie json.</span><span class="sxs-lookup"><span data-stu-id="1b4f5-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="1b4f5-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b4f5-141">Next steps</span></span>

<span data-ttu-id="1b4f5-142">Po mógł sprawdzić następnego skoku dla maszyny wirtualnej, można wyświetlić bezpieczeństwa zasobów sieciowych, odwiedzając [widok zabezpieczeń — omówienie](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1b4f5-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














