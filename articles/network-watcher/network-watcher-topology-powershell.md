---
title: "Wyświetl topologii obserwatora sieciowego Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób zapytania topologii sieci przy użyciu programu PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="5fac3-103">Wyświetl topologii obserwatora sieciowego przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fac3-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5fac3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fac3-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="5fac3-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="5fac3-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="5fac3-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="5fac3-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="5fac3-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="5fac3-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="5fac3-108">Funkcja topologii sieci obserwatora zapewnia wizualną reprezentację zasobów sieciowych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5fac3-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="5fac3-109">W portalu tej wizualizacji są prezentowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="5fac3-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="5fac3-110">Informacje dotyczące widoku topologii w portalu można pobrać za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fac3-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="5fac3-111">Dzięki temu informacje topologii bardziej elastyczne, dane mogą być używane przez inne narzędzia do tworzenia wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="5fac3-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="5fac3-112">W obszarze dwie relacje w modelu połączenia.</span><span class="sxs-lookup"><span data-stu-id="5fac3-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="5fac3-113">**Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="5fac3-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="5fac3-114">**Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="5fac3-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="5fac3-115">Poniżej znajduje się właściwości, które są zwracane podczas wykonywania zapytania interfejsu API REST topologii.</span><span class="sxs-lookup"><span data-stu-id="5fac3-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="5fac3-116">**Nazwa** — Nazwa zasobu</span><span class="sxs-lookup"><span data-stu-id="5fac3-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="5fac3-117">**Identyfikator** — identyfikator uri zasobu.</span><span class="sxs-lookup"><span data-stu-id="5fac3-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="5fac3-118">**Lokalizacja** — lokalizacji, w której istnieje zasób.</span><span class="sxs-lookup"><span data-stu-id="5fac3-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="5fac3-119">**skojarzenia** -listę skojarzeń odwołuje się do obiektu.</span><span class="sxs-lookup"><span data-stu-id="5fac3-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="5fac3-120">**Nazwa** — Nazwa zasobu, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="5fac3-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="5fac3-121">**resourceId** — element resourceId jest identyfikatorem uri zasobu, do którego odwołuje się powiązanie.</span><span class="sxs-lookup"><span data-stu-id="5fac3-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="5fac3-122">**Obiekt associationType** — ta wartość odwołuje się do relacji między obiekt podrzędny i obiektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="5fac3-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="5fac3-123">Prawidłowe wartości to **zawiera** lub **skojarzone**.</span><span class="sxs-lookup"><span data-stu-id="5fac3-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5fac3-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5fac3-124">Before you begin</span></span>

<span data-ttu-id="5fac3-125">W tym scenariuszu, należy użyć `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet można pobrać informacji o topologii.</span><span class="sxs-lookup"><span data-stu-id="5fac3-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="5fac3-126">Istnieje również artykuł na temat [pobrać topologii sieci z interfejsu API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="5fac3-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="5fac3-127">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5fac3-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="5fac3-128">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="5fac3-128">Scenario</span></span>

<span data-ttu-id="5fac3-129">Scenariusz omówione w tym artykule pobiera odpowiedź topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5fac3-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="5fac3-130">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="5fac3-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="5fac3-131">Pierwszym krokiem jest pobrać wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5fac3-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="5fac3-132">`$networkWatcher` Zmienna jest przekazywana do `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5fac3-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="5fac3-133">Pobrać topologii</span><span class="sxs-lookup"><span data-stu-id="5fac3-133">Retrieve topology</span></span>

<span data-ttu-id="5fac3-134">`Get-AzureRmNetworkWatcherTopology` Polecenie cmdlet pobiera topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5fac3-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="5fac3-135">Wyniki</span><span class="sxs-lookup"><span data-stu-id="5fac3-135">Results</span></span>

<span data-ttu-id="5fac3-136">Wyniki zwrócone ma właściwości name "zasoby", które zawiera treści odpowiedzi json dla `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5fac3-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="5fac3-137">Odpowiedź zawiera zasoby w grupie zabezpieczeń sieci i ich powiązania (to znaczy zawiera, skojarzone).</span><span class="sxs-lookup"><span data-stu-id="5fac3-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="5fac3-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fac3-138">Next steps</span></span>

<span data-ttu-id="5fac3-139">Dowiedz się, jak wizualizacji NSG dzienników przepływu z usługi Power BI, odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="5fac3-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


