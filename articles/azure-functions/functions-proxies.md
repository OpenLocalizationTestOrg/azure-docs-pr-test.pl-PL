---
title: "Praca z serwerów proxy w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Omówienie sposobu korzystania z serwerów proxy funkcji platformy Azure"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="982a2-103">Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="982a2-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="982a2-104">Proxy funkcji platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="982a2-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="982a2-105">Jest bezpłatne w wersji zapoznawczej, ale standardowych funkcji rozliczeń dotyczy wykonaniami serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="982a2-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="982a2-106">Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="982a2-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="982a2-107">W tym artykule opisano sposób konfigurowania i pracować z serwerów proxy funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="982a2-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="982a2-108">Dzięki tej funkcji można określić punkty końcowe na aplikację funkcji, które zostały zaimplementowane przez inny zasób.</span><span class="sxs-lookup"><span data-stu-id="982a2-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="982a2-109">Umożliwia te serwery proxy Podziel dużych interfejsu API na wiele aplikacji funkcji (tak jak to architektura mikrousługi), prezentując pojedynczą powierzchnię interfejsu API dla klientów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="982a2-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="982a2-110"><a name="enable"></a>Włącz usługę Azure Functions serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="982a2-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="982a2-111">Serwery proxy nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="982a2-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="982a2-112">Funkcja jest wyłączona, ale nie zostanie wykonany, można tworzyć serwery proxy.</span><span class="sxs-lookup"><span data-stu-id="982a2-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="982a2-113">Aby włączyć serwery proxy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="982a2-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="982a2-114">Otwórz [portalu Azure], a następnie przejdź do aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="982a2-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="982a2-115">Wybierz **funkcji ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="982a2-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="982a2-116">Przełącznik **włączyć proxy funkcji Azure (wersja zapoznawcza)** do **na**.</span><span class="sxs-lookup"><span data-stu-id="982a2-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="982a2-117">Można także wrócić tutaj można zaktualizować środowisko uruchomieniowe serwera proxy, gdy udostępnione nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="982a2-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="982a2-118"><a name="create"></a>Utwórz serwer proxy</span><span class="sxs-lookup"><span data-stu-id="982a2-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="982a2-119">W tej sekcji przedstawiono sposób tworzenia serwera proxy w portalu funkcji.</span><span class="sxs-lookup"><span data-stu-id="982a2-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="982a2-120">Otwórz [portalu Azure], a następnie przejdź do aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="982a2-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="982a2-121">W okienku po lewej stronie wybierz **nowego serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="982a2-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="982a2-122">Podaj nazwę serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="982a2-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="982a2-123">Skonfiguruj punktu końcowego, która jest widoczna w tym funkcji aplikacji, określając **szablon trasy** i **metod HTTP**.</span><span class="sxs-lookup"><span data-stu-id="982a2-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="982a2-124">Parametry te działają zgodnie z regułami dla [wyzwalaczy HTTP].</span><span class="sxs-lookup"><span data-stu-id="982a2-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="982a2-125">Ustaw **URL wewnętrznej bazy danych** do innego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="982a2-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="982a2-126">Ten punkt końcowy może być funkcją w innej aplikacji funkcji lub może być jakiegokolwiek interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="982a2-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="982a2-127">Wartość musi być statyczne i mogą się odwoływać do [ustawienia aplikacji] i [parametrów z żądania klienta oryginalnym].</span><span class="sxs-lookup"><span data-stu-id="982a2-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="982a2-128">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="982a2-128">Click **Create**.</span></span>

<span data-ttu-id="982a2-129">Serwer proxy obecnie istnieje jako nowy punkt końcowy w aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="982a2-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="982a2-130">Z perspektywy klienta jest odpowiednikiem HttpTrigger w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="982a2-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="982a2-131">Można wypróbować nowego serwera proxy, kopiując adres URL serwera Proxy i testowanie go z ulubionych klienta HTTP.</span><span class="sxs-lookup"><span data-stu-id="982a2-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="982a2-132"><a name="modify-requests-responses"></a>Modyfikowanie żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="982a2-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="982a2-133">Za pomocą proxy funkcji platformy Azure można modyfikować żądania i odpowiedzi z wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="982a2-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="982a2-134">Przekształcenia te można używać zmiennych, zgodnie z definicją w [używać zmiennych].</span><span class="sxs-lookup"><span data-stu-id="982a2-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="982a2-135"><a name="modify-backend-request"></a>Modyfikowanie żądania zaplecza</span><span class="sxs-lookup"><span data-stu-id="982a2-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="982a2-136">Domyślnie żądania zaplecza został zainicjowany jako kopia oryginalnego żądania.</span><span class="sxs-lookup"><span data-stu-id="982a2-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="982a2-137">Oprócz skonfigurowania adresu URL zaplecza, można wprowadzić zmiany do metody HTTP, nagłówki i parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="982a2-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="982a2-138">Zmodyfikowane wartości może się odwoływać [ustawienia aplikacji] i [parametrów z żądania klienta oryginalnym].</span><span class="sxs-lookup"><span data-stu-id="982a2-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="982a2-139">Obecnie nie są portalu obsługę modyfikowanie żądań zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="982a2-140">Aby dowiedzieć się, jak zastosować tę możliwość z proxies.json, zobacz [zdefiniować obiekt requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="982a2-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="982a2-141"><a name="modify-response"></a>Modyfikować odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="982a2-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="982a2-142">Domyślnie odpowiedzi klienta zostanie zainicjowany jako kopię odpowiedzi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="982a2-143">Kod stanu odpowiedzi, frazę przyczyny, nagłówki i treści, można wprowadzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="982a2-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="982a2-144">Zmodyfikowane wartości może się odwoływać [ustawienia aplikacji], [parametrów z żądania klienta oryginalnym], i [parametry z odpowiedzi zaplecza].</span><span class="sxs-lookup"><span data-stu-id="982a2-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="982a2-145">Obecnie nie są bez obsługi portalu modyfikowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="982a2-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="982a2-146">Aby dowiedzieć się, jak zastosować tę możliwość z proxies.json, zobacz [zdefiniować obiekt responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="982a2-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="982a2-147"><a name="using-variables"></a>Używać zmiennych</span><span class="sxs-lookup"><span data-stu-id="982a2-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="982a2-148">Konfiguracja serwera proxy dla muszą być statyczne.</span><span class="sxs-lookup"><span data-stu-id="982a2-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="982a2-149">Można warunku, aby używać zmiennych z oryginalnego żądania, odpowiedzi zaplecza lub ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="982a2-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="982a2-150"><a name="request-parameters"></a>Parametry żądania odwołania</span><span class="sxs-lookup"><span data-stu-id="982a2-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="982a2-151">Parametry żądania można użyć jako dane wejściowe, aby właściwość URL zaplecza lub w ramach modyfikowania żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="982a2-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="982a2-152">Niektóre parametry mogą być powiązane z szablonu trasy, który został określony w konfiguracji podstawowej serwera proxy, a inne osoby mogą pochodzić z właściwości z żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="982a2-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="982a2-153">Parametry szablonu trasy</span><span class="sxs-lookup"><span data-stu-id="982a2-153">Route template parameters</span></span>
<span data-ttu-id="982a2-154">Parametry, które są używane w szablonie trasy dostępnych może odwoływać się do nazwy.</span><span class="sxs-lookup"><span data-stu-id="982a2-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="982a2-155">Nazwy parametrów są ujęte w nawiasy klamrowe ({}).</span><span class="sxs-lookup"><span data-stu-id="982a2-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="982a2-156">Na przykład, jeśli serwer proxy ma szablon trasy, takich jak `/pets/{petId}`, adres URL zaplecza może zawierać wartości `{petId}`, jak w `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="982a2-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="982a2-157">Jeśli szablon trasy kończy w symboli wieloznacznych, takich jak `/api/{*restOfPath}`, wartość `{restOfPath}` jest reprezentację ciągu pozostałych segmentów ścieżki z żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="982a2-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="982a2-158">Dodatkowe parametry żądania</span><span class="sxs-lookup"><span data-stu-id="982a2-158">Additional request parameters</span></span>
<span data-ttu-id="982a2-159">Oprócz parametrów szablonu trasy można używać następujących wartości w wartości konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="982a2-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="982a2-160">**{Request.method wartość}** : Metoda HTTP, która jest używana na oryginalne żądanie.</span><span class="sxs-lookup"><span data-stu-id="982a2-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="982a2-161">**{request.headers. \<HeaderName\>}**: nagłówek, który może zostać odczytany z oryginalnego żądania.</span><span class="sxs-lookup"><span data-stu-id="982a2-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="982a2-162">Zastąp  *\<HeaderName\>*  o nazwie nagłówka, który chcesz odczytać.</span><span class="sxs-lookup"><span data-stu-id="982a2-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="982a2-163">Jeśli żądanie nie zawiera nagłówka, wartość będzie pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="982a2-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="982a2-164">**{request.querystring. \<ParameterName\>}**: parametr ciągu zapytania, który może zostać odczytany z oryginalnego żądania.</span><span class="sxs-lookup"><span data-stu-id="982a2-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="982a2-165">Zastąp  *\<ParameterName\>*  o nazwę parametru, który chcesz odczytać.</span><span class="sxs-lookup"><span data-stu-id="982a2-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="982a2-166">Jeśli parametr nie jest dostępna na żądanie, wartość będzie pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="982a2-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="982a2-167"><a name="response-parameters"></a>Parametry zaplecza odpowiedzi odwołania</span><span class="sxs-lookup"><span data-stu-id="982a2-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="982a2-168">Parametry odpowiedzi mogą być używane jako część modyfikowania odpowiedzi do klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="982a2-169">W wartości konfiguracji można używać następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="982a2-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="982a2-170">**{backend.response.statusCode}** : Kod stanu HTTP, który jest zwracany w odpowiedzi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="982a2-171">**{backend.response.statusReason}** : Fraza przyczyny protokołu HTTP, który jest zwracany w odpowiedzi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="982a2-172">**{backend.response.headers. \<HeaderName\>}**: nagłówek, który może zostać odczytany z odpowiedzi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="982a2-173">Zastąp  *\<HeaderName\>*  o nazwie nagłówka, który chcesz odczytać.</span><span class="sxs-lookup"><span data-stu-id="982a2-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="982a2-174">Jeśli żądanie nie zawiera nagłówka, wartość będzie pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="982a2-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="982a2-175"><a name="use-appsettings"></a>Odwołanie do ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="982a2-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="982a2-176">Można także odwoływać [ustawienia aplikacji określone dla aplikacji funkcja](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) przez wpisywania nazwy ustawienia w znaki procentu (%).</span><span class="sxs-lookup"><span data-stu-id="982a2-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="982a2-177">Na przykład adres URL zaplecza z *https://%ORDER_PROCESSING_HOST%/api/orders* byłyby "% ORDER_PROCESSING_HOST %" zastąpione przez ustawienie ORDER_PROCESSING_HOST.</span><span class="sxs-lookup"><span data-stu-id="982a2-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="982a2-178">Użyj ustawienia aplikacji dla hostów zaplecza w przypadku wielu wdrożeń lub środowisk testowych.</span><span class="sxs-lookup"><span data-stu-id="982a2-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="982a2-179">W ten sposób można upewnić się, że zawsze mówimy do prawej zaplecza dla tego środowiska.</span><span class="sxs-lookup"><span data-stu-id="982a2-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="982a2-180">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="982a2-180">Advanced configuration</span></span>

<span data-ttu-id="982a2-181">Serwery proxy, które można skonfigurować są przechowywane w pliku proxies.json, który znajduje się w folderze głównym katalogiem aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="982a2-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="982a2-182">Można ręcznie edytować ten plik i wdrożyć go jako część aplikacji przy użyciu jednej z [metody wdrażania](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) obsługiwane przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="982a2-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="982a2-183">Funkcja musi być [włączone](#enable) pliku do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="982a2-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="982a2-184">Jeśli nie zdefiniowano jednej z metod wdrażania, użytkownik może również współpracować z pliku proxies.json w portalu.</span><span class="sxs-lookup"><span data-stu-id="982a2-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="982a2-185">Przejdź do funkcji aplikacji, wybierz opcję **funkcji platformy**, a następnie wybierz **Edytor usług aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="982a2-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="982a2-186">W ten sposób można wyświetlić strukturę całego pliku aplikacji funkcji, a następnie wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="982a2-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="982a2-187">Proxies.JSON jest zdefiniowane przez obiekt serwery proxy, który składa się z nazwanym proxy oraz ich definicje.</span><span class="sxs-lookup"><span data-stu-id="982a2-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="982a2-188">Opcjonalnie, jeśli edytor obsługuje tę funkcję, możesz odwoływać się do [schematu JSON](http://json.schemastore.org/proxies) dla uzupełniania kodu.</span><span class="sxs-lookup"><span data-stu-id="982a2-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="982a2-189">Przykładowy plik może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="982a2-189">An example file might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="982a2-190">Każdy serwer proxy ma przyjazną nazwę, takich jak *proxy1* w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="982a2-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="982a2-191">Odpowiedni obiekt serwera proxy w definicji jest zdefiniowane przez następujących właściwościach:</span><span class="sxs-lookup"><span data-stu-id="982a2-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="982a2-192">**matchCondition**: wymagany — obiekt definiujący żądań, które wyzwalają wykonanie tego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="982a2-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="982a2-193">Zawiera dwie właściwości, które są udostępniane [wyzwalaczy HTTP]:</span><span class="sxs-lookup"><span data-stu-id="982a2-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="982a2-194">_metody_: Tablica metod HTTP, które odpowiada serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="982a2-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="982a2-195">Jeśli nie zostanie określony, serwer proxy reaguje na wszystkie metody HTTP na trasie.</span><span class="sxs-lookup"><span data-stu-id="982a2-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="982a2-196">_trasy_: wymagany — definiuje szablon trasy, kontrolowanie, które adresów URL żądań proxy odpowiada.</span><span class="sxs-lookup"><span data-stu-id="982a2-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="982a2-197">W odróżnieniu od w HTTP wyzwalaczy, nie ma wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="982a2-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="982a2-198">**backendUri**: adres URL zasobu zaplecza, do którego powinien być serwerem proxy żądania.</span><span class="sxs-lookup"><span data-stu-id="982a2-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="982a2-199">Ta wartość może odwoływać się parametry i ustawienia aplikacji z oryginalnego żądania klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="982a2-200">Jeśli ta właściwość nie jest uwzględniona, usługi Azure Functions odpowiada HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="982a2-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="982a2-201">**requestOverrides**: obiekt, który definiuje przekształcenia na żądanie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="982a2-202">Zobacz [zdefiniować obiekt requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="982a2-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="982a2-203">**responseOverrides**: obiekt, który definiuje przekształcenia odpowiedzi klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="982a2-204">Zobacz [zdefiniować obiekt responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="982a2-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="982a2-205">Właściwości trasy proxy funkcji Azure honoruje właściwości routePrefix konfiguracji hostów funkcji.</span><span class="sxs-lookup"><span data-stu-id="982a2-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="982a2-206">Jeśli chcesz dołączyć prefiksu, takich jak /api, musi być uwzględniona we właściwości trasy.</span><span class="sxs-lookup"><span data-stu-id="982a2-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="982a2-207"><a name="requestOverrides"></a>Zdefiniuj obiektu requestOverrides</span><span class="sxs-lookup"><span data-stu-id="982a2-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="982a2-208">Obiekt requestOverrides definiuje zmiany wprowadzone do żądania wywołanego zasobów wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="982a2-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="982a2-209">Obiekt jest zdefiniowane przez następujących właściwościach:</span><span class="sxs-lookup"><span data-stu-id="982a2-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="982a2-210">**backend.Request.Method**: metoda HTTP, która jest używana do wywołania wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="982a2-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="982a2-211">**backend.Request.QueryString. \<ParameterName\>**: parametr ciągu zapytania ustawioną dla wywołania wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="982a2-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="982a2-212">Zastąp  *\<ParameterName\>*  o nazwę parametru, który chcesz ustawić.</span><span class="sxs-lookup"><span data-stu-id="982a2-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="982a2-213">W przypadku pustego ciągu parametru nie jest uwzględniony w żądaniu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="982a2-214">**backend.Request.headers. \<HeaderName\>**: nagłówek, który można ustawić dla wywołania wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="982a2-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="982a2-215">Zastąp  *\<HeaderName\>*  o nazwie nagłówka, którą chcesz ustawić.</span><span class="sxs-lookup"><span data-stu-id="982a2-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="982a2-216">Jeśli podasz pustym ciągiem nagłówka nie znajduje się na żądanie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="982a2-217">Ustawienia aplikacji i parametrów wartości można odwoływać się z oryginalnego żądania klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="982a2-218">Przykładowa konfiguracja może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="982a2-218">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="982a2-219"><a name="responseOverrides"></a>Zdefiniuj obiektu responseOverrides</span><span class="sxs-lookup"><span data-stu-id="982a2-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="982a2-220">Obiekt requestOverrides definiuje zmiany wprowadzone do odpowiedzi, która jest przekazywane z powrotem do klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="982a2-221">Obiekt jest zdefiniowane przez następujących właściwościach:</span><span class="sxs-lookup"><span data-stu-id="982a2-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="982a2-222">**response.statusCode**: kod stanu HTTP ma zostać zwrócona do klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="982a2-223">**response.statusReason**: fraza przyczyny HTTP ma zostać zwrócona do klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="982a2-224">**Response.body**: reprezentację ciągu treści, która ma zostać zwrócona do klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="982a2-225">**Response.headers. \<HeaderName\>**: nagłówek, który można ustawić dla odpowiedzi do klienta.</span><span class="sxs-lookup"><span data-stu-id="982a2-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="982a2-226">Zastąp  *\<HeaderName\>*  o nazwie nagłówka, którą chcesz ustawić.</span><span class="sxs-lookup"><span data-stu-id="982a2-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="982a2-227">Jeśli podasz pustym ciągiem nagłówka nie jest uwzględniony w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="982a2-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="982a2-228">Ustawienia aplikacji, parametrów z żądania klienta oryginalnym i parametry wartości można odwoływać się z odpowiedzi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="982a2-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="982a2-229">Przykładowa konfiguracja może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="982a2-229">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="982a2-230">W tym przykładzie treści jest ustawiany bezpośrednio, więc nie `backendUri` właściwość jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="982a2-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="982a2-231">W przykładzie pokazano, jak można użyć do mocking interfejsów API Azure funkcji z serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="982a2-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="982a2-232">[portalu Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="982a2-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="982a2-233">[wyzwalaczy HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="982a2-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="982a2-234">[zdefiniować obiekt requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="982a2-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="982a2-235">[zdefiniować obiekt responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="982a2-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="982a2-236">[ustawienia aplikacji]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="982a2-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="982a2-237">[używać zmiennych]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="982a2-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="982a2-238">[parametrów z żądania klienta oryginalnym]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="982a2-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="982a2-239">[parametry z odpowiedzi zaplecza]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="982a2-239">[parameters from the back-end response]: #response-parameters</span></span>
