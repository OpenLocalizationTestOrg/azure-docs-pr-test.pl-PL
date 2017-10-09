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
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="789bc-103">Hostowanie wielu witryn usługi Application Gateway</span><span class="sxs-lookup"><span data-stu-id="789bc-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="789bc-104">Obsługujący wiele lokacji umożliwia tooconfigure więcej niż jednej aplikacji sieci web na powitania tego samego wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="789bc-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="789bc-105">Ta funkcja umożliwia tooconfigure efektywniejsze topologii wdrożeń sumując too20 witryn sieci Web tooone aplikacji bramy.</span><span class="sxs-lookup"><span data-stu-id="789bc-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="789bc-106">Każda witryna sieci Web może zostać skierowany tooits właścicielem puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="789bc-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="789bc-107">W hello poniższy przykład bramy aplikacji jest obsługujące ruch contoso.com i fabrikam.com z dwie pule serwera wewnętrznej nazywana ContosoServerPool i FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="789bc-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="789bc-109">Reguły są przetwarzane w kolejności hello, są one wyświetlane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="789bc-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="789bc-110">Jest odbiorników obejmujący wiele lokacji stanowczo zalecane tooconfigure pierwszy wirusowej tooconfiguring wcześniejsze podstawowe odbiornika.</span><span class="sxs-lookup"><span data-stu-id="789bc-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="789bc-111">Zapewni to zakończenie tego ruchu pobiera routingiem toohello powrót.</span><span class="sxs-lookup"><span data-stu-id="789bc-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="789bc-112">Jeśli podstawowy odbiornik znajduje się na początku listy i jest zgodny z żądaniem przychodzącym, jest ono przetwarzane przez ten odbiornik.</span><span class="sxs-lookup"><span data-stu-id="789bc-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="789bc-113">Żądania http://contoso.com są tooContosoServerPool routingiem i http://fabrikam.com są tooFabrikamServerPool routingiem.</span><span class="sxs-lookup"><span data-stu-id="789bc-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="789bc-114">Podobnie dwóch poddomen powitalne tej samej domeny nadrzędnej może być hostowana na hello tego samego wdrożenia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="789bc-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="789bc-115">Przykłady użycia domen podrzędnych mogą obejmować domeny http://blog.contoso.com i http://app.contoso.com hostowane na jednym wdrożeniu usługi Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="789bc-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="789bc-116">Nagłówki hosta i oznaczanie nazwy serwera (SNI, Server Name Indication)</span><span class="sxs-lookup"><span data-stu-id="789bc-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="789bc-117">Istnieją trzy typowych mechanizmów włączania wielu lokacji hostingu na powitania sam infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="789bc-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="789bc-118">Hostowanie wielu aplikacji sieci Web — każda z nich na unikatowym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="789bc-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="789bc-119">Użyj nazwa toohost wiele aplikacji sieci web na powitania tego samego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="789bc-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="789bc-120">Inne porty toohost wiele aplikacji sieci web na powitania tego samego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="789bc-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="789bc-121">Obecnie usługa Application Gateway pobiera jeden publiczny adres IP, na którym nasłuchuje ruchu.</span><span class="sxs-lookup"><span data-stu-id="789bc-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="789bc-122">Z tego względu obsługiwanie wielu aplikacji z oddzielnym adresem IP dla każdej z nich nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="789bc-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="789bc-123">Brama aplikacji w obsługuje obsługi wielu aplikacji każdego nasłuchiwania na inne porty, ale ten scenariusz wymaga hello aplikacji tooaccept ruch na portach niestandardowej, a nie często żądaną konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="789bc-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="789bc-124">Brama aplikacji w korzysta z protokołu HTTP 1.1 toohost nagłówków hosta więcej niż jednej witryny sieci Web na hello sam publiczny adres IP i portu.</span><span class="sxs-lookup"><span data-stu-id="789bc-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="789bc-125">Witaj witryn hostowanych na bramy aplikacji może również obsługa odciążanie protokołu SSL z rozszerzeniem TLS oznaczenia nazwy serwera (SNI).</span><span class="sxs-lookup"><span data-stu-id="789bc-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="789bc-126">W tym scenariuszu oznacza, że ten powitania klienta przeglądarki i wewnętrznej bazy danych kolektywu serwerów sieci web musi obsługiwać HTTP/1.1 i TLS rozszerzenia zgodnie z definicją w dokumencie RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="789bc-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="789bc-127">Element konfiguracji odbiornika</span><span class="sxs-lookup"><span data-stu-id="789bc-127">Listener configuration element</span></span>

<span data-ttu-id="789bc-128">Istniejące HTTPListener, który element konfiguracji jest rozszerzony toosupport hosta nazwa serwera Nazwa wskazanie elementów i, używany przez pulę zaplecza tooappropriate ruchu tooroute bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="789bc-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="789bc-129">Witaj następujący przykładowy kod to fragment hello HttpListeners elementu z pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="789bc-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="789bc-130">Użytkownik może odwiedzić [szablonu usługi Resource Manager przy użyciu wielu lokacji hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) zakończenia tooend na podstawie szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="789bc-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="789bc-131">Reguła routingu</span><span class="sxs-lookup"><span data-stu-id="789bc-131">Routing rule</span></span>

<span data-ttu-id="789bc-132">Nie została zmieniona w reguły routingu hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="789bc-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="789bc-133">Witaj routingu reguły "Basic" powinno być kontynuowane toobe wybrany tootie hello odpowiedniej lokacji odbiornika toohello odpowiedniej puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="789bc-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="789bc-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="789bc-134">Next steps</span></span>

<span data-ttu-id="789bc-135">Po szkoleniowe dotyczące obsługi wielu lokacji, przejdź zbyt[Utwórz bramę aplikacji przy użyciu wielu lokacji hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate bramę aplikacji z możliwością toosupport więcej niż jednej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="789bc-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

