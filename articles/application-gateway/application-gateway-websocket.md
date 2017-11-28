---
title: "Obsługa aaaWebSocket bramę aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie hello obsługi protokołu WebSocket bramy aplikacji."
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
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="6e44f-103">Omówienie obsługi protokołu WebSocket w bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="6e44f-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="6e44f-104">Brama aplikacji w zapewnia macierzystą obsługę protokołu WebSocket we wszystkich rozmiarów bramy.</span><span class="sxs-lookup"><span data-stu-id="6e44f-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="6e44f-105">Nie jest Włącz tooselectively użytkownika można skonfigurować ustawienie ani wyłączyć obsługę protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e44f-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="6e44f-106">Protokół WebSocket standaryzowane w [RFC6455](https://tools.ietf.org/html/rfc6455) umożliwia pełnego dupleksu komunikacji między serwerem klientem za pośrednictwem długo działające połączenia TCP.</span><span class="sxs-lookup"><span data-stu-id="6e44f-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="6e44f-107">Ta funkcja służy do większej liczby interaktywnych komunikacji między serwerem sieci web hello i powitania klienta, który może być dwukierunkowe, bez potrzeby hello sondowania jako wymagane w implementacji oparte na protokole HTTP.</span><span class="sxs-lookup"><span data-stu-id="6e44f-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="6e44f-108">WebSocket niski ma obciążenie w odróżnieniu od protokołu HTTP i można ponownemu hello sam połączenia TCP dla wielu żądań/odpowiedzi spowodować efektywniejsze wykorzystanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="6e44f-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="6e44f-109">Protokoły WebSocket są zaprojektowane toowork za pośrednictwem tradycyjnych HTTP portów 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="6e44f-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="6e44f-110">Aby kontynuować, przy użyciu standardowych odbiornika HTTP na port 80 i 443 tooreceive ruchu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e44f-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="6e44f-111">Ruch protokołu WebSocket jest to ukierunkowanej toohello WebSocket włączane serwera wewnętrznej bazy danych przy użyciu puli zaplecza odpowiednie hello określonego w zasadach bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e44f-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="6e44f-112">powitania serwera wewnętrznej bazy danych musi odpowiadać toohello aplikacji bramy sond, które zostały opisane w hello [omówienie sondy kondycji](application-gateway-probe-overview.md) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6e44f-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="6e44f-113">Sondy kondycji bramy aplikacji są tylko HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6e44f-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="6e44f-114">Każdy serwer wewnętrznej bazy danych musi odpowiadać sond tooHTTP dla aplikacji bramy tooroute WebSocket ruchu toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="6e44f-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="6e44f-115">Element konfiguracji odbiornika</span><span class="sxs-lookup"><span data-stu-id="6e44f-115">Listener configuration element</span></span>

<span data-ttu-id="6e44f-116">Istniejący odbiornik HTTP mogą być używane toosupport ruchu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e44f-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="6e44f-117">Hello poniżej przedstawiono fragment element httpListeners z przykładowego pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="6e44f-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="6e44f-118">Czy wymagane toosupport odbiorników HTTP i HTTPS protokołu WebSocket i zabezpieczania ruchu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e44f-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="6e44f-119">Podobnie można użyć hello [portal](application-gateway-create-gateway-portal.md) lub [PowerShell](application-gateway-create-gateway-arm.md) toocreate bramę aplikacji z odbiorników na ruch na porcie 80/443 toosupport protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e44f-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="6e44f-120">BackendAddressPool, BackendHttpSetting, konfiguracja usługi Routing i zasady</span><span class="sxs-lookup"><span data-stu-id="6e44f-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="6e44f-121">BackendAddressPool jest używane toodefine puli zaplecza przy użyciu protokołu WebSocket włączone serwerów.</span><span class="sxs-lookup"><span data-stu-id="6e44f-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="6e44f-122">Hello backendHttpSetting jest zdefiniowana z portem 80 i 443 wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6e44f-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="6e44f-123">właściwości Hello koligacji na podstawie plików cookie i requestTimeouts nie są istotne tooWebSocket ruchu.</span><span class="sxs-lookup"><span data-stu-id="6e44f-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="6e44f-124">Nie ma żadnej zmiany wymagane w regule routingu hello, "Basic" toohello odpowiednie odbiornika hello używane tootie odpowiadający puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6e44f-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="6e44f-125">Włączony protokół WebSocket wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="6e44f-125">WebSocket enabled backend</span></span>

<span data-ttu-id="6e44f-126">Z wewnętrzną bazą danych musi być serwerem sieci web HTTP/HTTPS na powitania skonfigurowane portu dla protokołu WebSocket toowork (zazwyczaj 80/443).</span><span class="sxs-lookup"><span data-stu-id="6e44f-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="6e44f-127">To wymaganie dotyczy, ponieważ protokół WebSocket wymaga hello toobe początkowego uzgadniania protokołu HTTP z protokołem uaktualnienia tooWebSocket jako pola nagłówka.</span><span class="sxs-lookup"><span data-stu-id="6e44f-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="6e44f-128">Witaj, poniżej przedstawiono przykładowy nagłówka:</span><span class="sxs-lookup"><span data-stu-id="6e44f-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="6e44f-129">Inną przyczyną tego jest sondy kondycji tej aplikacji bramy wewnętrznej bazy danych obsługuje tylko protokoły HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6e44f-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="6e44f-130">Jeśli powitania serwera wewnętrznej bazy danych nie odpowiada tooHTTP lub sond protokołu HTTPS, pochodzi z puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6e44f-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e44f-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e44f-131">Next steps</span></span>

<span data-ttu-id="6e44f-132">Po szkoleniowe dotyczące obsługi protokołu WebSocket, przejdź zbyt[Utwórz bramę aplikacji](application-gateway-create-gateway.md) aplikacji sieci web z obsługą tooget wprowadzenie do protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e44f-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

