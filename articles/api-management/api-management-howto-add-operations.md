---
title: "Jak dodać operacje do interfejsu API w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać operacje do interfejsu API w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="07f94-103">Jak dodać operacje do interfejsu API w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="07f94-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="07f94-104">Przed użyciem interfejsu API w usłudze API Management operacji musi zostać dodany.</span><span class="sxs-lookup"><span data-stu-id="07f94-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="07f94-105">W tym przewodniku pokazano, jak dodać i skonfigurować różne rodzaje operacji interfejsu API w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="07f94-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="07f94-106"><a name="add-operation"></a>Dodać operację</span><span class="sxs-lookup"><span data-stu-id="07f94-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="07f94-107">Działania są dodawane i skonfigurowane do interfejsu API w portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="07f94-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="07f94-108">Aby uzyskać dostęp do portalu wydawcy, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="07f94-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="07f94-110">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="07f94-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="07f94-111">Wybierz żądaną interfejsu API w portalu wydawcy, a następnie wybierz **operacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="07f94-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Operacje][api-management-operations]

<span data-ttu-id="07f94-113">Kliknij przycisk **operacji dodawania** można dodać nowej operacji.</span><span class="sxs-lookup"><span data-stu-id="07f94-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="07f94-114">**Nowej operacji** będą wyświetlane i **podpisu** będzie domyślnie wybierany kartę.</span><span class="sxs-lookup"><span data-stu-id="07f94-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Operacja dodania][api-management-add-operation]

<span data-ttu-id="07f94-116">Określ **zlecenie HTTP** wybierając z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="07f94-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![Metoda HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="07f94-118">Zdefiniuj szablon adresu URL, wpisz w fragmentu adresu URL składające się z jednego lub więcej segmentów ścieżki adresu URL i zero lub więcej parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="07f94-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="07f94-119">Szablon adresu URL, dołączone do podstawowego adresu URL interfejsu API, identyfikuje jednej operacji HTTP.</span><span class="sxs-lookup"><span data-stu-id="07f94-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="07f94-120">Może zawierać jeden lub więcej o nazwie części zmiennych, które są identyfikowane za pomocą nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="07f94-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="07f94-121">Części te zmienne są nazywane parametrów szablonu i są dynamicznie przypisywane wartości wyodrębnione z adresu URL żądania, gdy żądanie jest przetwarzane przez interfejs API zarządzania platformy.</span><span class="sxs-lookup"><span data-stu-id="07f94-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="07f94-122">Szablon adresu URL może zawierać wzorców symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="07f94-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="07f94-123">Na przykład określenie `/*` przekazuj wszystkie żądania dla tej metody HTTP na spód zakończy się usługi.</span><span class="sxs-lookup"><span data-stu-id="07f94-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![Szablon adresu URL][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="07f94-125">W razie potrzeby można określić **szablonu ponowne zapisywanie adresów URL**.</span><span class="sxs-lookup"><span data-stu-id="07f94-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="07f94-126">Dzięki temu można użyć standardowego szablonu adresu URL do przetwarzania przychodzących żądań na frontonu, podczas wywoływania zaplecza za pośrednictwem przekonwertowanego adresu URL zgodnie z szablonu ponownego zapisywania.</span><span class="sxs-lookup"><span data-stu-id="07f94-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="07f94-127">Parametry szablonu z szablonu adres URL powinien być używany w szablonie ponownego zapisywania.</span><span class="sxs-lookup"><span data-stu-id="07f94-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="07f94-128">W poniższym przykładzie pokazano, jak zawartości typu zakodowane jako segment ścieżki w usłudze sieci web z poprzedniego przykładu można podać jako parametr zapytania w interfejsie API opublikowane za pośrednictwem platformy interfejsu API zarządzania za pomocą szablonów adresu URL.</span><span class="sxs-lookup"><span data-stu-id="07f94-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![Ponowne zapisywanie adresów URL szablonu][api-management-url-template-rewrite]

<span data-ttu-id="07f94-130">Obiekty wywołujące do operacji zostanie użyty format `/customers?customerid=ALFKI` i to zostaną zmapowane do `/Customers('ALFKI')` po wywołaniu usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="07f94-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="07f94-131">**Wyświetl** nazwy i **opis** Podaj opis operacji i służą do zapewniania dokumentacji dla deweloperów przy użyciu tego interfejsu API w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="07f94-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Opis][api-management-description]

<span data-ttu-id="07f94-133">Opis operacji można określić jako zwykły tekst lub HTML w **opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="07f94-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="07f94-134"><a name="operation-caching"></a>Buforowanie operacji</span><span class="sxs-lookup"><span data-stu-id="07f94-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="07f94-135">Buforowanie odpowiedzi zmniejsza opóźnienia postrzegane przez konsumentów interfejsu API, obniża zużycie przepustowości i zmniejsza obciążenie HTTP sieci web usługi implementacja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="07f94-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="07f94-136">Aby łatwo i szybko włączyć buforowanie dla operacji, zaznacz **buforowanie** i sprawdź **włączyć** wyboru.</span><span class="sxs-lookup"><span data-stu-id="07f94-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Buforowanie][api-management-caching-tab]

<span data-ttu-id="07f94-138">**Czas trwania** określa okres czasu, w którym odpowiedzi operacji pozostaje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="07f94-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="07f94-139">Wartość domyślna to 3600 sekund lub 1 godzina.</span><span class="sxs-lookup"><span data-stu-id="07f94-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="07f94-140">Pamięć podręczna klucze są używane w celu rozróżnienia odpowiedzi, tak aby odpowiedzi odpowiadającą kluczowi każdego innego pamięci podręcznej zostanie uzyskać własną oddzielne wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="07f94-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="07f94-141">Opcjonalnie wprowadź parametrów ciągu zapytania określonego i/lub nagłówków HTTP, które ma być używana podczas obliczania wartości klucza pamięci podręcznej w **różne parametry ciągu zapytania** i **Vary przez nagłówki** odpowiednio pola tekstowe.</span><span class="sxs-lookup"><span data-stu-id="07f94-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="07f94-142">Gdy żaden nie jest adres URL określony, pełną żądania i służą następujące wartości nagłówka HTTP podczas generowania klucza pamięci podręcznej: **Akceptuj** i **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="07f94-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="07f94-143">Aby uzyskać więcej informacji o pamięci podręcznej i buforowania zasady, zobacz [jak pamięci podręcznej operacji wyniki w usłudze Azure API Management][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="07f94-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="07f94-144"><a name="request-parameters"></a>Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="07f94-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="07f94-145">Parametry operacji są zarządzane na karcie Parametry.</span><span class="sxs-lookup"><span data-stu-id="07f94-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="07f94-146">Parametry określone w **szablon adresu URL** na **podpisu** kartę są automatycznie dodawane i można zmienić, edytując szablon adresu URL.</span><span class="sxs-lookup"><span data-stu-id="07f94-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="07f94-147">Dodatkowe parametry, można wprowadzić ręcznie.</span><span class="sxs-lookup"><span data-stu-id="07f94-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="07f94-148">Aby dodać nowy parametr zapytania, kliknij przycisk **dodać parametru zapytania** i wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="07f94-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="07f94-149">**Nazwa** — Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="07f94-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="07f94-150">**Opis elementu** -krótki opis parametru (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="07f94-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="07f94-151">**Typ** — typ parametru, wybrane w polu listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="07f94-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="07f94-152">**Wartości** -wartości, które mogą być przypisane do tego parametru.</span><span class="sxs-lookup"><span data-stu-id="07f94-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="07f94-153">Jedna z wartości może być oznaczony jako domyślny (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="07f94-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="07f94-154">**Wymagane** — określ parametr obowiązkowy, zaznaczając pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="07f94-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Parametry żądania][api-management-request-parameters]

## <span data-ttu-id="07f94-156"><a name="request-body"></a>Treść żądania</span><span class="sxs-lookup"><span data-stu-id="07f94-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="07f94-157">Jeśli zezwala na operację (np. PUT, POST) i wymaga treści może podać przykład go we wszystkich obsługiwanych reprezentacja formaty (np. json, XML).</span><span class="sxs-lookup"><span data-stu-id="07f94-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="07f94-158">Treść żądania jest używana tylko w celach dokumentacji i nie jest weryfikowany.</span><span class="sxs-lookup"><span data-stu-id="07f94-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="07f94-159">Aby wprowadzić treści żądania, przełącz się do **treści** kartę.</span><span class="sxs-lookup"><span data-stu-id="07f94-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="07f94-160">Kliknij przycisk **dodać reprezentacja**, zacznij pisać nazwa żądanego typu zawartości (np. application/json), wybierz je w listy rozwijanej i Wklej przykład treści żądania żądaną w wybranym formacie w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="07f94-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Treść żądania][api-management-request-body]

<span data-ttu-id="07f94-162">W dodatkowego do oświadczenia, można także określić opcjonalny opis w **opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="07f94-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="07f94-163"><a name="responses"></a>Odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="07f94-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="07f94-164">Jest dobrą praktyką jest zawierają przykłady odpowiedzi dla wszystkich kodów stanu, które wywołują może wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="07f94-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="07f94-165">Każdy kod stanu może mieć więcej niż jeden przykład treści odpowiedzi, po jednej dla każdej z obsługiwanych typów zawartości.</span><span class="sxs-lookup"><span data-stu-id="07f94-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="07f94-166">Aby dodać odpowiedzi, kliknij przycisk **Dodaj** i zacznij pisać kod żądany stan.</span><span class="sxs-lookup"><span data-stu-id="07f94-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="07f94-167">W tym przykładzie jest kod stanu **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="07f94-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="07f94-168">Po wyświetleniu kod w listy rozwijanej wybierz go, a kod odpowiedzi jest tworzony i dodawany do operacji.</span><span class="sxs-lookup"><span data-stu-id="07f94-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Kod odpowiedzi][api-management-response-code]

<span data-ttu-id="07f94-170">Kliknij przycisk **dodać reprezentacja**, zacznij wpisywać nazwę odpowiedniego typu zawartości (np. application/json), a następnie wybierz na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="07f94-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Typ zawartości treści][api-management-response-body-content-type]

<span data-ttu-id="07f94-172">Wklej przykład treści odpowiedzi w wybranym formacie w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="07f94-172">Paste the response body example in the selected format into the text box.</span></span> 

![Treść odpowiedzi][api-management-response-body]

<span data-ttu-id="07f94-174">W razie potrzeby dodaj opcjonalny opis w **opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="07f94-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="07f94-175">Po skonfigurowaniu operacji, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="07f94-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="07f94-176"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07f94-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="07f94-177">Po dodaniu działania do interfejsu API, następnym krokiem jest skojarzenia interfejsu API z produktem i opublikuj go, dzięki czemu deweloperzy mogą wywoływać operacjach.</span><span class="sxs-lookup"><span data-stu-id="07f94-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="07f94-178">[Jak utworzyć i opublikować produktu][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="07f94-178">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
