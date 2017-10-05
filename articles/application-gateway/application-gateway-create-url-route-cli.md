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
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="6113e-103">Utwórz bramę aplikacji przy użyciu routingu opartego na ścieżkę 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6113e-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6113e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6113e-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="6113e-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="6113e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="6113e-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6113e-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="6113e-107">Na podstawie ścieżki routingu adresów URL umożliwia powiązanie tras na podstawie ścieżki adresu URL żądania Http.</span><span class="sxs-lookup"><span data-stu-id="6113e-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="6113e-108">Sprawdza, czy istnieje trasa do puli zaplecza skonfigurowane dla adresu URL, w bramie aplikacji, a wysyła ruchu sieciowego do określonych puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="6113e-109">Użycia routingu opartego na adres URL jest w celu zrównoważenia obciążenia żądaniami dla różnych typów zawartości do innego serwera zaplecza pul.</span><span class="sxs-lookup"><span data-stu-id="6113e-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="6113e-110">Routingu opartego na adres URL został wprowadzony nowy typ reguły na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6113e-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="6113e-111">Brama aplikacji ma dwa typy zasad: podstawowe i PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="6113e-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="6113e-112">Podstawowe reguły typu udostępnia usługę okrężnego dla pul zaplecza podczas PathBasedRouting oprócz dystrybucji działanie okrężne, uwzględnia również wzorzec ścieżki adresu URL żądania podczas wybierania puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-112">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="6113e-113">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="6113e-113">Scenario</span></span>

<span data-ttu-id="6113e-114">W poniższym przykładzie brama aplikacji jest obsługę ruchu dla domeny contoso.com z dwóch pul serwerów zaplecza: domyślna pula serwera i puli serwerów obrazu.</span><span class="sxs-lookup"><span data-stu-id="6113e-114">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="6113e-115">Żądania dla http://contoso.com/image * są kierowane do puli serwerów obrazu (imagesBackendPool), czy wzorzec ścieżki nie jest zgodny, domyślna pula serwera (appGatewayBackendPool) jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="6113e-115">Requests for http://contoso.com/image* are routed to image server pool (imagesBackendPool), if the path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![trasy adresu URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="6113e-117">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6113e-117">Log in to Azure</span></span>

<span data-ttu-id="6113e-118">Otwórz **wiersza polecenia usługi Microsoft Azure**i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="6113e-118">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="6113e-119">Można również użyć `az login` bez przełącznika dla nazwy logowania urządzenia, która wymaga wprowadzenie kodu na aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="6113e-119">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="6113e-120">Po wpisaniu powyższego przykładu znajduje się kod.</span><span class="sxs-lookup"><span data-stu-id="6113e-120">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="6113e-121">Przejdź do https://aka.ms/devicelogin w przeglądarce, aby kontynuować proces logowania.</span><span class="sxs-lookup"><span data-stu-id="6113e-121">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd przedstawiający urządzenia logowania][1]

<span data-ttu-id="6113e-123">W przeglądarce wprowadź otrzymany kod.</span><span class="sxs-lookup"><span data-stu-id="6113e-123">In the browser, enter the code you received.</span></span> <span data-ttu-id="6113e-124">Nastąpi przekierowanie do strony logowania.</span><span class="sxs-lookup"><span data-stu-id="6113e-124">You are redirected to a sign-in page.</span></span>

![przeglądarki, aby wprowadzić kod][2]

<span data-ttu-id="6113e-126">Po wprowadzeniu kodu użytkownik jest zalogowany, zamknij przeglądarkę, aby kontynuować na ze scenariuszem.</span><span class="sxs-lookup"><span data-stu-id="6113e-126">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![pomyślnie zalogował się][3]

## <a name="add-a-path-based-rule-to-an-existing-application-gateway"></a><span data-ttu-id="6113e-128">Dodawanie reguły na podstawie ścieżki do istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="6113e-128">Add a path-based rule to an existing application gateway</span></span>

<span data-ttu-id="6113e-129">Utwórz bramę aplikacji z reguły ścieżki zdefiniowane</span><span class="sxs-lookup"><span data-stu-id="6113e-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="6113e-130">Utwórz nową pulę zaplecza</span><span class="sxs-lookup"><span data-stu-id="6113e-130">Create a new back-end pool</span></span>

<span data-ttu-id="6113e-131">Skonfiguruj ustawienia bramy aplikacji **imagesBackendPool** dla ruchu sieciowego z równoważeniem obciążenia w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-131">Configure application gateway setting **imagesBackendPool** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="6113e-132">W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza nowej puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-132">In this example, you configure different back-end pool settings for the new back-end pool.</span></span> <span data-ttu-id="6113e-133">Każda pula zaplecza może mieć własne ustawienia puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="6113e-134">Ustawienia HTTP zaplecza są używane przez reguły do kierowania ruchu do właściwych elementów członkowskich puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-134">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="6113e-135">Określa protokół i port, który jest używany podczas wysyłania ruchu do elementów członkowskich puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6113e-135">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="6113e-136">Sesje bazujące na plikach cookie są też określane przez ustawienia HTTP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-136">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="6113e-137">Jeśli koligacja sesji bazujących na plikach cookie jest włączona, wysyła ruch do tego samego zaplecza co poprzednie żądania dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="6113e-137">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="6113e-138">Utwórz nowy port frontonu</span><span class="sxs-lookup"><span data-stu-id="6113e-138">Create a new front-end port</span></span>

<span data-ttu-id="6113e-139">Skonfiguruj port frontonu dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6113e-139">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="6113e-140">Obiekt konfiguracji portu frontonu jest używany przez odbiornik do definiowania, który port usługi Application Gateway nasłuchuje ruchu na odbiorniku.</span><span class="sxs-lookup"><span data-stu-id="6113e-140">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="6113e-141">Utwórz nowy</span><span class="sxs-lookup"><span data-stu-id="6113e-141">Create a new listener</span></span>

<span data-ttu-id="6113e-142">Skonfiguruj odbiornik.</span><span class="sxs-lookup"><span data-stu-id="6113e-142">Configure the listener.</span></span> <span data-ttu-id="6113e-143">W tym kroku dla odbiornika konfigurowany jest publiczny adres IP i port używane do odbierania przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6113e-143">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="6113e-144">W poniższym przykładzie przyjmuje wcześniej skonfigurowane konfiguracji IP frontonu, Konfiguracja portów frontonu i protokołu (http lub https) i konfiguruje odbiornika.</span><span class="sxs-lookup"><span data-stu-id="6113e-144">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="6113e-145">W tym przykładzie odbiornika nasłuchuje ruchu HTTP na porcie 82 publicznego adresu IP, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6113e-145">In this example, the listener listens to HTTP traffic on port 82 on the public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-the-url-path-map"></a><span data-ttu-id="6113e-146">Tworzenie mapy ścieżki adresu Url</span><span class="sxs-lookup"><span data-stu-id="6113e-146">Create the Url path map</span></span>

<span data-ttu-id="6113e-147">Konfiguruj adres URL reguły ścieżki dla pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-147">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="6113e-148">Ten krok umożliwia skonfigurowanie ścieżki względnej, używany przez bramę aplikacji, aby określić mapowanie między ścieżki adresu URL i puli zaplecza, które są przypisane do obsługi ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6113e-148">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6113e-149">Każda ścieżka musi rozpoczynać się od / i miejsce tylko "\*" jest dozwolone, jest na końcu.</span><span class="sxs-lookup"><span data-stu-id="6113e-149">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="6113e-150">Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="6113e-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="6113e-151">Ciąg przekazywani do dopasowania ścieżki nie zawiera żadnego tekstu po pierwszym "?" lub "#", a te znaki są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="6113e-151">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="6113e-152">Poniższy przykład tworzy jedną regułę "/ obrazów / *" ścieżkę routingu ruchu do wewnętrznej "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="6113e-152">The following example creates one rule for "/images/*" path routing traffic to back-end "imagesBackendPool."</span></span> <span data-ttu-id="6113e-153">Ta reguła zapewnia, że ruch dla każdego zestawu adresów URL jest kierowany do wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6113e-153">This rule ensures that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="6113e-154">Na przykład http://adatum.com/images/figure1.jpg przechodzi do "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="6113e-154">For example, http://adatum.com/images/figure1.jpg goes to "imagesBackendPool."</span></span> <span data-ttu-id="6113e-155">Jeśli ścieżka nie odpowiada żadnemu z reguły ścieżki wstępnie zdefiniowane, Konfiguracja mapowania ścieżki reguły konfiguruje również domyślna pula adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6113e-155">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="6113e-156">Na przykład http://adatum.com/shoppingcart/test.html prowadzi do pool1 określone jako domyślna pula niedopasowane ruchu.</span><span class="sxs-lookup"><span data-stu-id="6113e-156">For example, http://adatum.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6113e-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6113e-157">Next steps</span></span>

<span data-ttu-id="6113e-158">Jeśli chcesz dowiedzieć się więcej o odciążania protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6113e-158">If you want to learn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
