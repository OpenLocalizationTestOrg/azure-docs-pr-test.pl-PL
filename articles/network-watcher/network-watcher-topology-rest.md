---
title: "Wyświetl topologii obserwatora sieciowego Azure - interfejsu API REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób użycia interfejsu API REST do badania topologii sieci."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 568f3060da372f4a08cec342e04359172522cb69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="3f2f9-103">Wyświetl topologią obserwatora sieciowego za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="3f2f9-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3f2f9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f2f9-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="3f2f9-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="3f2f9-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="3f2f9-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="3f2f9-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="3f2f9-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="3f2f9-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="3f2f9-108">Funkcja topologii sieci obserwatora zapewnia wizualną reprezentację zasobów sieciowych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="3f2f9-109">W portalu tej wizualizacji są prezentowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="3f2f9-110">Informacje dotyczące widoku topologii w portalu można pobrać za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="3f2f9-111">Dzięki temu informacje topologii bardziej elastyczne, dane mogą być używane przez inne narzędzia do tworzenia wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="3f2f9-112">W obszarze dwie relacje w modelu połączenia.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="3f2f9-113">**Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="3f2f9-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="3f2f9-114">**Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="3f2f9-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="3f2f9-115">Poniżej znajduje się właściwości, które są zwracane podczas wykonywania zapytania interfejsu API REST topologii.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="3f2f9-116">**Nazwa** — Nazwa zasobu</span><span class="sxs-lookup"><span data-stu-id="3f2f9-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="3f2f9-117">**Identyfikator** — identyfikator uri zasobu.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="3f2f9-118">**Lokalizacja** — lokalizacji, w której istnieje zasób.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="3f2f9-119">**skojarzenia** -listę skojarzeń odwołuje się do obiektu.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="3f2f9-120">**Nazwa** — Nazwa zasobu, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="3f2f9-121">**resourceId** — element resourceId jest identyfikatorem uri zasobu, do którego odwołuje się powiązanie.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="3f2f9-122">**Obiekt associationType** — ta wartość odwołuje się do relacji między obiekt podrzędny i obiektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="3f2f9-123">Prawidłowe wartości to **zawiera** lub **skojarzone**.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3f2f9-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="3f2f9-124">Before you begin</span></span>

<span data-ttu-id="3f2f9-125">W tym scenariuszu można pobrać informacji o topologii.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-125">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="3f2f9-126">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-126">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="3f2f9-127">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="3f2f9-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="3f2f9-128">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3f2f9-129">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="3f2f9-129">Scenario</span></span>

<span data-ttu-id="3f2f9-130">Scenariusz omówione w tym artykule pobiera odpowiedź topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="3f2f9-131">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="3f2f9-131">Log in with ARMClient</span></span>

<span data-ttu-id="3f2f9-132">Zaloguj się do armclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-132">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="3f2f9-133">Pobrać topologii</span><span class="sxs-lookup"><span data-stu-id="3f2f9-133">Retrieve topology</span></span>

<span data-ttu-id="3f2f9-134">Poniższy przykład żądań topologii z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-134">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="3f2f9-135">Przykład jest parametry umożliwiające elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-135">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="3f2f9-136">Zamień wszystkie wartości z \< \> między nimi.</span><span class="sxs-lookup"><span data-stu-id="3f2f9-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="3f2f9-137">Następującą odpowiedź jest przykładem skróconą odpowiedzi, który jest zwracany, gdy pobrać topologii grupa zasobów:</span><span class="sxs-lookup"><span data-stu-id="3f2f9-137">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="3f2f9-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f2f9-138">Next steps</span></span>

<span data-ttu-id="3f2f9-139">Dowiedz się, jak wizualizacji NSG dzienników przepływu z usługi Power BI, odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3f2f9-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

