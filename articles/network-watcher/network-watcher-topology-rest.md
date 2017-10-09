---
title: "Topologia obserwatora sieciowego Azure aaaView — interfejs API REST | Dokumentacja firmy Microsoft"
description: W tym artykule opisano, jak toouse REST API tooquery topologii sieci.
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
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="4198b-103">Wyświetl topologią obserwatora sieciowego za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="4198b-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4198b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4198b-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="4198b-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="4198b-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="4198b-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="4198b-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="4198b-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="4198b-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="4198b-108">Funkcja topologii Hello obserwatora sieciowego zapewnia wizualną reprezentację hello zasobów sieciowych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4198b-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="4198b-109">W portalu hello tej wizualizacji przedstawiono tooyou automatycznie.</span><span class="sxs-lookup"><span data-stu-id="4198b-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="4198b-110">informacje Hello za hello widoku topologii w portalu hello mogą zostać pobrane za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4198b-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="4198b-111">Dzięki temu informacji dotyczących topologii hello bardziej elastyczne, hello danych mogą być używane przez inne narzędzia toobuild limit hello wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="4198b-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="4198b-112">w obszarze dwie relacje w modelu Hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="4198b-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="4198b-113">**Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="4198b-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="4198b-114">**Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="4198b-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="4198b-115">Witaj poniżej znajduje się właściwości, które są zwracane, gdy zapytanie hello interfejsu API REST topologii.</span><span class="sxs-lookup"><span data-stu-id="4198b-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="4198b-116">**Nazwa** — Witaj Nazwa zasobu hello</span><span class="sxs-lookup"><span data-stu-id="4198b-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="4198b-117">**Identyfikator** — Witaj identyfikatora uri zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="4198b-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="4198b-118">**Lokalizacja** — Witaj lokalizacji, w której istnieje zasób hello.</span><span class="sxs-lookup"><span data-stu-id="4198b-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="4198b-119">**skojarzenia** — lista toohello skojarzenia odwołuje się do obiektu.</span><span class="sxs-lookup"><span data-stu-id="4198b-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="4198b-120">**Nazwa** — nazwa hello hello odwołuje się do zasobu.</span><span class="sxs-lookup"><span data-stu-id="4198b-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="4198b-121">**resourceId** -hello resourceId jest identyfikatorem uri hello hello zasobu, do którego odwołuje się powiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="4198b-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="4198b-122">**Obiekt associationType** -hello relacja między hello obiektu podrzędnego i nadrzędnego hello odwołuje się do tej wartości.</span><span class="sxs-lookup"><span data-stu-id="4198b-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="4198b-123">Prawidłowe wartości to **zawiera** lub **skojarzone**.</span><span class="sxs-lookup"><span data-stu-id="4198b-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4198b-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4198b-124">Before you begin</span></span>

<span data-ttu-id="4198b-125">W tym scenariuszu można pobrać informacji o topologii hello.</span><span class="sxs-lookup"><span data-stu-id="4198b-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="4198b-126">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4198b-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="4198b-127">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="4198b-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="4198b-128">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="4198b-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="4198b-129">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="4198b-129">Scenario</span></span>

<span data-ttu-id="4198b-130">Scenariusz Hello omówione w tym artykule pobiera odpowiedź hello topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4198b-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="4198b-131">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="4198b-131">Log in with ARMClient</span></span>

<span data-ttu-id="4198b-132">Zaloguj się za tooarmclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4198b-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="4198b-133">Pobrać topologii</span><span class="sxs-lookup"><span data-stu-id="4198b-133">Retrieve topology</span></span>

<span data-ttu-id="4198b-134">Poniższy przykład Hello żądanie topologii hello hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4198b-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="4198b-135">przykład Witaj jest sparametryzowane tooallow elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="4198b-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="4198b-136">Zamień wszystkie wartości z \< \> między nimi.</span><span class="sxs-lookup"><span data-stu-id="4198b-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="4198b-137">powitania po odpowiedzi jest przykładem skróconą odpowiedzi, który jest zwracany, gdy pobrać topologii grupa zasobów:</span><span class="sxs-lookup"><span data-stu-id="4198b-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4198b-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4198b-138">Next steps</span></span>

<span data-ttu-id="4198b-139">Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="4198b-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

