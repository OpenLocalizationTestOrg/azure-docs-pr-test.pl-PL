---
title: "Konfigurowanie protokołu SSL odciążania - Azure Application Gateway - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje, aby utworzyć bramę aplikacji przy użyciu protokołu SSL odciążenia przez 2.0 interfejsu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: e8c1ba09daef09ef5002e33345905772961c1d93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="9b993-103">Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="9b993-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b993-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9b993-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="9b993-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b993-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="9b993-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b993-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="9b993-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9b993-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="9b993-108">Usługę Azure Application Gateway można skonfigurować tak, aby przerywała sesję protokołu SSL (Secure Sockets Layer) na poziomie bramy, co pozwoli na uniknięcie wykonywania kosztownych zadań szyfrowania protokołu SSL w kolektywie serwerów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9b993-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="9b993-109">Odciążanie protokołu SSL także upraszcza zarządzanie certyfikatami na serwerze frontonu.</span><span class="sxs-lookup"><span data-stu-id="9b993-109">SSL offload also simplifies certificate management at the front-end server.</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="9b993-110">Wymagania wstępne: Instalacja Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9b993-110">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="9b993-111">Aby wykonać kroki opisane w tym artykule, należy [instalowanie interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9b993-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="9b993-112">Wymagane składniki</span><span class="sxs-lookup"><span data-stu-id="9b993-112">Required components</span></span>

* <span data-ttu-id="9b993-113">**Pula serwerów zaplecza:** lista adresów IP serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9b993-113">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="9b993-114">Adresy IP na liście powinny należeć do podsieci sieci wirtualnej lub być publicznymi bądź wirtualnymi adresami IP.</span><span class="sxs-lookup"><span data-stu-id="9b993-114">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="9b993-115">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="9b993-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9b993-116">Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.</span><span class="sxs-lookup"><span data-stu-id="9b993-116">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="9b993-117">**Port frontonu:** port publiczny, który jest otwierany w bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b993-117">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="9b993-118">Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9b993-118">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="9b993-119">**Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="9b993-119">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9b993-120">**Reguła:** reguła wiąże odbiornik z pulą serwerów zaplecza i umożliwia zdefiniowanie, do której puli serwerów zaplecza ma być przekierowywany ruch w przypadku trafienia do określonego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9b993-120">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="9b993-121">Obecnie jest obsługiwana tylko reguła *podstawowa*.</span><span class="sxs-lookup"><span data-stu-id="9b993-121">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="9b993-122">Reguła *podstawowa* to dystrybucja obciążenia z działaniem okrężnym.</span><span class="sxs-lookup"><span data-stu-id="9b993-122">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="9b993-123">**Uwagi dotyczące konfiguracji dodatkowych**</span><span class="sxs-lookup"><span data-stu-id="9b993-123">**Additional configuration notes**</span></span>

<span data-ttu-id="9b993-124">W przypadku konfiguracji certyfikatów SSL protokół w polu **HttpListener** należy zmienić na *Https* (z uwzględnieniem wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="9b993-124">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="9b993-125">Element **SslCertificate** jest dodawany do odbiornika **HttpListener** z wartością zmiennej skonfigurowaną dla certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="9b993-125">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="9b993-126">Port frontonu należy zaktualizować do 443.</span><span class="sxs-lookup"><span data-stu-id="9b993-126">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="9b993-127">**Aby włączyć koligację opartą na plikach cookie**: bramę aplikacji można skonfigurować tak, aby żądanie z sesji klienta było zawsze kierowane do tej samej maszyny wirtualnej w kolektywie serwerów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9b993-127">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="9b993-128">W tym scenariuszu należy wstrzyknąć plik cookie sesji, który umożliwi bramie prawidłowe kierowanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="9b993-128">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="9b993-129">Aby włączyć koligację opartą na plikach cookie, ustaw element **CookieBasedAffinity** na wartość *Enabled* w elemencie **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="9b993-129">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="9b993-130">Skonfiguruj odciążanie protokołu SSL na istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b993-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port to be used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload the .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing the port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool to be used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using the new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking the listener to the back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="9b993-131">Utwórz bramę aplikacji z odciążania protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="9b993-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="9b993-132">Poniższy przykład tworzy bramę aplikacji z odciążania protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="9b993-132">The following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="9b993-133">Certyfikat i hasło muszą zostać zaktualizowane do prawidłowego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="9b993-133">The certificate and certificate password must be updated to a valid private key.</span></span>

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

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9b993-134">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b993-134">Get application gateway DNS name</span></span>

<span data-ttu-id="9b993-135">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="9b993-135">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="9b993-136">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="9b993-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9b993-137">Aby upewnić się, że użytkownicy końcowi mogą trafić bramę aplikacji, można użyć rekordu CNAME w celu wskazania publicznego punktu końcowego bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b993-137">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="9b993-138">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9b993-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9b993-139">Aby skonfigurować alias, należy pobrać szczegółów bramy aplikacji i jego skojarzonej nazwy IP DNS za pomocą elementu publicznego adresu IP dołączony na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b993-139">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="9b993-140">Nazwa DNS bramy aplikacji powinna zostać użyta w celu utworzenia rekordu CNAME, który wskazuje dwóm aplikacjom sieci Web tę nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="9b993-140">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="9b993-141">Korzystanie z rekordów A nie jest zalecane, ponieważ adres VIP może ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b993-141">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="9b993-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b993-142">Next steps</span></span>

<span data-ttu-id="9b993-143">Jeśli chcesz skonfigurować bramę aplikacji do użycia z wewnętrznego modułem równoważenia obciążenia, zobacz artykuł [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Tworzenie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="9b993-143">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="9b993-144">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="9b993-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="9b993-145">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="9b993-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="9b993-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="9b993-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
