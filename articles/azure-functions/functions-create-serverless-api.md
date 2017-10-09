---
title: "Interfejs API niekorzystającą przy użyciu usługi Azure Functions aaaCreate | Dokumentacja firmy Microsoft"
description: "Jak toocreate interfejs API niekorzystającą przy użyciu usługi Azure Functions"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="ba2ec-103">Utwórz interfejs API niekorzystającą przy użyciu usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ba2ec-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="ba2ec-104">W tym samouczku dowiesz się, jak usługi Azure Functions umożliwia toobuild wysoce skalowalna interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="ba2ec-105">Środowisko Azure Functions jest dostarczany z kolekcji wbudowanych HTTP wyzwalaczy i powiązań, które pozwalają łatwo tooauthor punkt końcowy w różnych językach, łącznie z Node.JS, C# i inne.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="ba2ec-106">W tym samouczku zostanie Dostosowywanie toohandle wyzwalacza HTTP dla akcji określonych w projekcie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="ba2ec-107">Należy również przygotować do powiększania interfejsu API integrowanie go z serwerów proxy funkcji platformy Azure i konfigurowanie zasymulować interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="ba2ec-108">Wszystko to odbywa się na górze hello funkcje niekorzystającą obliczeniowe środowiska, dlatego nie masz tooworry temat skalowania zasobów — wystarczy można skoncentrować się na logice interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba2ec-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ba2ec-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="ba2ec-110">Wynikowa funkcja Hello będzie służyć do hello pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="ba2ec-111">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="ba2ec-111">Sign in tooAzure</span></span>

<span data-ttu-id="ba2ec-112">Otwórz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-112">Open hello Azure portal.</span></span> <span data-ttu-id="ba2ec-113">toodo, zaloguj się za[https://portal.azure.com](https://portal.azure.com) z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="ba2ec-114">Dostosowywanie funkcji HTTP</span><span class="sxs-lookup"><span data-stu-id="ba2ec-114">Customize your HTTP function</span></span>

<span data-ttu-id="ba2ec-115">Domyślnie funkcji wyzwalanych przez protokół HTTP jest skonfigurowany tooaccept dowolnej metody HTTP.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="ba2ec-116">Jest również domyślny adres URL w postaci hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="ba2ec-117">Po wykonaniu hello Szybki Start, następnie `<funcname>` prawdopodobnie wygląda "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="ba2ec-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="ba2ec-118">W tej sekcji należy zmodyfikować hello funkcja toorespond tooGET tylko żądania kierowane do `/api/hello` zamiast tego trasy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="ba2ec-119">Przejdź w portalu Azure hello funkcji tooyour.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="ba2ec-120">Wybierz **integracji** w hello lewy pasek nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-120">Select **Integrate** in hello left navigation.</span></span>

![Dostosowywanie funkcji HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="ba2ec-122">Użyj ustawień wyzwalacza HTTP określoną w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="ba2ec-123">Pole</span><span class="sxs-lookup"><span data-stu-id="ba2ec-123">Field</span></span> | <span data-ttu-id="ba2ec-124">Wartość przykładowa</span><span class="sxs-lookup"><span data-stu-id="ba2ec-124">Sample value</span></span> | <span data-ttu-id="ba2ec-125">Opis</span><span class="sxs-lookup"><span data-stu-id="ba2ec-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="ba2ec-126">Dopuszczalnych metod HTTP</span><span class="sxs-lookup"><span data-stu-id="ba2ec-126">Allowed HTTP methods</span></span> | <span data-ttu-id="ba2ec-127">Wybrane metody zostaną usunięte</span><span class="sxs-lookup"><span data-stu-id="ba2ec-127">Selected methods</span></span> | <span data-ttu-id="ba2ec-128">Określa, jakie metody HTTP mogą być używane tooinvoke tej funkcji</span><span class="sxs-lookup"><span data-stu-id="ba2ec-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="ba2ec-129">Wybrane metody HTTP</span><span class="sxs-lookup"><span data-stu-id="ba2ec-129">Selected HTTP methods</span></span> | <span data-ttu-id="ba2ec-130">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="ba2ec-130">GET</span></span> | <span data-ttu-id="ba2ec-131">Umożliwia tylko wybrane toobe metod HTTP użytej tooinvoke tej funkcji</span><span class="sxs-lookup"><span data-stu-id="ba2ec-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="ba2ec-132">Szablon trasy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-132">Route template</span></span> | <span data-ttu-id="ba2ec-133">człon</span><span class="sxs-lookup"><span data-stu-id="ba2ec-133">/hello</span></span> | <span data-ttu-id="ba2ec-134">Określa, jakie trasy jest używane tooinvoke tej funkcji</span><span class="sxs-lookup"><span data-stu-id="ba2ec-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="ba2ec-135">Należy pamiętać, że nie zawiera hello `/api` podstawowa prefiks ścieżki w szablonie trasy hello, ponieważ jest to obsługiwane przez ustawienie globalne.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="ba2ec-136">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-136">Click **Save**.</span></span>

<span data-ttu-id="ba2ec-137">Dowiedz się więcej o dostosowywaniu funkcji HTTP w [powiązania HTTP funkcje platformy Azure i webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="ba2ec-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="ba2ec-138">Testowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ba2ec-138">Test your API</span></span>

<span data-ttu-id="ba2ec-139">Następnie przetestować toosee Twojego funkcja Praca z hello nowych powierzchni interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="ba2ec-140">Przejdź wstecz toohello programowanie strony, klikając nazwę funkcji hello na powitania lewy pasek nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="ba2ec-141">Kliknij przycisk **uzyskać adres URL funkcji** i skopiuj adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="ba2ec-142">Powinny pojawić się korzysta z hello `/api/hello` teraz trasy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="ba2ec-143">Kopiuj adres URL hello na nowej karcie przeglądarki lub preferowanego klienta REST.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="ba2ec-144">Przeglądarki użyje GET domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="ba2ec-145">Uruchamianie funkcji hello i upewnij się, że działa.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="ba2ec-146">Parametr "Nazwa" hello tooprovide może być konieczne jako kodu szybkiego startu hello toosatisfy ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="ba2ec-147">Można też spróbować wywołaniem punktu końcowego hello z innej tooconfirm — metoda HTTP hello funkcja nie została wykonana.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="ba2ec-148">W tym celu należy toouse klienta REST, takie jak cURL, Postman lub Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="ba2ec-149">Omówienie serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-149">Proxies overview</span></span>

<span data-ttu-id="ba2ec-150">W następnej sekcji hello będzie powierzchni interfejsu API za pośrednictwem serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="ba2ec-151">Azure funkcje serwera proxy jest funkcja w wersji zapoznawczej, umożliwiający tooforward żądań tooother zasobów.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="ba2ec-152">Tak jak zdefiniować punkt końcowy HTTP z wyzwalaczem HTTP, ale zamiast zapisywania tooexecute kodu, gdy jest wywoływana tego punktu końcowego, należy udostępnić implementację zdalnego tooa adresu URL.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="ba2ec-153">Dzięki temu toocompose API wielu źródeł w jednym powierzchni interfejsu API, który ułatwia tooconsume klientów.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="ba2ec-154">Jest to szczególnie przydatne, jeśli chcesz toobuild interfejsu API jako mikrousług.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="ba2ec-155">Serwer proxy może wskazywać tooany HTTP zasobów, takich jak:</span><span class="sxs-lookup"><span data-stu-id="ba2ec-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="ba2ec-156">Stan usługi Funkcje Azure</span><span class="sxs-lookup"><span data-stu-id="ba2ec-156">Azure Functions</span></span> 
- <span data-ttu-id="ba2ec-157">Aplikacje interfejsu API w [usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="ba2ec-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="ba2ec-158">Kontenery docker w [usługi aplikacji w systemie Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="ba2ec-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="ba2ec-159">Inne obsługiwane interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ba2ec-159">Any other hosted API</span></span>

<span data-ttu-id="ba2ec-160">toolearn więcej informacji na temat serwerów proxy, zobacz [Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)].</span><span class="sxs-lookup"><span data-stu-id="ba2ec-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="ba2ec-161">Tworzenie pierwszego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-161">Create your first proxy</span></span>

<span data-ttu-id="ba2ec-162">W tej sekcji utworzysz nowe proxy który służy jako tooyour frontonu ogólnego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="ba2ec-163">Konfigurowanie środowiska frontonu hello</span><span class="sxs-lookup"><span data-stu-id="ba2ec-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="ba2ec-164">Powtórz kroki od hello zbyt[tworzenia aplikacji funkcji](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate nową aplikację funkcji w co spowoduje utworzenie serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="ba2ec-165">Ta nowa aplikacja będzie służyć jako frontonu hello na interfejsie API i hello funkcji aplikacji, które zostały wcześniej edycji będzie służyć jako wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="ba2ec-166">Przejdź tooyour nowego serwera sieci Web funkcji aplikacji w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="ba2ec-167">Wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-167">Select **Settings**.</span></span> <span data-ttu-id="ba2ec-168">Następnie przełącz **włączyć proxy funkcji Azure (wersja zapoznawcza)** zbyt "na".</span><span class="sxs-lookup"><span data-stu-id="ba2ec-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="ba2ec-169">Wybierz **ustawienia platformy** i wybierz polecenie **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="ba2ec-170">Przewiń w dół za**ustawień aplikacji** i utworzyć nowe ustawienie z kluczem "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="ba2ec-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="ba2ec-171">Ustaw jej wartość host toohello aplikacji funkcji wewnętrznej bazy danych, takich jak `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="ba2ec-172">Jest to część adresu URL hello, które wcześniej zostały skopiowane podczas testowania funkcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="ba2ec-173">To ustawienie w konfiguracji hello później będziesz odwoływać.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="ba2ec-174">Ustawienia aplikacji są zalecane w przypadku tooprevent konfiguracji hosta hello zależność ustalony środowiska powitania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="ba2ec-175">Przy użyciu ustawień aplikacji oznacza, że konfiguracja serwera proxy hello można przenosić między środowiskami i zostaną zastosowane ustawienia specyficzne dla środowiska aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="ba2ec-176">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="ba2ec-177">Tworzenie serwera proxy na powitania serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="ba2ec-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="ba2ec-178">Przejdź wstecz tooyour frontonu funkcji aplikacji w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="ba2ec-179">W nawigacji po lewej stronie powitania, kliknij zbyt hello oraz znak "+" dalej "Serwery proxy (wersja zapoznawcza)".</span><span class="sxs-lookup"><span data-stu-id="ba2ec-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Tworzenie serwera proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="ba2ec-181">Użyj ustawień serwera proxy, jak określono w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="ba2ec-182">Pole</span><span class="sxs-lookup"><span data-stu-id="ba2ec-182">Field</span></span> | <span data-ttu-id="ba2ec-183">Wartość przykładowa</span><span class="sxs-lookup"><span data-stu-id="ba2ec-183">Sample value</span></span> | <span data-ttu-id="ba2ec-184">Opis</span><span class="sxs-lookup"><span data-stu-id="ba2ec-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="ba2ec-185">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ba2ec-185">Name</span></span> | <span data-ttu-id="ba2ec-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-186">HelloProxy</span></span> | <span data-ttu-id="ba2ec-187">Przyjazna nazwa używana tylko w przypadku zarządzania</span><span class="sxs-lookup"><span data-stu-id="ba2ec-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="ba2ec-188">Szablon trasy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-188">Route template</span></span> | <span data-ttu-id="ba2ec-189">/ api/hello</span><span class="sxs-lookup"><span data-stu-id="ba2ec-189">/api/hello</span></span> | <span data-ttu-id="ba2ec-190">Określa, jakie trasy jest używane tooinvoke ten serwer proxy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="ba2ec-191">Adres URL wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="ba2ec-191">Backend URL</span></span> | <span data-ttu-id="ba2ec-192">https://%HELLO_HOST%/API/Hello</span><span class="sxs-lookup"><span data-stu-id="ba2ec-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="ba2ec-193">Określa, że żądania hello toowhich punktu końcowego hello powinien być serwerem proxy</span><span class="sxs-lookup"><span data-stu-id="ba2ec-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="ba2ec-194">Należy pamiętać, że serwery proxy nie hello `/api` prefiks ścieżki podstawowej i ten musi być zawarte w szablonie trasy hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="ba2ec-195">Witaj `%HELLO_HOST%` składni będzie odwoływać się do ustawienia aplikacji hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="ba2ec-196">Witaj rozpoznać adres URL będzie wskazywać tooyour pierwotnej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="ba2ec-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-197">Click **Create**.</span></span>

<span data-ttu-id="ba2ec-198">Można wypróbować nowego serwera proxy, kopiując hello adres URL serwera Proxy i testowanie go w przeglądarce hello lub z ulubionych klienta HTTP.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="ba2ec-199">Utwórz zasymulować interfejs API</span><span class="sxs-lookup"><span data-stu-id="ba2ec-199">Create a mock API</span></span>

<span data-ttu-id="ba2ec-200">Następnie użyje toocreate proxy zasymulować interfejsu API dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="ba2ec-201">Dzięki temu programowanie klienta tooprogress, bez konieczności hello wewnętrznej bazy danych, w pełni wdrożone.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="ba2ec-202">Później w rozwoju należy utworzyć nową aplikację funkcji, która obsługuje tę logikę i przekierować tooit Twojego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="ba2ec-203">toocreate to mock interfejsu API, utworzymy nowe proxy przy użyciu hello [Edytor usług aplikacji](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="ba2ec-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="ba2ec-204">tooget pracę, przejdź tooyour funkcji aplikacji w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="ba2ec-205">Wybierz **funkcji platformy** i Znajdź **Edytor usług aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="ba2ec-206">Kliknięcie łącza zostanie otwarty Edytor usług aplikacji hello na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="ba2ec-207">Wybierz `proxies.json` w hello lewy pasek nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="ba2ec-208">To jest plik hello, którym przechowywana jest Konfiguracja hello wszystkie Twoje serwery proxy.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="ba2ec-209">Jeśli używany jest jeden hello [metody wdrażania funkcji](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), to jest plik hello mają być przechowywane w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="ba2ec-210">toolearn więcej informacji na temat tego pliku, zobacz [proxy Zaawansowana konfiguracja](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="ba2ec-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="ba2ec-211">Jeśli po wykonaniu wykonanej do tej pory, proxies.json Twojego powinna wyglądać hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="ba2ec-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="ba2ec-212">Następnie dodasz zasymulować interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-212">Next you'll add your mock API.</span></span> <span data-ttu-id="ba2ec-213">Zastąp plik proxies.json hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ba2ec-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="ba2ec-214">Spowoduje to dodanie nowego serwera proxy, "GetUserByName" bez hello backendUri właściwości.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="ba2ec-215">Zamiast kontaktować się z innym zasobem, modyfikuje hello domyślne odpowiedzi z serwerów proxy przy użyciu zastąpienia odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="ba2ec-216">Można także zastąpienia żądań i odpowiedzi w połączeniu z adresem URL wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="ba2ec-217">Jest to szczególnie przydatne, gdy pośredniczenie tooa starszej wersji systemu, gdzie może być konieczne toomodify nagłówków, parametry zapytania, toolearn itp. więcej informacji na temat zastąpienia żądań i odpowiedzi, zobacz [modyfikowanie żądań i odpowiedzi w proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="ba2ec-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="ba2ec-218">Test zasymulować interfejsu API przez wywołanie hello `/api/users/{username}` punktu końcowego za pomocą przeglądarki lub Twoje ulubione klienta REST.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="ba2ec-219">Należy się tooreplace _{username}_ z wartością ciągu reprezentujący nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba2ec-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba2ec-220">Next steps</span></span>

<span data-ttu-id="ba2ec-221">W tym samouczku można przedstawiono sposób toobuild i Dostosuj interfejs API na usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="ba2ec-222">Również wiesz, jak toobring wiele interfejsów API, w tym mocks, jednocześnie jako ujednoliconego powierzchni interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="ba2ec-223">Można użyć tych toobuild techniki limit interfejsów API żadnych złożoności, wszystkie podczas uruchamiania na powitania niekorzystającą obliczeniowe udostępniane przez usługi Azure Functions modelu.</span><span class="sxs-lookup"><span data-stu-id="ba2ec-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="ba2ec-224">Witaj następujące informacje mogą być pomocne podczas opracowywania dalsze interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="ba2ec-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="ba2ec-225">Azure powiązania HTTP funkcje i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="ba2ec-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="ba2ec-226">[Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]</span><span class="sxs-lookup"><span data-stu-id="ba2ec-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="ba2ec-227">Dokumentowanie funkcje interfejsu API Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="ba2ec-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
