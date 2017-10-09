---
title: "Topologia obserwatora sieciowego Azure aaaView — PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toouse PowerShell tooquery topologii sieci."
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
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="bf81d-103">Wyświetl topologii obserwatora sieciowego przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf81d-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bf81d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf81d-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="bf81d-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="bf81d-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="bf81d-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="bf81d-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="bf81d-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="bf81d-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="bf81d-108">Funkcja topologii Hello obserwatora sieciowego zapewnia wizualną reprezentację hello zasobów sieciowych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bf81d-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="bf81d-109">W portalu hello tej wizualizacji przedstawiono tooyou automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bf81d-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="bf81d-110">informacje Hello za hello widoku topologii w portalu hello mogą zostać pobrane za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf81d-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="bf81d-111">Dzięki temu informacji dotyczących topologii hello bardziej elastyczne, hello danych mogą być używane przez inne narzędzia toobuild limit hello wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="bf81d-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="bf81d-112">w obszarze dwie relacje w modelu Hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="bf81d-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="bf81d-113">**Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="bf81d-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="bf81d-114">**Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="bf81d-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="bf81d-115">Witaj poniżej znajduje się właściwości, które są zwracane, gdy zapytanie hello interfejsu API REST topologii.</span><span class="sxs-lookup"><span data-stu-id="bf81d-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="bf81d-116">**Nazwa** — Witaj Nazwa zasobu hello</span><span class="sxs-lookup"><span data-stu-id="bf81d-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="bf81d-117">**Identyfikator** — Witaj identyfikatora uri zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="bf81d-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="bf81d-118">**Lokalizacja** — Witaj lokalizacji, w której istnieje zasób hello.</span><span class="sxs-lookup"><span data-stu-id="bf81d-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="bf81d-119">**skojarzenia** — lista toohello skojarzenia odwołuje się do obiektu.</span><span class="sxs-lookup"><span data-stu-id="bf81d-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="bf81d-120">**Nazwa** — nazwa hello hello odwołuje się do zasobu.</span><span class="sxs-lookup"><span data-stu-id="bf81d-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="bf81d-121">**resourceId** -hello resourceId jest identyfikatorem uri hello hello zasobu, do którego odwołuje się powiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="bf81d-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="bf81d-122">**Obiekt associationType** -hello relacja między hello obiektu podrzędnego i nadrzędnego hello odwołuje się do tej wartości.</span><span class="sxs-lookup"><span data-stu-id="bf81d-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="bf81d-123">Prawidłowe wartości to **zawiera** lub **skojarzone**.</span><span class="sxs-lookup"><span data-stu-id="bf81d-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bf81d-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="bf81d-124">Before you begin</span></span>

<span data-ttu-id="bf81d-125">W tym scenariuszu, należy użyć hello `Get-AzureRmNetworkWatcherTopology` informacje topologii hello tooretrieve polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf81d-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="bf81d-126">Istnieje również artykuł na temat zbyt[pobrać topologii sieci z interfejsu API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="bf81d-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="bf81d-127">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="bf81d-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="bf81d-128">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="bf81d-128">Scenario</span></span>

<span data-ttu-id="bf81d-129">Scenariusz Hello omówione w tym artykule pobiera odpowiedź hello topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bf81d-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="bf81d-130">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="bf81d-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="bf81d-131">pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="bf81d-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="bf81d-132">Witaj `$networkWatcher` zmienna jest przekazywana toohello `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf81d-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="bf81d-133">Pobrać topologii</span><span class="sxs-lookup"><span data-stu-id="bf81d-133">Retrieve topology</span></span>

<span data-ttu-id="bf81d-134">Witaj `Get-AzureRmNetworkWatcherTopology` polecenie cmdlet pobiera hello topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bf81d-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="bf81d-135">Wyniki</span><span class="sxs-lookup"><span data-stu-id="bf81d-135">Results</span></span>

<span data-ttu-id="bf81d-136">Witaj wyników zwróconych ma właściwości name "zasoby", które zawiera treść odpowiedzi json hello hello `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf81d-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="bf81d-137">odpowiedź Hello zawiera zasoby hello w hello sieciowej grupy zabezpieczeń i ich powiązania (to znaczy zawiera, skojarzone).</span><span class="sxs-lookup"><span data-stu-id="bf81d-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bf81d-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf81d-138">Next steps</span></span>

<span data-ttu-id="bf81d-139">Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="bf81d-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


