---
title: "na podstawie aaaURL zawartości Omówienie routingu | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie hello adres URL aplikacji bramy routingu opartego na protokole zawartości, konfiguracji UrlPathMap i PathBasedRouting reguły."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a>Routing oparty na ścieżkach URL — omówienie

Adres URL routingu opartego na ścieżkę umożliwia możesz tooroute ruchu tooback-end pul serwerów oparte na ścieżkach do adresu URL żądania hello. 

Jednego ze scenariuszy hello jest tooroute żądania pul serwerów wewnętrznej bazy danych toodifferent różne typy zawartości.

W hello poniższy przykład, Application Gateway obsługuje ruchu dla domeny contoso.com z trzech pul serwerów zaplecza na przykład: VideoServerPool, ImageServerPool i DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

Żądania dla http://contoso.com/video * są tooVideoServerPool routingiem i http://contoso.com/images * są tooImageServerPool routingiem. DefaultServerPool jest zaznaczone, jeśli żadna hello ścieżki wzorce nie zgadza się.

> [!IMPORTANT]
> Reguły są przetwarzane w kolejności hello, są one wyświetlane w portalu hello. Jest odbiorników obejmujący wiele lokacji stanowczo zalecane tooconfigure pierwszy wirusowej tooconfiguring wcześniejsze podstawowe odbiornika.  Dzięki temu zakończenia tego ruchu pobiera routingiem toohello powrót. Jeśli podstawowy odbiornik znajduje się na początku listy i jest zgodny z żądaniem przychodzącym, jest ono przetwarzane przez ten odbiornik.

## <a name="urlpathmap-configuration-element"></a>Element konfiguracji UrlPathMap

Hello urlPathMap element jest mapowania puli serwerów używanych toospecify wzorce ścieżki tooback-end. Witaj następujący przykładowy kod to fragment hello urlPathMap elementu z pliku szablonu.

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> PathPattern: To ustawienie znajduje się lista toomatch wzorce ścieżki. Każdy musi rozpoczynać się od / i miejsce tylko hello "*" jest dozwolone, jest na powitania zakończenia po "/". Hello ciąg przekazywani toohello dopasowania ścieżki nie zawiera żadnego tekstu po hello najpierw? lub #, a te znaki nie są dozwolone w tym miejscu.

Aby uzyskać więcej informacji, zobacz [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) (Szablon usługi Resource Manager korzystający z routingu opartego na adresach URL).

## <a name="pathbasedrouting-rule"></a>Reguła PathBasedRouting

RequestRoutingRule typu PathBasedRouting jest używane toobind urlPathMap tooa odbiornika. Wszystkie żądania otrzymane dla tego odbiornika są kierowane zgodnie z zasadami określonymi w elemencie urlPathMap.
Fragment reguły PathBasedRouting:

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a>Następne kroki

Po naukę na podstawie adresu URL routingu zawartości, przejdź zbyt[Utwórz bramę aplikacji przy użyciu routingu opartego na adres URL](application-gateway-create-url-route-portal.md) toocreate bramę aplikacji z reguł routingu adresów URL.
