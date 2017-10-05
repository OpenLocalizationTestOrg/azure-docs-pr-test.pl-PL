---
title: "Obsługa protokołu WebSocket w bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie obsługi protokołu WebSocket bramy aplikacji."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="1cde5-103">Omówienie obsługi protokołu WebSocket w bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1cde5-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="1cde5-104">Brama aplikacji w zapewnia macierzystą obsługę protokołu WebSocket we wszystkich rozmiarów bramy.</span><span class="sxs-lookup"><span data-stu-id="1cde5-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="1cde5-105">Brak ma użytkownika można skonfigurować ustawienia selektywnie włączać lub wyłączać obsługę protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="1cde5-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="1cde5-106">Protokół WebSocket standaryzowane w [RFC6455](https://tools.ietf.org/html/rfc6455) umożliwia pełnego dupleksu komunikacji między serwerem klientem za pośrednictwem długo działające połączenia TCP.</span><span class="sxs-lookup"><span data-stu-id="1cde5-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="1cde5-107">Ta funkcja służy do większej liczby interaktywnych komunikacji między serwerem sieci web i klienta, który może być dwukierunkowe, bez konieczności sondowania jako wymagane w implementacji oparte na protokole HTTP.</span><span class="sxs-lookup"><span data-stu-id="1cde5-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="1cde5-108">Protokół WebSocket niski ma narzut w odróżnieniu od protokołu HTTP i można ponownie użyć tego samego połączenia TCP dla wielu żądań/odpowiedzi spowodować efektywniejsze wykorzystanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="1cde5-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="1cde5-109">Protokoły WebSocket są przeznaczone do pracy za pośrednictwem tradycyjnych HTTP portów 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="1cde5-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="1cde5-110">Aby kontynuować, przy użyciu standardowych odbiornika HTTP na porcie 80 i 443 do odbierania ruchu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="1cde5-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="1cde5-111">Ruch protokołu WebSocket jest następnie przekierowywane do serwera zaplecza włączone protokołu WebSocket przy użyciu puli zaplecza odpowiednie określonego w zasadach bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cde5-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="1cde5-112">Serwer wewnętrznej bazy danych musi odpowiadać na sond bramy aplikacji, które zostały opisane w [omówienie sondy kondycji](application-gateway-probe-overview.md) sekcji.</span><span class="sxs-lookup"><span data-stu-id="1cde5-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="1cde5-113">Sondy kondycji bramy aplikacji są tylko HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1cde5-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="1cde5-114">Każdy serwer wewnętrznej bazy danych musi odpowiadać na badania HTTP bramy aplikacji przekierowujący ruch protokołu WebSocket do serwera.</span><span class="sxs-lookup"><span data-stu-id="1cde5-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="1cde5-115">Element konfiguracji odbiornika</span><span class="sxs-lookup"><span data-stu-id="1cde5-115">Listener configuration element</span></span>

<span data-ttu-id="1cde5-116">Istniejący odbiornik HTTP może służyć do obsługi ruchu sieciowego protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="1cde5-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="1cde5-117">Poniżej przedstawiono fragment element httpListeners z przykładowego pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="1cde5-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="1cde5-118">Będzie potrzebny odbiorników HTTP i HTTPS do obsługi protokołu WebSocket i zabezpieczania ruchu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="1cde5-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="1cde5-119">Podobnie można użyć [portal](application-gateway-create-gateway-portal.md) lub [PowerShell](application-gateway-create-gateway-arm.md) Aby utworzyć bramę aplikacji za pomocą obiektów nasłuchujących na porcie 80/443 do obsługi ruchu sieciowego protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="1cde5-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="1cde5-120">BackendAddressPool, BackendHttpSetting, konfiguracja usługi Routing i zasady</span><span class="sxs-lookup"><span data-stu-id="1cde5-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="1cde5-121">BackendAddressPool służy do definiowania puli zaplecza przy użyciu protokołu WebSocket włączone serwerów.</span><span class="sxs-lookup"><span data-stu-id="1cde5-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="1cde5-122">BackendHttpSetting jest zdefiniowana z portem 80 i 443 wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1cde5-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="1cde5-123">Właściwości koligacji na podstawie plików cookie i requestTimeouts nie mają znaczenia dla ruchu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="1cde5-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="1cde5-124">Nie ma żadnej zmiany wymagane w regule routingu, "Basic" służy do powiązanie odpowiednie odbiornika do odpowiedniej puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1cde5-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a><span data-ttu-id="1cde5-125">Włączony protokół WebSocket wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="1cde5-125">WebSocket enabled backend</span></span>

<span data-ttu-id="1cde5-126">Z wewnętrzną bazą danych musi być serwerem sieci web HTTP/HTTPS na skonfigurowanego portu dla protokołu WebSocket do pracy (zazwyczaj 80/443).</span><span class="sxs-lookup"><span data-stu-id="1cde5-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="1cde5-127">To wymaganie dotyczy, ponieważ protokół WebSocket wymaga początkowego uzgadniania się wraz z uaktualnieniem protokołu WebSocket jako pole nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="1cde5-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="1cde5-128">Poniżej przedstawiono przykład nagłówka:</span><span class="sxs-lookup"><span data-stu-id="1cde5-128">The following is an example of a header:</span></span>

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

<span data-ttu-id="1cde5-129">Inną przyczyną tego jest sondy kondycji tej aplikacji bramy wewnętrznej bazy danych obsługuje tylko protokoły HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1cde5-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="1cde5-130">Jeśli serwer wewnętrznej bazy danych nie odpowiada na HTTP lub HTTPS, sond, pochodzi z puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1cde5-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cde5-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cde5-131">Next steps</span></span>

<span data-ttu-id="1cde5-132">Po szkoleniowe dotyczące obsługi protokołu WebSocket, przejdź do [Utwórz bramę aplikacji](application-gateway-create-gateway.md) aby zacząć korzystać z protokołu WebSocket aplikacji sieci web z obsługą.</span><span class="sxs-lookup"><span data-stu-id="1cde5-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

