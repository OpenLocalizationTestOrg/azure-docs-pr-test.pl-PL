---
title: "aaaWorkflow działań i wyzwalaczy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Działania przepływu pracy i Wyzwalacze dla usługi Azure Logic Apps

Aplikacje logiki składają się z wyzwalacze i akcje. Istnieją typy sześciu wyzwalaczy. Każdy typ ma inny interfejs i inaczej. Również informacje na temat innych szczegółów sprawdzając szczegóły hello hello [język definicji przepływu pracy](logic-apps-workflow-definition-language.md).  
  
Poniżej toolearn więcej informacji na temat wyzwalacze i akcje i jak można ich używać toobuild logic apps tooimprove Twojego procesów biznesowych i przepływów pracy.  
  
### <a name="triggers"></a>Wyzwalacze  

Wyzwalacz określa hello wywołania, które mogą inicjować uruchomienia przepływu pracy aplikacji logiki. Poniżej przedstawiono hello tooinitiate dwa sposoby uruchomienia przepływu pracy:  
  
-   Wyzwalacz sondowania  

-   Wyzwalacz wypychania - przez wywołanie hello [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Wszystkich wyzwalaczy zawierać tych elementów najwyższego poziomu:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Typy wyzwalaczy i ich dane wejściowe  

Można używać tych typów wyzwalaczy:
  
-   **Żądanie** \- sprawia, że aplikacja logiki hello punktu końcowego dla toocall możesz  
  
-   **Cykl** \- uruchamiany zgodnie z harmonogramem zdefiniowanym  
  
-   **HTTP** \- sonduje punkt końcowy HTTP sieci web. Hello HTTP punktu końcowego musi być zgodna określonym kontraktem wyzwalająca tooa \- przy użyciu 202\-wzorca asynchronicznego, lub tablicę  
  
-   **ApiConnection** \- wyzwolenia ankiety, takich jak hello HTTP, jednak jego zalet hello [zarządzany przez firmę Microsoft interfejsy API](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- otwiera jako punkt końcowy, podobne toohello ręczne wyzwalacza, jednak również wywołuje limit tooa określony adres URL tooregister i wyrejestrować  
  
-   **ApiConnectionWebhook** \- działa jak hello wyzwalacza HTTPWebhook dzięki wykorzystaniu hello zarządzany przez firmę Microsoft interfejsy API       
    Każdy typ wyzwalacza ma inny zestaw **dane wejściowe** definiuje zachowanie.  
  
## <a name="request-trigger"></a>Wyzwalacz żądania  

Tego wyzwalacza służy jako punkt końcowy, który należy wywołać za pomocą żądania HTTP tooinvoke aplikacji logiki. Wyzwalacz żądania wygląda następująco:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Istnieje również opcjonalny właściwości o nazwie **schematu**:  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|Schemat|Nie|Weryfikuje żądanie przychodzące hello schematu JSON. Przydatne w przypadku kolejnych kroków wiedzieć, który tooreference właściwości Pomoc.|

tooinvoke ten punkt końcowy należy toocall hello *listCallbackUrl* interfejsu API. Zobacz [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Wyzwalacz cyklu  

Wyzwalacz cyklu jest jedną, która będzie uruchamiana na zdefiniowanym harmonogramem. Takie wyzwalacz może wyglądać w tym przykładzie:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Jak widać, jest prosty sposób toorun przepływ pracy.  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|frequency|Tak|Jak często hello wyzwalacza wykonuje. Używać tylko jednej z następujących wartości: sekundy, minuty, godziny, dnia, tygodnia, miesiąc lub rok|  
|interval|Tak|Interwał hello podana częstotliwość cyklu hello|  
|startTime|Nie|Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.|  
|Strefa czasowa|Brak|Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.|  
  
Można również zaplanować toostart wyzwalacza w pewnym momencie w przyszłości hello wykonywania. Na przykład jeśli chcesz toostart co tydzień raport w każdy poniedziałek można zaplanować toostart aplikacji logiki hello w każdy poniedziałek, tworząc następujące wyzwalacza hello:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>Wyzwalacz HTTP  

HTTP wyzwalacze sondowania określony punkt końcowy i hello odpowiedzi toodetermine Sprawdź, czy mają zostać wykonane hello przepływu pracy. Obiekt danych wejściowych Hello przyjmuje hello zbiór tooconstruct wymagane parametry połączenia HTTP:  
  
|Nazwa elementu|Wymagane|Opis|Typ|  
|----------------|------------|---------------|--------|  
|— Metoda|Tak|Może być jedną z następujących metod HTTP hello: GET, POST, PUT, DELETE, poprawki lub HEAD|Ciąg|  
|Identyfikator URI|Tak|Witaj punkt końcowy http lub https, który jest wywoływana. Maksymalnie 2 kilobajtów.|Ciąg|  
|— zapytania|Nie|Obiekt reprezentujący adres URL toohello tooadd hello kwerendy parametrów. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.|Obiekt|  
|Nagłówki|Nie|Obiekt reprezentujący każdego hello nagłówki, które są wysyłane żądania toohello. Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Obiekt|  
|Treści|Nie|Obiekt reprezentujący ładunku hello, wysyłany toohello punktu końcowego.|Obiekt|  
|retryPolicy|Nie|Obiekt, który można dostosować zachowanie przy ponownych prób hello 4xx lub 5xx błędów.|Obiekt|  
|Uwierzytelnianie|Nie|Reprezentuje metodę hello hello żądania uwierzytelniania. Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority` domyślnie ta wartość jest `https://login.windows.net` gdy nie jest określony, można używać różnych odbiorców, takich jak`https://login.windows\-ppe.net`|Obiekt|  
  
Witaj wyzwalacza HTTP wymaga hello tooconform HTTP API z określonym wzorcem toowork z aplikacji logiki. Wymaga hello następujące pola:  
  
|Odpowiedź|Opis|  
|------------|---------------|  
|Kod stanu|Kod stanu 200 \(OK\) toocause Uruchom. Każdy kod stanu nie powoduje uruchomienia.|  
|Spróbuj ponownie\-po nagłówka|Liczba sekund do aplikacji logiki hello ponownie sonduje hello punktu końcowego.|  
|Nagłówek lokalizacji|Witaj toocall adres URL na powitania dalej interwału sondowania. Jeśli nie zostanie określony, oryginalny adres URL hello jest używany.|  
  
Oto kilka przykładów różne zachowania dla różnych typów żądań:  
  
|Kod odpowiedzi|Spróbuj ponownie\-po|Zachowanie|  
|-----------------|----------------|------------|  
|200|\(Brak\)|Nie prawidłowy wyzwalacza, ponów próbę\-po sond dla następnego żądania hello jest nigdy nie hello wymagane lub inny aparat.|  
|202|60|Nie wyzwalają hello przepływu pracy. Witaj następnej próbie odbywa się w jednej minuty.|  
|200|10|Uruchamianie przepływu pracy hello i sprawdź ponownie więcej zawartości za 10 sekund.|  
|400|\(Brak\)|Nieprawidłowe żądanie, nie uruchamiaj hello przepływu pracy. W przypadku nie **ponów zasad** zdefiniowany, zostanie użyty hello domyślne zasady. Po osiągnięciu hello liczby ponownych prób hello wyzwalacz nie jest już prawidłowy.|  
|500|\(Brak\)|Błąd serwera, nie uruchamiaj hello przepływu pracy.  W przypadku nie **ponów zasad** zdefiniowany, zostanie użyty hello domyślne zasady. Po osiągnięciu hello liczby ponownych prób hello wyzwalacz nie jest już prawidłowy.|  
  
dane wyjściowe Hello wyzwalacza HTTP wyglądać w tym przykładzie:  
  
|Nazwa elementu|Opis|Typ|  
|----------------|---------------|--------|  
|Nagłówki|Witaj nagłówki odpowiedzi http hello.|Obiekt|  
|Treści|Treść Hello hello odpowiedzi http.|Obiekt|  
  
## <a name="api-connection-trigger"></a>Połączenie z interfejsem API wyzwalacza  

Witaj interfejsu API połączenia wyzwalacz jest podobne wyzwalacza HTTP toohello w jego podstawowych funkcji. Jednak parametry hello identyfikowanie akcji hello są różne. Oto przykład:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Nazwa elementu|Wymagane|Typ|Opis|  
|----------------|------------|--------|---------------|  
|Host|Tak||Witaj ApiApp hostowana bramy i identyfikator.|  
|— Metoda|Tak|Ciąg|Może być jedną z następujących metod HTTP hello: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**|  
|— zapytania|Nie|Obiekt|Reprezentuje hello zapytania parametry toobe dodać toohello adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello. Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek hello, wysyłany toohello punktu końcowego.|  
|retryPolicy|Nie|Obiekt|Umożliwia zachowanie ponawiania hello toocustomize 4xx lub 5xx błędów.|  
|Uwierzytelnianie|Nie|Obiekt|Reprezentuje metodę hello hello żądania uwierzytelniania. Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
Witaj właściwości hosta są:  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|runtimeUrl interfejsu API|Tak|punkt końcowy Hello hello zarządzanego interfejsu API.|  
|Nazwa połączenia||Musi być odwołanie tooa parametr o nazwie `$connection` i jest nazwą hello hello zarządzane połączenia interfejsu API, które hello używa przepływu pracy.|
  
dane wyjściowe Hello wyzwalacza połączenia interfejsu API są:
  
|Nazwa elementu|Typ|Opis|  
|----------------|--------|---------------|  
|Nagłówki|Obiekt|Witaj nagłówki odpowiedzi http hello.|  
|Treści|Obiekt|Treść Hello hello odpowiedzi http.|  
  
## <a name="httpwebhook-trigger"></a>Wyzwalacz HTTPWebhook  

Otwiera wyzwalacza HTTPWebhook Hello punktu końcowego, podobne toohello wyzwalacza ręczne, ale hello wyzwalacza HTTPWebhook również uwidacznia tooa określony adres URL tooregister i wyrejestrować. Oto przykład co wyzwalacz HTTPWebhook może wyglądać tak:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Wiele z tych sekcji są opcjonalne i zachowanie hello hello elementu Webhook jest zależna od sekcje są udostępniane lub pominięta.  
właściwości elementu Webhook Hello są następujące:  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|Subskrypcja|Nie|Witaj wychodzące żądania, które jest wywoływane, gdy wyzwalacz hello jest tworzony i wykonuje hello początkowej rejestracji.|  
|Anulowanie subskrypcji|Nie|Witaj wychodzące żądanie usunięcia hello wyzwalacza.|  
  
-   **Subskrypcja** jest Witaj wychodzące połączenia, który wprowadził toostart tooevents nasłuchiwania. To wywołanie rozpoczyna się od hello są tego samego zestawu parametrów, które hello normalne akcji HTTP. Ten wychodzących wywołanie żadnych hello czas przepływu pracy zmiany w dowolny sposób, na przykład po każdej zmianie poświadczeń hello są wycofane lub zmiany parametrów wejściowych hello wyzwalacza.
  
    toosupport to wywołanie, jest nowa funkcja: `@listCallbackUrl()`. Ta funkcja zwraca unikatowy adres URL dla tego wyzwalacza określonych w tym przepływie pracy. Reprezentuje hello Unikatowy identyfikator dla punktów końcowych hello, używających hello usługi REST.  
  
-   **Anulowanie subskrypcji** jest wywoływane, gdy operacja renderuje tego wyzwalacza nieprawidłowe, w tym:  
  
    -   Usuwanie lub wyłączanie hello wyzwalacza  
  
    -   Usuwanie lub wyłączanie hello przepływu pracy  
  
    -   Usuwanie lub wyłączanie hello subskrypcji  
  
    Aplikacja logiki Hello automatycznie wywołuje hello subskrypcję akcji. Parametry Hello są funkcja toothis hello sam hello wyzwalacza HTTP.  
  
    Witaj dane wyjściowe wyzwalacza HTTPWebhook hello są hello treść żądania przychodzące hello:  
  
|Nazwa elementu|Typ|Opis|  
|-----------------|--------|---------------|  
|Nagłówki|Obiekt|nagłówki Hello hello żądania http.|  
|Treści|Obiekt|Treść Hello hello żądania http.|  

Można określić limity akcji elementu webhook w hello taki sam jak [limity asynchroniczne HTTP](#asynchronous-limits).
  

## <a name="conditions"></a>Warunki  

Dla dowolnego wyzwalacza można użyć co najmniej jeden toodetermine warunki czy uruchamiania przepływu pracy hello lub nie. Na przykład:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

W takim przypadku hello tylko wyzwalaczy raportu podczas przepływu hello `sendReports` parametr ma wartość tootrue. Na koniec warunków może odwoływać się hello kod stanu hello wyzwalacza. Na przykład należy można rozpocząć wyłączyć przepływ pracy tylko w przypadku witryny sieci Web zwraca kod stanu 500, w następujący sposób:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Gdy dowolne wyrażenie odwołuje się kod stanu hello wyzwalacza hello \(w żaden sposób\), hello domyślne zachowanie \(wyzwalacza tylko na 200 \(OK\) \) zostanie zastąpiony. Na przykład, jeśli chcesz tootrigger na kod stanu 200 i kod stanu 201 masz tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` jako warunek.  
  
## <a name="start-multiple-runs-for-a-request"></a>Uruchom wielu uruchomień dla żądania

tookick poza wielu uruchomień dla pojedynczego żądania `splitOn` jest przydatne, na przykład, jeśli chcesz toopoll punktu końcowego, który może mieć wiele nowych elementów między interwałami sondowania.
  
Z `splitOn`, określ właściwość hello ładunku odpowiedzi hello zawierający hello tablicę elementów, z których każdy ma toostart toouse Uruchom hello wyzwalacza. Załóżmy na przykład, że masz interfejs API, który zwraca powitania po odpowiedzi:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
Aplikację logiki tylko musi hello wierszy zawartości, więc można konstruować wyzwalacz tak jak ten przykład:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Następnie w definicji przepływu pracy hello, `@triggerBody().name` zwraca `mycoolrow` dla pierwszego uruchomienia hello i `another row` dla hello drugim przebiegu. wygląd danych wyjściowych wyzwalacza Hello tak jak ten przykład:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Dlatego jeśli używasz `SplitOn`, nie można pobrać właściwości hello, które są poza hello tablicy, w tym przypadku hello `Status` pola.  
  
> [!NOTE]  
> W tym przykładzie używamy hello `?` tooavoid stanie operator toobe awarii, jeśli hello `Rows` nie ma właściwości. 
  
## <a name="single-run-instance"></a>Pojedyncze wystąpienie wykonywania

Można skonfigurować wyzwalacze, które ma fire tooonly właściwości cyklu, jeśli wszystkie aktywnej przebiegi została ukończona. W przypadku podczas uruchamiania w trakcie zaplanowanego cyklu wyzwalacz hello pomija i czekać na powitania następnego zaplanowanego cyklu interwału toocheck ponownie.

Można to ustawienie można skonfigurować za pomocą opcji operacji hello:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Typy i dane wejściowe  

Istnieje wiele typów działań, każde z nich unikatowe zachowanie. Akcje kolekcji może zawierać wielu akcji w obrębie samego.

### <a name="standard-actions"></a>Działania standardowe  

-   **HTTP** ta akcja wymaga punktu końcowego HTTP sieci web.  
  
-   **ApiConnection** \- ta akcja działa jak hello akcji HTTP, ale używa hello API zarządzany przez firmę Microsoft.  
  
-   **ApiConnectionWebhook** \- jak HTTPWebhook, ale używa hello API zarządzany przez firmę Microsoft.  
  
-   **Odpowiedź** \- tej akcji określa odpowiedzi dla połączenia przychodzącego.  
  
-   **Poczekaj** \- ta akcja proste czeka stałą lub określonego czasu.  
  
-   **Przepływ pracy** \- tej akcji reprezentuje zagnieżdżony przepływ pracy.  

-   **Funkcja** \- tej akcji reprezentuje funkcję platformy Azure.

### <a name="collection-actions"></a>Akcje kolekcji

-   **Zakres** \- ta akcja jest logiczne grupowanie innych działań.

-   **Warunek** \- ta akcja oblicza wyrażenie i wykonuje hello odpowiednich wyników w oddziale firmy.

-   **Instrukcja ForEach** \- ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu.

-   **Dopóki** \- ta akcja pętli wykonuje działania wewnętrzny dopóki tootrue powoduje warunek.
  
Każdy typ działania ma inny zestaw **dane wejściowe** definiującą zachowanie akcji.  
  
## <a name="http-action"></a>Akcja HTTP  

HTTP działania Wywołaj określony punkt końcowy i toodetermine odpowiedzi hello Sprawdź, czy powinno być ono uruchomione hello przepływu pracy. Witaj **dane wejściowe** obiektu przyjmuje hello zbiór wywołania hello HTTP tooconstruct wymaganych parametrów:  
  
|Nazwa elementu|Wymagane|Typ|Opis|  
|----------------|------------|--------|---------------|  
|— Metoda|Tak|Ciąg|Może być jedną z następujących metod HTTP hello: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**|  
|Identyfikator URI|Tak|Ciąg|Witaj punkt końcowy http lub https, który jest wywoływana. Maksymalna długość wynosi 2 kilobajtów.|  
|— zapytania|Nie|Obiekt|Reprezentuje adres URL toohello tooadd hello kwerendy parametrów. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello. Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek hello, wysyłany toohello punktu końcowego.|  
|retryPolicy|Nie|Obiekt|Umożliwia dostosowanie hello zachowanie ponownych prób dla 4xx lub 5xx błędów.|  
|operationsOptions|Nie|Ciąg|Definiuje zestaw hello toooverride specjalnego zachowania.|  
|Uwierzytelnianie|Nie|Obiekt|Reprezentuje metodę hello hello żądania uwierzytelniania. Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority`. Domyślnie jest to `https://login.windows.net` gdy nie jest określony, ale możesz użyć innych grup odbiorców, takich jak`https://login.windows\-ppe.net`|  
  
Akcje HTTP \(i połączenie z interfejsem API\) Obsługa akcji ponów zasad. Zasady ponawiania stosuje toointermittent błędów, jak stan HTTP jest określony kodów 408 429 i 5xx w wyjątki łączności tooany dodanie. Ta zasada jest opisana przy użyciu hello *retryPolicy* obiekt zdefiniowany w sposób pokazany poniżej:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Interwał ponawiania prób Hello jest określona w formacie ISO 8601 hello. Ten interwał ma domyślne i minimalna wartość 20 sekund, podczas hello wartość maksymalna to jedna godzina. Hello domyślne, a maksymalna liczba ponowień to cztery godziny. Jeśli nie określono definicji zasad ponawiania hello, `fixed` strategii jest używany z domyślnej wartości interwału i liczba ponownych prób. zasady ponawiania hello toodisable, ustaw jej typ zbyt`None`.  
  
Na przykład hello następującej akcji ponowi próbę pobrano najnowsze wiadomości powitania dwa razy, jeśli występują sporadyczne awarie, dla wszystkich trzech wykonaniami, z 30-sekundowe opóźnienie między kolejnymi próbami:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Asynchroniczne wzorce

Domyślnie wszystkie działania oparte na protokole HTTP obsługuje hello wzorzec standardowych operacji asynchronicznej. Dlatego jeśli powitania serwera zdalnego wskazuje Żądanie hello jest zaakceptowano do przetwarzania z 202 \(zaakceptowane\) odpowiedzi, aparat Logic Apps hello śledzi sondowania hello adres URL określony w nagłówku lokalizacji odpowiedź hello aż do osiągnięcia terminal Stan \(bez\-202 odpowiedzi\).  
  
zachowanie asynchroniczne hello toodisable wcześniej opisane, ustaw `DisableAsyncPattern` opcję hello akcji w danych wejściowych. W takim przypadku dane wyjściowe hello akcji hello jest oparta na hello początkowej 202 odpowiedzi z serwera hello.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Limity asynchroniczne

Asynchroniczny wzorzec może być ograniczone w jego czas trwania tooa określonego interwału czasu.  Jeśli hello czas upływający bez osiągnięcia terminali stanu, zostaną oznaczone jako hello stan akcji hello `Cancelled` przy użyciu kodu `ActionTimedOut`.  limit czasu limit Hello jest określony w formacie ISO 8601.  Można określić limity z hello następującej składni:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>Połączenie z interfejsem API  

Połączenie z interfejsem API jest akcja, która odwołuje się do łącznika zarządzany przez firmę Microsoft.
Ta akcja wymaga odwołania tooa prawidłowe połączenie, a informacje o hello interfejsu API i parametrów wymaganych.

|Nazwa elementu|Wymagane|Typ|Opis|  
|----------------|------------|--------|---------------|  
|Host|Tak|Obiekt|Reprezentuje hello łącznika informacje, takie jak hello runtimeUrl i odwołanie toohello obiektu połączenia|
|— Metoda|Tak|Ciąg|Może być jedną z następujących metod HTTP hello: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**|  
|Ścieżka|Tak|Ciąg|Ścieżka Hello operacji hello interfejsu API.|  
|— zapytania|Nie|Obiekt|Reprezentuje adres URL toohello tooadd hello kwerendy parametrów. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello. Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek hello, wysyłany toohello punktu końcowego.|  
|retryPolicy|Nie|Obiekt|Umożliwia dostosowanie hello zachowanie ponownych prób dla 4xx lub 5xx błędów.|  
|operationsOptions|Nie|Ciąg|Definiuje zestaw hello toooverride specjalnego zachowania.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>Połączenie z interfejsem API akcji elementu webhook

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Można określić limity akcji elementu webhook w hello taki sam jak [limity asynchroniczne HTTP](#asynchronous-limits).
  
## <a name="response-action"></a>Akcja odpowiedzi  

Ten typ akcji zawiera hello ładunku całej odpowiedzi z żądania HTTP i obejmuje statusCode, treści i nagłówków:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
Akcja odpowiedzi Hello ma specjalne ograniczenia, które nie stosuje określone akcje tooother. W szczególności:  
  
-   Akcje reakcji nie może być równoległe w definicji, ponieważ wymagane jest żądanie przychodzące toohello deterministyczne odpowiedzi.  
  
-   Po osiągnięciu akcji odpowiedzi po otrzymaniu odpowiedzi hello przychodzące żądanie akcji hello jest uznawany za nie powiodło się \(konflikt\), i w związku z tym jest hello Uruchom `Failed`.  
  
-   Przepływ pracy z akcjami odpowiedzi nie może mieć `splitOn` w jego wyzwalacza jedno wywołanie powoduje, że wiele przebiegów. W związku z tym to powinny być weryfikowane podczas przepływu hello jest PUT i Przyczyna nieprawidłowe żądanie.  
  
## <a name="wait-action"></a>Poczekaj akcji  

Witaj `wait` akcji wstrzymuje wykonywanie przepływu pracy dla hello określonego interwału. Na przykład toowait 15 minut, można użyć ta Wstawka kodu:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
Alternatywnie toowait do określonego momentu w czasie, można użyć w tym przykładzie:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> czas oczekiwania Hello albo można użyć hello **interwał** obiektu lub hello **do momentu** obiektu, ale nie oba.  
  
|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|interval|Nie|Obiekt|Witaj poczekaj oparte na czas trwania.|  
|Interwał|Tak|Ciąg|Jeden z tych przedziałów: sekundy, minuty, godziny, dnia, tygodnia, miesiąca, roku.|  
|Liczba interwale|Tak|Ciąg|Czas trwania oparte na powitania podane wewnętrzny jednostki.|  
|do czasu|Nie|Obiekt|Witaj poczekaj oparte na punkt w czasie trwania.|  
|do sygnatury czasowej|Tak|Ciąg|Ciąg &#124; hello punktu w czasie w formacie UTC wygaśnięcia hello oczekiwania.|  

## <a name="query-action"></a>Akcja kwerendy

Witaj `query` akcja umożliwia filtrowanie na podstawie warunku tablicy. Na przykład numery tooselect jest większa niż 2, można:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Witaj dane wyjściowe hello `query` tablicę, która ma elementy z tablicy wejściowej hello, które spełniają warunek hello jest akcja.

> [!NOTE]
> Jeśli wartości nie spełniają hello `where` warunku, hello wyniku jest pusta tablica.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|Z|Tak|Tablica|Tablica źródłowa Hello.|
|gdzie|Tak|Ciąg|Witaj warunku tooapply tooeach elementu tablicy źródłowej hello.|

## <a name="select-action"></a>Wybierz akcję

Witaj `select` pozwala projektów każdy element tablicy na nową wartość.
Na przykład tooconvert jako tablica liczb na tablicę obiektów, można użyć:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Witaj dane wyjściowe hello `select` tablicę, która ma hello samą liczność hello tablicy wejściowej z każdym elementem przekształcone jako określone hello jest akcja `select` właściwości. Jeśli dane wejściowe hello jest pusta tablica, dane wyjściowe hello jest również pustą tablicę.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|Z|Tak|Tablica|Tablica źródłowa Hello.|
|Wybierz|Tak|Dowolne|Witaj projekcji tooapply tooeach elementu tablicy źródłowej hello.|

## <a name="terminate-action"></a>Zakończenie akcji

Hello akcji Zakończenie zatrzymuje wykonywanie hello przepływu pracy, przerywanie wszystkie akcje locie i pomija wszystkie pozostałe akcje. Na przykład tooterminate Uruchom ze stanem ****, można użyć następującego fragmentu hello:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Akcje już ukończone nie dotyczy hello przerwanie działania.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|runStatus|Tak|Ciąg|obiekt docelowy Hello stan uruchomienia. Albo **nie powiodło się** lub **anulowane**.|
|runError|Nie|Obiekt|Szczegóły błędu Hello. Tylko obsługiwane w przypadku **runStatus** ustawiono zbyt****.|
|Kod runError|Nie|Ciąg|Witaj, uruchom kod błędu.|
|komunikat runError|Nie|Ciąg|Witaj, uruchom komunikat o błędzie.|

## <a name="compose-action"></a>Redagowanie akcji

Witaj akcji tworzenia umożliwia utworzenia dowolnego obiektu. dane wyjściowe Hello hello tworzą akcji jest wynikiem hello oceny jej danych wejściowych. Na przykład można użyć hello tworzą dane wyjściowe toomerge akcji wiele działań:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Witaj **Redaguj** akcji mogą być używane tooconstruct żadnych danych wyjściowych, w tym obiektów, tablic i innego typu obsługiwane przez logikę aplikacji, takich jak XML i pliku binarnego.

## <a name="table-action"></a>Akcja tabeli

Witaj `table` pozwala tooconvert jako tablicę elementów do **CSV** lub **HTML** tabeli.

Załóżmy, że @triggerBodyjest)

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

Natomiast akcja hello można zdefiniować jako

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

dałby w efekcie Hello powyżej

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>jabłek</td></tr><tr><td>1</td><td>Pomarańcze</td></tr></tbody></table>"

W tabeli hello toocustomize kolejności można określić kolumny hello jawnie. Na przykład:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

dałby w efekcie Hello powyżej

<table><thead><tr><th>Tworzy identyfikator</th><th>description</th></tr></thead><tbody><tr><td>0</td><td>Nowa jabłek</td></tr><tr><td>1</td><td>świeżych pomarańczy</td></tr></tbody></table>"

Jeśli hello `from` wartość właściwości jest pusta tablica, dane wyjściowe hello jest pusta tabela.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|Z|Tak|Tablica|Tablica źródłowa Hello.|
|Format|Tak|Ciąg|Witaj format, albo **CSV** lub **HTML**.|
|kolumny|Nie|Tablica|Witaj kolumny. Umożliwia toooverride hello domyślnego kształtu hello tabeli.|
|Nagłówek kolumny|Nie|Ciąg|Nagłówek Hello hello kolumny.|
|wartość w kolumnie|Tak|Ciąg|wartość Hello hello kolumny.|

## <a name="workflow-action"></a>Działania przepływu pracy   

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Identyfikator hosta|Tak|Ciąg|Identyfikator zasobu Hello hello przepływu pracy, które mają toocall.|  
|Nazwa_wyzwalacza hosta|Tak|Ciąg|Nazwa Hello hello wyzwalacza, które mają tooinvoke.|  
|— zapytania|Nie|Obiekt|Reprezentuje adres URL toohello tooadd hello kwerendy parametrów. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello. Na przykład tooset hello język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek hello wysyłane toohello punktu końcowego.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Sprawdzanie dostępu jest podejmowana hello przepływu pracy \(dokładniej, wyzwalacz hello\), co oznacza muszą uzyskać dostęp toohello przepływu pracy.  
  
Witaj danych wyjściowych ze hello `workflow` akcji są oparte na zdefiniowane w hello `response` działań w przepływie pracy podrzędny hello. Jeśli nie zdefiniowano żadnego `response` akcji, a następnie hello dane wyjściowe są puste.  

## <a name="function-action"></a>Akcja — funkcja   

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|id — funkcja|Tak|Ciąg|Identyfikator zasobu Hello hello funkcji, które mają tooinvoke.|  
|— Metoda|Nie|Ciąg|Hello metoda HTTP używana funkcja hello tooinvoke. Domyślnie jest `POST` gdy nie został określony.|  
|— zapytania|Nie|Obiekt|Reprezentuje adres URL toohello tooadd hello kwerendy parametrów. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` toohello adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje wszystkich nagłówków hello, które są wysyłane żądania toohello. Na przykład tooset hello język i typ na żądanie: `"headers" : { "Accept-Language": "en-us" }`.|  
|Treści|Nie|Obiekt|Reprezentuje ładunek hello wysyłane toohello punktu końcowego.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Podczas zapisywania aplikacji logiki hello wykonać testy na powitania odwołuje się do funkcji:
-   Należy toohave dostępu toohello funkcji.
-   Tylko standardowy wyzwalacza HTTP lub ogólny wyzwalacza elementu webhook JSON jest dozwolone.
-   Nie powinna mieć żadnej trasy zdefiniowane.
-   Tylko "funkcji" i "anonymous" autoryzacji na poziomie jest dozwolone.

adres URL wyzwalacza Hello jest pobrać, w pamięci podręcznej i używany w czasie wykonywania. Dlatego jeśli żadnej operacji unieważnia URL hello w pamięci podręcznej, hello akcja zakończy się niepowodzeniem w czasie wykonywania. toowork wokół, Zapisz hello aplikacji logiki ponownie, co będzie powodować tooretrieve aplikacji logiki i pamięci podręcznej adres URL wyzwalacza hello ponownie.

## <a name="collection-actions-scopes-and-loops"></a>Akcje kolekcji (zakresy i pętle)

Niektóre typy działań mogą zawierać działania w ramach samodzielnie. Odwołanie do działań w ramach kolekcji można odwoływać się bezpośrednio poza hello kolekcji. Jeśli zdefiniowano `http` w zakresie `@body('http')` jest nadal ważny w dowolnym miejscu w przepływie pracy. Akcje w ramach kolekcji można `runAfter` tylko innych działań w ramach hello tej samej kolekcji.

## <a name="scope-action"></a>Akcja zakresu

Witaj `scope` pozwala logicznie grupy działań w przepływie pracy.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Tooexecute wewnętrzny akcje w zakresie hello|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>Akcja ForEach

Ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu. Domyślnie program hello foreach pętla jest wykonywana równolegle (20 wykonaniami równolegle w czasie). Można ustawić zasady wykonywania przy użyciu hello `operationOptions` parametru.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Tooexecute wewnętrzny akcje w ramach hello pętli|
|Instrukcja foreach|Tak|Ciąg|Witaj tooiterate tablicy za pośrednictwem|
|operationOptions|Brak|Ciąg|Wszystkie opcje operacji zachowanie. Aktualnie obsługuje tylko `sequential` iteracji tooexecute sekwencyjnie (domyślne zachowanie to równoległych)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Do działania

Ta akcja pętli wykonuje akcje wewnętrzny dopóki tootrue powoduje warunek.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Tooexecute wewnętrzny akcje w ramach hello pętli|
|wyrażenie|Tak|Ciąg|Witaj tooevaluate wyrażenie po każdej iteracji|
|Limit|Tak|Obiekt|limity Hello hello pętli — co najmniej jeden limit musi być zdefiniowana|
|Liczba|Brak|int|Hello limit toohello liczba iteracji, które mogą być wykonywane|
|timeout|Brak|Ciąg|Witaj limitu czasu dla jak długo powinien pętli.  Formacie ISO 8601|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Warunki — Jeśli akcja

Witaj `If` pozwala ocenić warunku i wykonywanie gałęzi oparte na czy hello wynikiem wyrażenia jest zbyt`true`.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Tooexecute wewnętrzny akcje, gdy wyrażenie zbyt`true`|
|wyrażenie|Tak|Ciąg|Witaj tooevaluate wyrażenia|
|else|Brak|Obiekt|Tooexecute wewnętrzny akcje, gdy wyrażenie zbyt`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Witaj poniższej tabeli przedstawiono przykłady warunków użycia wyrażeń w akcji:  
  
|Wartość JSON|wynik|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Żadnej wartości, które są używane do oceny tootrue powoduje, że toopass tego warunku. Obsługiwane są tylko wyrażenia logiczne. tooconvert innych typów tooBoolean, użyj funkcji `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Porównanie funkcji są obsługiwane. Przykładowo hello tutaj hello akcji tylko wykonuje się, gdy dane wyjściowe hello act1 jest większy niż próg hello.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Funkcje logiki są również obsługiwane toocreate zagnieżdżonych wyrażeń logicznych. W takim przypadku hello operacja zostanie wykonana, gdy dane wyjściowe hello act1 jest powyżej wartości progowej hello lub poniżej 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Toocheck funkcje tablicy można użyć, jeśli tablicy nie ma żadnych elementów. W takim przypadku hello operacja zostanie wykonana, gdy hello błędy tablica jest pusta.| 
|`"expression": "parameters('hasSpecialAction')"`|Błąd — nie jest prawidłowym warunku, ponieważ @ jest wymagany dla warunków.|  
  
Jeśli wynikiem warunku jest pomyślnie, warunek hello jest oznaczony jako `Succeeded`. Akcje w ramach jednej hello `actions` lub `else` obiektów ocenić za`Succeeded` po wykonaniu i zakończyło się pomyślnie, `Failed` po wykonaniu i nie powiodło się, lub `Skipped` po gałąź, nie została wykonana.

## <a name="next-steps"></a>Następne kroki

[Interfejs API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)
