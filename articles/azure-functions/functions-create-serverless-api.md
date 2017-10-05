---
title: "Utwórz interfejs API niekorzystającą przy użyciu usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Jak utworzyć interfejs API niekorzystającą przy użyciu usługi Azure Functions"
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="fba63-103">Utwórz interfejs API niekorzystającą przy użyciu usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fba63-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="fba63-104">W tym samouczku dowiesz się, jak usługi Azure Functions umożliwia tworzenie wysoce skalowalna interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="fba63-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="fba63-105">Środowisko Azure Functions jest dostarczany z kolekcji wbudowanych HTTP wyzwalaczy i powiązań, które ułatwiają tworzenie punktu końcowego w różnych językach, łącznie z Node.JS, C# i inne.</span><span class="sxs-lookup"><span data-stu-id="fba63-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="fba63-106">W tym samouczku będzie dostosować wyzwalacz protokołu HTTP do obsługi określonych akcji w projekcie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fba63-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="fba63-107">Należy również przygotować do powiększania interfejsu API integrowanie go z serwerów proxy funkcji platformy Azure i konfigurowanie zasymulować interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="fba63-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="fba63-108">Wszystko to odbywa się na górze środowiska obliczeniowe bez serwera funkcji, nie trzeba martwić skalowania zasobów — wystarczy można skoncentrować się na logice interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fba63-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fba63-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fba63-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="fba63-110">Funkcja wynikowy będzie służyć do pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="fba63-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="fba63-111">Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fba63-111">Sign in to Azure</span></span>

<span data-ttu-id="fba63-112">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fba63-112">Open the Azure portal.</span></span> <span data-ttu-id="fba63-113">Aby to zrobić, zaloguj się do [https://portal.azure.com](https://portal.azure.com) z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fba63-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="fba63-114">Dostosowywanie funkcji HTTP</span><span class="sxs-lookup"><span data-stu-id="fba63-114">Customize your HTTP function</span></span>

<span data-ttu-id="fba63-115">Domyślnie funkcja wyzwalanych przez protokół HTTP jest skonfigurowany do akceptowania dowolnej metody HTTP.</span><span class="sxs-lookup"><span data-stu-id="fba63-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="fba63-116">Jest również domyślny adres URL w postaci `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="fba63-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="fba63-117">Po wykonaniu procedury szybkiego startu, następnie `<funcname>` prawdopodobnie wygląda "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="fba63-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="fba63-118">W tej sekcji należy zmodyfikować funkcji ma odpowiadać tylko na żądania GET względem `/api/hello` zamiast tego trasy.</span><span class="sxs-lookup"><span data-stu-id="fba63-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="fba63-119">Przejdź do funkcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fba63-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="fba63-120">Wybierz **integracji** na lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="fba63-120">Select **Integrate** in the left navigation.</span></span>

![Dostosowywanie funkcji HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="fba63-122">Użyj ustawień wyzwalacza HTTP określoną w tabeli.</span><span class="sxs-lookup"><span data-stu-id="fba63-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="fba63-123">Pole</span><span class="sxs-lookup"><span data-stu-id="fba63-123">Field</span></span> | <span data-ttu-id="fba63-124">Wartość przykładowa</span><span class="sxs-lookup"><span data-stu-id="fba63-124">Sample value</span></span> | <span data-ttu-id="fba63-125">Opis</span><span class="sxs-lookup"><span data-stu-id="fba63-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="fba63-126">Dopuszczalnych metod HTTP</span><span class="sxs-lookup"><span data-stu-id="fba63-126">Allowed HTTP methods</span></span> | <span data-ttu-id="fba63-127">Wybrane metody zostaną usunięte</span><span class="sxs-lookup"><span data-stu-id="fba63-127">Selected methods</span></span> | <span data-ttu-id="fba63-128">Określa, jakie metody HTTP może służyć do wywołania tej funkcji</span><span class="sxs-lookup"><span data-stu-id="fba63-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="fba63-129">Wybrane metody HTTP</span><span class="sxs-lookup"><span data-stu-id="fba63-129">Selected HTTP methods</span></span> | <span data-ttu-id="fba63-130">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="fba63-130">GET</span></span> | <span data-ttu-id="fba63-131">Umożliwia tylko wybrane metody HTTP używanego do wywołania tej funkcji</span><span class="sxs-lookup"><span data-stu-id="fba63-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="fba63-132">Szablon trasy</span><span class="sxs-lookup"><span data-stu-id="fba63-132">Route template</span></span> | <span data-ttu-id="fba63-133">człon</span><span class="sxs-lookup"><span data-stu-id="fba63-133">/hello</span></span> | <span data-ttu-id="fba63-134">Określa, jakie trasy służy do wywoływania tej funkcji</span><span class="sxs-lookup"><span data-stu-id="fba63-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="fba63-135">Należy pamiętać, że nie zawiera `/api` podstawowa prefiks ścieżki w szablonie trasy, ponieważ jest to obsługiwane przez ustawienie globalne.</span><span class="sxs-lookup"><span data-stu-id="fba63-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="fba63-136">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fba63-136">Click **Save**.</span></span>

<span data-ttu-id="fba63-137">Dowiedz się więcej o dostosowywaniu funkcji HTTP w [powiązania HTTP funkcje platformy Azure i webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fba63-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="fba63-138">Testowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fba63-138">Test your API</span></span>

<span data-ttu-id="fba63-139">Następnie należy przetestować funkcję wyświetlić go do pracy z nowego powierzchni interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fba63-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="fba63-140">Przejdź z powrotem do strony programowanie klikając nazwę funkcji, na lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="fba63-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="fba63-141">Kliknij przycisk **uzyskać adres URL funkcji** i skopiuj adres URL.</span><span class="sxs-lookup"><span data-stu-id="fba63-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="fba63-142">Powinny pojawić się go używa `/api/hello` teraz trasy.</span><span class="sxs-lookup"><span data-stu-id="fba63-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="fba63-143">Skopiuj adres URL do nowej karty przeglądarki lub preferowanego klienta REST.</span><span class="sxs-lookup"><span data-stu-id="fba63-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="fba63-144">Przeglądarki użyje GET domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fba63-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="fba63-145">Uruchom funkcję i upewnij się, że działa.</span><span class="sxs-lookup"><span data-stu-id="fba63-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="fba63-146">Użytkownik może być konieczne podanie parametru "name" jako ciąg zapytania do zaspokojenia kodu Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="fba63-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="fba63-147">Można też spróbować wywoływanie punkt końcowy z innej metody HTTP, aby upewnić się, że funkcja nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fba63-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="fba63-148">W tym celu należy użyć klienta REST, takie jak cURL, Postman lub Fiddler.</span><span class="sxs-lookup"><span data-stu-id="fba63-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="fba63-149">Omówienie serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="fba63-149">Proxies overview</span></span>

<span data-ttu-id="fba63-150">W następnej sekcji zostanie powierzchni interfejsu API za pośrednictwem serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="fba63-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="fba63-151">Azure funkcje serwera proxy jest funkcja w wersji zapoznawczej, który służy do przesyłania żądań do innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="fba63-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="fba63-152">Zdefiniuj punkt końcowy HTTP, podobnie jak wyzwalacza HTTP, ale zamiast pisania kodu do wykonania, gdy jest wywoływana tego punktu końcowego, podaj adres URL do zdalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fba63-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="fba63-153">Umożliwia utworzenie wielu źródeł interfejsu API w jednym powierzchni interfejsu API, który ułatwia klientom korzystać.</span><span class="sxs-lookup"><span data-stu-id="fba63-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="fba63-154">Jest to szczególnie przydatne, jeśli chcesz skompilować jako mikrousług interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fba63-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="fba63-155">Serwer proxy może wskazywać dowolnego zasobu HTTP, takie jak:</span><span class="sxs-lookup"><span data-stu-id="fba63-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="fba63-156">Stan usługi Funkcje Azure</span><span class="sxs-lookup"><span data-stu-id="fba63-156">Azure Functions</span></span> 
- <span data-ttu-id="fba63-157">Aplikacje interfejsu API w [usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="fba63-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="fba63-158">Kontenery docker w [usługi aplikacji w systemie Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="fba63-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="fba63-159">Inne obsługiwane interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fba63-159">Any other hosted API</span></span>

<span data-ttu-id="fba63-160">Aby dowiedzieć się więcej na temat serwerów proxy, zobacz [Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)].</span><span class="sxs-lookup"><span data-stu-id="fba63-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="fba63-161">Tworzenie pierwszego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="fba63-161">Create your first proxy</span></span>

<span data-ttu-id="fba63-162">W tej sekcji utworzysz nowego serwera proxy, który służy jako frontonu do ogólnego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fba63-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="fba63-163">Konfigurowanie środowiska serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="fba63-163">Setting up the frontend environment</span></span>

<span data-ttu-id="fba63-164">Powtórz kroki, aby [tworzenia aplikacji funkcji](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) Aby utworzyć nową aplikację funkcji spowoduje utworzenie serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="fba63-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="fba63-165">Ta nowa aplikacja będzie służyć jako frontonu dla naszych interfejsu API i aplikacji funkcji, które zostały wcześniej edycji będzie służyć jako wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fba63-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="fba63-166">Przejdź do nowej aplikacji funkcji serwera sieci Web w portalu.</span><span class="sxs-lookup"><span data-stu-id="fba63-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="fba63-167">Wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="fba63-167">Select **Settings**.</span></span> <span data-ttu-id="fba63-168">Następnie przełącz **włączyć proxy funkcji Azure (wersja zapoznawcza)** do "Na".</span><span class="sxs-lookup"><span data-stu-id="fba63-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="fba63-169">Wybierz **ustawienia platformy** i wybierz polecenie **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="fba63-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="fba63-170">Przewiń w dół do **ustawień aplikacji** i utworzyć nowe ustawienie z kluczem "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="fba63-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="fba63-171">Ustaw jej wartość na hoście aplikacji funkcji wewnętrznej bazy danych, takich jak `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="fba63-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="fba63-172">Jest to część adresu URL, które wcześniej zostały skopiowane podczas testowania funkcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="fba63-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="fba63-173">To ustawienie w konfiguracji później będziesz odwoływać.</span><span class="sxs-lookup"><span data-stu-id="fba63-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="fba63-174">Ustawienia aplikacji są zalecane w przypadku konfiguracji hosta zapobiec zależności środowiska ustalony dla serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="fba63-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="fba63-175">Przy użyciu ustawień aplikacji oznacza, że konfiguracja serwera proxy można przenosić między środowiskami i zostaną zastosowane ustawienia aplikacji dla określonego środowiska.</span><span class="sxs-lookup"><span data-stu-id="fba63-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="fba63-176">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fba63-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="fba63-177">Tworzenie serwera proxy na frontonie</span><span class="sxs-lookup"><span data-stu-id="fba63-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="fba63-178">Przejdź z powrotem do aplikacji funkcji serwera sieci Web w portalu.</span><span class="sxs-lookup"><span data-stu-id="fba63-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="fba63-179">W obszarze nawigacji po lewej stronie, kliknij znak "+" obok "Serwery proxy (wersja zapoznawcza)".</span><span class="sxs-lookup"><span data-stu-id="fba63-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![Tworzenie serwera proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="fba63-181">Użyj ustawień serwera proxy, jak określono w tabeli.</span><span class="sxs-lookup"><span data-stu-id="fba63-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="fba63-182">Pole</span><span class="sxs-lookup"><span data-stu-id="fba63-182">Field</span></span> | <span data-ttu-id="fba63-183">Wartość przykładowa</span><span class="sxs-lookup"><span data-stu-id="fba63-183">Sample value</span></span> | <span data-ttu-id="fba63-184">Opis</span><span class="sxs-lookup"><span data-stu-id="fba63-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="fba63-185">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fba63-185">Name</span></span> | <span data-ttu-id="fba63-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="fba63-186">HelloProxy</span></span> | <span data-ttu-id="fba63-187">Przyjazna nazwa używana tylko w przypadku zarządzania</span><span class="sxs-lookup"><span data-stu-id="fba63-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="fba63-188">Szablon trasy</span><span class="sxs-lookup"><span data-stu-id="fba63-188">Route template</span></span> | <span data-ttu-id="fba63-189">/ api/hello</span><span class="sxs-lookup"><span data-stu-id="fba63-189">/api/hello</span></span> | <span data-ttu-id="fba63-190">Określa, jakie trasy służy do wywoływania tego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="fba63-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="fba63-191">Adres URL wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="fba63-191">Backend URL</span></span> | <span data-ttu-id="fba63-192">https://%HELLO_HOST%/API/Hello</span><span class="sxs-lookup"><span data-stu-id="fba63-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="fba63-193">Określa, do którego powinien być serwerem proxy żądania punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="fba63-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="fba63-194">Należy pamiętać, że nie ma serwerów proxy `/api` prefiks ścieżki podstawowej i ten musi być zawarte w szablonie trasy.</span><span class="sxs-lookup"><span data-stu-id="fba63-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="fba63-195">`%HELLO_HOST%` Składni będzie odwoływać się do ustawienia aplikacji utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="fba63-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="fba63-196">Funkcja oryginalnego wskaże rozpoznać adres URL.</span><span class="sxs-lookup"><span data-stu-id="fba63-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="fba63-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fba63-197">Click **Create**.</span></span>

<span data-ttu-id="fba63-198">Można wypróbować nowego serwera proxy, kopiując adres URL serwera Proxy i testowanie go w przeglądarce lub z ulubionych klienta HTTP.</span><span class="sxs-lookup"><span data-stu-id="fba63-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="fba63-199">Utwórz zasymulować interfejs API</span><span class="sxs-lookup"><span data-stu-id="fba63-199">Create a mock API</span></span>

<span data-ttu-id="fba63-200">Następnie użyje serwer proxy można utworzyć zasymulować interfejsu API dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fba63-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="fba63-201">Dzięki temu programowanie klienta do postępu, bez konieczności wewnętrznej bazy danych, w pełni wdrożone.</span><span class="sxs-lookup"><span data-stu-id="fba63-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="fba63-202">Później w rozwoju należy utworzyć nową aplikację funkcji, która obsługuje tę logikę i przekierowywania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="fba63-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="fba63-203">Aby utworzyć ten zasymulować interfejs API, utworzymy nowe proxy przy użyciu tego czasu [Edytor usług aplikacji](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="fba63-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="fba63-204">Aby rozpocząć, przejdź do aplikacji funkcji w portalu.</span><span class="sxs-lookup"><span data-stu-id="fba63-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="fba63-205">Wybierz **funkcji platformy** i Znajdź **Edytor usług aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="fba63-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="fba63-206">Kliknięcie łącza zostanie otwarty Edytor usługi aplikacji na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="fba63-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="fba63-207">Wybierz `proxies.json` na lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="fba63-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="fba63-208">To jest plik zawierający konfigurację dla wszystkich sieci serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="fba63-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="fba63-209">Jeśli używany jest jeden z [metody wdrażania funkcji](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), jest to plik mają być przechowywane w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="fba63-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="fba63-210">Aby dowiedzieć się więcej na temat tego pliku, zobacz [proxy Zaawansowana konfiguracja](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="fba63-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="fba63-211">Jeśli wykonaniu wykonanej do tej pory, proxies.json Twojego powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="fba63-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

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

<span data-ttu-id="fba63-212">Następnie dodasz zasymulować interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fba63-212">Next you'll add your mock API.</span></span> <span data-ttu-id="fba63-213">Zastąp plik proxies.json następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fba63-213">Replace your proxies.json file with the following:</span></span>

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

<span data-ttu-id="fba63-214">Spowoduje to dodanie nowego serwera proxy, "GetUserByName" bez właściwości backendUri.</span><span class="sxs-lookup"><span data-stu-id="fba63-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="fba63-215">Zamiast kontaktować się z innym zasobem, modyfikuje domyślny z serwerów proxy przy użyciu zastąpienia odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fba63-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="fba63-216">Można także zastąpienia żądań i odpowiedzi w połączeniu z adresem URL wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fba63-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="fba63-217">Jest to szczególnie przydatne podczas pośredniczenie dla starszej wersji systemu, której użytkownik może być konieczne zmodyfikowanie nagłówków, zapytania parametry itp. Aby dowiedzieć się więcej na temat zastąpienia żądań i odpowiedzi, zobacz [modyfikowanie żądań i odpowiedzi w proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="fba63-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="fba63-218">Testowanie zasymulować interfejsu API przez wywołanie metody `/api/users/{username}` punktu końcowego za pomocą przeglądarki lub Twoje ulubione klienta REST.</span><span class="sxs-lookup"><span data-stu-id="fba63-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="fba63-219">Pamiętaj zastąpić _{username}_ z wartością ciągu reprezentujący nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fba63-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fba63-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fba63-220">Next steps</span></span>

<span data-ttu-id="fba63-221">W tym samouczku przedstawiono sposób tworzenia i dostosowywania interfejsu API na usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fba63-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="fba63-222">Przedstawiono również sposób Przełącz wielu interfejsów API, mocks, w tym razem jako powierzchnię interfejsu API unified.</span><span class="sxs-lookup"><span data-stu-id="fba63-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="fba63-223">Te techniki służy do tworzenia interfejsów API żadnych złożoności wszystkie uruchomionej na modelu niekorzystającą obliczeniowe udostępniane przez usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fba63-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="fba63-224">Następujące informacje mogą być pomocne podczas opracowywania dalsze interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="fba63-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="fba63-225">Azure powiązania HTTP funkcje i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="fba63-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="fba63-226">[Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]</span><span class="sxs-lookup"><span data-stu-id="fba63-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="fba63-227">Dokumentowanie funkcje interfejsu API Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="fba63-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
