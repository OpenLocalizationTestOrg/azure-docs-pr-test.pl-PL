---
title: "aaaHow tooadd tooan operacje interfejsu API w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd tooan operacje interfejsu API w usłudze Azure API Management."
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
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="838a7-103">Jak tooadd tooan operacje interfejsu API w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="838a7-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="838a7-104">Przed użyciem interfejsu API w usłudze API Management operacji musi zostać dodany.</span><span class="sxs-lookup"><span data-stu-id="838a7-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="838a7-105">Ten przewodnik przedstawia jak tooadd i konfigurowania różnych typów tooan operacje interfejsu API w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="838a7-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="838a7-106"><a name="add-operation"></a>Dodać operację</span><span class="sxs-lookup"><span data-stu-id="838a7-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="838a7-107">Operacje są dodawane i tooan interfejsu API w portalu wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="838a7-108">tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="838a7-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="838a7-110">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="838a7-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="838a7-111">Wybierz hello żądana interfejsu API w portalu wydawcy hello i wybierz opcję hello **operacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="838a7-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![Operacje][api-management-operations]

<span data-ttu-id="838a7-113">Kliknij przycisk **operacji dodawania** tooadd nowej operacji.</span><span class="sxs-lookup"><span data-stu-id="838a7-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="838a7-114">Witaj **nowej operacji** będą wyświetlane i hello **podpisu** będzie domyślnie wybierany kartę.</span><span class="sxs-lookup"><span data-stu-id="838a7-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Operacja dodania][api-management-add-operation]

<span data-ttu-id="838a7-116">Określ hello **zlecenie HTTP** wybierając z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![Metoda HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="838a7-118">Zdefiniuj szablon adresu URL hello wpisując fragmentu adresu URL składające się z jednego lub więcej segmentów ścieżki adresu URL i zero lub więcej parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="838a7-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="838a7-119">Szablon adresu URL Hello, dołączany toohello podstawowy adres URL hello interfejsu API, identyfikuje jednej operacji HTTP.</span><span class="sxs-lookup"><span data-stu-id="838a7-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="838a7-120">Może zawierać jeden lub więcej o nazwie części zmiennych, które są identyfikowane za pomocą nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="838a7-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="838a7-121">Części te zmienne są nazywane parametrów szablonu i są dynamicznie przypisywane wartości wyodrębniony z adresu URL żądania hello, gdy trwa przetwarzanie żądania hello przez platformę interfejsu API zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="838a7-122">Szablon adresu URL Hello mogą obejmować wzorców symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="838a7-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="838a7-123">Na przykład określenie `/*` przekazuj wszystkie żądania dotyczące toohello metody powrót tego HTTP zakończy się usługi.</span><span class="sxs-lookup"><span data-stu-id="838a7-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![Szablon adresu URL][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="838a7-125">W razie potrzeby można określić hello **szablonu ponowne zapisywanie adresów URL**.</span><span class="sxs-lookup"><span data-stu-id="838a7-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="838a7-126">Dzięki temu można toouse hello standardowy szablon adresu URL do przetwarzania przychodzących żądań na powitania frontonu, podczas wywoływania hello zaplecza za pośrednictwem adresu URL przekonwertowanego zgodnie z toohello ponownego zapisywania szablonu.</span><span class="sxs-lookup"><span data-stu-id="838a7-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="838a7-127">Parametry szablonu z szablonu adresu URL hello powinien być używany w szablonie ponownego zapisywania hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="838a7-128">Witaj poniższy przykład przedstawia sposób zawartości typu zakodowane jako segment ścieżki w hello usługi sieci web z poprzedniego przykładu hello można podać jako parametr zapytania w hello interfejsu API opublikowane za pośrednictwem hello platformy zarządzania interfejsu API przy użyciu szablonów URL hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![Ponowne zapisywanie adresów URL szablonu][api-management-url-template-rewrite]

<span data-ttu-id="838a7-130">Operacja toohello wywołań zostanie użyty hello format `/customers?customerid=ALFKI` i będzie to zbyt mapować`/Customers('ALFKI')` po wywołaniu hello usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="838a7-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="838a7-131">**Wyświetl** nazwy i **opis** Podaj opis operacji hello i są używane tooprovide dokumentacji deweloperzy toohello przy użyciu tego interfejsu API w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Opis][api-management-description]

<span data-ttu-id="838a7-133">Opis operacji Hello można określić jako zwykły tekst lub HTML w hello **opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="838a7-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="838a7-134"><a name="operation-caching"></a>Buforowanie operacji</span><span class="sxs-lookup"><span data-stu-id="838a7-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="838a7-135">Buforowanie odpowiedzi zmniejsza opóźnienia postrzegane przez konsumentów hello interfejsu API, obniża zużycie przepustowości i hello zmniejsza obciążenie wdrażanie usługi sieci web HTTP hello hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="838a7-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="838a7-136">tooeasily i szybko włączyć buforowanie dla operacji hello, wybierz hello **buforowanie** i sprawdź hello **włączyć** wyboru.</span><span class="sxs-lookup"><span data-stu-id="838a7-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Buforowanie][api-management-caching-tab]

<span data-ttu-id="838a7-138">**Czas trwania** określa okres czasu, podczas których hello odpowiedź operacji pozostaje w pamięci podręcznej hello hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="838a7-139">Hello wartość domyślna wynosi 3600 sekund lub 1 godzina.</span><span class="sxs-lookup"><span data-stu-id="838a7-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="838a7-140">Buforowanie kluczy są używane toodifferentiate między odpowiedzi, aby odpowiedź hello odpowiadającego klucz pamięci podręcznej różnych tooeach otrzyma własną oddzielne wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="838a7-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="838a7-141">Opcjonalnie wprowadź parametrów ciągu zapytania określonego i/lub toobe nagłówki HTTP używany w obliczeniu wartości klucza pamięci podręcznej na powitania **różne parametry ciągu zapytania** i **Vary przez nagłówki** odpowiednio pola tekstowe.</span><span class="sxs-lookup"><span data-stu-id="838a7-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="838a7-142">Gdy żaden nie jest adres URL określony, pełną żądania i hello następujące wartości nagłówka HTTP są używane podczas generowania klucza pamięci podręcznej: **Akceptuj** i **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="838a7-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="838a7-143">Aby uzyskać więcej informacji o pamięci podręcznej i buforowania zasady, zobacz [jak wynikiem Azure API Management operacji toocache][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="838a7-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="838a7-144"><a name="request-parameters"></a>Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="838a7-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="838a7-145">Parametry operacji są zarządzane na powitania karta Parametry. Parametry określone w hello **szablon adresu URL** na powitania **podpisu** kartę są automatycznie dodawane i można zmienić, edytując hello szablon adresu URL.</span><span class="sxs-lookup"><span data-stu-id="838a7-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="838a7-146">Dodatkowe parametry, można wprowadzić ręcznie.</span><span class="sxs-lookup"><span data-stu-id="838a7-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="838a7-147">tooadd nowy parametr zapytania, kliknij przycisk **dodać parametru zapytania** , a następnie wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="838a7-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="838a7-148">**Nazwa** — Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="838a7-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="838a7-149">**Opis elementu** -krótki opis parametru hello (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="838a7-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="838a7-150">**Typ** — wybrany hello rozwijanej Typ parametru.</span><span class="sxs-lookup"><span data-stu-id="838a7-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="838a7-151">**Wartości** -wartości, które można przypisać parametru toothis.</span><span class="sxs-lookup"><span data-stu-id="838a7-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="838a7-152">Jedna z wartości hello może być oznaczony jako domyślny (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="838a7-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="838a7-153">**Wymagane** -był parametru hello zaznaczając pole wyboru hello jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="838a7-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![Parametry żądania][api-management-request-parameters]

## <span data-ttu-id="838a7-155"><a name="request-body"></a>Treść żądania</span><span class="sxs-lookup"><span data-stu-id="838a7-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="838a7-156">Jeśli zezwala na operację hello (np. PUT, POST) i wymaga treści może podać przykład go we wszystkich hello obsługiwane formaty reprezentacja (np. json, XML).</span><span class="sxs-lookup"><span data-stu-id="838a7-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="838a7-157">Treść żądania Hello jest używany tylko w celach dokumentacji i nie jest weryfikowany.</span><span class="sxs-lookup"><span data-stu-id="838a7-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="838a7-158">tooenter treści żądania, Przełącz toohello **treści** kartę.</span><span class="sxs-lookup"><span data-stu-id="838a7-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="838a7-159">Kliknij przycisk **dodać reprezentacja**, wpisz nazwę odpowiedniego typu zawartości (np. application/json), wybierz je w listy rozwijanej hello i Wklej hello potrzeby przykład treści żądania w wybranym formacie hello w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Treść żądania][api-management-request-body]

<span data-ttu-id="838a7-161">W dodatkowych toorepresentations, można także określić opcjonalny opis w hello **opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="838a7-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="838a7-162"><a name="responses"></a>Odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="838a7-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="838a7-163">Należy dobrze przykłady tooprovide odpowiedzi dla wszystkich kodów stanu, które może powodować hello operacji.</span><span class="sxs-lookup"><span data-stu-id="838a7-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="838a7-164">Każdy kod stanu może mieć więcej niż jeden przykład treści odpowiedzi, po jednej dla każdego z hello obsługiwane typy zawartości.</span><span class="sxs-lookup"><span data-stu-id="838a7-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="838a7-165">tooadd odpowiedzi, kliknij przycisk **Dodaj** i zacznij pisać kod stanu hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="838a7-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="838a7-166">Taki stan hello przykładowy kod jest **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="838a7-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="838a7-167">Gdy kod hello jest wyświetlany w listy rozwijanej hello, zaznacz go i hello kod odpowiedzi jest utworzony i dodany tooyour operacji.</span><span class="sxs-lookup"><span data-stu-id="838a7-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Kod odpowiedzi][api-management-response-code]

<span data-ttu-id="838a7-169">Kliknij przycisk **dodać reprezentacja**zacznij wpisywać ciąg hello nazwa żądanego typu zawartości (np. application/json), a następnie wybierz pozycję w hello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="838a7-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Typ zawartości treści][api-management-response-body-content-type]

<span data-ttu-id="838a7-171">Wklej przykład treści odpowiedzi Witaj w wybranym formacie hello w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="838a7-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Treść odpowiedzi][api-management-response-body]

<span data-ttu-id="838a7-173">W razie potrzeby dodaj opcjonalny opis w hello **opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="838a7-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="838a7-174">Po skonfigurowaniu operacji powitania kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="838a7-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="838a7-175"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="838a7-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="838a7-176">Po dodaniu interfejsu API tooan operacji hello, hello następnym krokiem jest tooassociate hello interfejsu API z produktem i opublikować go, dzięki czemu deweloperzy mogą wywoływać operacjach.</span><span class="sxs-lookup"><span data-stu-id="838a7-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="838a7-177">[Jak toocreate i opublikuj produktu][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="838a7-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
