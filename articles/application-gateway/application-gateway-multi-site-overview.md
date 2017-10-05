---
title: "Hostowanie wielu witryn w usłudze Azure Application Gateway | Microsoft Docs"
description: "Ta strona zawiera omówienie obsługi wielu witryn w usłudze Application Gateway."
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
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="41642-103">Hostowanie wielu witryn usługi Application Gateway</span><span class="sxs-lookup"><span data-stu-id="41642-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="41642-104">Hostowanie wielu witryn pozwala na skonfigurowanie więcej niż jednej aplikacji sieci Web na tym samym wystąpieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41642-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="41642-105">Ta funkcja umożliwia skonfigurowanie bardziej wydajnej topologii dla wdrożeń przez dodanie maksymalnie 20 witryn sieci Web do jednej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41642-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="41642-106">Każdą witrynę sieci Web można skierować do jej puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="41642-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="41642-107">W poniższym przykładzie usługa Application Gateway obsługuje ruch dla domen contoso.com i fabrikam.com z dwóch pul serwerów zaplecza o nazwach ContosoServerPool i FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="41642-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="41642-109">Reguły są przetwarzane w kolejności, w jakiej znajdują się na liście w portalu.</span><span class="sxs-lookup"><span data-stu-id="41642-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="41642-110">Zdecydowanie zaleca się skonfigurowanie odbiorników obejmujących wiele lokacji przed skonfigurowaniem podstawowego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="41642-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="41642-111">Zapewni to skierowanie ruchu do odpowiedniego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="41642-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="41642-112">Jeśli podstawowy odbiornik znajduje się na początku listy i jest zgodny z żądaniem przychodzącym, jest ono przetwarzane przez ten odbiornik.</span><span class="sxs-lookup"><span data-stu-id="41642-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="41642-113">Żądania dla adresu http://contoso.com są kierowane do puli ContosoServerPool, a dla adresu http://fabrikam.com — do puli FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="41642-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="41642-114">Podobnie dwie domeny podrzędne tej samej domeny nadrzędnej mogą być hostowane na tym samym wdrożeniu usługi Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41642-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="41642-115">Przykłady użycia domen podrzędnych mogą obejmować domeny http://blog.contoso.com i http://app.contoso.com hostowane na jednym wdrożeniu usługi Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41642-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="41642-116">Nagłówki hosta i oznaczanie nazwy serwera (SNI, Server Name Indication)</span><span class="sxs-lookup"><span data-stu-id="41642-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="41642-117">Istnieją trzy popularne mechanizmy włączania hostingu wielu witryn w tej samej infrastrukturze.</span><span class="sxs-lookup"><span data-stu-id="41642-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="41642-118">Hostowanie wielu aplikacji sieci Web — każda z nich na unikatowym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="41642-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="41642-119">Użycie nazwy hosta do hostowania wielu aplikacji sieci Web na tym samym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="41642-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="41642-120">Użycie różnych portów do hostowania wielu aplikacji sieci Web na tym samym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="41642-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="41642-121">Obecnie usługa Application Gateway pobiera jeden publiczny adres IP, na którym nasłuchuje ruchu.</span><span class="sxs-lookup"><span data-stu-id="41642-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="41642-122">Z tego względu obsługiwanie wielu aplikacji z oddzielnym adresem IP dla każdej z nich nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="41642-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="41642-123">Usługa Application Gateway obsługuje hostowanie wielu aplikacji, z których każda nasłuchuje na innym porcie, ale ten scenariusz wymaga, aby aplikacje akceptowały ruch na portach niestandardowych, co często nie jest pożądaną konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="41642-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="41642-124">Usługa Application Gateway bazuje na nagłówkach hosta HTTP 1.1 w celu hostowania więcej niż jednej witryny sieci Web na tym samym publicznym adresie IP i porcie.</span><span class="sxs-lookup"><span data-stu-id="41642-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="41642-125">Witryny hostowane w usłudze Application Gateway mogą także obsługiwać odciążanie protokołu SSL za pomocą rozszerzenia TLS oznaczania nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="41642-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="41642-126">Ten scenariusz oznacza, że przeglądarka i farma sieci Web zaplecza klienta muszą obsługiwać protokół HTTP/1.1 i rozszerzenie TLS zgodnie ze standardem RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="41642-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="41642-127">Element konfiguracji odbiornika</span><span class="sxs-lookup"><span data-stu-id="41642-127">Listener configuration element</span></span>

<span data-ttu-id="41642-128">Istniejący element konfiguracji HTTPListener został ulepszony na potrzeby obsługi elementów oznaczania nazwy hosta i nazwy serwera, co jest używane przez usługę Application Gateway w celu kierowania ruchu do odpowiedniej puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="41642-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="41642-129">Poniższy przykład kodu jest fragmentem elementu HttpListeners z pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="41642-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="41642-130">Możesz odwiedzić stronę [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) (Szablon usługi Resource Manager z zastosowaniem hostowania wielu witryn), aby zapoznać się z kompleksowym wdrożeniem opartym na szablonie.</span><span class="sxs-lookup"><span data-stu-id="41642-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="41642-131">Reguła routingu</span><span class="sxs-lookup"><span data-stu-id="41642-131">Routing rule</span></span>

<span data-ttu-id="41642-132">Reguła routingu nie wymaga żadnej zmiany.</span><span class="sxs-lookup"><span data-stu-id="41642-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="41642-133">Nadal należy wybierać podstawową regułę routingu „Basic” w celu powiązania odpowiedniego odbiornika witryny z właściwą pulą adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="41642-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="41642-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41642-134">Next steps</span></span>

<span data-ttu-id="41642-135">Po zapoznaniu się z informacjami o hostowaniu wielu witryn przejdź do [tworzenia bramy aplikacji przy użyciu hostowania wielu witryn](application-gateway-create-multisite-azureresourcemanager-powershell.md), aby utworzyć bramę aplikacji z możliwością obsługi więcej niż jednej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="41642-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

