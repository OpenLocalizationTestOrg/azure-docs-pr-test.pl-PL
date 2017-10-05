---
title: "Utwórz bramę aplikacji przy użyciu reguł routingu adresów URL - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące tworzenia, konfigurowania bramy usługi aplikacji Azure przy użyciu reguł routingu adresów URL"
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
ms.openlocfilehash: 958049830d6753ec26635f18f8f8b2fabdec0733
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Utwórz bramę aplikacji przy użyciu routingu opartego na ścieżkę 2.0 interfejsu wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-create-url-route-cli.md)

Na podstawie ścieżki routingu adresów URL umożliwia powiązanie tras na podstawie ścieżki adresu URL żądania Http. Sprawdza, czy istnieje trasa do puli zaplecza skonfigurowane dla adresu URL, w bramie aplikacji, a wysyła ruchu sieciowego do określonych puli zaplecza. Użycia routingu opartego na adres URL jest w celu zrównoważenia obciążenia żądaniami dla różnych typów zawartości do innego serwera zaplecza pul.

Routingu opartego na adres URL został wprowadzony nowy typ reguły na bramie aplikacji. Brama aplikacji ma dwa typy zasad: podstawowe i PathBasedRouting. Podstawowe reguły typu udostępnia usługę okrężnego dla pul zaplecza podczas PathBasedRouting oprócz dystrybucji działanie okrężne, uwzględnia również wzorzec ścieżki adresu URL żądania podczas wybierania puli zaplecza.

## <a name="scenario"></a>Scenariusz

W poniższym przykładzie brama aplikacji jest obsługę ruchu dla domeny contoso.com z dwóch pul serwerów zaplecza: domyślna pula serwera i puli serwerów obrazu.

Żądania dla http://contoso.com/image * są kierowane do puli serwerów obrazu (imagesBackendPool), czy wzorzec ścieżki nie jest zgodny, domyślna pula serwera (appGatewayBackendPool) jest zaznaczona.

![trasy adresu URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Otwórz **wiersza polecenia usługi Microsoft Azure**i zaloguj się. 

```azurecli
az login -u "username"
```

> [!NOTE]
> Można również użyć `az login` bez przełącznika dla nazwy logowania urządzenia, która wymaga wprowadzenie kodu na aka.ms/devicelogin.

Po wpisaniu powyższego przykładu znajduje się kod. Przejdź do https://aka.ms/devicelogin w przeglądarce, aby kontynuować proces logowania.

![cmd przedstawiający urządzenia logowania][1]

W przeglądarce wprowadź otrzymany kod. Nastąpi przekierowanie do strony logowania.

![przeglądarki, aby wprowadzić kod][2]

Po wprowadzeniu kodu użytkownik jest zalogowany, zamknij przeglądarkę, aby kontynuować na ze scenariuszem.

![pomyślnie zalogował się][3]

## <a name="add-a-path-based-rule-to-an-existing-application-gateway"></a>Dodawanie reguły na podstawie ścieżki do istniejącej bramy aplikacji

Utwórz bramę aplikacji z reguły ścieżki zdefiniowane

### <a name="create-a-new-back-end-pool"></a>Utwórz nową pulę zaplecza

Skonfiguruj ustawienia bramy aplikacji **imagesBackendPool** dla ruchu sieciowego z równoważeniem obciążenia w puli zaplecza. W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza nowej puli zaplecza. Każda pula zaplecza może mieć własne ustawienia puli zaplecza.  Ustawienia HTTP zaplecza są używane przez reguły do kierowania ruchu do właściwych elementów członkowskich puli zaplecza. Określa protokół i port, który jest używany podczas wysyłania ruchu do elementów członkowskich puli wewnętrznej bazy danych. Sesje bazujące na plikach cookie są też określane przez ustawienia HTTP zaplecza.  Jeśli koligacja sesji bazujących na plikach cookie jest włączona, wysyła ruch do tego samego zaplecza co poprzednie żądania dla każdego pakietu.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Utwórz nowy port frontonu

Skonfiguruj port frontonu dla bramy aplikacji. Obiekt konfiguracji portu frontonu jest używany przez odbiornik do definiowania, który port usługi Application Gateway nasłuchuje ruchu na odbiorniku.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Utwórz nowy

Skonfiguruj odbiornik. W tym kroku dla odbiornika konfigurowany jest publiczny adres IP i port używane do odbierania przychodzącego ruchu sieciowego. W poniższym przykładzie przyjmuje wcześniej skonfigurowane konfiguracji IP frontonu, Konfiguracja portów frontonu i protokołu (http lub https) i konfiguruje odbiornika. W tym przykładzie odbiornika nasłuchuje ruchu HTTP na porcie 82 publicznego adresu IP, który został utworzony wcześniej.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-the-url-path-map"></a>Tworzenie mapy ścieżki adresu Url

Konfiguruj adres URL reguły ścieżki dla pul zaplecza. Ten krok umożliwia skonfigurowanie ścieżki względnej, używany przez bramę aplikacji, aby określić mapowanie między ścieżki adresu URL i puli zaplecza, które są przypisane do obsługi ruchu przychodzącego.

> [!IMPORTANT]
> Każda ścieżka musi rozpoczynać się od / i miejsce tylko "\*" jest dozwolone, jest na końcu. Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *. Ciąg przekazywani do dopasowania ścieżki nie zawiera żadnego tekstu po pierwszym "?" lub "#", a te znaki są niedozwolone. 

Poniższy przykład tworzy jedną regułę "/ obrazów / *" ścieżkę routingu ruchu do wewnętrznej "imagesBackendPool." Ta reguła zapewnia, że ruch dla każdego zestawu adresów URL jest kierowany do wewnętrznej bazy danych. Na przykład http://adatum.com/images/figure1.jpg przechodzi do "imagesBackendPool." Jeśli ścieżka nie odpowiada żadnemu z reguły ścieżki wstępnie zdefiniowane, Konfiguracja mapowania ścieżki reguły konfiguruje również domyślna pula adresów zaplecza. Na przykład http://adatum.com/shoppingcart/test.html prowadzi do pool1 określone jako domyślna pula niedopasowane ruchu.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz dowiedzieć się więcej o odciążania protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
