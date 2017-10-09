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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Tworzenie OpenAPI 2.0 (Swagger) metadanych dla aplikacji funkcji (wersja zapoznawcza)

Ten dokument przeprowadzi Cię hello krok po kroku proces tworzenia definicji OpenAPI dla prosty interfejs API hostowany na usługi Azure Functions.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>Co to jest OpenAPI (Swagger)?
[Swagger metadanych](http://swagger.io/) jest plik definiujący funkcje hello trybów interfejsu API działania i umożliwia funkcję hosting toobe interfejsu API REST, używane przez wiele różnych innego oprogramowania. Oferty firmy Microsoft, takich jak rozwiązania PowerApps i [aplikacje interfejsu API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), a także narzędzi takich jak 3 programistycznych firmy [Postman](https://www.getpostman.com/docs/importing_swagger) i [wiele pakietów więcej](http://swagger.io/tools/) Zezwalaj na wszystkie Twoje toobe interfejsu API używane z Definicji struktury swagger.

## <a name="prepare-function"></a>Tworzenie funkcji za pomocą prostego interfejsu API
  toocreate definicji OpenAPI, najpierw musisz toocreate funkcji z prosty interfejs API. Jeśli masz już interfejs API hostowany w aplikacji funkcji, można pominąć proste toohello następnej sekcji
1. Utwórz nową aplikację funkcji.
    1. [Azure portal](https://portal.azure.com)  >  `+ New` > Wyszukaj "Funkcja aplikacji"
1. Utwórz nową funkcję wyzwalacza HTTP w nowej aplikacji funkcji
    1. Funkcja jest wstępnie wypełniony kod definiujący bardzo prosty interfejs API REST.
    1. Dowolny ciąg przekazany toohello funkcji jako parametr zapytania lub w treści hello jest zwracana jako "Hello {danych wejściowych}"
1. Przejdź toohello `Integrate` kartę nową funkcję wyzwalacza HTTP
    1. Przełącz `Allowed HTTP methods` zbyt`Selected methods`
    1. W `Selected HTTP methods` Usuń zaznaczenie pola wyboru co zlecenie, z wyjątkiem POST.
    ![Metody HTTP wybranych](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Ten krok uprości definicja interfejsu API na dalszym etapie.

## <a name="enable"></a>Włączanie obsługi definicji interfejsu API
1. Przejdź za`your function name` > `Platform Features` > `API Definition`
![kartę definicja.](./media/functions-api-definition-getting-started/definitiontab.png)
1. Ustaw `API Definition Source` zbyt`Function (preview)`
    1. Ten krok powoduje włączenie zestaw opcji OpenAPI dla funkcji aplikacji, w tym toohost punktu końcowego pliku OpenAPI z domeny aplikacji funkcji, wbudowanego kopię hello [Edytor OpenAPI](http://editor.swagger.io)i generator definicji Szybki Start.
![Definicja włączone](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Tworzenie definicja interfejsu API z szablonu
1. Kliknij pozycję `Generate API Definition template`.
    1. Ten krok skanuje aplikacji funkcji dla funkcji wyzwalacza HTTP i używa informacji hello w toogenerate functions.json OpenAPI dokumentu.
1. Dodaj obiekt operacji zbyt`paths: /api/yourfunctionroute post:`
    1. Witaj szybkiego startu OpenAPI dokument jest konspektu pełne doc OpenAPI. Wymaga to więcej metadanych toobe pełnej definicji OpenAPI, takie jak szablony odpowiedzi i obiekty operacji.
    1. Obiekt operacji próbki Hello poniżej ma wypełniony tworzy/zużywa sekcji, obiekt parameter i obiekt odpowiedzi.
    
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
    >  x-ms Podsumowanie zawiera nazwę wyświetlaną w aplikacji logiki, przepływu i rozwiązaniu PowerApps.
    >
    > Zapoznaj się z [Dostosowywanie definicji struktury Swagger Twoje rozwiązanie PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn więcej.

1. Kliknij przycisk `save` toosave zmiany ![Dodawanie definicji szablonu](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Korzystanie z definicji interfejsu API
1. Kopia programu `API definition URL` i wklej go do nowego tooview kartę przeglądarki dokumencie OpenAPI raw.
1. Możesz zaimportować numer OpenAPI dokumentu tooany narzędzi do testowania i integracji za pomocą tego adresu URL.
    1. Wiele zasobów platformy Azure są import stanie tooautomatically OpenAPI dokumentu przy użyciu hello adres URL definicji interfejsu API, który jest zapisywany w ustawieniach aplikacji funkcji. Jako część hello `Function` źródła definicji interfejsu API, modyfikacjom tego adresu url dla Ciebie.


## <a name="test-definition"></a>Przy użyciu tootest interfejs użytkownika programu Swagger hello definicja interfejsu API
Są to testowanie narzędzi wbudowanych w widoku interfejsu użytkownika toohello edytora definicji interfejsu API hello osadzonego. Dodawanie klucza interfejsu API, a następnie użyj hello `Try this operation` przycisk w każdej z metod. Narzędzie Hello użyje Twoich żądań hello tooformat definicji interfejsu API i pomyślnej odpowiedzi oznacza, że definicja poprawne.

### <a name="steps"></a>kroki:

1. Skopiuj klucz interfejsu API — funkcja
    1. klucz interfejsu API Hello znajdują się w funkcji wyzwalacza HTTP w obszarze `function name` > `Keys` > `Function Keys` 
   ![klawisze funkcyjne](./media/functions-api-definition-getting-started/functionkey.png)
1. Przejdź toohello `API Definition` strony.
    1. Kliknij przycisk `Authenticate` i dodać u góry hello toohello klucza interfejsu API funkcji zabezpieczeń obiektu.
  ![Klucz OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. Wybierz`/api/yourfunctionroute` > `POST`
1. Kliknij przycisk `Try it out` , a następnie wprowadź tootest nazwy
1. Powinny pojawić się wynik wskazujący Powodzenie, w obszarze `Pretty` 
 ![testu definicji interfejsu API](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Następne kroki
* [Definicja OpenAPI w Functions — omówienie](functions-api-definition.md)
  * Przeczytaj dokumentację pełna hello, aby uzyskać więcej informacji na temat obsługi OpenAPI.
* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)  
  * Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.
* [Repozytorium GitHub usługi Azure Functions](https://github.com/Azure/Azure-Functions/)
  * Sprawdź toogive GitHub funkcje hello nam opinii na temat Podglądu pomocy technicznej definicji interfejsu API hello! Należy to problem GitHub dla wszystkich elementów, które chcesz zaktualizować toosee.
