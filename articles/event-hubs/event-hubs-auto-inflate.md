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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Automatyczne skalowanie w górę jednostek przepływności usługi Azure Event Hubs

## <a name="overview"></a>Omówienie

Usługa Azure Event Hubs to wysoce skalowalna danych przesyłania strumieniowego platformy. Tak klienci usługi Event Hubs często zwiększenie ich użycia po dołączania toohello usługi. Wzrost wymagają zwiększa hello wstępnie określone przepływności jednostki (TUs) tooscale centra zdarzeń i obsługiwać większe szybkości transferu. Witaj *zwiększyć automatycznie* funkcji usługi Event hubs jest automatycznie skalowany hello liczby TUs toomeet użycia potrzeb. Zwiększenie TUs uniemożliwia ograniczania scenariuszy, w którym:

* Transfer danych przychodzących danych, które przekraczają stawki ustawić TUs.
* Żądanie wyjście danych, które przekraczają stawki ustawić TUs.

## <a name="how-auto-inflate-works"></a>Jak zwiększyć automatycznie działa

Ruch centra zdarzeń jest kontrolowana przez jednostki przepływności. Pojedynczy TU umożliwia 1 MB na sekundę przychodzące i dwa razy ilość wyjście. Standardowa usługa Event Hubs można skonfigurować za pomocą 1-20 jednostek przepływności. Zwiększyć automatycznie włącza toostart małych z jednostki przepływności wymagana minimalna hello. Funkcja Hello skaluje automatycznie następnie toohello limit maksymalnej liczby jednostek przepływności, które są potrzebne, w zależności od hello wzrost ruchu. Podniesienie automatycznie udostępnia hello następujące korzyści:

- Wydajne skalowanie toostart mechanizmu małe i skalowania w górę podczas powiększania.
- Automatycznie skalować toohello określonego górny limit bez ograniczania przepustowości problemów.
- Większą kontrolę nad skalowania, jak możesz kontrolować, kiedy i jak dużo tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Włącz zwiększyć automatycznie w przestrzeni nazw

Można włączyć lub wyłączyć zwiększyć automatycznie w przestrzeni nazw przy użyciu jednej z następujących metod hello:

1. Witaj [portalu Azure](https://portal.azure.com).
2. Szablon usługi Azure Resource Manager.

### <a name="enable-auto-inflate-through-hello-portal"></a>Włącz zwiększyć automatycznie za pośrednictwem portalu hello

Podczas tworzenia przestrzeni nazw usługi Event Hubs można włączyć hello zwiększyć automatycznie funkcji w przestrzeni nazw:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Po włączeniu tej opcji możesz uruchomić małych na jednostek przepływności i skalować w miarę wzrostu użycie. Witaj górny limit inflacji nie wpływa na o cenach, która jest zależna od liczby hello TUs używane na godzinę.

Można również włączyć zwiększyć automatycznie przy użyciu hello **skali** opcji w bloku ustawień hello w portalu hello:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Włącz automatyczne-zwiększyć przy użyciu szablonu usługi Azure Resource Manager

Podniesienie automatycznej można włączyć podczas wdrażania szablonu usługi Azure Resource Manager. Na przykład zestaw hello `isAutoInflateEnabled` właściwości zbyt**true** i ustaw `maximumThroughputUnits` too10.

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

Hello pełną szablonu, zobacz hello [utworzyć centra zdarzeń w przestrzeni nazw i Włącz zwiększyć](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) szablonu w witrynie GitHub.

## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
