---
title: "aaaGetting uruchomiono z metadanymi OpenAPI w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do korzystania z obsługą OpenAPI w funkcji platformy Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="1ec6c-103">Tworzenie OpenAPI 2.0 (Swagger) metadanych dla aplikacji funkcji (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="1ec6c-104">Ten dokument przeprowadzi Cię hello krok po kroku proces tworzenia definicji OpenAPI dla prosty interfejs API hostowany na usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="1ec6c-105">Co to jest OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="1ec6c-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="1ec6c-106">[Swagger metadanych](http://swagger.io/) jest plik definiujący funkcje hello trybów interfejsu API działania i umożliwia funkcję hosting toobe interfejsu API REST, używane przez wiele różnych innego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="1ec6c-107">Oferty firmy Microsoft, takich jak rozwiązania PowerApps i [aplikacje interfejsu API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), a także narzędzi takich jak 3 programistycznych firmy [Postman](https://www.getpostman.com/docs/importing_swagger) i [wiele pakietów więcej](http://swagger.io/tools/) Zezwalaj na wszystkie Twoje toobe interfejsu API używane z Definicji struktury swagger.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="1ec6c-108"><a name="prepare-function"></a>Tworzenie funkcji za pomocą prostego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1ec6c-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="1ec6c-109">toocreate definicji OpenAPI, najpierw musisz toocreate funkcji z prosty interfejs API.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="1ec6c-110">Jeśli masz już interfejs API hostowany w aplikacji funkcji, można pominąć proste toohello następnej sekcji</span><span class="sxs-lookup"><span data-stu-id="1ec6c-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="1ec6c-111">Utwórz nową aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="1ec6c-112">[Azure portal](https://portal.azure.com)  >  `+ New` > Wyszukaj "Funkcja aplikacji"</span><span class="sxs-lookup"><span data-stu-id="1ec6c-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="1ec6c-113">Utwórz nową funkcję wyzwalacza HTTP w nowej aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="1ec6c-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="1ec6c-114">Funkcja jest wstępnie wypełniony kod definiujący bardzo prosty interfejs API REST.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="1ec6c-115">Dowolny ciąg przekazany toohello funkcji jako parametr zapytania lub w treści hello jest zwracana jako "Hello {danych wejściowych}"</span><span class="sxs-lookup"><span data-stu-id="1ec6c-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="1ec6c-116">Przejdź toohello `Integrate` kartę nową funkcję wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="1ec6c-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="1ec6c-117">Przełącz `Allowed HTTP methods` zbyt`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="1ec6c-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="1ec6c-118">W `Selected HTTP methods` Usuń zaznaczenie pola wyboru co zlecenie, z wyjątkiem POST.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="1ec6c-119">![Metody HTTP wybranych](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="1ec6c-120">Ten krok uprości definicja interfejsu API na dalszym etapie.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="1ec6c-121"><a name="enable"></a>Włączanie obsługi definicji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1ec6c-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="1ec6c-122">Przejdź za`your function name` > `Platform Features` > `API Definition`
![kartę definicja.](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="1ec6c-123">Ustaw `API Definition Source` zbyt`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="1ec6c-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="1ec6c-124">Ten krok powoduje włączenie zestaw opcji OpenAPI dla funkcji aplikacji, w tym toohost punktu końcowego pliku OpenAPI z domeny aplikacji funkcji, wbudowanego kopię hello [Edytor OpenAPI](http://editor.swagger.io)i generator definicji Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="1ec6c-125">![Definicja włączone](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="1ec6c-126"><a name="create-definition"></a>Tworzenie definicja interfejsu API z szablonu</span><span class="sxs-lookup"><span data-stu-id="1ec6c-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="1ec6c-127">Kliknij pozycję `Generate API Definition template`.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="1ec6c-128">Ten krok skanuje aplikacji funkcji dla funkcji wyzwalacza HTTP i używa informacji hello w toogenerate functions.json OpenAPI dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="1ec6c-129">Dodaj obiekt operacji zbyt`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="1ec6c-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="1ec6c-130">Witaj szybkiego startu OpenAPI dokument jest konspektu pełne doc OpenAPI. Wymaga to więcej metadanych toobe pełnej definicji OpenAPI, takie jak szablony odpowiedzi i obiekty operacji.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="1ec6c-131">Obiekt operacji próbki Hello poniżej ma wypełniony tworzy/zużywa sekcji, obiekt parameter i obiekt odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="1ec6c-132">x-ms Podsumowanie zawiera nazwę wyświetlaną w aplikacji logiki, przepływu i rozwiązaniu PowerApps.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="1ec6c-133">Zapoznaj się z [Dostosowywanie definicji struktury Swagger Twoje rozwiązanie PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="1ec6c-134">Kliknij przycisk `save` toosave zmiany ![Dodawanie definicji szablonu](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="1ec6c-135"><a name="use-definition"></a>Korzystanie z definicji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1ec6c-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="1ec6c-136">Kopia programu `API definition URL` i wklej go do nowego tooview kartę przeglądarki dokumencie OpenAPI raw.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="1ec6c-137">Możesz zaimportować numer OpenAPI dokumentu tooany narzędzi do testowania i integracji za pomocą tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="1ec6c-138">Wiele zasobów platformy Azure są import stanie tooautomatically OpenAPI dokumentu przy użyciu hello adres URL definicji interfejsu API, który jest zapisywany w ustawieniach aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="1ec6c-139">Jako część hello `Function` źródła definicji interfejsu API, modyfikacjom tego adresu url dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="1ec6c-140"><a name="test-definition"></a>Przy użyciu tootest interfejs użytkownika programu Swagger hello definicja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1ec6c-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="1ec6c-141">Są to testowanie narzędzi wbudowanych w widoku interfejsu użytkownika toohello edytora definicji interfejsu API hello osadzonego.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="1ec6c-142">Dodawanie klucza interfejsu API, a następnie użyj hello `Try this operation` przycisk w każdej z metod.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="1ec6c-143">Narzędzie Hello użyje Twoich żądań hello tooformat definicji interfejsu API i pomyślnej odpowiedzi oznacza, że definicja poprawne.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="1ec6c-144">kroki:</span><span class="sxs-lookup"><span data-stu-id="1ec6c-144">Steps:</span></span>

1. <span data-ttu-id="1ec6c-145">Skopiuj klucz interfejsu API — funkcja</span><span class="sxs-lookup"><span data-stu-id="1ec6c-145">Copy your function API key</span></span>
    1. <span data-ttu-id="1ec6c-146">klucz interfejsu API Hello znajdują się w funkcji wyzwalacza HTTP w obszarze `function name` > `Keys` > `Function Keys` 
   ![klawisze funkcyjne](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="1ec6c-147">Przejdź toohello `API Definition` strony.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="1ec6c-148">Kliknij przycisk `Authenticate` i dodać u góry hello toohello klucza interfejsu API funkcji zabezpieczeń obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="1ec6c-149">![Klucz OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="1ec6c-150">Wybierz`/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="1ec6c-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="1ec6c-151">Kliknij przycisk `Try it out` , a następnie wprowadź tootest nazwy</span><span class="sxs-lookup"><span data-stu-id="1ec6c-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="1ec6c-152">Powinny pojawić się wynik wskazujący Powodzenie, w obszarze `Pretty` 
 ![testu definicji interfejsu API](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="1ec6c-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ec6c-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ec6c-153">Next steps</span></span>
* [<span data-ttu-id="1ec6c-154">Definicja OpenAPI w Functions — omówienie</span><span class="sxs-lookup"><span data-stu-id="1ec6c-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="1ec6c-155">Przeczytaj dokumentację pełna hello, aby uzyskać więcej informacji na temat obsługi OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="1ec6c-156">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1ec6c-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="1ec6c-157">Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="1ec6c-158">Repozytorium GitHub usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1ec6c-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="1ec6c-159">Sprawdź toogive GitHub funkcje hello nam opinii na temat Podglądu pomocy technicznej definicji interfejsu API hello!</span><span class="sxs-lookup"><span data-stu-id="1ec6c-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="1ec6c-160">Należy to problem GitHub dla wszystkich elementów, które chcesz zaktualizować toosee.</span><span class="sxs-lookup"><span data-stu-id="1ec6c-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
