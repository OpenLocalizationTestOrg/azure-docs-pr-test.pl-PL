---
title: "aaaConfigure SSL odciążania - Azure Application Gateway - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate odciążania bramę aplikacji przy użyciu protokołu SSL przez 2.0 interfejsu wiersza polecenia platformy Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="34a19-103">Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="34a19-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="34a19-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34a19-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="34a19-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a19-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="34a19-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a19-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="34a19-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="34a19-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="34a19-108">Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="34a19-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="34a19-109">Odciążanie protokołu SSL także upraszcza zarządzanie certyfikatami na powitania serwera frontonu.</span><span class="sxs-lookup"><span data-stu-id="34a19-109">SSL offload also simplifies certificate management at hello front-end server.</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="34a19-110">Wymagania wstępne: Instalacja hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34a19-110">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="34a19-111">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="34a19-111">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="34a19-112">Wymagane składniki</span><span class="sxs-lookup"><span data-stu-id="34a19-112">Required components</span></span>

* <span data-ttu-id="34a19-113">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="34a19-113">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="34a19-114">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="34a19-114">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="34a19-115">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="34a19-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="34a19-116">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="34a19-116">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="34a19-117">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="34a19-117">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="34a19-118">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="34a19-118">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="34a19-119">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te ustawienia są z uwzględnieniem wielkości liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="34a19-119">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="34a19-120">**Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="34a19-120">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="34a19-121">Obecnie tylko hello *podstawowe* reguła jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="34a19-121">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="34a19-122">Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.</span><span class="sxs-lookup"><span data-stu-id="34a19-122">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="34a19-123">**Uwagi dotyczące konfiguracji dodatkowych**</span><span class="sxs-lookup"><span data-stu-id="34a19-123">**Additional configuration notes**</span></span>

<span data-ttu-id="34a19-124">Do konfigurowania certyfikatów SSL, hello protokół **HttpListener** należy zmienić zbyt*Https* (z uwzględnieniem wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="34a19-124">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="34a19-125">Witaj **SslCertificate** zbyt dodany element**HttpListener** z wartości zmiennej hello skonfigurowanej dla certyfikatu SSL hello.</span><span class="sxs-lookup"><span data-stu-id="34a19-125">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="34a19-126">port frontonu Hello powinien być zaktualizowany too443.</span><span class="sxs-lookup"><span data-stu-id="34a19-126">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="34a19-127">**koligacji na podstawie plików cookie tooenable**: bramy aplikacji może być skonfigurowany tooensure żądania z sesji klienta jest zawsze ukierunkowanej toohello tej samej maszyny Wirtualnej w hello kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="34a19-127">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="34a19-128">W tym scenariuszu odbywa się przez uruchomienie pliku cookie sesji, umożliwiającą hello bramy toodirect ruch odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="34a19-128">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="34a19-129">Ustaw koligacji na podstawie plików cookie tooenable **CookieBasedAffinity** za*włączone* w hello **elementu BackendHttpSettings** elementu.</span><span class="sxs-lookup"><span data-stu-id="34a19-129">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="34a19-130">Skonfiguruj odciążanie protokołu SSL na istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="34a19-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="34a19-131">Utwórz bramę aplikacji z odciążania protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="34a19-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="34a19-132">następujące przykładowe Hello tworzy bramę aplikacji z odciążania protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="34a19-132">hello following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="34a19-133">Witaj certyfikat i hasło certyfikatu musi być zaktualizowany tooa prawidłowego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="34a19-133">hello certificate and certificate password must be updated tooa valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="34a19-134">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="34a19-134">Get application gateway DNS name</span></span>

<span data-ttu-id="34a19-135">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="34a19-135">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="34a19-136">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="34a19-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="34a19-137">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="34a19-137">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="34a19-138">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34a19-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="34a19-139">tooconfigure aliasu, pobrać szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="34a19-139">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="34a19-140">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="34a19-140">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="34a19-141">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34a19-141">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a><span data-ttu-id="34a19-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34a19-142">Next steps</span></span>

<span data-ttu-id="34a19-143">Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB), zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="34a19-143">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="34a19-144">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="34a19-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="34a19-145">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="34a19-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="34a19-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="34a19-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
