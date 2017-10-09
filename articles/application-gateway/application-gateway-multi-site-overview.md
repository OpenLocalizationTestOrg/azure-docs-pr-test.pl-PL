---
title: aaaHosting wielu witryn w bramie aplikacji Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello pomocy technicznej obejmujący wiele lokacji bramy aplikacji."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Hostowanie wielu witryn usługi Application Gateway

Obsługujący wiele lokacji umożliwia tooconfigure więcej niż jednej aplikacji sieci web na powitania tego samego wystąpienia bramy aplikacji. Ta funkcja umożliwia tooconfigure efektywniejsze topologii wdrożeń sumując too20 witryn sieci Web tooone aplikacji bramy. Każda witryna sieci Web może zostać skierowany tooits właścicielem puli wewnętrznej bazy danych. W hello poniższy przykład bramy aplikacji jest obsługujące ruch contoso.com i fabrikam.com z dwie pule serwera wewnętrznej nazywana ContosoServerPool i FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Reguły są przetwarzane w kolejności hello, są one wyświetlane w portalu hello. Jest odbiorników obejmujący wiele lokacji stanowczo zalecane tooconfigure pierwszy wirusowej tooconfiguring wcześniejsze podstawowe odbiornika.  Zapewni to zakończenie tego ruchu pobiera routingiem toohello powrót. Jeśli podstawowy odbiornik znajduje się na początku listy i jest zgodny z żądaniem przychodzącym, jest ono przetwarzane przez ten odbiornik.

Żądania http://contoso.com są tooContosoServerPool routingiem i http://fabrikam.com są tooFabrikamServerPool routingiem.

Podobnie dwóch poddomen powitalne tej samej domeny nadrzędnej może być hostowana na hello tego samego wdrożenia bramy aplikacji. Przykłady użycia domen podrzędnych mogą obejmować domeny http://blog.contoso.com i http://app.contoso.com hostowane na jednym wdrożeniu usługi Application Gateway.

## <a name="host-headers-and-server-name-indication-sni"></a>Nagłówki hosta i oznaczanie nazwy serwera (SNI, Server Name Indication)

Istnieją trzy typowych mechanizmów włączania wielu lokacji hostingu na powitania sam infrastruktury.

1. Hostowanie wielu aplikacji sieci Web — każda z nich na unikatowym adresie IP.
2. Użyj nazwa toohost wiele aplikacji sieci web na powitania tego samego adresu IP.
3. Inne porty toohost wiele aplikacji sieci web na powitania tego samego adresu IP.

Obecnie usługa Application Gateway pobiera jeden publiczny adres IP, na którym nasłuchuje ruchu. Z tego względu obsługiwanie wielu aplikacji z oddzielnym adresem IP dla każdej z nich nie jest obecnie obsługiwane. Brama aplikacji w obsługuje obsługi wielu aplikacji każdego nasłuchiwania na inne porty, ale ten scenariusz wymaga hello aplikacji tooaccept ruch na portach niestandardowej, a nie często żądaną konfiguracją. Brama aplikacji w korzysta z protokołu HTTP 1.1 toohost nagłówków hosta więcej niż jednej witryny sieci Web na hello sam publiczny adres IP i portu. Witaj witryn hostowanych na bramy aplikacji może również obsługa odciążanie protokołu SSL z rozszerzeniem TLS oznaczenia nazwy serwera (SNI). W tym scenariuszu oznacza, że ten powitania klienta przeglądarki i wewnętrznej bazy danych kolektywu serwerów sieci web musi obsługiwać HTTP/1.1 i TLS rozszerzenia zgodnie z definicją w dokumencie RFC 6066.

## <a name="listener-configuration-element"></a>Element konfiguracji odbiornika

Istniejące HTTPListener, który element konfiguracji jest rozszerzony toosupport hosta nazwa serwera Nazwa wskazanie elementów i, używany przez pulę zaplecza tooappropriate ruchu tooroute bramy aplikacji. Witaj następujący przykładowy kod to fragment hello HttpListeners elementu z pliku szablonu.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Użytkownik może odwiedzić [szablonu usługi Resource Manager przy użyciu wielu lokacji hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) zakończenia tooend na podstawie szablonu wdrożenia.

## <a name="routing-rule"></a>Reguła routingu

Nie została zmieniona w reguły routingu hello wymagane. Witaj routingu reguły "Basic" powinno być kontynuowane toobe wybrany tootie hello odpowiedniej lokacji odbiornika toohello odpowiedniej puli adresów zaplecza.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Następne kroki

Po szkoleniowe dotyczące obsługi wielu lokacji, przejdź zbyt[Utwórz bramę aplikacji przy użyciu wielu lokacji hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate bramę aplikacji z możliwością toosupport więcej niż jednej aplikacji sieci web.

