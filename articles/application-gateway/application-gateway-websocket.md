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
# <a name="overview-of-websocket-support-in-application-gateway"></a>Omówienie obsługi protokołu WebSocket w bramy aplikacji

Brama aplikacji w zapewnia macierzystą obsługę protokołu WebSocket we wszystkich rozmiarów bramy. Nie jest Włącz tooselectively użytkownika można skonfigurować ustawienie ani wyłączyć obsługę protokołu WebSocket. 

Protokół WebSocket standaryzowane w [RFC6455](https://tools.ietf.org/html/rfc6455) umożliwia pełnego dupleksu komunikacji między serwerem klientem za pośrednictwem długo działające połączenia TCP. Ta funkcja służy do większej liczby interaktywnych komunikacji między serwerem sieci web hello i powitania klienta, który może być dwukierunkowe, bez potrzeby hello sondowania jako wymagane w implementacji oparte na protokole HTTP. WebSocket niski ma obciążenie w odróżnieniu od protokołu HTTP i można ponownemu hello sam połączenia TCP dla wielu żądań/odpowiedzi spowodować efektywniejsze wykorzystanie zasobów. Protokoły WebSocket są zaprojektowane toowork za pośrednictwem tradycyjnych HTTP portów 80 i 443.

Aby kontynuować, przy użyciu standardowych odbiornika HTTP na port 80 i 443 tooreceive ruchu protokołu WebSocket. Ruch protokołu WebSocket jest to ukierunkowanej toohello WebSocket włączane serwera wewnętrznej bazy danych przy użyciu puli zaplecza odpowiednie hello określonego w zasadach bramy aplikacji. powitania serwera wewnętrznej bazy danych musi odpowiadać toohello aplikacji bramy sond, które zostały opisane w hello [omówienie sondy kondycji](application-gateway-probe-overview.md) sekcji. Sondy kondycji bramy aplikacji są tylko HTTP/HTTPS. Każdy serwer wewnętrznej bazy danych musi odpowiadać sond tooHTTP dla aplikacji bramy tooroute WebSocket ruchu toohello serwera.

## <a name="listener-configuration-element"></a>Element konfiguracji odbiornika

Istniejący odbiornik HTTP mogą być używane toosupport ruchu protokołu WebSocket. Hello poniżej przedstawiono fragment element httpListeners z przykładowego pliku szablonu. Czy wymagane toosupport odbiorników HTTP i HTTPS protokołu WebSocket i zabezpieczania ruchu protokołu WebSocket. Podobnie można użyć hello [portal](application-gateway-create-gateway-portal.md) lub [PowerShell](application-gateway-create-gateway-arm.md) toocreate bramę aplikacji z odbiorników na ruch na porcie 80/443 toosupport protokołu WebSocket.

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>BackendAddressPool, BackendHttpSetting, konfiguracja usługi Routing i zasady

BackendAddressPool jest używane toodefine puli zaplecza przy użyciu protokołu WebSocket włączone serwerów. Hello backendHttpSetting jest zdefiniowana z portem 80 i 443 wewnętrznej bazy danych. właściwości Hello koligacji na podstawie plików cookie i requestTimeouts nie są istotne tooWebSocket ruchu. Nie ma żadnej zmiany wymagane w regule routingu hello, "Basic" toohello odpowiednie odbiornika hello używane tootie odpowiadający puli adresów zaplecza. 

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

## <a name="websocket-enabled-backend"></a>Włączony protokół WebSocket wewnętrznej bazy danych

Z wewnętrzną bazą danych musi być serwerem sieci web HTTP/HTTPS na powitania skonfigurowane portu dla protokołu WebSocket toowork (zazwyczaj 80/443). To wymaganie dotyczy, ponieważ protokół WebSocket wymaga hello toobe początkowego uzgadniania protokołu HTTP z protokołem uaktualnienia tooWebSocket jako pola nagłówka. Witaj, poniżej przedstawiono przykładowy nagłówka:

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

Inną przyczyną tego jest sondy kondycji tej aplikacji bramy wewnętrznej bazy danych obsługuje tylko protokoły HTTP i HTTPS. Jeśli powitania serwera wewnętrznej bazy danych nie odpowiada tooHTTP lub sond protokołu HTTPS, pochodzi z puli zaplecza.

## <a name="next-steps"></a>Następne kroki

Po szkoleniowe dotyczące obsługi protokołu WebSocket, przejdź zbyt[Utwórz bramę aplikacji](application-gateway-create-gateway.md) aplikacji sieci web z obsługą tooget wprowadzenie do protokołu WebSocket.

