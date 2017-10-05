---
title: "Działania przepływu pracy i wyzwalaczy - Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Działania przepływu pracy i Wyzwalacze dla usługi Azure Logic Apps

Aplikacje logiki składają się z wyzwalacze i akcje. Istnieją typy sześciu wyzwalaczy. Każdy typ ma inny interfejs i inaczej. Możesz także dowiedzieć się inne szczegóły sprawdzając szczegóły [język definicji przepływu pracy](logic-apps-workflow-definition-language.md).  
  
W dalszej Dowiedz się więcej o wyzwalacze i akcje i jak można ich używać do tworzenia aplikacji logiki, aby ulepszyć Twoje procesów biznesowych i przepływów pracy.  
  
### <a name="triggers"></a>Wyzwalacze  

Wyzwalacz określa wywołania, które mogą inicjować uruchomienia przepływu pracy aplikacji logiki. Poniżej przedstawiono dwa różne sposoby, aby zainicjować do uruchomienia przepływu pracy:  
  
-   Wyzwalacz sondowania  

-   Wyzwalacz wypychania - wywołując [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)  
  
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
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Typy wyzwalaczy i ich dane wejściowe  

Można używać tych typów wyzwalaczy:
  
-   **Żądanie** \- sprawia, że aplikację logiki punktu końcowego, aby wywołać  
  
-   **Cykl** \- uruchamiany zgodnie z harmonogramem zdefiniowanym  
  
-   **HTTP** \- sonduje punkt końcowy HTTP sieci web. Punkt końcowy HTTP musi być zgodna z określonym kontraktem wyzwalająca \- przy użyciu 202\-wzorca asynchronicznego, lub tablicę  
  
-   **ApiConnection** \- wyzwolenia ankiety, takich jak HTTP, jednak ją korzysta z [zarządzany przez firmę Microsoft interfejsy API](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- otwiera jako punkt końcowy, podobnie jak ręczne wyzwalacza, jednak również wywołuje określony adres URL do rejestrowania i wyrejestrowania  
  
-   **ApiConnectionWebhook** \- Operates, takich jak wyzwalacza HTTPWebhook dzięki wykorzystaniu interfejsów API zarządzany przez firmę Microsoft       
    Każdy typ wyzwalacza ma inny zestaw **dane wejściowe** definiuje zachowanie.  
  
## <a name="request-trigger"></a>Wyzwalacz żądania  

Tego wyzwalacza służy jako punkt końcowy, który należy wywołać za pomocą żądania HTTP do wywołania aplikacji logiki. Wyzwalacz żądania wygląda następująco:  
  
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
|Schemat|Nie|Schematu JSON, która weryfikuje żądanie przychodzące. Przydatne w przypadku myśl kolejnych kroków znać właściwości, które ma dotyczyć odwołanie.|

Aby wywołać ten punkt końcowy, należy wywołać *listCallbackUrl* interfejsu API. Zobacz [interfejsu API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows).  
  
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

Jak widać, jest prosty sposób, aby uruchomić przepływ pracy.  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|częstotliwość|Tak|Jak często wykonuje wyzwalacza. Używać tylko jednej z następujących wartości: sekundy, minuty, godziny, dnia, tygodnia, miesiąc lub rok|  
|Interwał|Tak|Interwał częstotliwości danego cyklu|  
|startTime|Nie|Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.|  
|Strefa czasowa|Brak|Jeśli czas rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, zostanie użyta tej strefy czasowej.|  
  
Można również zaplanować wyzwalacz można uruchomić wykonywania w pewnym momencie w przyszłości. Na przykład jeśli chcesz uruchomić raport co tydzień w każdy poniedziałek można zaplanować aplikację logiki, aby uruchomić każdy poniedziałek, tworząc następujące wyzwalacz:  

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

HTTP wyzwalacze sondowania określony punkt końcowy i sprawdź odpowiedzi, aby określić, czy można wykonać przepływu pracy. Obiekt dane wejściowe przyjmuje zbiór parametrów wymaganych do utworzenia połączenia HTTP:  
  
|Nazwa elementu|Wymagane|Opis|Typ|  
|----------------|------------|---------------|--------|  
|— Metoda|Tak|Może być jedną z następujących metod HTTP: GET, POST, PUT, DELETE, poprawki lub HEAD|Ciąg|  
|Identyfikator URI|Tak|Końcowy http lub https, która jest wywoływana. Maksymalnie 2 kilobajtów.|Ciąg|  
|— zapytania|Nie|Obiekt reprezentujący parametry zapytania, aby dodać do adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.|Obiekt|  
|Nagłówki|Nie|Obiekt reprezentujący listę nagłówków, które są wysyłane do żądania. Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Obiekt|  
|Treści|Nie|Obiekt reprezentujący ładunku, które są wysyłane do punktu końcowego.|Obiekt|  
|retryPolicy|Nie|Obiekt, który można dostosować zachowanie ponownych prób dla 4xx lub 5xx błędów.|Obiekt|  
|Uwierzytelnianie|Nie|Reprezentuje metodę uwierzytelniania żądania. Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority` domyślnie ta wartość jest `https://login.windows.net` gdy nie jest określony, można używać różnych odbiorców, takich jak`https://login.windows\-ppe.net`|Obiekt|  
  
Wyzwalacza HTTP wymaga interfejsu API HTTP był zgodny z określonym wzorcem do sprawnej współpracy z aplikacji logiki. Wymaga on następujące pola:  
  
|Odpowiedź|Opis|  
|------------|---------------|  
|Kod stanu|Kod stanu 200 \(OK\) spowodować do uruchomienia. Każdy kod stanu nie powoduje uruchomienia.|  
|Spróbuj ponownie\-po nagłówka|Liczba sekund do aplikacji logiki sonduje ponownie punkt końcowy.|  
|Nagłówek lokalizacji|Adres URL do wywołania w następnym interwału sondowania. Jeśli nie zostanie określony, używany jest oryginalny adres URL.|  
  
Oto kilka przykładów różne zachowania dla różnych typów żądań:  
  
|Kod odpowiedzi|Spróbuj ponownie\-po|Zachowanie|  
|-----------------|----------------|------------|  
|200|\(Brak\)|Nie prawidłowy wyzwalacza, ponów próbę\-po jest wymagane, lub #else aparat nigdy nie sonduje dla następnego żądania.|  
|202|60|Nie wyzwala przepływ pracy. Przy następnej próbie odbywa się w jednej minuty.|  
|200|10|Uruchamianie przepływu pracy i sprawdź ponownie więcej zawartości za 10 sekund.|  
|400|\(Brak\)|Nieprawidłowe żądanie, nie uruchamiaj przepływ pracy. W przypadku nie **ponów zasad** zdefiniowany, zostanie użyta domyślna zasada. Po osiągnięciu liczby ponownych prób wyzwalacz nie jest już prawidłowy.|  
|500|\(Brak\)|Błąd serwera, nie uruchamiaj przepływ pracy.  W przypadku nie **ponów zasad** zdefiniowany, zostanie użyta domyślna zasada. Po osiągnięciu liczby ponownych prób wyzwalacz nie jest już prawidłowy.|  
  
Dane wyjściowe wyzwalacza HTTP wyglądać w tym przykładzie:  
  
|Nazwa elementu|Opis|Typ|  
|----------------|---------------|--------|  
|Nagłówki|Nagłówki odpowiedzi http.|Obiekt|  
|Treści|Treść odpowiedzi http.|Obiekt|  
  
## <a name="api-connection-trigger"></a>Połączenie z interfejsem API wyzwalacza  

Wyzwalacz połączenia interfejsu API jest podobny do wyzwalacza HTTP w jego podstawowych funkcji. Jednak parametry do identyfikacji akcji są różne. Oto przykład:  
  
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
|Host|Tak||ApiApp hostowana bramy i identyfikator.|  
|— Metoda|Tak|Ciąg|Może być jedną z następujących metod HTTP: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**|  
|— zapytania|Nie|Obiekt|Reprezentuje parametry zapytania, które mają zostać dodane do adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje listę nagłówków, które są wysyłane do żądania. Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek, które są wysyłane do punktu końcowego.|  
|retryPolicy|Nie|Obiekt|Umożliwia dostosowanie zachowanie ponownych prób dla 4xx lub 5xx błędów.|  
|Uwierzytelnianie|Nie|Obiekt|Reprezentuje metodę uwierzytelniania żądania. Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
Właściwości hosta są:  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|runtimeUrl interfejsu API|Tak|Punkt końcowy zarządzanego interfejsu API.|  
|Nazwa połączenia||Musi być odwołaniem do parametru o nazwie `$connection` , a to nazwa zarządzanego połączenia interfejsu API, używanych przez przepływ pracy.|
  
Dostępne są następujące dane wyjściowe wyzwalacza połączenia interfejsu API:
  
|Nazwa elementu|Typ|Opis|  
|----------------|--------|---------------|  
|Nagłówki|Obiekt|Nagłówki odpowiedzi http.|  
|Treści|Obiekt|Treść odpowiedzi http.|  
  
## <a name="httpwebhook-trigger"></a>Wyzwalacz HTTPWebhook  

Wyzwalacz HTTPWebhook otwiera punkt końcowy jest podobny do ręcznego wyzwalacza, ale określony adres URL do rejestrowania i wyrejestrowania uwidacznia również HTTPWebhook wyzwalacza. Oto przykład co wyzwalacz HTTPWebhook może wyglądać tak:  

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

Wiele z tych sekcji są opcjonalne i zachowanie elementu Webhook jest zależna od sekcje są udostępniane lub pominięta.  
Właściwości elementu Webhook są następujące:  
  
|Nazwa elementu|Wymagane|Opis|  
|----------------|------------|---------------|  
|Subskrypcja|Nie|Żądania wychodzącego jest wywoływane, gdy wyzwalacza jest tworzony i wykonuje początkowe rejestracyjny.|  
|Anulowanie subskrypcji|Nie|Żądania wychodzącego po usunięciu wyzwalacza.|  
  
-   **Subskrypcja** jest wywołanie wychodzących, które ma na celu rozpoczyna nasłuchiwanie zdarzeń. To wywołanie rozpoczyna się od tego samego zestawu parametrów, które wykonują normalnego działania protokołu HTTP. Ta wychodzących wywołanie żadnego zmianie przepływu pracy w dowolny sposób, na przykład, jeśli poświadczenia zostały wycofane, lub zmień parametry wejściowe tego wyzwalacza.
  
    Aby zapewnić obsługę tego wywołania, jest nowa funkcja: `@listCallbackUrl()`. Ta funkcja zwraca unikatowy adres URL dla tego wyzwalacza określonych w tym przepływie pracy. Reprezentuje unikatowy identyfikator dla punktów końcowych, które używają usługi REST.  
  
-   **Anulowanie subskrypcji** jest wywoływane, gdy operacja renderuje tego wyzwalacza nieprawidłowe, w tym:  
  
    -   Usuwanie lub wyłączanie wyzwalacza  
  
    -   Usuwanie lub wyłączanie przepływu pracy  
  
    -   Usunięcie lub wyłączenie subskrypcji  
  
    Aplikacja logiki automatycznie wywołuje akcję anulowania subskrypcji. Parametry tej funkcji są takie same jak wyzwalacza HTTP.  
  
    Dane wyjściowe wyzwalacza HTTPWebhook są zawartość żądania przychodzącego, jeśli:  
  
|Nazwa elementu|Typ|Opis|  
|-----------------|--------|---------------|  
|Nagłówki|Obiekt|Nagłówki żądania http.|  
|Treści|Obiekt|Treść żądania http.|  

Można określić limity akcji elementu webhook w taki sam sposób jak [limity asynchroniczne HTTP](#asynchronous-limits).
  

## <a name="conditions"></a>Warunki  

Dla dowolnego wyzwalacza można użyć co najmniej jednego warunku można określić, czy przepływ pracy, należy uruchomić lub nie. Na przykład:  

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

W takim przypadku tylko wyzwalacze raportu podczas przepływu pracy `sendReports` parametr ma wartość true. Na koniec warunków może odwoływać się kod stanu wyzwalacza. Na przykład należy można rozpocząć wyłączyć przepływ pracy tylko w przypadku witryny sieci Web zwraca kod stanu 500, w następujący sposób:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Jeśli dowolne wyrażenie odwołuje się kod stanu wyzwalacza \(w żaden sposób\), domyślne zachowanie \(wyzwalacza tylko na 200 \(OK\) \) zostanie zastąpiony. Na przykład, jeśli chcesz wyzwolić na kod stanu 201 i kodem stanu 200, użytkownik musi zawierać: `@or(equals(triggers().code, 200),equals(triggers().code,201))` jako warunek.  
  
## <a name="start-multiple-runs-for-a-request"></a>Uruchom wielu uruchomień dla żądania

Aby rozpocząć poza wielu uruchomień dla pojedynczego żądania `splitOn` jest przydatne, na przykład, gdy chcesz przeprowadzać sondowanie punktu końcowego, który może mieć wiele nowych elementów między interwałami sondowania.
  
Z `splitOn`, określ właściwość ładunku odpowiedzi, który zawiera tablicę elementów, z których każdy ma być używany do uruchamiania wykonywania wyzwalacza. Załóżmy na przykład, że masz interfejs API, który zwraca następującą odpowiedź:  
  
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
  
Aplikację logiki musi tylko zawartość wierszy, można utworzyć wyzwalacz tak jak ten przykład:  
  
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
  
Następnie w definicji przepływu pracy `@triggerBody().name` zwraca `mycoolrow` dla przy pierwszym uruchomieniu i `another row` dla drugiego przebiegu. Wygląd danych wyjściowych wyzwalacz tak jak ten przykład:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Dlatego jeśli używasz `SplitOn`, nie można pobrać właściwości, które są poza tablicy, w tym przypadku `Status` pola.  
  
> [!NOTE]  
> W tym przykładzie używamy `?` operatora, aby można było uniknąć awarii, jeśli `Rows` nie ma właściwości. 
  
## <a name="single-run-instance"></a>Pojedyncze wystąpienie wykonywania

Można skonfigurować wyzwalacze, które mają właściwość cyklu uruchomienie tylko, jeśli wszystkie aktywnej przebiegi została ukończona. W przypadku podczas uruchamiania w trakcie zaplanowanego cyklu wyzwalacza pomija i czeka, aż do następnego interwał cyklu zaplanowane, aby ponownie sprawdzić.

Można to ustawienie można skonfigurować za pomocą opcji operacji:

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
  
-   **ApiConnection** \- ta akcja działa jak akcja HTTP, ale korzysta z interfejsów API zarządzany przez firmę Microsoft.  
  
-   **ApiConnectionWebhook** \- jak HTTPWebhook, ale używa interfejsów API zarządzany przez firmę Microsoft.  
  
-   **Odpowiedź** \- tej akcji określa odpowiedzi dla połączenia przychodzącego.  
  
-   **Poczekaj** \- ta akcja proste czeka stałą lub określonego czasu.  
  
-   **Przepływ pracy** \- tej akcji reprezentuje zagnieżdżony przepływ pracy.  

-   **Funkcja** \- tej akcji reprezentuje funkcję platformy Azure.

### <a name="collection-actions"></a>Akcje kolekcji

-   **Zakres** \- ta akcja jest logiczne grupowanie innych działań.

-   **Warunek** \- ta akcja oblicza wyrażenie i wykonuje odpowiednie gałęzi wynik.

-   **Instrukcja ForEach** \- ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu.

-   **Dopóki** \- ta akcja pętli wykonuje działania wewnętrzne, dopóki warunek wyników do wartości true.
  
Każdy typ działania ma inny zestaw **dane wejściowe** definiującą zachowanie akcji.  
  
## <a name="http-action"></a>Akcja HTTP  

Akcje HTTP wywołać określony punkt końcowy i sprawdź odpowiedzi, aby określić, czy należy uruchomić przepływ pracy. **Dane wejściowe** obiekt ma zestaw parametrów wymaganych do utworzenia połączenia HTTP:  
  
|Nazwa elementu|Wymagane|Typ|Opis|  
|----------------|------------|--------|---------------|  
|— Metoda|Tak|Ciąg|Może być jedną z następujących metod HTTP: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**|  
|Identyfikator URI|Tak|Ciąg|Końcowy http lub https, która jest wywoływana. Maksymalna długość wynosi 2 kilobajtów.|  
|— zapytania|Nie|Obiekt|Reprezentuje parametry zapytania, aby dodać do adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje listę nagłówków, które są wysyłane do żądania. Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek, które są wysyłane do punktu końcowego.|  
|retryPolicy|Nie|Obiekt|Pozwala dostosować zachowanie ponownych prób dla 4xx lub 5xx błędów.|  
|operationsOptions|Nie|Ciąg|Definiuje zestaw specjalnego zachowania do zastąpienia.|  
|Uwierzytelnianie|Nie|Obiekt|Reprezentuje metodę uwierzytelniania żądania. Aby uzyskać więcej informacji na ten obiekt, zobacz [uwierzytelniania połączeń wychodzących harmonogramu](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Poza harmonogramem, jest jedna właściwość więcej obsługiwanych: `authority`. Domyślnie jest to `https://login.windows.net` gdy nie jest określony, ale możesz użyć innych grup odbiorców, takich jak`https://login.windows\-ppe.net`|  
  
Akcje HTTP \(i połączenie z interfejsem API\) Obsługa akcji ponów zasad. Zasady ponawiania dotyczy sporadycznych błędów jest określony jako kodów stanu HTTP 408 429 i 5xx, oprócz wszelkie wyjątki łączności. Ta zasada jest opisana przy użyciu *retryPolicy* obiekt zdefiniowany w sposób pokazany poniżej:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Interwał ponawiania prób jest określona w formacie ISO 8601. Ten interwał ma wartości domyślnej i co najmniej 20 sekund, podczas gdy wartość maksymalna to jedna godzina. Domyślne i maksymalnej liczby ponownych prób odpowiada czterem godzinom. Jeśli nie określono definicji zasad ponawiania, `fixed` strategii jest używany z domyślnej wartości interwału i liczba ponownych prób. Aby wyłączyć zasady ponawiania, ustaw jej typ `None`.  
  
Na przykład następujące działania ponowne próby pobierania najnowsze dwa razy, jeśli występują sporadyczne awarie, dla wszystkich trzech wykonaniami, z 30-sekundowe opóźnienie między kolejnymi próbami:  
  
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

Domyślnie wszystkie działania oparte na protokole HTTP obsługuje wzorzec standardowych operacji asynchronicznej. Dlatego w przypadku zdalnego serwera wskazuje, czy żądanie jest zaakceptowano do przetwarzania z 202 \(zaakceptowane\) odpowiedzi, aparat Logic Apps śledzi sondowania adres URL określony w odpowiedzi nagłówek lokalizacji do momentu osiągnięcia terminali stanu \(bez\-202 odpowiedzi\).  
  
Aby wyłączyć asynchroniczne zachowanie opisany powyżej, ustaw `DisableAsyncPattern` opcji w danych wejściowych działania. W takim przypadku dane wyjściowe działania jest oparty na początkowej 202 odpowiedzi z serwera.  
  
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

Asynchroniczny wzorzec może być ograniczone w jego czas trwania na określonym interwale.  Jeśli interwał czasu musi upłynąć bez osiągnięcia terminali stanu, zostaną oznaczone jako stan akcji `Cancelled` przy użyciu kodu `ActionTimedOut`.  Limit czasu został określony w formacie ISO 8601.  Limity można określić przy użyciu następującej składni:

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
Ta akcja wymaga odwołania do prawidłowe połączenie, a informacje na temat interfejsu API i parametrów wymaganych.

|Nazwa elementu|Wymagane|Typ|Opis|  
|----------------|------------|--------|---------------|  
|Host|Tak|Obiekt|Reprezentuje informacje łącznika, takie jak runtimeUrl i odwołania do obiektu połączenia|
|— Metoda|Tak|Ciąg|Może być jedną z następujących metod HTTP: **UZYSKAĆ**, **POST**, **PUT**, **usunąć**, **poprawka**, lub  **HEAD**|  
|Ścieżka|Tak|Ciąg|Ścieżka operacji interfejsu API.|  
|— zapytania|Nie|Obiekt|Reprezentuje parametry zapytania, aby dodać do adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje listę nagłówków, które są wysyłane do żądania. Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje ładunek, które są wysyłane do punktu końcowego.|  
|retryPolicy|Nie|Obiekt|Pozwala dostosować zachowanie ponownych prób dla 4xx lub 5xx błędów.|  
|operationsOptions|Nie|Ciąg|Definiuje zestaw specjalnego zachowania do zastąpienia.|  

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

Można określić limity akcji elementu webhook w taki sam sposób jak [limity asynchroniczne HTTP](#asynchronous-limits).
  
## <a name="response-action"></a>Akcja odpowiedzi  

Ten typ akcji zawiera ładunek całej odpowiedzi z żądania HTTP i obejmuje statusCode, treści i nagłówków:  
  
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
  
Akcja odpowiedź ma specjalne ograniczenia, które nie dotyczą innych działań. W szczególności:  
  
-   Akcje reakcji nie może być równoległe w definicji deterministyczne odpowiedzi na żądania przychodzącego, jeśli jest wymagana.  
  
-   Po osiągnięciu akcji odpowiedzi po otrzymaniu odpowiedzi żądania przychodzącego, jeśli akcja jest uznawany za nie powiodło się \(konflikt\), i w związku z tym jest uruchomienie `Failed`.  
  
-   Przepływ pracy z akcjami odpowiedzi nie może mieć `splitOn` w jego wyzwalacza jedno wywołanie powoduje, że wiele przebiegów. W związku z tym to powinny być weryfikowane po przepływ, PUT i Przyczyna nieprawidłowe żądanie.  
  
## <a name="wait-action"></a>Poczekaj akcji  

`wait` Akcji wstrzymuje wykonywanie przepływu pracy dla określonego interwału. Na przykład aby poczekaj 15 minut, można użyć ta Wstawka kodu:  
  
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
  
Można również czekać, aż do określonego momentu w czasie, można użyć w tym przykładzie:  
  
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
> Czas oczekiwania albo można użyć **interwał** obiektu lub **do momentu** obiektu, ale nie oba.  
  
|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Interwał|Nie|Obiekt|Czas oczekiwania, oparte na czas.|  
|Interwał|Tak|Ciąg|Jeden z tych przedziałów: sekundy, minuty, godziny, dnia, tygodnia, miesiąca, roku.|  
|Liczba interwale|Tak|Ciąg|Czas trwania oparte na danej jednostce wewnętrznego.|  
|do czasu|Nie|Obiekt|Czas oczekiwania na podstawie punktu w czasie.|  
|do sygnatury czasowej|Tak|Ciąg|Ciąg &#124; Do punktu w czasie w formacie UTC wygaśnięcia czas oczekiwania.|  

## <a name="query-action"></a>Akcja kwerendy

`query` Akcja umożliwia filtrowanie na podstawie warunku tablicy. Na przykład aby wybrać liczby większe niż 2, można:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Dane wyjściowe z `query` akcji jest tablicę, która ma elementy z tablicy wejściowej, które spełniają warunek.

> [!NOTE]
> Jeśli spełniać żadnych wartości `where` warunek, wynik ma być pustą tablicą.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|Z|Tak|Tablica|Tablica źródłowa.|
|gdzie|Tak|Ciąg|Warunek, którego chcesz zastosować do każdego elementu tablicy źródłowej.|

## <a name="select-action"></a>Wybierz akcję

`select` Pozwala projektów każdy element tablicy na nową wartość.
Na przykład aby przekonwertować tablicy liczb znajdujących się na tablicę obiektów, można:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Dane wyjściowe `select` akcji jest tablicą, który ma tego samego Kardynalność jako tablica wejściowa z każdym elementem przekształcone zgodnie z definicją w `select` właściwości. Jeśli dane wejściowe jest pusta tablica, dane wyjściowe jest również być pustą tablicą.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|Z|Tak|Tablica|Tablica źródłowa.|
|Wybierz|Tak|Dowolne|Projekcji, które można zastosować do każdego elementu tablicy źródłowej.|

## <a name="terminate-action"></a>Zakończenie akcji

Akcja zakończenia zatrzymuje wykonywanie uruchomienia przepływu pracy, przerywanie wszystkie akcje locie i pomija wszystkie pozostałe akcje. Na przykład, aby zakończyć wykonywania o stanie ****, można użyć następującego fragmentu kodu:

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
> Akcja zakończenia nie dotyczy działania już zakończone.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|runStatus|Tak|Ciąg|Obiekt docelowy stan uruchomienia. Albo **nie powiodło się** lub **anulowane**.|
|runError|Nie|Obiekt|Szczegóły błędu. Tylko obsługiwane w przypadku **runStatus** ustawiono ****.|
|Kod runError|Nie|Ciąg|Błąd podczas wykonywania kodu.|
|komunikat runError|Nie|Ciąg|Komunikat uruchamiania.|

## <a name="compose-action"></a>Redagowanie akcji

Redaguj pozwala utworzenia dowolnego obiektu. Dane wyjściowe działania Redaguj jest wynikiem obliczenia wejścia. Na przykład umożliwia akcji tworzenia Scal dane wyjściowe z wielu czynności:

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
> **Redaguj** akcja może zostać użyta do skonstruowania żadnych danych wyjściowych, w tym obiektów, tablic i innego typu obsługiwane przez logikę aplikacji, takich jak XML i pliku binarnego.

## <a name="table-action"></a>Akcja tabeli

`table` Umożliwia konwertowanie tablicę elementów do **CSV** lub **HTML** tabeli.

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

Natomiast akcji można zdefiniować jako

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Powyższe dałby w efekcie

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>jabłek</td></tr><tr><td>1</td><td>Pomarańcze</td></tr></tbody></table>"

Aby dostosować tabeli, należy określić kolumny jawnie. Na przykład:

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

Powyższe dałby w efekcie

<table><thead><tr><th>Tworzy identyfikator</th><th>Opis elementu</th></tr></thead><tbody><tr><td>0</td><td>Nowa jabłek</td></tr><tr><td>1</td><td>świeżych pomarańczy</td></tr></tbody></table>"

Jeśli `from` wartość właściwości jest pusta tablica, dane wyjściowe jest pusta tabela.

|Nazwa|Wymagane|Typ|Opis|
|--------|------------|--------|---------------|
|Z|Tak|Tablica|Tablica źródłowa.|
|Format|Tak|Ciąg|Format, albo **CSV** lub **HTML**.|
|kolumny|Nie|Tablica|Kolumny. Umożliwia zastąpienie domyślnego kształtu tabeli.|
|Nagłówek kolumny|Nie|Ciąg|Nagłówek kolumny.|
|wartość w kolumnie|Tak|Ciąg|Wartość kolumny.|

## <a name="workflow-action"></a>Działania przepływu pracy   

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Identyfikator hosta|Tak|Ciąg|Identyfikator zasobu przepływu pracy, który ma zostać wywołana.|  
|Nazwa_wyzwalacza hosta|Tak|Ciąg|Nazwa wyzwalacza, który chcesz wywołać.|  
|— zapytania|Nie|Obiekt|Reprezentuje parametry zapytania, aby dodać do adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje listę nagłówków, które są wysyłane do żądania. Na przykład, aby ustawić język i typ żądania:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Treści|Nie|Obiekt|Reprezentuje obciążenie wysyłane do punktu końcowego.|  
  
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
  
Sprawdzanie dostępu jest wprowadzone w przepływie pracy \(dokładniej, wyzwalacz\), co oznacza, potrzebny jest dostęp do przepływu pracy.  
  
Dane wyjściowe z `workflow` akcji są oparte na zdefiniowane w `response` działania w przepływie pracy podrzędnych. Jeśli nie zdefiniowano żadnego `response` akcji, a następnie dane wyjściowe są puste.  

## <a name="function-action"></a>Akcja — funkcja   

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|id — funkcja|Tak|Ciąg|Identyfikator zasobu do wywołania funkcji.|  
|— Metoda|Nie|Ciąg|Metoda HTTP używana do wywołania funkcji. Domyślnie jest `POST` gdy nie został określony.|  
|— zapytania|Nie|Obiekt|Reprezentuje parametry zapytania, aby dodać do adresu URL. Na przykład `"queries" : { "api-version": "2015-02-01" }` dodaje `?api-version=2015-02-01` do adresu URL.|  
|Nagłówki|Nie|Obiekt|Reprezentuje listę nagłówków, które są wysyłane do żądania. Na przykład, aby ustawić język i typ na żądanie: `"headers" : { "Accept-Language": "en-us" }`.|  
|Treści|Nie|Obiekt|Reprezentuje obciążenie wysyłane do punktu końcowego.|  

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

Podczas zapisywania aplikacji logiki, wykonujemy kontroli niektórych funkcji, do którego istnieje odwołanie:
-   Musisz mieć dostęp do funkcji.
-   Tylko standardowy wyzwalacza HTTP lub ogólny wyzwalacza elementu webhook JSON jest dozwolone.
-   Nie powinna mieć żadnej trasy zdefiniowane.
-   Tylko "funkcji" i "anonymous" autoryzacji na poziomie jest dozwolone.

Adres URL wyzwalacza jest pobierana, w pamięci podręcznej i używany w czasie wykonywania. Dlatego jeśli żadnej operacji unieważnia pamięci podręcznej adres URL, akcja zakończy się niepowodzeniem w czasie wykonywania. Aby obejść ten problem, należy zapisać aplikację logiki, co spowoduje aplikację logiki, aby pobrać i ponownie pamięci podręcznej adres URL wyzwalacza.

## <a name="collection-actions-scopes-and-loops"></a>Akcje kolekcji (zakresy i pętle)

Niektóre typy działań mogą zawierać działania w ramach samodzielnie. Odwołanie do działań w ramach kolekcji można odwoływać się bezpośrednio poza kolekcji. Jeśli zdefiniowano `http` w zakresie `@body('http')` jest nadal ważny w dowolnym miejscu w przepływie pracy. Akcje w ramach kolekcji można `runAfter` tylko innych działań w ramach tej samej kolekcji.

## <a name="scope-action"></a>Akcja zakresu

`scope` Pozwala logicznie grupy działań w przepływie pracy.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Wewnętrzny akcje do wykonania w zakresie|

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

Ta akcja pętli iteruje tablicy i wykonuje akcje wewnętrzny dla każdego elementu. Domyślnie pętli foreach wykonuje równoległe (20 wykonaniami równolegle w czasie). Można ustawić zasady wykonywania przy użyciu `operationOptions` parametru.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Wewnętrzny akcje do wykonania w pętli|
|Instrukcja foreach|Tak|Ciąg|Tablicy w celu wykonania iteracji|
|operationOptions|Brak|Ciąg|Wszystkie opcje operacji zachowanie. Obsługuje obecnie tylko `sequential` do wykonywania iteracji sekwencyjnie (domyślne zachowanie to równoległych)|

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

Ta akcja pętli wykonuje akcje wewnętrzny dopóki warunek wyników do wartości true.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Wewnętrzny akcje do wykonania w pętli|
|wyrażenie|Tak|Ciąg|Wyrażenie do oceny po każdej iteracji|
|Limit|Tak|Obiekt|Limity dla pętli — co najmniej jeden limit musi być zdefiniowana|
|Liczba|Brak|int|Limit liczby iteracji, które mogą być wykonywane|
|Limit czasu|Brak|Ciąg|Limit czasu na czas powinien pętli.  Formacie ISO 8601|


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

`If` Pozwala ocenić warunku i wykonywanie gałęzi według tego, czy wyrażenie daje w wyniku `true`.

|Nazwa|Wymagane|Typ|Opis|  
|--------|------------|--------|---------------|  
|Akcje|Tak|Obiekt|Wewnętrzny akcje do wykonania, gdy wyrażenie daje w wyniku`true`|
|wyrażenie|Tak|Ciąg|Wyrażenie do oceny|
|else|Brak|Obiekt|Wewnętrzny akcje do wykonania, gdy wyrażenie daje w wyniku`false`|
  
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
  
W poniższej tabeli przedstawiono przykłady warunków użycia wyrażeń w akcji:  
  
|Wartość JSON|wynik|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Żadnej wartości, które są używane do oceny na wartość true powoduje, że ten stan do przekazania. Obsługiwane są tylko wyrażenia logiczne. Aby przekonwertować inne typy Boolean, użyj funkcji `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Porównanie funkcji są obsługiwane. Na przykład tutaj Akcja wykonywana tylko po act1 danych wyjściowych jest większy niż próg.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Logika funkcje są również obsługiwane do tworzenia zagnieżdżonych wyrażeń logicznych. W takim przypadku operacja zostanie wykonana, gdy dane wyjściowe act1 jest powyżej wartości progowej lub poniżej 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Możesz użyć funkcji tablicy, aby sprawdzić, czy wszystkie elementy tablicy. W takim przypadku operacja zostanie wykonana, gdy macierz błędów jest pusta.| 
|`"expression": "parameters('hasSpecialAction')"`|Błąd — nie jest prawidłowym warunku, ponieważ @ jest wymagany dla warunków.|  
  
Jeśli wynikiem warunku jest pomyślnie, warunek zostanie oznaczona jako `Succeeded`. Akcje w ramach jednej `actions` lub `else` obliczać obiektów `Succeeded` po wykonaniu i zakończyło się pomyślnie, `Failed` po wykonaniu i nie powiodło się, lub `Skipped` po gałąź, nie została wykonana.

## <a name="next-steps"></a>Następne kroki

[Interfejs API REST usługi przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)
