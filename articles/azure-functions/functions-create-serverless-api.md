---
title: "Utwórz interfejs API niekorzystającą przy użyciu usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Jak utworzyć interfejs API niekorzystającą przy użyciu usługi Azure Functions"
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Utwórz interfejs API niekorzystającą przy użyciu usługi Azure Functions

W tym samouczku dowiesz się, jak usługi Azure Functions umożliwia tworzenie wysoce skalowalna interfejsów API. Środowisko Azure Functions jest dostarczany z kolekcji wbudowanych HTTP wyzwalaczy i powiązań, które ułatwiają tworzenie punktu końcowego w różnych językach, łącznie z Node.JS, C# i inne. W tym samouczku będzie dostosować wyzwalacz protokołu HTTP do obsługi określonych akcji w projekcie interfejsu API. Należy również przygotować do powiększania interfejsu API integrowanie go z serwerów proxy funkcji platformy Azure i konfigurowanie zasymulować interfejsów API. Wszystko to odbywa się na górze środowiska obliczeniowe bez serwera funkcji, nie trzeba martwić skalowania zasobów — wystarczy można skoncentrować się na logice interfejsu API.

## <a name="prerequisites"></a>Wymagania wstępne 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

Funkcja wynikowy będzie służyć do pozostałej części tego samouczka.

### <a name="sign-in-to-azure"></a>Logowanie do platformy Azure

Otwórz Azure portal. Aby to zrobić, zaloguj się do [https://portal.azure.com](https://portal.azure.com) z Twoim kontem platformy Azure.

## <a name="customize-your-http-function"></a>Dostosowywanie funkcji HTTP

Domyślnie funkcja wyzwalanych przez protokół HTTP jest skonfigurowany do akceptowania dowolnej metody HTTP. Jest również domyślny adres URL w postaci `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Po wykonaniu procedury szybkiego startu, następnie `<funcname>` prawdopodobnie wygląda "HttpTriggerJS1". W tej sekcji należy zmodyfikować funkcji ma odpowiadać tylko na żądania GET względem `/api/hello` zamiast tego trasy. 

Przejdź do funkcji w portalu Azure. Wybierz **integracji** na lewym pasku nawigacyjnym.

![Dostosowywanie funkcji HTTP](./media/functions-create-serverless-api/customizing-http.png)

Użyj ustawień wyzwalacza HTTP określoną w tabeli.

| Pole | Wartość przykładowa | Opis |
|---|---|---|
| Dopuszczalnych metod HTTP | Wybrane metody zostaną usunięte | Określa, jakie metody HTTP może służyć do wywołania tej funkcji |
| Wybrane metody HTTP | POBIERZ | Umożliwia tylko wybrane metody HTTP używanego do wywołania tej funkcji |
| Szablon trasy | człon | Określa, jakie trasy służy do wywoływania tej funkcji |

Należy pamiętać, że nie zawiera `/api` podstawowa prefiks ścieżki w szablonie trasy, ponieważ jest to obsługiwane przez ustawienie globalne.

Kliknij pozycję **Zapisz**.

Dowiedz się więcej o dostosowywaniu funkcji HTTP w [powiązania HTTP funkcje platformy Azure i webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Testowanie interfejsu API

Następnie należy przetestować funkcję wyświetlić go do pracy z nowego powierzchni interfejsu API.

Przejdź z powrotem do strony programowanie klikając nazwę funkcji, na lewym pasku nawigacyjnym.

Kliknij przycisk **uzyskać adres URL funkcji** i skopiuj adres URL. Powinny pojawić się go używa `/api/hello` teraz trasy.

Skopiuj adres URL do nowej karty przeglądarki lub preferowanego klienta REST. Przeglądarki użyje GET domyślnie.

Uruchom funkcję i upewnij się, że działa. Użytkownik może być konieczne podanie parametru "name" jako ciąg zapytania do zaspokojenia kodu Szybki Start.

Można też spróbować wywoływanie punkt końcowy z innej metody HTTP, aby upewnić się, że funkcja nie jest uruchomiona. W tym celu należy użyć klienta REST, takie jak cURL, Postman lub Fiddler.

## <a name="proxies-overview"></a>Omówienie serwerów proxy

W następnej sekcji zostanie powierzchni interfejsu API za pośrednictwem serwera proxy. Azure funkcje serwera proxy jest funkcja w wersji zapoznawczej, który służy do przesyłania żądań do innych zasobów. Zdefiniuj punkt końcowy HTTP, podobnie jak wyzwalacza HTTP, ale zamiast pisania kodu do wykonania, gdy jest wywoływana tego punktu końcowego, podaj adres URL do zdalnego wdrożenia. Umożliwia utworzenie wielu źródeł interfejsu API w jednym powierzchni interfejsu API, który ułatwia klientom korzystać. Jest to szczególnie przydatne, jeśli chcesz skompilować jako mikrousług interfejsu API.

Serwer proxy może wskazywać dowolnego zasobu HTTP, takie jak:
- Stan usługi Funkcje Azure 
- Aplikacje interfejsu API w [usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Kontenery docker w [usługi aplikacji w systemie Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Inne obsługiwane interfejsu API

Aby dowiedzieć się więcej na temat serwerów proxy, zobacz [Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)].

## <a name="create-your-first-proxy"></a>Tworzenie pierwszego serwera proxy

W tej sekcji utworzysz nowego serwera proxy, który służy jako frontonu do ogólnego interfejsu API. 

### <a name="setting-up-the-frontend-environment"></a>Konfigurowanie środowiska serwera sieci Web

Powtórz kroki, aby [tworzenia aplikacji funkcji](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) Aby utworzyć nową aplikację funkcji spowoduje utworzenie serwera proxy. Ta nowa aplikacja będzie służyć jako frontonu dla naszych interfejsu API i aplikacji funkcji, które zostały wcześniej edycji będzie służyć jako wewnętrznej bazy danych.

Przejdź do nowej aplikacji funkcji serwera sieci Web w portalu.

Wybierz **ustawienia**. Następnie przełącz **włączyć proxy funkcji Azure (wersja zapoznawcza)** do "Na".

Wybierz **ustawienia platformy** i wybierz polecenie **ustawienia aplikacji**.

Przewiń w dół do **ustawień aplikacji** i utworzyć nowe ustawienie z kluczem "HELLO_HOST". Ustaw jej wartość na hoście aplikacji funkcji wewnętrznej bazy danych, takich jak `<YourApp>.azurewebsites.net`. Jest to część adresu URL, które wcześniej zostały skopiowane podczas testowania funkcji HTTP. To ustawienie w konfiguracji później będziesz odwoływać.

> [!NOTE] 
> Ustawienia aplikacji są zalecane w przypadku konfiguracji hosta zapobiec zależności środowiska ustalony dla serwera proxy. Przy użyciu ustawień aplikacji oznacza, że konfiguracja serwera proxy można przenosić między środowiskami i zostaną zastosowane ustawienia aplikacji dla określonego środowiska.

Kliknij pozycję **Zapisz**.

### <a name="creating-a-proxy-on-the-frontend"></a>Tworzenie serwera proxy na frontonie

Przejdź z powrotem do aplikacji funkcji serwera sieci Web w portalu.

W obszarze nawigacji po lewej stronie, kliknij znak "+" obok "Serwery proxy (wersja zapoznawcza)".

![Tworzenie serwera proxy](./media/functions-create-serverless-api/creating-proxy.png)

Użyj ustawień serwera proxy, jak określono w tabeli.

| Pole | Wartość przykładowa | Opis |
|---|---|---|
| Nazwa | HelloProxy | Przyjazna nazwa używana tylko w przypadku zarządzania |
| Szablon trasy | / api/hello | Określa, jakie trasy służy do wywoływania tego serwera proxy |
| Adres URL wewnętrznej bazy danych | https://%HELLO_HOST%/API/Hello | Określa, do którego powinien być serwerem proxy żądania punktu końcowego |

Należy pamiętać, że nie ma serwerów proxy `/api` prefiks ścieżki podstawowej i ten musi być zawarte w szablonie trasy.

`%HELLO_HOST%` Składni będzie odwoływać się do ustawienia aplikacji utworzone wcześniej. Funkcja oryginalnego wskaże rozpoznać adres URL.

Kliknij przycisk **Utwórz**.

Można wypróbować nowego serwera proxy, kopiując adres URL serwera Proxy i testowanie go w przeglądarce lub z ulubionych klienta HTTP.

## <a name="create-a-mock-api"></a>Utwórz zasymulować interfejs API

Następnie użyje serwer proxy można utworzyć zasymulować interfejsu API dla rozwiązania. Dzięki temu programowanie klienta do postępu, bez konieczności wewnętrznej bazy danych, w pełni wdrożone. Później w rozwoju należy utworzyć nową aplikację funkcji, która obsługuje tę logikę i przekierowywania serwera proxy.

Aby utworzyć ten zasymulować interfejs API, utworzymy nowe proxy przy użyciu tego czasu [Edytor usług aplikacji](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). Aby rozpocząć, przejdź do aplikacji funkcji w portalu. Wybierz **funkcji platformy** i Znajdź **Edytor usług aplikacji**. Kliknięcie łącza zostanie otwarty Edytor usługi aplikacji na nowej karcie.

Wybierz `proxies.json` na lewym pasku nawigacyjnym. To jest plik zawierający konfigurację dla wszystkich sieci serwerów proxy. Jeśli używany jest jeden z [metody wdrażania funkcji](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), jest to plik mają być przechowywane w kontroli źródła. Aby dowiedzieć się więcej na temat tego pliku, zobacz [proxy Zaawansowana konfiguracja](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Jeśli wykonaniu wykonanej do tej pory, proxies.json Twojego powinna wyglądać następująco:

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

Następnie dodasz zasymulować interfejsu API. Zastąp plik proxies.json następujące czynności:

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

Spowoduje to dodanie nowego serwera proxy, "GetUserByName" bez właściwości backendUri. Zamiast kontaktować się z innym zasobem, modyfikuje domyślny z serwerów proxy przy użyciu zastąpienia odpowiedzi. Można także zastąpienia żądań i odpowiedzi w połączeniu z adresem URL wewnętrznej bazy danych. Jest to szczególnie przydatne podczas pośredniczenie dla starszej wersji systemu, której użytkownik może być konieczne zmodyfikowanie nagłówków, zapytania parametry itp. Aby dowiedzieć się więcej na temat zastąpienia żądań i odpowiedzi, zobacz [modyfikowanie żądań i odpowiedzi w proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Testowanie zasymulować interfejsu API przez wywołanie metody `/api/users/{username}` punktu końcowego za pomocą przeglądarki lub Twoje ulubione klienta REST. Pamiętaj zastąpić _{username}_ z wartością ciągu reprezentujący nazwę użytkownika.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono sposób tworzenia i dostosowywania interfejsu API na usługi Azure Functions. Przedstawiono również sposób Przełącz wielu interfejsów API, mocks, w tym razem jako powierzchnię interfejsu API unified. Te techniki służy do tworzenia interfejsów API żadnych złożoności wszystkie uruchomionej na modelu niekorzystającą obliczeniowe udostępniane przez usługi Azure Functions.

Następujące informacje mogą być pomocne podczas opracowywania dalsze interfejsu API:

- [Azure powiązania HTTP funkcje i elementu webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]
- [Dokumentowanie funkcje interfejsu API Azure (wersja zapoznawcza)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Praca z serwerów proxy funkcji Azure (wersja zapoznawcza)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
