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
# <a name="work-with-azure-functions-proxies-preview"></a>Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)

> [!NOTE] 
> Proxy funkcji platformy Azure jest obecnie w przeglądzie. Jest bezpłatne w wersji zapoznawczej, ale standardowych funkcji rozliczeń dotyczy wykonaniami tooproxy. Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

W tym artykule opisano sposób tooconfigure i korzystanie z serwerów proxy funkcji platformy Azure. Dzięki tej funkcji można określić punkty końcowe na aplikację funkcji, które zostały zaimplementowane przez inny zasób. Te serwery proxy toobreak dużych interfejsu API do wielu aplikacji funkcji (tak jak to architektura mikrousługi), można użyć podczas prezentując pojedynczą powierzchnię interfejsu API dla klientów.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Włącz usługę Azure Functions serwerów proxy

Serwery proxy nie są domyślnie włączone. Serwery proxy można utworzyć podczas hello funkcja jest wyłączona, ale nie zostanie wykonany. proxy tooenable hello następujące:

1. Otwórz hello [portalu Azure], a następnie przejdź tooyour funkcji aplikacji.
2. Wybierz **funkcji ustawienia aplikacji**.
3. Przełącznik **włączyć proxy funkcji Azure (wersja zapoznawcza)** za**na**.

Można także wrócić tu tooupdate powitania serwera proxy w czasie wykonywania jako nowe funkcje staną się dostępne.


## <a name="create"></a>Utwórz serwer proxy

W tej sekcji przedstawiono, jak toocreate, a serwer proxy w hello funkcje portalu.

1. Otwórz hello [portalu Azure], a następnie przejdź tooyour funkcji aplikacji.
2. Wybierz w okienku po lewej stronie powitania **nowego serwera proxy**.
3. Podaj nazwę serwera proxy.
4. Skonfiguruj hello punktu końcowego, która jest widoczna w tym funkcji aplikacji, określając hello **szablon trasy** i **metod HTTP**. Te parametry działają zgodnie z zasady toohello [wyzwalaczy HTTP].
5. Zestaw hello **URL wewnętrznej bazy danych** tooanother punktu końcowego. Ten punkt końcowy może być funkcją w innej aplikacji funkcji lub może być jakiegokolwiek interfejsu API. Hello wartość nie jest konieczne toobe statyczne i mogą się odwoływać do [ustawienia aplikacji] i [parametrów z żądania klienta oryginalnym hello].
6. Kliknij przycisk **Utwórz**.

Serwer proxy obecnie istnieje jako nowy punkt końcowy w aplikacji funkcji. Z perspektywy klienta jest równoważne tooan HttpTrigger w funkcji platformy Azure. Można wypróbować nowego serwera proxy, kopiując hello adres URL serwera Proxy i testowanie go z ulubionych klienta HTTP.

## <a name="modify-requests-responses"></a>Modyfikowanie żądań i odpowiedzi

Za pomocą proxy funkcji platformy Azure można modyfikować żądania tooand odpowiedzi z hello wewnętrznego. Przekształcenia te można używać zmiennych, zgodnie z definicją w [używać zmiennych].

### <a name="modify-backend-request"></a>Modyfikowanie hello zaplecza żądania

Domyślnie hello zaplecza żądania został zainicjowany jako kopię hello oryginalne żądanie. Ponadto toosetting hello wewnętrznego adresu URL, możesz wprowadzić metoda HTTP toohello zmiany, nagłówki i parametrów ciągu zapytania. Witaj zmodyfikowane wartości może się odwoływać [ustawienia aplikacji] i [parametrów z żądania klienta oryginalnym hello].

Obecnie nie są portalu obsługę modyfikowanie żądań zaplecza. toolearn tooapply tej możliwości z proxies.json, zobacz temat [zdefiniować obiekt requestOverrides].

### <a name="modify-response"></a>Modyfikowanie hello odpowiedzi

Domyślnie powitania klienta odpowiedzi został zainicjowany jako kopię hello zaplecza odpowiedzi. Możesz wprowadzić kod stanu odpowiedzi toohello zmiany, frazę przyczyny, nagłówki i treść. Witaj zmodyfikowane wartości może się odwoływać [ustawienia aplikacji], [parametrów z żądania klienta oryginalnym hello], i [parametry z odpowiedzi zaplecza hello].

Obecnie nie są bez obsługi portalu modyfikowania odpowiedzi. toolearn tooapply tej możliwości z proxies.json, zobacz temat [zdefiniować obiekt responseOverrides].

## <a name="using-variables"></a>Używać zmiennych

Hello konfigurację serwera proxy nie jest konieczne toobe statycznych. Można go warunku zmienne toouse hello oryginalne żądanie, hello zaplecza odpowiedzi lub ustawień aplikacji.

### <a name="request-parameters"></a>Parametry żądania odwołania

Parametry żądania można użyć jako danych wejściowych właściwość URL zaplecza toohello lub w ramach modyfikowania żądania i odpowiedzi. Niektóre parametry mogą być powiązane z hello szablon trasy, który został określony w konfiguracji podstawowej serwera proxy hello i inne osoby mogą pochodzić z właściwości hello żądania przychodzącego.

#### <a name="route-template-parameters"></a>Parametry szablonu trasy
Parametry, które są używane w szablonie trasy hello są dostępne toobe wskazywana przez nazwę. nazwy parametrów Hello są ujęte w nawiasy klamrowe ({}).

Na przykład, jeśli serwer proxy ma szablon trasy, takich jak `/pets/{petId}`, adres URL zaplecza hello może zawierać wartości hello `{petId}`, jak w `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Jeśli szablon trasy hello kończy w symboli wieloznacznych, takich jak `/api/{*restOfPath}`, hello wartość `{restOfPath}` jest hello pozostałych segmentów ścieżki z żądania przychodzącego hello reprezentację ciągu.

#### <a name="additional-request-parameters"></a>Dodatkowe parametry żądania
Ponadto toohello parametry szablonu trasy, hello następujące wartości można użyć w wartości konfiguracji:

* **{Request.method wartość}** : hello metoda HTTP, która jest używana na powitania oryginalne żądanie.
* **{request.headers. \<HeaderName\>}**: nagłówek, który może zostać odczytany z hello oryginalne żądanie. Zastąp  *\<HeaderName\>*  o nazwie hello hello nagłówka, które mają tooread. Jeśli hello nagłówka nie znajduje się na żądanie hello, wartość hello będzie hello pusty ciąg.
* **{request.querystring. \<ParameterName\>}**: parametr ciągu zapytania, który może zostać odczytany z hello oryginalne żądanie. Zastąp  *\<ParameterName\>*  o nazwie hello parametru hello, które mają tooread. Jeśli parametr hello jest niedostępna na żądanie hello, wartość hello będzie hello pusty ciąg.

### <a name="response-parameters"></a>Parametry zaplecza odpowiedzi odwołania

Parametry odpowiedzi mogą być używane jako część modyfikowanie hello odpowiedzi toohello klienta. Witaj następujące wartości mogą być używane w wartości konfiguracji:

* **{backend.response.statusCode}** : hello kod stanu HTTP, który jest zwracany w odpowiedzi zaplecza hello.
* **{backend.response.statusReason}** : fraza przyczyny hello HTTP, który jest zwracany w odpowiedzi zaplecza hello.
* **{backend.response.headers. \<HeaderName\>}**: nagłówek, który może zostać odczytany z hello zaplecza odpowiedzi. Zastąp  *\<HeaderName\>*  o nazwie hello nagłówka hello ma tooread. Jeśli hello nagłówka nie znajduje się na żądanie hello, wartość hello będzie hello pusty ciąg.

### <a name="use-appsettings"></a>Odwołanie do ustawienia aplikacji

Można także odwoływać [ustawienia aplikacji określone dla aplikacji funkcja hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) wpisując nazwę ustawienia hello w znaki procentu (%).

Na przykład adres URL zaplecza z *https://%ORDER_PROCESSING_HOST%/api/orders* byłyby "% ORDER_PROCESSING_HOST %" zastąpione hello hello ORDER_PROCESSING_HOST ustawienia.

> [!TIP] 
> Użyj ustawienia aplikacji dla hostów zaplecza w przypadku wielu wdrożeń lub środowisk testowych. W ten sposób można zapewnić zawsze komunikuje powrót toohello zakończenia dla tego środowiska.

## <a name="advanced-configuration"></a>Konfiguracja zaawansowana

proxy Hello, które można skonfigurować są przechowywane w pliku proxies.json, który znajduje się w katalogu głównym hello funkcja katalogu aplikacji. Można ręcznie edytować ten plik i wdróż je jako część aplikacji, gdy przy użyciu jednej z hello [metody wdrażania](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) obsługiwane przez funkcje. Funkcja Hello musi być [włączone](#enable) dla toobe pliku hello przetworzone. 

> [!TIP] 
> Jeśli nie zdefiniowano jednej z metod wdrażania hello, użytkownik może również współpracować z pliku proxies.json hello w portalu hello. Przejdź tooyour funkcji aplikacji, wybierz opcję **funkcji platformy**, a następnie wybierz **Edytor usług aplikacji**. W ten sposób można wyświetlić hello cały plik struktury aplikacji funkcji, a następnie wprowadź zmiany.

Proxies.JSON jest zdefiniowane przez obiekt serwery proxy, który składa się z nazwanym proxy oraz ich definicje. Opcjonalnie, jeśli edytor obsługuje tę funkcję, możesz odwoływać się do [schematu JSON](http://json.schemastore.org/proxies) dla uzupełniania kodu. Przykładowy plik może wyglądać hello następujące czynności:

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

Każdy serwer proxy ma przyjazną nazwę, takich jak *proxy1* w hello poprzedzających przykład. Witaj odpowiedni obiekt definicji serwera proxy jest zdefiniowane przez hello następujące właściwości:

* **matchCondition**: wymagany — obiekt definiujący hello żądań, które wyzwolić wykonywanie hello tego serwera proxy. Zawiera dwie właściwości, które są udostępniane [wyzwalaczy HTTP]:
    * _metody_: odpowiada tablicę metody hello HTTP, które hello serwera proxy. Jeśli nie zostanie określony, hello proxy odpowiada tooall metod HTTP na powitania trasy.
    * _trasy_: wymagany — definiuje hello szablon trasy, kontrolowanie, które adresów URL żądań proxy odpowiada. W odróżnieniu od w HTTP wyzwalaczy, nie ma wartości domyślnej.
* **backendUri**: adres URL hello hello zasobów zaplecza toowhich hello żądania powinien być serwerem proxy. Ta wartość może odwoływać się ustawienia aplikacji i parametrów z żądania klienta oryginalnym hello. Jeśli ta właściwość nie jest uwzględniona, usługi Azure Functions odpowiada HTTP 200 OK.
* **requestOverrides**: obiekt, który definiuje przekształcenia toohello zaplecza żądania. Zobacz [zdefiniować obiekt requestOverrides].
* **responseOverrides**: obiekt, który definiuje przekształcenia toohello klienta odpowiedzi. Zobacz [zdefiniować obiekt responseOverrides].

> [!NOTE] 
> właściwości trasy Hello Azure funkcji proxy honoruje właściwości routePrefix hello hello funkcje hosta konfiguracji. Jeśli chcesz tooinclude prefiksu, takich jak /api, muszą być zawarte w hello właściwości trasy.

### <a name="requestOverrides"></a>Zdefiniuj obiektu requestOverrides

Obiekt requestOverrides Hello definiuje zmiany wprowadzone żądania toohello wywołanego hello zasobów wewnętrznych. Obiekt Hello jest zdefiniowany przez hello następujące właściwości:

* **backend.Request.Method**: hello metoda HTTP, która została użyta toocall hello zaplecza.
* **backend.Request.QueryString. \<ParameterName\>**: ustawioną dla zaplecza hello wywołania toohello parametr ciągu zapytania. Zastąp  *\<ParameterName\>*  o nazwie hello parametru hello, które mają tooset. W przypadku pustego ciągu hello parametru hello jest niedostępna na powitania zaplecza żądania.
* **backend.Request.headers. \<HeaderName\>**: nagłówek, który można ustawić dla hello wywołania toohello zaplecza. Zastąp  *\<HeaderName\>*  o nazwie hello hello nagłówka, które mają tooset. Jeśli podasz hello pusty ciąg hello nagłówka nie znajduje się na powitania zaplecza żądania.

Wartości można odwoływać się ustawienia aplikacji i parametrów z żądania klienta oryginalnym hello.

Przykładowa konfiguracja może wyglądać hello następujące czynności:

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

### <a name="responseOverrides"></a>Zdefiniuj obiektu responseOverrides

Obiekt requestOverrides Hello definiuje zmiany wprowadzone w odpowiedzi toohello, która ma wstecz toohello zakończyło się powodzeniem. Obiekt Hello jest zdefiniowany przez hello następujące właściwości:

* **response.statusCode**: toobe kod stanu hello HTTP zwrócił toohello klienta.
* **response.statusReason**: toobe fraza przyczyny hello HTTP zwrócony toohello klienta.
* **Response.body**: hello treści toobe reprezentację ciągu hello zwrócił toohello klienta.
* **Response.headers. \<HeaderName\>**: nagłówek, który można ustawić dla hello odpowiedzi toohello klienta. Zastąp  *\<HeaderName\>*  o nazwie hello hello nagłówka, które mają tooset. Jeśli podasz pusty ciąg hello hello nagłówka nie znajduje się na powitania odpowiedzi.

Ustawienia aplikacji, parametrów z żądania klienta oryginalnym hello i parametry wartości można odwoływać się z hello zaplecza odpowiedzi.

Przykładowa konfiguracja może wyglądać hello następujące czynności:

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
> W tym przykładzie treści hello jest ustawiany bezpośrednio, więc nie `backendUri` właściwość jest wymagana. przykład Witaj pokazuje, jak można użyć do mocking interfejsów API Azure funkcji z serwerów proxy.

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
