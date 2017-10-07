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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Konfigurowanie zapory aplikacji sieci web w nowej lub istniejącej bramy aplikacji przy użyciu wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-web-application-firewall-cli.md)

Dowiedz się, jak toocreate zapory aplikacji sieci web włączone bramy aplikacji lub Dodaj bramy sieci web aplikacji zapory tooan istniejących aplikacji.

Hello zapory aplikacji sieci web (WAF) brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, ataki skryptów między witrynami i hijacks sesji.

Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7. Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie. Brama aplikacji w oferuje wiele funkcji aplikacji dostarczania kontrolera (ADC), w tym HTTP załadować równoważenia, opartych na pliku cookie sesji koligacji, Odciążanie bezpiecznego secure sockets layer (SSL), sondy kondycji niestandardowych, obsługę wielu lokacji i wielu innych. toofind pełną listę obsługiwanych funkcji, odwiedź stronę: [brama Omówienie aplikacji](application-gateway-introduction.md).

Hello artykule przedstawiono sposób zbyt[dodawania bramy sieci web aplikacji zapory tooan istniejących aplikacji](#add-web-application-firewall-to-an-existing-application-gateway) i [Utwórz bramę aplikacji, która używa zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall).

![Scenariusz obrazu][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Wymagania wstępne: Instalacja hello Azure CLI 2.0

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Różnice w konfiguracji zapory aplikacji sieci Web

Jeśli znasz [Utwórz bramę aplikacji z wiersza polecenia platformy Azure](application-gateway-create-gateway-cli.md), zrozumieć hello SKU ustawienia tooconfigure podczas tworzenia bramy aplikacji. Zapory aplikacji sieci Web udostępnia dodatkowe ustawienia toodefine podczas konfigurowania hello jednostki SKU bramy aplikacji. Brak dodatkowych zmian wprowadzonych na nadana bramie aplikacji hello.

| **Ustawienie** | **Szczegóły**
|---|---|
|**SKU** |Bramy normalne aplikacji bez zapory aplikacji sieci Web obsługuje **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży**rozmiary. Wprowadzenie hello zapory aplikacji sieci Web, istnieją dwie dodatkowe jednostki SKU, **zapory aplikacji sieci Web\_średni** i **zapory aplikacji sieci Web\_duży**. Zapory aplikacji sieci Web nie jest obsługiwana w bramach małych aplikacji.|
|**Tryb** | To ustawienie jest tryb hello zapory aplikacji sieci Web. dozwolone wartości to **wykrywania** i **zapobiegania**. Gdy zapory aplikacji sieci Web jest skonfigurowana w trybie wykrywania, wszystkie zagrożenia są przechowywane w pliku dziennika. W trybie zapobiegania zdarzenia są nadal rejestrowane, ale osoba atakująca hello otrzymuje 403 nieautoryzowanego odpowiedź z bramy aplikacji hello.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Dodawanie sieci web aplikacji zapory tooan istniejącej bramy aplikacji

Witaj śledzenia zmian polecenia istniejącą bramę aplikacji obsługującej tooa zapory aplikacji sieci Web bramy standardowej aplikacji.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

To polecenie aktualizuje bramy aplikacji hello zapory aplikacji sieci web. Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) toounderstand jak tooview dzienniki bramy aplikacji. Powodu toohello zabezpieczeń rodzaj zapory aplikacji sieci Web dzienniki toobe należy regularnie weryfikowane toounderstand hello stan zabezpieczeń aplikacji sieci web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web

Witaj następujące polecenie tworzy bramę aplikacji z zapory aplikacji sieci web.

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
> Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe hello są skonfigurowane z CRS 3.0 do ochrony.

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure rekord CNAME Pobieranie szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.

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

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak zasady toocustomize zapory aplikacji sieci Web, odwiedzając: [dostosować reguły zapory aplikacji sieci web za pośrednictwem hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
