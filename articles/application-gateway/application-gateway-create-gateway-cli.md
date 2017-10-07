---
title: "aaaCreate bramę aplikacji Azure — 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate bramę aplikacji przy użyciu hello Azure CLI 2.0 w Menedżerze zasobów"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Tworzenie bramy aplikacji przy użyciu hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-gateway-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-gateway.md)
> * [Szablon usługi Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](application-gateway-create-gateway-cli.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-create-gateway-cli.md)

Brama aplikacji jest dedykowany urządzenie wirtualne, która udostępnia kontroler dostarczania aplikacji (ADC) jako usługa, oferty różnych warstwy 7 załadować równoważenia możliwości aplikacji.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="prerequisite-install-hello-azure-cli-20"></a>Wymagania wstępne: Instalacja hello Azure CLI 2.0

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Jeśli nie masz konta platformy Azure, można je utworzyć. Zarejestruj się, aby skorzystać z [bezpłatnego demo](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenariusz

W tym scenariuszu możesz dowiedzieć się, jak bramy aplikacji przy użyciu toocreate hello portalu Azure.

W tym scenariuszu obejmują:

* Utwórz bramę aplikacji średnia z dwóch wystąpień.
* Tworzenie sieci wirtualnej o nazwie AdatumAppGatewayVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.
* Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.

> [!NOTE]
> Dodatkowa konfiguracja bramy aplikacji hello, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji hello i nie podczas pierwszego wdrożenia.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Brama aplikacji w Azure wymaga jego własnej podsieci. Podczas tworzenia sieci wirtualnej, upewnij się, pozostaw toohave miejsce za mało adresów wielu podsieci. Po wdrożeniu tooa podsieci bramy aplikacji bramy tylko dodatkowych aplikacji można dodać podsieci toohello.

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Otwórz hello **wiersza polecenia usługi Microsoft Azure**i zaloguj się. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> Można również użyć `az login` bez hello przełącznika dla nazwy logowania urządzenia, która wymaga wprowadzenie kodu na aka.ms/devicelogin.

Po wpisaniu hello poprzedzających przykład znajduje się kod. Przejdź toohttps://aka.ms/devicelogin w procesie logowania hello toocontinue przeglądarki.

![cmd przedstawiający urządzenia logowania][1]

W przeglądarce hello wprowadź otrzymany kod hello. Jesteś tooa przekierowanego strony logowania.

![Kod tooenter przeglądarki][2]

Po wprowadzeniu kodu hello użytkownik jest zalogowany, zamknij hello toocontinue przeglądarki ze scenariuszem hello.

![pomyślnie zalogował się][3]

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Przed utworzeniem bramy aplikacji hello, grupy zasobów jest utworzyć bramę aplikacji hello toocontain. Oto Hello hello polecenia.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Utwórz bramę aplikacji hello

Hello adresy IP używane dla hello wewnętrznej bazy danych są adresami IP powitania serwera wewnętrznej bazy danych. Te wartości można albo prywatnych adresów IP w sieci wirtualnej hello, publiczne adresy IP lub nazwy FQDN dla serwerów zaplecza. Witaj poniższy przykład tworzy bramę aplikacji przy użyciu ustawień konfiguracyjnych dodatkowe ustawienia protokołu http, porty i zasady.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Hello poprzednim przykładzie pokazano wiele właściwości, które nie są wymagane podczas tworzenia hello bramy aplikacji. Witaj poniższy przykład kodu tworzy bramę aplikacji hello wymagane informacje.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Aby uzyskać listę parametrów, które można podać podczas hello tworzenia, uruchom następujące polecenie: `az network application-gateway create --help`.

W tym przykładzie tworzy bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika hello, puli zaplecza, ustawienia http zaplecza i zasady. Możesz zmodyfikować toosuit te ustawienia wdrożenia po aprowizacji hello zakończy się pomyślnie.
Jeśli masz już aplikację sieci web zdefiniowane z puli zaplecza hello w hello w poprzednich krokach utworzono raz, równoważenie obciążenia sieciowego rozpoczyna się.

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../dns/dns-custom-domain.md). tooconfigure aliasu, pobrać szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.


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

## <a name="delete-all-resources"></a>Usuwanie wszystkich zasobów

toodelete wszystkie zasoby są tworzone w tym artykule pełną hello następujące kroki:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak sondy kondycji niestandardowych toocreate odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)

Dowiedz się, jak tooconfigure odciążanie protokołu SSL i kosztowne odszyfrowywania SSL podjęcia hello wyłączone serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
