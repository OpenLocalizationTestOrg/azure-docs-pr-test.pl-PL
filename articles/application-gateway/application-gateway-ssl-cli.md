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
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a>Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ssl-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ssl.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-ssl-cli.md)

Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web. Odciążanie protokołu SSL także upraszcza zarządzanie certyfikatami na powitania serwera frontonu.

## <a name="prerequisite-install-hello-azure-cli-20"></a>Wymagania wstępne: Instalacja hello Azure CLI 2.0

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="required-components"></a>Wymagane składniki

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te ustawienia są z uwzględnieniem wielkości liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika. Obecnie tylko hello *podstawowe* reguła jest obsługiwana. Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.

**Uwagi dotyczące konfiguracji dodatkowych**

Do konfigurowania certyfikatów SSL, hello protokół **HttpListener** należy zmienić zbyt*Https* (z uwzględnieniem wielkości liter). Witaj **SslCertificate** zbyt dodany element**HttpListener** z wartości zmiennej hello skonfigurowanej dla certyfikatu SSL hello. port frontonu Hello powinien być zaktualizowany too443.

**koligacji na podstawie plików cookie tooenable**: bramy aplikacji może być skonfigurowany tooensure żądania z sesji klienta jest zawsze ukierunkowanej toohello tej samej maszyny Wirtualnej w hello kolektywu serwerów sieci web. W tym scenariuszu odbywa się przez uruchomienie pliku cookie sesji, umożliwiającą hello bramy toodirect ruch odpowiednio. Ustaw koligacji na podstawie plików cookie tooenable **CookieBasedAffinity** za*włączone* w hello **elementu BackendHttpSettings** elementu.

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a>Skonfiguruj odciążanie protokołu SSL na istniejącą bramę aplikacji

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

## <a name="create-an-application-gateway-with-ssl-offload"></a>Utwórz bramę aplikacji z odciążania protokołu SSL

następujące przykładowe Hello tworzy bramę aplikacji z odciążania protokołu SSL.  Witaj certyfikat i hasło certyfikatu musi być zaktualizowany tooa prawidłowego klucza prywatnego.

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

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure aliasu, pobrać szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.


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

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB), zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).

Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)
