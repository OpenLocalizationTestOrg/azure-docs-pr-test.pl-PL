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
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="e77df-103">Routing oparty na ścieżkach URL — omówienie</span><span class="sxs-lookup"><span data-stu-id="e77df-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="e77df-104">Adres URL routingu opartego na ścieżkę umożliwia możesz tooroute ruchu tooback-end pul serwerów oparte na ścieżkach do adresu URL żądania hello.</span><span class="sxs-lookup"><span data-stu-id="e77df-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="e77df-105">Jednego ze scenariuszy hello jest tooroute żądania pul serwerów wewnętrznej bazy danych toodifferent różne typy zawartości.</span><span class="sxs-lookup"><span data-stu-id="e77df-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="e77df-106">W hello poniższy przykład, Application Gateway obsługuje ruchu dla domeny contoso.com z trzech pul serwerów zaplecza na przykład: VideoServerPool, ImageServerPool i DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="e77df-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="e77df-108">Żądania dla http://contoso.com/video * są tooVideoServerPool routingiem i http://contoso.com/images * są tooImageServerPool routingiem.</span><span class="sxs-lookup"><span data-stu-id="e77df-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="e77df-109">DefaultServerPool jest zaznaczone, jeśli żadna hello ścieżki wzorce nie zgadza się.</span><span class="sxs-lookup"><span data-stu-id="e77df-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e77df-110">Reguły są przetwarzane w kolejności hello, są one wyświetlane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e77df-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="e77df-111">Jest odbiorników obejmujący wiele lokacji stanowczo zalecane tooconfigure pierwszy wirusowej tooconfiguring wcześniejsze podstawowe odbiornika.</span><span class="sxs-lookup"><span data-stu-id="e77df-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="e77df-112">Dzięki temu zakończenia tego ruchu pobiera routingiem toohello powrót.</span><span class="sxs-lookup"><span data-stu-id="e77df-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="e77df-113">Jeśli podstawowy odbiornik znajduje się na początku listy i jest zgodny z żądaniem przychodzącym, jest ono przetwarzane przez ten odbiornik.</span><span class="sxs-lookup"><span data-stu-id="e77df-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="e77df-114">Element konfiguracji UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="e77df-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="e77df-115">Hello urlPathMap element jest mapowania puli serwerów używanych toospecify wzorce ścieżki tooback-end.</span><span class="sxs-lookup"><span data-stu-id="e77df-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="e77df-116">Witaj następujący przykładowy kod to fragment hello urlPathMap elementu z pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="e77df-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="e77df-117">PathPattern: To ustawienie znajduje się lista toomatch wzorce ścieżki.</span><span class="sxs-lookup"><span data-stu-id="e77df-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="e77df-118">Każdy musi rozpoczynać się od / i miejsce tylko hello "*" jest dozwolone, jest na powitania zakończenia po "/".</span><span class="sxs-lookup"><span data-stu-id="e77df-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="e77df-119">Hello ciąg przekazywani toohello dopasowania ścieżki nie zawiera żadnego tekstu po hello najpierw? lub #, a te znaki nie są dozwolone w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e77df-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="e77df-120">Aby uzyskać więcej informacji, zobacz [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) (Szablon usługi Resource Manager korzystający z routingu opartego na adresach URL).</span><span class="sxs-lookup"><span data-stu-id="e77df-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="e77df-121">Reguła PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="e77df-121">PathBasedRouting rule</span></span>

<span data-ttu-id="e77df-122">RequestRoutingRule typu PathBasedRouting jest używane toobind urlPathMap tooa odbiornika.</span><span class="sxs-lookup"><span data-stu-id="e77df-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="e77df-123">Wszystkie żądania otrzymane dla tego odbiornika są kierowane zgodnie z zasadami określonymi w elemencie urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="e77df-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="e77df-124">Fragment reguły PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="e77df-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e77df-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e77df-125">Next steps</span></span>

<span data-ttu-id="e77df-126">Po naukę na podstawie adresu URL routingu zawartości, przejdź zbyt[Utwórz bramę aplikacji przy użyciu routingu opartego na adres URL](application-gateway-create-url-route-portal.md) toocreate bramę aplikacji z reguł routingu adresów URL.</span><span class="sxs-lookup"><span data-stu-id="e77df-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
