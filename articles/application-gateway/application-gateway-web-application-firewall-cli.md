---
title: "Zapora aplikacji sieci web aaaConfigure — brama aplikacji w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wskazówki dotyczące sposobu przy użyciu toostart Zapora aplikacji sieci web w istniejącej lub nowej bramy aplikacji."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="cdff2-103">Konfigurowanie zapory aplikacji sieci web w nowej lub istniejącej bramy aplikacji przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cdff2-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cdff2-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cdff2-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="cdff2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdff2-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="cdff2-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cdff2-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="cdff2-107">Dowiedz się, jak toocreate zapory aplikacji sieci web włączone bramy aplikacji lub Dodaj bramy sieci web aplikacji zapory tooan istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="cdff2-108">Hello zapory aplikacji sieci web (WAF) brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, ataki skryptów między witrynami i hijacks sesji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="cdff2-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="cdff2-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="cdff2-110">Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="cdff2-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="cdff2-111">Brama aplikacji w oferuje wiele funkcji aplikacji dostarczania kontrolera (ADC), w tym HTTP załadować równoważenia, opartych na pliku cookie sesji koligacji, Odciążanie bezpiecznego secure sockets layer (SSL), sondy kondycji niestandardowych, obsługę wielu lokacji i wielu innych.</span><span class="sxs-lookup"><span data-stu-id="cdff2-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="cdff2-112">toofind pełną listę obsługiwanych funkcji, odwiedź stronę: [brama Omówienie aplikacji](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cdff2-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="cdff2-113">Hello artykule przedstawiono sposób zbyt[dodawania bramy sieci web aplikacji zapory tooan istniejących aplikacji](#add-web-application-firewall-to-an-existing-application-gateway) i [Utwórz bramę aplikacji, która używa zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="cdff2-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Scenariusz obrazu][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="cdff2-115">Wymagania wstępne: Instalacja hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cdff2-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="cdff2-116">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="cdff2-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="cdff2-117">Różnice w konfiguracji zapory aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cdff2-117">WAF configuration differences</span></span>

<span data-ttu-id="cdff2-118">Jeśli znasz [Utwórz bramę aplikacji z wiersza polecenia platformy Azure](application-gateway-create-gateway-cli.md), zrozumieć hello SKU ustawienia tooconfigure podczas tworzenia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="cdff2-119">Zapory aplikacji sieci Web udostępnia dodatkowe ustawienia toodefine podczas konfigurowania hello jednostki SKU bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="cdff2-120">Brak dodatkowych zmian wprowadzonych na nadana bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cdff2-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="cdff2-121">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="cdff2-121">**Setting**</span></span> | <span data-ttu-id="cdff2-122">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="cdff2-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="cdff2-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="cdff2-123">**SKU**</span></span> |<span data-ttu-id="cdff2-124">Bramy normalne aplikacji bez zapory aplikacji sieci Web obsługuje **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży**rozmiary.</span><span class="sxs-lookup"><span data-stu-id="cdff2-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="cdff2-125">Wprowadzenie hello zapory aplikacji sieci Web, istnieją dwie dodatkowe jednostki SKU, **zapory aplikacji sieci Web\_średni** i **zapory aplikacji sieci Web\_duży**.</span><span class="sxs-lookup"><span data-stu-id="cdff2-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="cdff2-126">Zapory aplikacji sieci Web nie jest obsługiwana w bramach małych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="cdff2-127">**Tryb**</span><span class="sxs-lookup"><span data-stu-id="cdff2-127">**Mode**</span></span> | <span data-ttu-id="cdff2-128">To ustawienie jest tryb hello zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cdff2-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="cdff2-129">dozwolone wartości to **wykrywania** i **zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="cdff2-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="cdff2-130">Gdy zapory aplikacji sieci Web jest skonfigurowana w trybie wykrywania, wszystkie zagrożenia są przechowywane w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="cdff2-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="cdff2-131">W trybie zapobiegania zdarzenia są nadal rejestrowane, ale osoba atakująca hello otrzymuje 403 nieautoryzowanego odpowiedź z bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cdff2-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="cdff2-132">Dodawanie sieci web aplikacji zapory tooan istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="cdff2-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="cdff2-133">Witaj śledzenia zmian polecenia istniejącą bramę aplikacji obsługującej tooa zapory aplikacji sieci Web bramy standardowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="cdff2-134">To polecenie aktualizuje bramy aplikacji hello zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cdff2-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="cdff2-135">Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) toounderstand jak tooview dzienniki bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="cdff2-136">Powodu toohello zabezpieczeń rodzaj zapory aplikacji sieci Web dzienniki toobe należy regularnie weryfikowane toounderstand hello stan zabezpieczeń aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cdff2-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="cdff2-137">Utwórz bramę aplikacji z zapory aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="cdff2-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="cdff2-138">Witaj następujące polecenie tworzy bramę aplikacji z zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cdff2-138">hello following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="cdff2-139">Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe hello są skonfigurowane z CRS 3.0 do ochrony.</span><span class="sxs-lookup"><span data-stu-id="cdff2-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="cdff2-140">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="cdff2-140">Get application gateway DNS name</span></span>

<span data-ttu-id="cdff2-141">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="cdff2-142">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="cdff2-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="cdff2-143">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cdff2-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="cdff2-144">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cdff2-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="cdff2-145">tooconfigure rekord CNAME Pobieranie szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="cdff2-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="cdff2-146">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="cdff2-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="cdff2-147">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdff2-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="cdff2-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdff2-148">Next steps</span></span>

<span data-ttu-id="cdff2-149">Dowiedz się, jak zasady toocustomize zapory aplikacji sieci Web, odwiedzając: [dostosować reguły zapory aplikacji sieci web za pośrednictwem hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cdff2-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
