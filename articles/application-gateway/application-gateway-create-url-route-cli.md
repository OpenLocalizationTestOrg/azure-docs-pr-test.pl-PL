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
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="5b60b-103">Utwórz bramę aplikacji przy użyciu routingu opartego na ścieżkę 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5b60b-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b60b-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b60b-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="5b60b-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b60b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="5b60b-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5b60b-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="5b60b-107">Na podstawie ścieżki routingu adresów URL umożliwia możesz tooassociate tras na podstawie hello ścieżki adresu URL żądania Http.</span><span class="sxs-lookup"><span data-stu-id="5b60b-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="5b60b-108">Sprawdza, czy jest skonfigurowane dla adresu URL hello przedstawionych w hello brama aplikacji w puli zaplecza tooa trasy, a wysyła toohello ruchu sieciowego hello zdefiniowanymi w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5b60b-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="5b60b-109">Użycia routingu opartego na adres URL jest tooload równoważenie żądań dla pul serwerów zaplecza toodifferent różne typy zawartości.</span><span class="sxs-lookup"><span data-stu-id="5b60b-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="5b60b-110">Na podstawie adresu URL routingu wprowadza nową bramę tooapplication typ reguły.</span><span class="sxs-lookup"><span data-stu-id="5b60b-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="5b60b-111">Brama aplikacji ma dwa typy zasad: podstawowe i PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="5b60b-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="5b60b-112">Typu podstawowe reguły stanowi usługa okrężnego dla zaplecza hello pul podczas PathBasedRouting dodatkowo dystrybucji działania okrężnego tooround, uwzględnia również wzorzec ścieżki adresu URL żądania hello podczas wybierania hello puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5b60b-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="5b60b-113">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="5b60b-113">Scenario</span></span>

<span data-ttu-id="5b60b-114">W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com z dwóch pul serwerów zaplecza: domyślna pula serwera i puli serwerów obrazu.</span><span class="sxs-lookup"><span data-stu-id="5b60b-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="5b60b-115">Żądania dla http://contoso.com/image * są kierowane do puli serwerów tooimage (imagesBackendPool), jeśli hello wzorzec ścieżki nie jest zgodny, domyślna pula serwera (appGatewayBackendPool) jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="5b60b-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![trasy adresu URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="5b60b-117">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="5b60b-117">Log in tooAzure</span></span>

<span data-ttu-id="5b60b-118">Otwórz hello **wiersza polecenia usługi Microsoft Azure**i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="5b60b-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="5b60b-119">Można również użyć `az login` bez hello przełącznika dla nazwy logowania urządzenia, która wymaga wprowadzenie kodu na aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="5b60b-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="5b60b-120">Po wpisaniu hello poprzedzających przykład znajduje się kod.</span><span class="sxs-lookup"><span data-stu-id="5b60b-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="5b60b-121">Przejdź toohttps://aka.ms/devicelogin w procesie logowania hello toocontinue przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="5b60b-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd przedstawiający urządzenia logowania][1]

<span data-ttu-id="5b60b-123">W przeglądarce hello wprowadź otrzymany kod hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="5b60b-124">Jesteś tooa przekierowanego strony logowania.</span><span class="sxs-lookup"><span data-stu-id="5b60b-124">You are redirected tooa sign-in page.</span></span>

![Kod tooenter przeglądarki][2]

<span data-ttu-id="5b60b-126">Po wprowadzeniu kodu hello użytkownik jest zalogowany, zamknij hello toocontinue przeglądarki ze scenariuszem hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![pomyślnie zalogował się][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="5b60b-128">Dodaj istniejącą bramę aplikacji na podstawie ścieżki reguły tooan</span><span class="sxs-lookup"><span data-stu-id="5b60b-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="5b60b-129">Utwórz bramę aplikacji z reguły ścieżki zdefiniowane</span><span class="sxs-lookup"><span data-stu-id="5b60b-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="5b60b-130">Utwórz nową pulę zaplecza</span><span class="sxs-lookup"><span data-stu-id="5b60b-130">Create a new back-end pool</span></span>

<span data-ttu-id="5b60b-131">Skonfiguruj ustawienia bramy aplikacji **imagesBackendPool** hello równoważeniem obciążenia ruchu sieciowego w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="5b60b-132">W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza dla nowej puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="5b60b-133">Każda pula zaplecza może mieć własne ustawienia puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5b60b-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="5b60b-134">Ustawienia HTTP zaplecza są używane przez członków puli zaplecza poprawne toohello reguły tooroute ruchu.</span><span class="sxs-lookup"><span data-stu-id="5b60b-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="5b60b-135">Określa hello protokół i port, który jest używany podczas wysyłania ruchu członków puli zaplecza toohello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="5b60b-136">Ustawienia HTTP zaplecza hello również ustala oparte na pliku cookie sesji.</span><span class="sxs-lookup"><span data-stu-id="5b60b-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="5b60b-137">U możliwia koligacji na podstawie plików cookie sesji wysyła toohello ruch tego samego wewnętrznej bazy danych jako poprzedniego żądania dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="5b60b-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="5b60b-138">Utwórz nowy port frontonu</span><span class="sxs-lookup"><span data-stu-id="5b60b-138">Create a new front-end port</span></span>

<span data-ttu-id="5b60b-139">Skonfiguruj hello portów frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b60b-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="5b60b-140">obiekt konfiguracji portów frontonu Hello jest używany przez toodefine odbiornika, port bramy aplikacji hello nasłuchuje ruchu na powitania odbiornika.</span><span class="sxs-lookup"><span data-stu-id="5b60b-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="5b60b-141">Utwórz nowy</span><span class="sxs-lookup"><span data-stu-id="5b60b-141">Create a new listener</span></span>

<span data-ttu-id="5b60b-142">Skonfiguruj odbiornik hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-142">Configure hello listener.</span></span> <span data-ttu-id="5b60b-143">Ten krok obejmuje skonfigurowanie odbiornika hello hello publicznego adresu IP i port używany tooreceive przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5b60b-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="5b60b-144">Poniższy przykład Hello przyjmuje konfiguracji IP frontonu hello wcześniej skonfigurowane, Konfiguracja portów frontonu i protokołu (http lub https) i konfiguruje hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="5b60b-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="5b60b-145">W tym przykładzie odbiornika hello nasłuchuje tooHTTP ruch na porcie 82 hello publiczny adres IP, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5b60b-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="5b60b-146">Tworzenie mapy ścieżki adresu Url hello</span><span class="sxs-lookup"><span data-stu-id="5b60b-146">Create hello Url path map</span></span>

<span data-ttu-id="5b60b-147">Konfiguruj adres URL reguły ścieżki dla pul zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="5b60b-148">Ten krok umożliwia skonfigurowanie ścieżki względnej hello używany przez aplikację bramy toodefine hello mapowanie między ścieżki adresu URL, które puli zaplecza przypisano toohandle hello przychodzący ruch.</span><span class="sxs-lookup"><span data-stu-id="5b60b-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b60b-149">Każda ścieżka musi rozpoczynać się od / i miejsce tylko hello "\*" jest dozwolone, znajduje się na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="5b60b-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="5b60b-150">Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="5b60b-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="5b60b-151">Hello ciąg przekazywani toohello dopasowania ścieżki nie zawiera żadnego tekstu po hello najpierw "?" lub "#", a te znaki są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="5b60b-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="5b60b-152">Witaj poniższy przykład tworzy jedną regułę "/ obrazów / *" ścieżkę routingu ruchu tooback-end "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="5b60b-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="5b60b-153">Ta reguła zapewnia, że ruchu dla każdego zestawu adresów URL jest kierowany toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5b60b-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="5b60b-154">Na przykład http://adatum.com/images/figure1.jpg prowadzi zbyt "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="5b60b-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="5b60b-155">Jeśli ścieżka hello nie odpowiada żadnemu z reguły ścieżki wstępnie zdefiniowane hello, hello reguły ścieżki mapy konfiguracji konfiguruje również domyślna pula adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5b60b-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="5b60b-156">Na przykład http://adatum.com/shoppingcart/test.html przechodzi toopool1 określone jako hello domyślnej puli niedopasowane ruchu.</span><span class="sxs-lookup"><span data-stu-id="5b60b-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5b60b-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b60b-157">Next steps</span></span>

<span data-ttu-id="5b60b-158">Jeśli chcesz toolearn o odciążania protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5b60b-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
