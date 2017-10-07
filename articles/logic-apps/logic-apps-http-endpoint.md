---
title: "aaaCall, wyzwalacza lub zagnieździć przepływy pracy z punktów końcowych HTTP - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Konfigurowanie toocall punktów końcowych HTTP, wyzwalacza lub zagnieżdżania przepływy pracy dla usługi Azure Logic Apps"
services: logic-apps
keywords: "przepływy pracy, punktów końcowych HTTP"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Wywołaj wyzwalacz, lub zagnieżdżania przepływy pracy z punktów końcowych HTTP w aplikacji logiki

Natywnie mogą uwidaczniać synchroniczne końcowych HTTP jako Wyzwalacze w aplikacji logiki, aby można wyzwolić lub wywołać aplikacje logiki przy użyciu adresu URL. Można zagnieżdżać przepływów pracy w aplikacjach logiki za pomocą wzorca można wywołać punktów końcowych.

punkty końcowe HTTP toocreate, można dodać te wyzwalacze, dzięki czemu aplikacje logiki może odbierać przychodzące żądania:

* [Żądanie](../connectors/connectors-native-reqres.md)

* [Element Webhook połączenia interfejsu API](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [Element webhook protokołu HTTP](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Mimo że nasze przykłady użycia hello **żądania** wyzwalacza, będzie można użyć dowolnego z hello na liście wyzwalaczy HTTP, a wszystkie zasady tak samo zastosować toohello inne typy wyzwalacza.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Konfigurowanie punktu końcowego HTTP dla aplikacji logiki

punkt końcowy HTTP toocreate dodać wyzwalacz, który może odbierać przychodzące żądania.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure"). Przejdź do aplikacji logiki tooyour i otwórz projektanta aplikacji logiki.

2. Dodaj wyzwalacz, który umożliwia aplikacji logiki odbierania żądań przychodzących. Na przykład dodać hello **żądania** aplikacji logiki tooyour wyzwalacza.

3.  W obszarze **żądania schematu JSON treści**, można opcjonalnie wprowadzić schematu JSON dla ładunku hello (dane) spodziewać się hello tooreceive wyzwalacza.

    Projektant Hello używa tego schematu do generowania tokenów, że aplikację logiki można użyć tooconsume, analizy i przekazywania danych z wyzwalacza hello przez przepływ pracy. 
    Więcej informacji o [tokeny generowane na podstawie schematów JSON](#generated-tokens).

    Na przykład wprowadź schematu hello wyświetlany w Projektancie hello:

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Dodaj akcję żądania hello][1]

    > [!TIP]
    > 
    > Schemat przykładowy ładunek JSON można generować za pomocą narzędzia, takie jak [jsonschema.net](http://jsonschema.net/), lub w hello **żądania** wyzwalacza, wybierając **Użyj przykładowy ładunek toogenerate schematu**. 
    > Wprowadź przykładowy ładunek, a następnie wybierz pozycję **gotowe**.

    Na przykład ten przykładowy ładunek:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    generuje ten schemat:

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  Zapisz aplikację logiki. W obszarze **HTTP POST toothis URL**, powinna być teraz widoczna wygenerowanego wywołania zwrotnego adresu URL, tak jak ten przykład:

    ![Wywołanie zwrotne wygenerowany adres URL punktu końcowego](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Ten adres URL zawiera klucz dostępu sygnatury dostępu Współdzielonego w hello parametry zapytania, które są używane do uwierzytelniania. 
    Można również uzyskać adres URL punktu końcowego HTTP hello z Twojej Omówienie aplikacji logiki w hello portalu Azure. W obszarze **historii wyzwalacza**, wybierz wyzwalacz:

    ![Adres URL punktu końcowego HTTP GET z portalu Azure][2]

    Można także uzyskać adres URL hello za sprawą tego wywołania:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Zmień metodę HTTP hello wyzwalacza

Domyślnie program hello **żądania** wyzwalacza oczekuje żądania HTTP POST, ale można użyć innej metody HTTP. 

> [!NOTE]
> Można określić tylko jedną metodę typu.

1. W Twojej **żądania** wyzwalania, wybierz **Pokaż zaawansowane opcje**.

2. Otwórz hello **metody** listy. Na przykład wybierz **UZYSKAĆ** tak, aby można było testować punkt końcowy HTTP URL później.

    > [!NOTE]
    > Wybierz inne metody HTTP lub określić metodę niestandardowych aplikacji logiki.

    ![Zmień metodę HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Akceptować parametry przez adres URL punktu końcowego HTTP

Parametry tooaccept adres URL punktu końcowego HTTP, należy dostosować ścieżkę względną do tego wyzwalacza.

1. W Twojej **żądania** wyzwalania, wybierz **Pokaż zaawansowane opcje**. 

2. W obszarze **metody**, określ metodę hello HTTP, które mają toouse Twojego żądania. Na przykład wybierz hello **UZYSKAĆ** metody, jeśli nie jest jeszcze, dzięki czemu można sprawdzić adres URL punkt końcowy HTTP.

      > [!NOTE]
      > Po określeniu ścieżki względnej wyzwalacza metody HTTP należy również jawnie określić wyzwalacza.

3. W obszarze **ścieżki względnej**, określ ścieżkę względną hello parametru hello adres URL powinien akceptują, na przykład `customers/{customerID}`.

    ![Określ metodę HTTP hello i ścieżka względna dla parametru](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse hello parametr, Dodaj **odpowiedzi** aplikacji logiki tooyour akcji. (W obszarze wyzwalacz, wybierz **nowy krok** > **Dodaj akcję** > **odpowiedzi**) 

5. Do odpowiedzi **treści**, obejmuje hello tokenu dla parametru hello, określonej ścieżki względnej do tego wyzwalacza.

    Na przykład tooreturn `Hello {customerID}`, aktualizacja do odpowiedzi **treści** z `Hello {customerID token}`. 
    listy zawartości dynamicznej Hello powinna występować i Pokaż hello `customerID` tokenu dla tooselect użytkownik.

    ![Dodaj parametr tooresponse treści](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    Twoje **treści** powinna wyglądać następująco:

    ![Treść odpowiedzi z parametrem](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Zapisz aplikację logiki. 

    Adres URL punktu końcowego HTTP zawiera teraz hello ścieżki względnej, na przykład: 

    HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest Twojego punkt końcowy HTTP, kopiowania i wklejania hello zaktualizowane adres URL w innym oknie przeglądarki, ale zastępuje `{customerID}` z `123456`, i naciśnij klawisz Enter.

    Ten tekst powinien być wyświetlony w przeglądarce: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Tokeny generowane na podstawie schematów JSON aplikacji logiki

Jeśli podasz schematu JSON w Twojej **żądania** Wyzwól program hello projektanta aplikacji logiki generuje tokeny na potrzeby właściwości w tym schemacie. Można następnie użyć tych tokenów przekazywania danych za pomocą przepływu pracy aplikacji logiki.

Na przykład, jeśli dodasz hello `title` i `name` właściwości tooyour schematu JSON, tokenów są teraz dostępne toouse w kolejnych krokach przepływu pracy. 

Oto hello pełną schematu JSON:

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Utwórz zagnieżdżone przepływy pracy dla usługi logic apps

Przepływy pracy można zagnieździć w aplikacji logiki przez dodanie innych aplikacji logiki, które mogą odbierać żądań. tooinclude tych aplikacji logiki, Dodaj hello **Azure Logic Apps — wybierz przepływ pracy aplikacji logiki** akcji tooyour wyzwalacza. Następnie możesz wybrać z kwalifikujących się logiki aplikacji.

![Dodaj inną aplikację logiki](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Wyzwalacza logiki aplikacji za pomocą punktów końcowych HTTP lub wywołać

Po utworzeniu punktu końcowego HTTP, możesz wyzwolić aplikację logiki za pośrednictwem `POST` metody toohello pełny adres URL. Aplikacje logiki mają wbudowaną obsługę dostęp bezpośredni punktów końcowych.

## <a name="reference-content-from-an-incoming-request"></a>Odwołanie do zawartości z przychodzącego żądania

Jeśli typ zawartości hello jest `application/json`, możesz odwoływać właściwości z żądania przychodzącego hello. W przeciwnym razie zawartość jest traktowany jako pojedyncza jednostka binarne przekazywanej tooother interfejsów API. Ta zawartość wewnątrz przepływu pracy hello tooreference, należy przekonwertować tej zawartości. Na przykład w przypadku przekazania `application/xml` zawartości, można użyć `@xpath()` do wyodrębnienia XPath lub `@json()` do konwertowania XML tooJSON. Dowiedz się więcej o [Praca z typami zawartości](../logic-apps/logic-apps-content-type.md).

Witaj tooget dane wyjściowe z żądania przychodzącego, można użyć hello `@triggerOutputs()` funkcji. dane wyjściowe Hello może wyglądać w tym przykładzie:

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

Witaj tooaccess `body` właściwości w szczególności służy hello `@triggerBody()` skrótów. 

## <a name="respond-toorequests"></a>Odpowiedź toorequests

Możesz toorespond toocertain żądań, które uruchamiają aplikację logiki, zwracając obiekt wywołujący toohello zawartości. Kod stanu hello tooconstruct, nagłówek i treść odpowiedzi można użyć hello **odpowiedzi** akcji. Ta akcja może występować w dowolnym miejscu w aplikacji logiki, nie tylko na końcu hello przepływ pracy.

> [!NOTE] 
> Jeśli nie zawiera aplikacji logiki **odpowiedzi**, odpowiada punkt końcowy hello HTTP *natychmiast* z **202 zaakceptowane** stanu. Ponadto dla oryginalnego żądania tooget hello odpowiedź hello, wszystkich kroków wymaganych do odpowiedzi hello musi zakończyć się w obrębie hello [limit czasu żądania](./logic-apps-limits-and-config.md) chyba, że wywołanie przepływu pracy hello jako aplikację logiki zagnieżdżonych. Jeśli się nie dzieje nie otrzymano odpowiedzi w ramach tego limitu, hello przychodzące żądanie upłynie limit czasu i odbiera odpowiedź hello HTTP **408 Limit czasu klienta**. Dla aplikacji logiki zagnieżdżonych aplikacji logiki nadrzędnego hello nadal toowait dla odpowiedzi do czasu ukończenia, niezależnie od tego, ile czasu jest wymagana.

### <a name="construct-hello-response"></a>Konstrukcja hello odpowiedzi

W treści odpowiedzi hello może zawierać więcej niż jeden nagłówek i dowolnego typu zawartości. W naszym przykładzie odpowiedzi, nagłówek hello Określa, czy odpowiedź hello ma typ zawartości `application/json`. i zawiera treść hello `title` i `name`, oparte na wcześniej dodano hello schematu JSON hello **żądania** wyzwalacza.

![Akcja odpowiedzi HTTP][3]

Odpowiedzi ma następujące właściwości:

| Właściwość | Opis |
| --- | --- |
| statusCode |Określa kod stanu hello HTTP odpowiada toohello żądania przychodzącego. Ten kod może być prawidłowym stanem kodu, który rozpoczyna się od 2xx, 4xx lub 5xx. Kody stanu 3xx nie są dozwolone. |
| Nagłówki |Definiuje dowolną liczbę tooinclude nagłówki odpowiedzi hello. |
| Treści |Określa obiekt treści, która może być ciągiem, obiekt JSON lub nawet binarny zawartości przywoływanej z poprzedniego kroku. |

Oto, jakie schematu JSON hello prawdopodobnie teraz dla hello **odpowiedzi** akcji:

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> Wybierz tooview hello pełnej JSON definicji aplikacji logiki, na powitania projektanta aplikacji logiki, **widok Kod**.

## <a name="q--a"></a>Pytania i odpowiedzi

#### <a name="q-what-about-url-security"></a>Pytanie: jak adres URL zabezpieczeń?

A: azure generuje bezpieczne logiki wywołania zwrotnego adresy URL aplikacji przy użyciu udostępnionych podpis dostępu (SAS). Ta sygnatura przekazuje jako parametr zapytania i musi zostać zweryfikowany przed mogą wyzwalać aplikację logiki. Platforma Azure generuje podpisu hello przy użyciu unikatowej kombinacji wartości klucza tajnego dla każdej aplikacji logiki, nazwa wyzwalacza hello i hello operacja, która jest wykonywana. Dlatego jeśli ktoś ma klucz aplikacji logiki tajny toohello dostępu, nie można wygenerować prawidłowego podpisu.

   > [!IMPORTANT]
   > Produkcyjnego i systemów zabezpieczeń zaleca przed wywołaniem bezpośrednio z przeglądarki hello aplikację logiki, ponieważ:
   > 
   > * w adresie URL hello pojawi się Hello udostępniony klucz dostępu.
   > * Nie można zarządzać bezpieczna zasady zawartości powodu domen tooshared wielu odbiorców aplikacji logiki.

#### <a name="q-can-i-configure-http-endpoints-further"></a>Pytanie: czy można skonfigurować dodatkowe punkty końcowe HTTP?

Odpowiedź: tak punktów końcowych HTTP obsługuje bardziej zaawansowanych konfiguracji za pomocą [ **zarządzanie interfejsami API**](../api-management/api-management-key-concepts.md). Ta usługa również oferuje możliwości hello tooconsistently możesz zarządzać wszystkie swoje interfejsy API, łącznie z aplikacji logiki, konfigurowanie niestandardowych nazw domen, użyj więcej metod uwierzytelniania i inne, na przykład:

* [Metoda żądania zmiany hello](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Segmenty adresu URL hello hello żądania zmiany](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Konfigurowanie domeny zarządzanie interfejsami API w hello [portalu Azure](https://portal.azure.com/ "portalu Azure")
* Konfigurowanie zasad toocheck dla uwierzytelniania podstawowego

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>Pytanie: jakie zmieniony podczas migracji hello schematu w hello 1 grudnia 2014 r. w wersji zapoznawczej?

Odpowiedź: w tym miejscu znajduje się podsumowanie dotyczące tych zmian:

| Wersja zapoznawcza 1 grudnia 2014 r. | 1 czerwca 2016 r. |
| --- | --- |
| Kliknij przycisk **odbiornik HTTP** aplikacji interfejsu API |Kliknij przycisk **ręczne wyzwalacza** (wymagane dla żadnej aplikacji interfejsu API) |
| Ustawienia odbiornika HTTP "*automatycznie wysyła odpowiedź*" |Zawierają **odpowiedzi** akcji lub nie znajduje się w hello definicji przepływu pracy |
| Skonfiguruj uwierzytelnianie podstawowe lub OAuth |za pomocą interfejsu API zarządzania |
| Skonfiguruj HTTP — metoda |W obszarze **Pokaż zaawansowane opcje**, wybierz metodę HTTP |
| Konfigurowanie ścieżki względnej |W obszarze **Pokaż zaawansowane opcje**, Dodaj ścieżkę względną |
| Odwołanie hello treści przychodzące za pośrednictwem`@triggerOutputs().body.Content` |Odwołanie za pośrednictwem`@triggerOutputs().body` |
| **Wyślij odpowiedź HTTP** akcji na powitania odbiornika HTTP |Kliknij przycisk **żądania tooHTTP odpowiedź** (wymagane dla żadnej aplikacji interfejsu API) |

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

* [Tworzenie definicji aplikacji logiki](./logic-apps-author-definitions.md)
* [Obsługa błędów i wyjątków](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
