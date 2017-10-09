---
title: "Interfejs API niekorzystającą przy użyciu usługi Azure Functions aaaCreate | Dokumentacja firmy Microsoft"
description: "Jak toocreate interfejs API niekorzystającą przy użyciu usługi Azure Functions"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Utwórz interfejs API niekorzystającą przy użyciu usługi Azure Functions

W tym samouczku dowiesz się, jak usługi Azure Functions umożliwia toobuild wysoce skalowalna interfejsów API. Środowisko Azure Functions jest dostarczany z kolekcji wbudowanych HTTP wyzwalaczy i powiązań, które pozwalają łatwo tooauthor punkt końcowy w różnych językach, łącznie z Node.JS, C# i inne. W tym samouczku zostanie Dostosowywanie toohandle wyzwalacza HTTP dla akcji określonych w projekcie interfejsu API. Należy również przygotować do powiększania interfejsu API integrowanie go z serwerów proxy funkcji platformy Azure i konfigurowanie zasymulować interfejsów API. Wszystko to odbywa się na górze hello funkcje niekorzystającą obliczeniowe środowiska, dlatego nie masz tooworry temat skalowania zasobów — wystarczy można skoncentrować się na logice interfejsu API.

## <a name="prerequisites"></a>Wymagania wstępne 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

Wynikowa funkcja Hello będzie służyć do hello pozostałej części tego samouczka.

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

Otwórz hello portalu Azure. toodo, zaloguj się za[https://portal.azure.com](https://portal.azure.com) z Twoim kontem platformy Azure.

## <a name="customize-your-http-function"></a>Dostosowywanie funkcji HTTP

Domyślnie funkcji wyzwalanych przez protokół HTTP jest skonfigurowany tooaccept dowolnej metody HTTP. Jest również domyślny adres URL w postaci hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Po wykonaniu hello Szybki Start, następnie `<funcname>` prawdopodobnie wygląda "HttpTriggerJS1". W tej sekcji należy zmodyfikować hello funkcja toorespond tooGET tylko żądania kierowane do `/api/hello` zamiast tego trasy. 

Przejdź w portalu Azure hello funkcji tooyour. Wybierz **integracji** w hello lewy pasek nawigacyjny.

![Dostosowywanie funkcji HTTP](./media/functions-create-serverless-api/customizing-http.png)

Użyj ustawień wyzwalacza HTTP określoną w tabeli hello.

| Pole | Wartość przykładowa | Opis |
|---|---|---|
| Dopuszczalnych metod HTTP | Wybrane metody zostaną usunięte | Określa, jakie metody HTTP mogą być używane tooinvoke tej funkcji |
| Wybrane metody HTTP | POBIERZ | Umożliwia tylko wybrane toobe metod HTTP użytej tooinvoke tej funkcji |
| Szablon trasy | człon | Określa, jakie trasy jest używane tooinvoke tej funkcji |

Należy pamiętać, że nie zawiera hello `/api` podstawowa prefiks ścieżki w szablonie trasy hello, ponieważ jest to obsługiwane przez ustawienie globalne.

Kliknij pozycję **Zapisz**.

Dowiedz się więcej o dostosowywaniu funkcji HTTP w [powiązania HTTP funkcje platformy Azure i webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Testowanie interfejsu API

Następnie przetestować toosee Twojego funkcja Praca z hello nowych powierzchni interfejsu API.

Przejdź wstecz toohello programowanie strony, klikając nazwę funkcji hello na powitania lewy pasek nawigacyjny.

Kliknij przycisk **uzyskać adres URL funkcji** i skopiuj adres URL hello. Powinny pojawić się korzysta z hello `/api/hello` teraz trasy.

Kopiuj adres URL hello na nowej karcie przeglądarki lub preferowanego klienta REST. Przeglądarki użyje GET domyślnie.

Uruchamianie funkcji hello i upewnij się, że działa. Parametr "Nazwa" hello tooprovide może być konieczne jako kodu szybkiego startu hello toosatisfy ciągu zapytania.

Można też spróbować wywołaniem punktu końcowego hello z innej tooconfirm — metoda HTTP hello funkcja nie została wykonana. W tym celu należy toouse klienta REST, takie jak cURL, Postman lub Fiddler.

## <a name="proxies-overview"></a>Omówienie serwerów proxy

W następnej sekcji hello będzie powierzchni interfejsu API za pośrednictwem serwera proxy. Azure funkcje serwera proxy jest funkcja w wersji zapoznawczej, umożliwiający tooforward żądań tooother zasobów. Tak jak zdefiniować punkt końcowy HTTP z wyzwalaczem HTTP, ale zamiast zapisywania tooexecute kodu, gdy jest wywoływana tego punktu końcowego, należy udostępnić implementację zdalnego tooa adresu URL. Dzięki temu toocompose API wielu źródeł w jednym powierzchni interfejsu API, który ułatwia tooconsume klientów. Jest to szczególnie przydatne, jeśli chcesz toobuild interfejsu API jako mikrousług.

Serwer proxy może wskazywać tooany HTTP zasobów, takich jak:
- Stan usługi Funkcje Azure 
- Aplikacje interfejsu API w [usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Kontenery docker w [usługi aplikacji w systemie Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Inne obsługiwane interfejsu API

toolearn więcej informacji na temat serwerów proxy, zobacz [Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)].

## <a name="create-your-first-proxy"></a>Tworzenie pierwszego serwera proxy

W tej sekcji utworzysz nowe proxy który służy jako tooyour frontonu ogólnego interfejsu API. 

### <a name="setting-up-hello-frontend-environment"></a>Konfigurowanie środowiska frontonu hello

Powtórz kroki od hello zbyt[tworzenia aplikacji funkcji](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate nową aplikację funkcji w co spowoduje utworzenie serwera proxy. Ta nowa aplikacja będzie służyć jako frontonu hello na interfejsie API i hello funkcji aplikacji, które zostały wcześniej edycji będzie służyć jako wewnętrznej bazy danych.

Przejdź tooyour nowego serwera sieci Web funkcji aplikacji w portalu hello.

Wybierz **ustawienia**. Następnie przełącz **włączyć proxy funkcji Azure (wersja zapoznawcza)** zbyt "na".

Wybierz **ustawienia platformy** i wybierz polecenie **ustawienia aplikacji**.

Przewiń w dół za**ustawień aplikacji** i utworzyć nowe ustawienie z kluczem "HELLO_HOST". Ustaw jej wartość host toohello aplikacji funkcji wewnętrznej bazy danych, takich jak `<YourApp>.azurewebsites.net`. Jest to część adresu URL hello, które wcześniej zostały skopiowane podczas testowania funkcji HTTP. To ustawienie w konfiguracji hello później będziesz odwoływać.

> [!NOTE] 
> Ustawienia aplikacji są zalecane w przypadku tooprevent konfiguracji hosta hello zależność ustalony środowiska powitania serwera proxy. Przy użyciu ustawień aplikacji oznacza, że konfiguracja serwera proxy hello można przenosić między środowiskami i zostaną zastosowane ustawienia specyficzne dla środowiska aplikacji hello.

Kliknij pozycję **Zapisz**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Tworzenie serwera proxy na powitania serwera sieci Web

Przejdź wstecz tooyour frontonu funkcji aplikacji w portalu hello.

W nawigacji po lewej stronie powitania, kliknij zbyt hello oraz znak "+" dalej "Serwery proxy (wersja zapoznawcza)".

![Tworzenie serwera proxy](./media/functions-create-serverless-api/creating-proxy.png)

Użyj ustawień serwera proxy, jak określono w tabeli hello.

| Pole | Wartość przykładowa | Opis |
|---|---|---|
| Nazwa | HelloProxy | Przyjazna nazwa używana tylko w przypadku zarządzania |
| Szablon trasy | / api/hello | Określa, jakie trasy jest używane tooinvoke ten serwer proxy |
| Adres URL wewnętrznej bazy danych | https://%HELLO_HOST%/API/Hello | Określa, że żądania hello toowhich punktu końcowego hello powinien być serwerem proxy |

Należy pamiętać, że serwery proxy nie hello `/api` prefiks ścieżki podstawowej i ten musi być zawarte w szablonie trasy hello.

Witaj `%HELLO_HOST%` składni będzie odwoływać się do ustawienia aplikacji hello utworzony wcześniej. Witaj rozpoznać adres URL będzie wskazywać tooyour pierwotnej funkcji.

Kliknij przycisk **Utwórz**.

Można wypróbować nowego serwera proxy, kopiując hello adres URL serwera Proxy i testowanie go w przeglądarce hello lub z ulubionych klienta HTTP.

## <a name="create-a-mock-api"></a>Utwórz zasymulować interfejs API

Następnie użyje toocreate proxy zasymulować interfejsu API dla rozwiązania. Dzięki temu programowanie klienta tooprogress, bez konieczności hello wewnętrznej bazy danych, w pełni wdrożone. Później w rozwoju należy utworzyć nową aplikację funkcji, która obsługuje tę logikę i przekierować tooit Twojego serwera proxy.

toocreate to mock interfejsu API, utworzymy nowe proxy przy użyciu hello [Edytor usług aplikacji](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget pracę, przejdź tooyour funkcji aplikacji w portalu hello. Wybierz **funkcji platformy** i Znajdź **Edytor usług aplikacji**. Kliknięcie łącza zostanie otwarty Edytor usług aplikacji hello na nowej karcie.

Wybierz `proxies.json` w hello lewy pasek nawigacyjny. To jest plik hello, którym przechowywana jest Konfiguracja hello wszystkie Twoje serwery proxy. Jeśli używany jest jeden hello [metody wdrażania funkcji](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), to jest plik hello mają być przechowywane w kontroli źródła. toolearn więcej informacji na temat tego pliku, zobacz [proxy Zaawansowana konfiguracja](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Jeśli po wykonaniu wykonanej do tej pory, proxies.json Twojego powinna wyglądać hello poniżej:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Następnie dodasz zasymulować interfejsu API. Zastąp plik proxies.json hello następujące czynności:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Spowoduje to dodanie nowego serwera proxy, "GetUserByName" bez hello backendUri właściwości. Zamiast kontaktować się z innym zasobem, modyfikuje hello domyślne odpowiedzi z serwerów proxy przy użyciu zastąpienia odpowiedzi. Można także zastąpienia żądań i odpowiedzi w połączeniu z adresem URL wewnętrznej bazy danych. Jest to szczególnie przydatne, gdy pośredniczenie tooa starszej wersji systemu, gdzie może być konieczne toomodify nagłówków, parametry zapytania, toolearn itp. więcej informacji na temat zastąpienia żądań i odpowiedzi, zobacz [modyfikowanie żądań i odpowiedzi w proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Test zasymulować interfejsu API przez wywołanie hello `/api/users/{username}` punktu końcowego za pomocą przeglądarki lub Twoje ulubione klienta REST. Należy się tooreplace _{username}_ z wartością ciągu reprezentujący nazwę użytkownika.

## <a name="next-steps"></a>Następne kroki

W tym samouczku można przedstawiono sposób toobuild i Dostosuj interfejs API na usługi Azure Functions. Również wiesz, jak toobring wiele interfejsów API, w tym mocks, jednocześnie jako ujednoliconego powierzchni interfejsu API. Można użyć tych toobuild techniki limit interfejsów API żadnych złożoności, wszystkie podczas uruchamiania na powitania niekorzystającą obliczeniowe udostępniane przez usługi Azure Functions modelu.

Witaj następujące informacje mogą być pomocne podczas opracowywania dalsze interfejsu API:

- [Azure powiązania HTTP funkcje i elementu webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]
- [Dokumentowanie funkcje interfejsu API Azure (wersja zapoznawcza)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
