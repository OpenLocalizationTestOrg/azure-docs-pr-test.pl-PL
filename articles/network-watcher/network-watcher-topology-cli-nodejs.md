---
title: "Topologia obserwatora sieciowego Azure aaaView — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooquery toouse Azure CLI 1.0 topologii sieci."
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
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="819cc-103">Wyświetl topologią obserwatora sieciowego za pomocą interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="819cc-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="819cc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="819cc-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="819cc-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="819cc-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="819cc-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="819cc-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="819cc-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="819cc-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="819cc-108">Funkcja topologii Hello obserwatora sieciowego zapewnia wizualną reprezentację hello zasobów sieciowych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="819cc-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="819cc-109">W portalu hello tej wizualizacji przedstawiono tooyou automatycznie.</span><span class="sxs-lookup"><span data-stu-id="819cc-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="819cc-110">informacje Hello za hello widoku topologii w portalu hello mogą zostać pobrane za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="819cc-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="819cc-111">Dzięki temu informacji dotyczących topologii hello bardziej elastyczne, hello danych mogą być używane przez inne narzędzia toobuild limit hello wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="819cc-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="819cc-112">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="819cc-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="819cc-113">w obszarze dwie relacje w modelu Hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="819cc-113">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="819cc-114">**Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="819cc-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="819cc-115">**Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną</span><span class="sxs-lookup"><span data-stu-id="819cc-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="819cc-116">Witaj poniżej znajduje się właściwości, które są zwracane, gdy zapytanie hello interfejsu API REST topologii.</span><span class="sxs-lookup"><span data-stu-id="819cc-116">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="819cc-117">**Nazwa** — Witaj Nazwa zasobu hello</span><span class="sxs-lookup"><span data-stu-id="819cc-117">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="819cc-118">**Identyfikator** — Witaj identyfikatora uri zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="819cc-118">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="819cc-119">**Lokalizacja** — Witaj lokalizacji, w której istnieje zasób hello.</span><span class="sxs-lookup"><span data-stu-id="819cc-119">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="819cc-120">**skojarzenia** — lista toohello skojarzenia odwołuje się do obiektu.</span><span class="sxs-lookup"><span data-stu-id="819cc-120">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="819cc-121">**Nazwa** — nazwa hello hello odwołuje się do zasobu.</span><span class="sxs-lookup"><span data-stu-id="819cc-121">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="819cc-122">**resourceId** -hello resourceId jest identyfikatorem uri hello hello zasobu, do którego odwołuje się powiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="819cc-122">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="819cc-123">**Obiekt associationType** -hello relacja między hello obiektu podrzędnego i nadrzędnego hello odwołuje się do tej wartości.</span><span class="sxs-lookup"><span data-stu-id="819cc-123">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="819cc-124">Prawidłowe wartości to **zawiera** lub **skojarzone**.</span><span class="sxs-lookup"><span data-stu-id="819cc-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="819cc-125">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="819cc-125">Before you begin</span></span>

<span data-ttu-id="819cc-126">W tym scenariuszu, należy użyć hello `network watcher topology` informacje topologii hello tooretrieve polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="819cc-126">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="819cc-127">Istnieje również artykuł na temat zbyt[pobrać topologii sieci z interfejsu API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="819cc-127">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="819cc-128">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="819cc-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="819cc-129">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="819cc-129">Scenario</span></span>

<span data-ttu-id="819cc-130">Scenariusz Hello omówione w tym artykule pobiera odpowiedź hello topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="819cc-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="819cc-131">Pobrać topologii</span><span class="sxs-lookup"><span data-stu-id="819cc-131">Retrieve topology</span></span>

<span data-ttu-id="819cc-132">Witaj `network watcher topology` polecenie cmdlet pobiera hello topologii dla określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="819cc-132">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="819cc-133">Dodaj hello argument "--json" tooview oput hello w formacie json</span><span class="sxs-lookup"><span data-stu-id="819cc-133">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="819cc-134">Wyniki</span><span class="sxs-lookup"><span data-stu-id="819cc-134">Results</span></span>

<span data-ttu-id="819cc-135">Witaj wyników zwróconych ma właściwości name "zasoby", które zawiera treść odpowiedzi json hello hello `network watcher topology` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="819cc-135">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="819cc-136">odpowiedź Hello zawiera zasoby hello w hello sieciowej grupy zabezpieczeń i ich powiązania (to znaczy zawiera, skojarzone).</span><span class="sxs-lookup"><span data-stu-id="819cc-136">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="819cc-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="819cc-137">Next steps</span></span>

<span data-ttu-id="819cc-138">Dowiedz się więcej o hello reguły zabezpieczeń, które są stosowane tooyour zasobów sieciowych, odwiedzając [Omówienie widoku grupy zabezpieczeń](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="819cc-138">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
