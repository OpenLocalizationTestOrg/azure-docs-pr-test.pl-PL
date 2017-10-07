---
title: "aaaWork z serwerów proxy w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Omówienie toouse proxy funkcji platformy Azure"
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
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="5dca1-103">Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="5dca1-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="5dca1-104">Proxy funkcji platformy Azure jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="5dca1-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="5dca1-105">Jest bezpłatne w wersji zapoznawczej, ale standardowych funkcji rozliczeń dotyczy wykonaniami tooproxy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="5dca1-106">Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="5dca1-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="5dca1-107">W tym artykule opisano sposób tooconfigure i korzystanie z serwerów proxy funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dca1-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="5dca1-108">Dzięki tej funkcji można określić punkty końcowe na aplikację funkcji, które zostały zaimplementowane przez inny zasób.</span><span class="sxs-lookup"><span data-stu-id="5dca1-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="5dca1-109">Te serwery proxy toobreak dużych interfejsu API do wielu aplikacji funkcji (tak jak to architektura mikrousługi), można użyć podczas prezentując pojedynczą powierzchnię interfejsu API dla klientów.</span><span class="sxs-lookup"><span data-stu-id="5dca1-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="5dca1-110"><a name="enable"></a>Włącz usługę Azure Functions serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="5dca1-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="5dca1-111">Serwery proxy nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="5dca1-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="5dca1-112">Serwery proxy można utworzyć podczas hello funkcja jest wyłączona, ale nie zostanie wykonany.</span><span class="sxs-lookup"><span data-stu-id="5dca1-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="5dca1-113">proxy tooenable hello następujące:</span><span class="sxs-lookup"><span data-stu-id="5dca1-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="5dca1-114">Otwórz hello [portalu Azure], a następnie przejdź tooyour funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dca1-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="5dca1-115">Wybierz **funkcji ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5dca1-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="5dca1-116">Przełącznik **włączyć proxy funkcji Azure (wersja zapoznawcza)** za**na**.</span><span class="sxs-lookup"><span data-stu-id="5dca1-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="5dca1-117">Można także wrócić tu tooupdate powitania serwera proxy w czasie wykonywania jako nowe funkcje staną się dostępne.</span><span class="sxs-lookup"><span data-stu-id="5dca1-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="5dca1-118"><a name="create"></a>Utwórz serwer proxy</span><span class="sxs-lookup"><span data-stu-id="5dca1-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="5dca1-119">W tej sekcji przedstawiono, jak toocreate, a serwer proxy w hello funkcje portalu.</span><span class="sxs-lookup"><span data-stu-id="5dca1-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="5dca1-120">Otwórz hello [portalu Azure], a następnie przejdź tooyour funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dca1-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="5dca1-121">Wybierz w okienku po lewej stronie powitania **nowego serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="5dca1-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="5dca1-122">Podaj nazwę serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="5dca1-123">Skonfiguruj hello punktu końcowego, która jest widoczna w tym funkcji aplikacji, określając hello **szablon trasy** i **metod HTTP**.</span><span class="sxs-lookup"><span data-stu-id="5dca1-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="5dca1-124">Te parametry działają zgodnie z zasady toohello [wyzwalaczy HTTP].</span><span class="sxs-lookup"><span data-stu-id="5dca1-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="5dca1-125">Zestaw hello **URL wewnętrznej bazy danych** tooanother punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5dca1-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="5dca1-126">Ten punkt końcowy może być funkcją w innej aplikacji funkcji lub może być jakiegokolwiek interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5dca1-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="5dca1-127">Hello wartość nie jest konieczne toobe statyczne i mogą się odwoływać do [ustawienia aplikacji] i [parametrów z żądania klienta oryginalnym hello].</span><span class="sxs-lookup"><span data-stu-id="5dca1-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="5dca1-128">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5dca1-128">Click **Create**.</span></span>

<span data-ttu-id="5dca1-129">Serwer proxy obecnie istnieje jako nowy punkt końcowy w aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="5dca1-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="5dca1-130">Z perspektywy klienta jest równoważne tooan HttpTrigger w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dca1-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="5dca1-131">Można wypróbować nowego serwera proxy, kopiując hello adres URL serwera Proxy i testowanie go z ulubionych klienta HTTP.</span><span class="sxs-lookup"><span data-stu-id="5dca1-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="5dca1-132"><a name="modify-requests-responses"></a>Modyfikowanie żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5dca1-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="5dca1-133">Za pomocą proxy funkcji platformy Azure można modyfikować żądania tooand odpowiedzi z hello wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="5dca1-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="5dca1-134">Przekształcenia te można używać zmiennych, zgodnie z definicją w [używać zmiennych].</span><span class="sxs-lookup"><span data-stu-id="5dca1-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="5dca1-135"><a name="modify-backend-request"></a>Modyfikowanie hello zaplecza żądania</span><span class="sxs-lookup"><span data-stu-id="5dca1-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="5dca1-136">Domyślnie hello zaplecza żądania został zainicjowany jako kopię hello oryginalne żądanie.</span><span class="sxs-lookup"><span data-stu-id="5dca1-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="5dca1-137">Ponadto toosetting hello wewnętrznego adresu URL, możesz wprowadzić metoda HTTP toohello zmiany, nagłówki i parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="5dca1-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="5dca1-138">Witaj zmodyfikowane wartości może się odwoływać [ustawienia aplikacji] i [parametrów z żądania klienta oryginalnym hello].</span><span class="sxs-lookup"><span data-stu-id="5dca1-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="5dca1-139">Obecnie nie są portalu obsługę modyfikowanie żądań zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5dca1-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="5dca1-140">toolearn tooapply tej możliwości z proxies.json, zobacz temat [zdefiniować obiekt requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="5dca1-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="5dca1-141"><a name="modify-response"></a>Modyfikowanie hello odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5dca1-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="5dca1-142">Domyślnie powitania klienta odpowiedzi został zainicjowany jako kopię hello zaplecza odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="5dca1-143">Możesz wprowadzić kod stanu odpowiedzi toohello zmiany, frazę przyczyny, nagłówki i treść.</span><span class="sxs-lookup"><span data-stu-id="5dca1-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="5dca1-144">Witaj zmodyfikowane wartości może się odwoływać [ustawienia aplikacji], [parametrów z żądania klienta oryginalnym hello], i [parametry z odpowiedzi zaplecza hello].</span><span class="sxs-lookup"><span data-stu-id="5dca1-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="5dca1-145">Obecnie nie są bez obsługi portalu modyfikowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="5dca1-146">toolearn tooapply tej możliwości z proxies.json, zobacz temat [zdefiniować obiekt responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="5dca1-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="5dca1-147"><a name="using-variables"></a>Używać zmiennych</span><span class="sxs-lookup"><span data-stu-id="5dca1-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="5dca1-148">Hello konfigurację serwera proxy nie jest konieczne toobe statycznych.</span><span class="sxs-lookup"><span data-stu-id="5dca1-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="5dca1-149">Można go warunku zmienne toouse hello oryginalne żądanie, hello zaplecza odpowiedzi lub ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dca1-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="5dca1-150"><a name="request-parameters"></a>Parametry żądania odwołania</span><span class="sxs-lookup"><span data-stu-id="5dca1-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="5dca1-151">Parametry żądania można użyć jako danych wejściowych właściwość URL zaplecza toohello lub w ramach modyfikowania żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="5dca1-152">Niektóre parametry mogą być powiązane z hello szablon trasy, który został określony w konfiguracji podstawowej serwera proxy hello i inne osoby mogą pochodzić z właściwości hello żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="5dca1-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="5dca1-153">Parametry szablonu trasy</span><span class="sxs-lookup"><span data-stu-id="5dca1-153">Route template parameters</span></span>
<span data-ttu-id="5dca1-154">Parametry, które są używane w szablonie trasy hello są dostępne toobe wskazywana przez nazwę.</span><span class="sxs-lookup"><span data-stu-id="5dca1-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="5dca1-155">nazwy parametrów Hello są ujęte w nawiasy klamrowe ({}).</span><span class="sxs-lookup"><span data-stu-id="5dca1-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="5dca1-156">Na przykład, jeśli serwer proxy ma szablon trasy, takich jak `/pets/{petId}`, adres URL zaplecza hello może zawierać wartości hello `{petId}`, jak w `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="5dca1-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="5dca1-157">Jeśli szablon trasy hello kończy w symboli wieloznacznych, takich jak `/api/{*restOfPath}`, hello wartość `{restOfPath}` jest hello pozostałych segmentów ścieżki z żądania przychodzącego hello reprezentację ciągu.</span><span class="sxs-lookup"><span data-stu-id="5dca1-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="5dca1-158">Dodatkowe parametry żądania</span><span class="sxs-lookup"><span data-stu-id="5dca1-158">Additional request parameters</span></span>
<span data-ttu-id="5dca1-159">Ponadto toohello parametry szablonu trasy, hello następujące wartości można użyć w wartości konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="5dca1-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="5dca1-160">**{Request.method wartość}** : hello metoda HTTP, która jest używana na powitania oryginalne żądanie.</span><span class="sxs-lookup"><span data-stu-id="5dca1-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="5dca1-161">**{request.headers. \<HeaderName\>}**: nagłówek, który może zostać odczytany z hello oryginalne żądanie.</span><span class="sxs-lookup"><span data-stu-id="5dca1-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="5dca1-162">Zastąp  *\<HeaderName\>*  o nazwie hello hello nagłówka, które mają tooread.</span><span class="sxs-lookup"><span data-stu-id="5dca1-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="5dca1-163">Jeśli hello nagłówka nie znajduje się na żądanie hello, wartość hello będzie hello pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="5dca1-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="5dca1-164">**{request.querystring. \<ParameterName\>}**: parametr ciągu zapytania, który może zostać odczytany z hello oryginalne żądanie.</span><span class="sxs-lookup"><span data-stu-id="5dca1-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="5dca1-165">Zastąp  *\<ParameterName\>*  o nazwie hello parametru hello, które mają tooread.</span><span class="sxs-lookup"><span data-stu-id="5dca1-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="5dca1-166">Jeśli parametr hello jest niedostępna na żądanie hello, wartość hello będzie hello pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="5dca1-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="5dca1-167"><a name="response-parameters"></a>Parametry zaplecza odpowiedzi odwołania</span><span class="sxs-lookup"><span data-stu-id="5dca1-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="5dca1-168">Parametry odpowiedzi mogą być używane jako część modyfikowanie hello odpowiedzi toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5dca1-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="5dca1-169">Witaj następujące wartości mogą być używane w wartości konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="5dca1-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="5dca1-170">**{backend.response.statusCode}** : hello kod stanu HTTP, który jest zwracany w odpowiedzi zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="5dca1-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="5dca1-171">**{backend.response.statusReason}** : fraza przyczyny hello HTTP, który jest zwracany w odpowiedzi zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="5dca1-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="5dca1-172">**{backend.response.headers. \<HeaderName\>}**: nagłówek, który może zostać odczytany z hello zaplecza odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="5dca1-173">Zastąp  *\<HeaderName\>*  o nazwie hello nagłówka hello ma tooread.</span><span class="sxs-lookup"><span data-stu-id="5dca1-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="5dca1-174">Jeśli hello nagłówka nie znajduje się na żądanie hello, wartość hello będzie hello pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="5dca1-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="5dca1-175"><a name="use-appsettings"></a>Odwołanie do ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="5dca1-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="5dca1-176">Można także odwoływać [ustawienia aplikacji określone dla aplikacji funkcja hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) wpisując nazwę ustawienia hello w znaki procentu (%).</span><span class="sxs-lookup"><span data-stu-id="5dca1-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="5dca1-177">Na przykład adres URL zaplecza z *https://%ORDER_PROCESSING_HOST%/api/orders* byłyby "% ORDER_PROCESSING_HOST %" zastąpione hello hello ORDER_PROCESSING_HOST ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5dca1-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="5dca1-178">Użyj ustawienia aplikacji dla hostów zaplecza w przypadku wielu wdrożeń lub środowisk testowych.</span><span class="sxs-lookup"><span data-stu-id="5dca1-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="5dca1-179">W ten sposób można zapewnić zawsze komunikuje powrót toohello zakończenia dla tego środowiska.</span><span class="sxs-lookup"><span data-stu-id="5dca1-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="5dca1-180">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="5dca1-180">Advanced configuration</span></span>

<span data-ttu-id="5dca1-181">proxy Hello, które można skonfigurować są przechowywane w pliku proxies.json, który znajduje się w katalogu głównym hello funkcja katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dca1-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="5dca1-182">Można ręcznie edytować ten plik i wdróż je jako część aplikacji, gdy przy użyciu jednej z hello [metody wdrażania](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) obsługiwane przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="5dca1-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="5dca1-183">Funkcja Hello musi być [włączone](#enable) dla toobe pliku hello przetworzone.</span><span class="sxs-lookup"><span data-stu-id="5dca1-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="5dca1-184">Jeśli nie zdefiniowano jednej z metod wdrażania hello, użytkownik może również współpracować z pliku proxies.json hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="5dca1-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="5dca1-185">Przejdź tooyour funkcji aplikacji, wybierz opcję **funkcji platformy**, a następnie wybierz **Edytor usług aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5dca1-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="5dca1-186">W ten sposób można wyświetlić hello cały plik struktury aplikacji funkcji, a następnie wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="5dca1-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="5dca1-187">Proxies.JSON jest zdefiniowane przez obiekt serwery proxy, który składa się z nazwanym proxy oraz ich definicje.</span><span class="sxs-lookup"><span data-stu-id="5dca1-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="5dca1-188">Opcjonalnie, jeśli edytor obsługuje tę funkcję, możesz odwoływać się do [schematu JSON](http://json.schemastore.org/proxies) dla uzupełniania kodu.</span><span class="sxs-lookup"><span data-stu-id="5dca1-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="5dca1-189">Przykładowy plik może wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5dca1-189">An example file might look like hello following:</span></span>

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

<span data-ttu-id="5dca1-190">Każdy serwer proxy ma przyjazną nazwę, takich jak *proxy1* w hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="5dca1-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="5dca1-191">Witaj odpowiedni obiekt definicji serwera proxy jest zdefiniowane przez hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5dca1-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="5dca1-192">**matchCondition**: wymagany — obiekt definiujący hello żądań, które wyzwolić wykonywanie hello tego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="5dca1-193">Zawiera dwie właściwości, które są udostępniane [wyzwalaczy HTTP]:</span><span class="sxs-lookup"><span data-stu-id="5dca1-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="5dca1-194">_metody_: odpowiada tablicę metody hello HTTP, które hello serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="5dca1-195">Jeśli nie zostanie określony, hello proxy odpowiada tooall metod HTTP na powitania trasy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="5dca1-196">_trasy_: wymagany — definiuje hello szablon trasy, kontrolowanie, które adresów URL żądań proxy odpowiada.</span><span class="sxs-lookup"><span data-stu-id="5dca1-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="5dca1-197">W odróżnieniu od w HTTP wyzwalaczy, nie ma wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="5dca1-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="5dca1-198">**backendUri**: adres URL hello hello zasobów zaplecza toowhich hello żądania powinien być serwerem proxy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="5dca1-199">Ta wartość może odwoływać się ustawienia aplikacji i parametrów z żądania klienta oryginalnym hello.</span><span class="sxs-lookup"><span data-stu-id="5dca1-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="5dca1-200">Jeśli ta właściwość nie jest uwzględniona, usługi Azure Functions odpowiada HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="5dca1-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="5dca1-201">**requestOverrides**: obiekt, który definiuje przekształcenia toohello zaplecza żądania.</span><span class="sxs-lookup"><span data-stu-id="5dca1-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="5dca1-202">Zobacz [zdefiniować obiekt requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="5dca1-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="5dca1-203">**responseOverrides**: obiekt, który definiuje przekształcenia toohello klienta odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="5dca1-204">Zobacz [zdefiniować obiekt responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="5dca1-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="5dca1-205">właściwości trasy Hello Azure funkcji proxy honoruje właściwości routePrefix hello hello funkcje hosta konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5dca1-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="5dca1-206">Jeśli chcesz tooinclude prefiksu, takich jak /api, muszą być zawarte w hello właściwości trasy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="5dca1-207"><a name="requestOverrides"></a>Zdefiniuj obiektu requestOverrides</span><span class="sxs-lookup"><span data-stu-id="5dca1-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="5dca1-208">Obiekt requestOverrides Hello definiuje zmiany wprowadzone żądania toohello wywołanego hello zasobów wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="5dca1-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="5dca1-209">Obiekt Hello jest zdefiniowany przez hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5dca1-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="5dca1-210">**backend.Request.Method**: hello metoda HTTP, która została użyta toocall hello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5dca1-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="5dca1-211">**backend.Request.QueryString. \<ParameterName\>**: ustawioną dla zaplecza hello wywołania toohello parametr ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="5dca1-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="5dca1-212">Zastąp  *\<ParameterName\>*  o nazwie hello parametru hello, które mają tooset.</span><span class="sxs-lookup"><span data-stu-id="5dca1-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="5dca1-213">W przypadku pustego ciągu hello parametru hello jest niedostępna na powitania zaplecza żądania.</span><span class="sxs-lookup"><span data-stu-id="5dca1-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="5dca1-214">**backend.Request.headers. \<HeaderName\>**: nagłówek, który można ustawić dla hello wywołania toohello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5dca1-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="5dca1-215">Zastąp  *\<HeaderName\>*  o nazwie hello hello nagłówka, które mają tooset.</span><span class="sxs-lookup"><span data-stu-id="5dca1-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="5dca1-216">Jeśli podasz hello pusty ciąg hello nagłówka nie znajduje się na powitania zaplecza żądania.</span><span class="sxs-lookup"><span data-stu-id="5dca1-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="5dca1-217">Wartości można odwoływać się ustawienia aplikacji i parametrów z żądania klienta oryginalnym hello.</span><span class="sxs-lookup"><span data-stu-id="5dca1-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="5dca1-218">Przykładowa konfiguracja może wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5dca1-218">An example configuration might look like hello following:</span></span>

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

### <span data-ttu-id="5dca1-219"><a name="responseOverrides"></a>Zdefiniuj obiektu responseOverrides</span><span class="sxs-lookup"><span data-stu-id="5dca1-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="5dca1-220">Obiekt requestOverrides Hello definiuje zmiany wprowadzone w odpowiedzi toohello, która ma wstecz toohello zakończyło się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5dca1-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="5dca1-221">Obiekt Hello jest zdefiniowany przez hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5dca1-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="5dca1-222">**response.statusCode**: toobe kod stanu hello HTTP zwrócił toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5dca1-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="5dca1-223">**response.statusReason**: toobe fraza przyczyny hello HTTP zwrócony toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5dca1-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="5dca1-224">**Response.body**: hello treści toobe reprezentację ciągu hello zwrócił toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5dca1-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="5dca1-225">**Response.headers. \<HeaderName\>**: nagłówek, który można ustawić dla hello odpowiedzi toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="5dca1-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="5dca1-226">Zastąp  *\<HeaderName\>*  o nazwie hello hello nagłówka, które mają tooset.</span><span class="sxs-lookup"><span data-stu-id="5dca1-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="5dca1-227">Jeśli podasz pusty ciąg hello hello nagłówka nie znajduje się na powitania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="5dca1-228">Ustawienia aplikacji, parametrów z żądania klienta oryginalnym hello i parametry wartości można odwoływać się z hello zaplecza odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5dca1-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="5dca1-229">Przykładowa konfiguracja może wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5dca1-229">An example configuration might look like hello following:</span></span>

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
> <span data-ttu-id="5dca1-230">W tym przykładzie treści hello jest ustawiany bezpośrednio, więc nie `backendUri` właściwość jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="5dca1-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="5dca1-231">przykład Witaj pokazuje, jak można użyć do mocking interfejsów API Azure funkcji z serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="5dca1-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[portalu Azure]: https://portal.azure.com
[wyzwalaczy HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[zdefiniować obiekt requestOverrides]: #requestOverrides
[zdefiniować obiekt responseOverrides]: #responseOverrides
[ustawienia aplikacji]: #use-appsettings
[używać zmiennych]: #using-variables
[parametrów z żądania klienta oryginalnym hello]: #request-parameters
[parametry z odpowiedzi zaplecza hello]: #response-parameters
