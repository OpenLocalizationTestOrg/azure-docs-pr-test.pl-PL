---
title: "Skala aaaAutomatically jednostek przepływności usługi Azure Event Hubs | Dokumentacja firmy Microsoft"
description: "Przestrzeń nazw tooautomatically skali jednostek przepływności, Włącz zwiększyć automatycznie"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="1515a-103">Automatyczne skalowanie w górę jednostek przepływności usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1515a-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="1515a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1515a-104">Overview</span></span>

<span data-ttu-id="1515a-105">Usługa Azure Event Hubs to wysoce skalowalna danych przesyłania strumieniowego platformy.</span><span class="sxs-lookup"><span data-stu-id="1515a-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="1515a-106">Tak klienci usługi Event Hubs często zwiększenie ich użycia po dołączania toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="1515a-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="1515a-107">Wzrost wymagają zwiększa hello wstępnie określone przepływności jednostki (TUs) tooscale centra zdarzeń i obsługiwać większe szybkości transferu.</span><span class="sxs-lookup"><span data-stu-id="1515a-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="1515a-108">Witaj *zwiększyć automatycznie* funkcji usługi Event hubs jest automatycznie skalowany hello liczby TUs toomeet użycia potrzeb.</span><span class="sxs-lookup"><span data-stu-id="1515a-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="1515a-109">Zwiększenie TUs uniemożliwia ograniczania scenariuszy, w którym:</span><span class="sxs-lookup"><span data-stu-id="1515a-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="1515a-110">Transfer danych przychodzących danych, które przekraczają stawki ustawić TUs.</span><span class="sxs-lookup"><span data-stu-id="1515a-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="1515a-111">Żądanie wyjście danych, które przekraczają stawki ustawić TUs.</span><span class="sxs-lookup"><span data-stu-id="1515a-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="1515a-112">Jak zwiększyć automatycznie działa</span><span class="sxs-lookup"><span data-stu-id="1515a-112">How Auto-inflate works</span></span>

<span data-ttu-id="1515a-113">Ruch centra zdarzeń jest kontrolowana przez jednostki przepływności.</span><span class="sxs-lookup"><span data-stu-id="1515a-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="1515a-114">Pojedynczy TU umożliwia 1 MB na sekundę przychodzące i dwa razy ilość wyjście.</span><span class="sxs-lookup"><span data-stu-id="1515a-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="1515a-115">Standardowa usługa Event Hubs można skonfigurować za pomocą 1-20 jednostek przepływności.</span><span class="sxs-lookup"><span data-stu-id="1515a-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="1515a-116">Zwiększyć automatycznie włącza toostart małych z jednostki przepływności wymagana minimalna hello.</span><span class="sxs-lookup"><span data-stu-id="1515a-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="1515a-117">Funkcja Hello skaluje automatycznie następnie toohello limit maksymalnej liczby jednostek przepływności, które są potrzebne, w zależności od hello wzrost ruchu.</span><span class="sxs-lookup"><span data-stu-id="1515a-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="1515a-118">Podniesienie automatycznie udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1515a-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="1515a-119">Wydajne skalowanie toostart mechanizmu małe i skalowania w górę podczas powiększania.</span><span class="sxs-lookup"><span data-stu-id="1515a-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="1515a-120">Automatycznie skalować toohello określonego górny limit bez ograniczania przepustowości problemów.</span><span class="sxs-lookup"><span data-stu-id="1515a-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="1515a-121">Większą kontrolę nad skalowania, jak możesz kontrolować, kiedy i jak dużo tooscale.</span><span class="sxs-lookup"><span data-stu-id="1515a-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="1515a-122">Włącz zwiększyć automatycznie w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="1515a-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="1515a-123">Można włączyć lub wyłączyć zwiększyć automatycznie w przestrzeni nazw przy użyciu jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="1515a-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="1515a-124">Witaj [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1515a-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1515a-125">Szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1515a-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="1515a-126">Włącz zwiększyć automatycznie za pośrednictwem portalu hello</span><span class="sxs-lookup"><span data-stu-id="1515a-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="1515a-127">Podczas tworzenia przestrzeni nazw usługi Event Hubs można włączyć hello zwiększyć automatycznie funkcji w przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="1515a-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="1515a-128">Po włączeniu tej opcji możesz uruchomić małych na jednostek przepływności i skalować w miarę wzrostu użycie.</span><span class="sxs-lookup"><span data-stu-id="1515a-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="1515a-129">Witaj górny limit inflacji nie wpływa na o cenach, która jest zależna od liczby hello TUs używane na godzinę.</span><span class="sxs-lookup"><span data-stu-id="1515a-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="1515a-130">Można również włączyć zwiększyć automatycznie przy użyciu hello **skali** opcji w bloku ustawień hello w portalu hello:</span><span class="sxs-lookup"><span data-stu-id="1515a-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="1515a-131">Włącz automatyczne-zwiększyć przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1515a-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="1515a-132">Podniesienie automatycznej można włączyć podczas wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1515a-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="1515a-133">Na przykład zestaw hello `isAutoInflateEnabled` właściwości zbyt**true** i ustaw `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="1515a-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="1515a-134">Hello pełną szablonu, zobacz hello [utworzyć centra zdarzeń w przestrzeni nazw i Włącz zwiększyć](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) szablonu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="1515a-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1515a-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1515a-135">Next steps</span></span>

<span data-ttu-id="1515a-136">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="1515a-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="1515a-137">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1515a-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1515a-138">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="1515a-138">Create an Event Hub</span></span>](event-hubs-create.md)
