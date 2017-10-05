---
title: "Wyświetl topologii obserwatora sieciowego Azure - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób użycia interfejsu wiersza polecenia Azure do badania topologii sieci."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5be8e103f9a1f32117a4ed3be73bff021db1186d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="d5ec2-103">Wyświetl topologia obserwatora sieciowego z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d5ec2-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d5ec2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5ec2-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="d5ec2-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="d5ec2-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="d5ec2-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="d5ec2-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="d5ec2-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d5ec2-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="d5ec2-108">Funkcja topologii sieci obserwatora zapewnia wizualną reprezentację zasobów sieciowych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="d5ec2-109">W portalu tej wizualizacji są prezentowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="d5ec2-110">Informacje dotyczące widoku topologii w portalu można pobrać za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="d5ec2-111">Dzięki temu informacje topologii bardziej elastyczne, dane mogą być używane przez inne narzędzia do tworzenia wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="d5ec2-112">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d5ec2-113">Obserwatora sieciowego aktualnie używa interfejsu wiersza polecenia platformy Azure w wersji 1.0 do obsługi interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="d5ec2-114">W obszarze dwie relacje w modelu połączenia.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-114">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="d5ec2-115">**Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="d5ec2-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="d5ec2-116">**Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="d5ec2-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="d5ec2-117">Poniżej znajduje się właściwości, które są zwracane podczas wykonywania zapytania interfejsu API REST topologii.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-117">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="d5ec2-118">**Nazwa** — Nazwa zasobu</span><span class="sxs-lookup"><span data-stu-id="d5ec2-118">**name** - The name of the resource</span></span>
* <span data-ttu-id="d5ec2-119">**Identyfikator** — identyfikator uri zasobu.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-119">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="d5ec2-120">**Lokalizacja** — lokalizacji, w której istnieje zasób.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-120">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="d5ec2-121">**skojarzenia** -listę skojarzeń odwołuje się do obiektu.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-121">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="d5ec2-122">**Nazwa** — Nazwa zasobu, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-122">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="d5ec2-123">**resourceId** — element resourceId jest identyfikatorem uri zasobu, do którego odwołuje się powiązanie.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-123">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="d5ec2-124">**Obiekt associationType** — ta wartość odwołuje się do relacji między obiekt podrzędny i obiektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-124">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="d5ec2-125">Prawidłowe wartości to **zawiera** lub **skojarzone**.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d5ec2-126">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d5ec2-126">Before you begin</span></span>

<span data-ttu-id="d5ec2-127">W tym scenariuszu, należy użyć `network watcher topology` polecenia cmdlet można pobrać informacji o topologii.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-127">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="d5ec2-128">Istnieje również artykuł na temat [pobrać topologii sieci z interfejsu API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d5ec2-128">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="d5ec2-129">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-129">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d5ec2-130">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="d5ec2-130">Scenario</span></span>

<span data-ttu-id="d5ec2-131">Scenariusz omówione w tym artykule pobiera odpowiedź topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-131">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="d5ec2-132">Pobrać topologii</span><span class="sxs-lookup"><span data-stu-id="d5ec2-132">Retrieve topology</span></span>

<span data-ttu-id="d5ec2-133">`network watcher topology` Polecenie cmdlet pobiera topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-133">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="d5ec2-134">Dodaj argument "--json" Aby wyświetlić oput w formacie json</span><span class="sxs-lookup"><span data-stu-id="d5ec2-134">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="d5ec2-135">Wyniki</span><span class="sxs-lookup"><span data-stu-id="d5ec2-135">Results</span></span>

<span data-ttu-id="d5ec2-136">Wyniki zwrócone ma właściwości name "zasoby", które zawiera treści odpowiedzi json dla `network watcher topology` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5ec2-136">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="d5ec2-137">Odpowiedź zawiera zasoby w grupie zabezpieczeń sieci i ich powiązania (to znaczy zawiera, skojarzone).</span><span class="sxs-lookup"><span data-stu-id="d5ec2-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="d5ec2-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5ec2-138">Next steps</span></span>

<span data-ttu-id="d5ec2-139">Dowiedz się więcej na temat reguł zabezpieczeń, które są stosowane do zasobów sieciowych, odwiedzając [Omówienie widoku grupy zabezpieczeń](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d5ec2-139">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
