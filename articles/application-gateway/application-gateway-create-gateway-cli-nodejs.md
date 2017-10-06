---
title: "aaaCreate bramę aplikacji Azure — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate bramę aplikacji przy użyciu hello Azure CLI 1.0 w Menedżerze zasobów"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Tworzenie bramy aplikacji przy użyciu hello wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-gateway-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-gateway.md)
> * [Szablon usługi Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](application-gateway-create-gateway-cli.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7. Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie. Brama aplikacji ma następujące funkcje dostarczania aplikacji hello: HTTP załadować sondy kondycji niestandardowych równoważenia koligacji na podstawie plików cookie sesji i odciążanie protokołu Secure Sockets Layer (SSL) i obsługę wielu lokacji.

## <a name="prerequisite-install-hello-azure-cli"></a>Wymagania wstępne: Instalacja hello wiersza polecenia platformy Azure

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](../xplat-cli-install.md) i potrzebna jest zbyt[logowania tooAzure](../xplat-cli-connect.md). 

> [!NOTE]
> Jeśli nie masz konta platformy Azure, można je utworzyć. Zarejestruj się, aby skorzystać z [bezpłatnego demo](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenariusz

W tym scenariuszu możesz dowiedzieć się, jak bramy aplikacji przy użyciu toocreate hello portalu Azure.

W tym scenariuszu obejmują:

* Utwórz bramę aplikacji średnia z dwóch wystąpień.
* Tworzenie sieci wirtualnej o nazwie ContosoVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.
* Utwórz podsieć o nazwie subnet01, która używa 10.0.0.0/28 bloku CIDR.

> [!NOTE]
> Dodatkowa konfiguracja bramy aplikacji hello, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji hello i nie podczas pierwszego wdrożenia.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Brama aplikacji w Azure wymaga jego własnej podsieci. Podczas tworzenia sieci wirtualnej, upewnij się, pozostaw toohave miejsce za mało adresów wielu podsieci. Po wdrożeniu tooa podsieci bramy aplikacji jedynymi dodatkowymi aplikacji bramy są toobe można dodać podsieci toohello.

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Otwórz hello **wiersza polecenia usługi Microsoft Azure**i zaloguj się. 

```azurecli-interactive
azure login
```

Po wpisaniu hello poprzedzających przykład znajduje się kod. Przejdź toohttps://aka.ms/devicelogin w procesie logowania hello toocontinue przeglądarki.

![cmd przedstawiający urządzenia logowania][1]

W przeglądarce hello wprowadź otrzymany kod hello. Jesteś tooa przekierowanego strony logowania.

![Kod tooenter przeglądarki][2]

Po wprowadzeniu kodu hello użytkownik jest zalogowany, zamknij hello toocontinue przeglądarki ze scenariuszem hello.

![pomyślnie zalogował się][3]

## <a name="switch-tooresource-manager-mode"></a>Przełącz tryb Manager tooResource

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Przed utworzeniem bramy aplikacji hello, grupy zasobów jest utworzyć bramę aplikacji hello toocontain. Oto Hello hello polecenia.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej

Po utworzeniu grupy zasobów hello sieci wirtualnej jest tworzona dla bramy aplikacji hello.  W hello poniższy przykład przestrzeni adresowej hello było jako 10.0.0.0/16 zgodnie z definicją w hello poprzedzających uwagi scenariusza.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Tworzenie podsieci

Po utworzeniu sieci wirtualnej hello podsieci jest dodawany do bramy aplikacji hello.  Jeśli planujesz toouse brama aplikacji w aplikacji sieci web hostowanych w hello sam wirtualnych sieci jako bramę aplikacji hello, za mało miejsca w innej podsieci, czy tooleave.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Utwórz bramę aplikacji hello

Po utworzeniu sieci wirtualnej hello i podsieć hello wymagania wstępne dla bramy aplikacji hello są spełnione. Ponadto hasło certyfikatu i hello wcześniej eksportowanego pliku PFX certyfikatu hello są wymagane dla powitania po kroku: hello adresy IP używane dla zaplecza hello są hello adresów IP dla serwera wewnętrznej bazy danych. Te wartości można albo prywatnych adresów IP w sieci wirtualnej hello, publiczne adresy IP lub nazwy FQDN dla serwerów zaplecza.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Lista parametrów, które można podać podczas tworzenia, uruchom następujące polecenie hello: **brama aplikacji w sieci azure, Utwórz — Pomoc**.

W tym przykładzie tworzy bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika hello, puli zaplecza, ustawienia http zaplecza i zasady. Możesz zmodyfikować toosuit te ustawienia wdrożenia po aprowizacji hello zakończy się pomyślnie.
Jeśli masz już aplikację sieci web zdefiniowane z puli zaplecza hello w hello w poprzednich krokach utworzono raz, równoważenie obciążenia sieciowego rozpoczyna się.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak sondy kondycji niestandardowych toocreate odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)

Dowiedz się, jak tooconfigure odciążanie protokołu SSL i kosztowne odszyfrowywania SSL podjęcia hello wyłączone serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
