---
title: "zasady bramę aplikacji przy użyciu routingu adresów URL - aaaCreate 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfiguruj bramę aplikacji Azure przy użyciu reguł routingu adresów URL"
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
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Utwórz bramę aplikacji przy użyciu routingu opartego na ścieżkę 2.0 interfejsu wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-create-url-route-cli.md)

Na podstawie ścieżki routingu adresów URL umożliwia możesz tooassociate tras na podstawie hello ścieżki adresu URL żądania Http. Sprawdza, czy jest skonfigurowane dla adresu URL hello przedstawionych w hello brama aplikacji w puli zaplecza tooa trasy, a wysyła toohello ruchu sieciowego hello zdefiniowanymi w puli zaplecza. Użycia routingu opartego na adres URL jest tooload równoważenie żądań dla pul serwerów zaplecza toodifferent różne typy zawartości.

Na podstawie adresu URL routingu wprowadza nową bramę tooapplication typ reguły. Brama aplikacji ma dwa typy zasad: podstawowe i PathBasedRouting. Typu podstawowe reguły stanowi usługa okrężnego dla zaplecza hello pul podczas PathBasedRouting dodatkowo dystrybucji działania okrężnego tooround, uwzględnia również wzorzec ścieżki adresu URL żądania hello podczas wybierania hello puli zaplecza.

## <a name="scenario"></a>Scenariusz

W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com z dwóch pul serwerów zaplecza: domyślna pula serwera i puli serwerów obrazu.

Żądania dla http://contoso.com/image * są kierowane do puli serwerów tooimage (imagesBackendPool), jeśli hello wzorzec ścieżki nie jest zgodny, domyślna pula serwera (appGatewayBackendPool) jest zaznaczone.

![trasy adresu URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Otwórz hello **wiersza polecenia usługi Microsoft Azure**i zaloguj się. 

```azurecli
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

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Dodaj istniejącą bramę aplikacji na podstawie ścieżki reguły tooan

Utwórz bramę aplikacji z reguły ścieżki zdefiniowane

### <a name="create-a-new-back-end-pool"></a>Utwórz nową pulę zaplecza

Skonfiguruj ustawienia bramy aplikacji **imagesBackendPool** hello równoważeniem obciążenia ruchu sieciowego w puli zaplecza hello. W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza dla nowej puli zaplecza hello. Każda pula zaplecza może mieć własne ustawienia puli zaplecza.  Ustawienia HTTP zaplecza są używane przez członków puli zaplecza poprawne toohello reguły tooroute ruchu. Określa hello protokół i port, który jest używany podczas wysyłania ruchu członków puli zaplecza toohello. Ustawienia HTTP zaplecza hello również ustala oparte na pliku cookie sesji.  U możliwia koligacji na podstawie plików cookie sesji wysyła toohello ruch tego samego wewnętrznej bazy danych jako poprzedniego żądania dla każdego pakietu.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Utwórz nowy port frontonu

Skonfiguruj hello portów frontonu bramy aplikacji. obiekt konfiguracji portów frontonu Hello jest używany przez toodefine odbiornika, port bramy aplikacji hello nasłuchuje ruchu na powitania odbiornika.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Utwórz nowy

Skonfiguruj odbiornik hello. Ten krok obejmuje skonfigurowanie odbiornika hello hello publicznego adresu IP i port używany tooreceive przychodzącego ruchu sieciowego. Poniższy przykład Hello przyjmuje konfiguracji IP frontonu hello wcześniej skonfigurowane, Konfiguracja portów frontonu i protokołu (http lub https) i konfiguruje hello odbiornika. W tym przykładzie odbiornika hello nasłuchuje tooHTTP ruch na porcie 82 hello publiczny adres IP, który został utworzony wcześniej.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Tworzenie mapy ścieżki adresu Url hello

Konfiguruj adres URL reguły ścieżki dla pul zaplecza hello. Ten krok umożliwia skonfigurowanie ścieżki względnej hello używany przez aplikację bramy toodefine hello mapowanie między ścieżki adresu URL, które puli zaplecza przypisano toohandle hello przychodzący ruch.

> [!IMPORTANT]
> Każda ścieżka musi rozpoczynać się od / i miejsce tylko hello "\*" jest dozwolone, znajduje się na końcu hello. Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *. Hello ciąg przekazywani toohello dopasowania ścieżki nie zawiera żadnego tekstu po hello najpierw "?" lub "#", a te znaki są niedozwolone. 

Witaj poniższy przykład tworzy jedną regułę "/ obrazów / *" ścieżkę routingu ruchu tooback-end "imagesBackendPool." Ta reguła zapewnia, że ruchu dla każdego zestawu adresów URL jest kierowany toohello wewnętrznej bazy danych. Na przykład http://adatum.com/images/figure1.jpg prowadzi zbyt "imagesBackendPool." Jeśli ścieżka hello nie odpowiada żadnemu z reguły ścieżki wstępnie zdefiniowane hello, hello reguły ścieżki mapy konfiguracji konfiguruje również domyślna pula adresów zaplecza. Na przykład http://adatum.com/shoppingcart/test.html przechodzi toopool1 określone jako hello domyślnej puli niedopasowane ruchu.

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

Jeśli chcesz toolearn o odciążania protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
