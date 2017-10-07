---
title: "aaaCreate web API i interfejsów API REST łączników - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie sieci web toocall interfejsów API i interfejsów API REST z interfejsów API, usług lub systemów w przepływach pracy systemu integracji z usługą Azure Logic Apps"
keywords: "sieci Web API, interfejsy API REST, łączniki, przepływy pracy, integracji systemu"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Tworzenie niestandardowych interfejsów API łączników dla usługi logic apps

Mimo że Azure Logic Apps oferuje [100 + łączników](../connectors/apis-list.md) czy można użyć w przepływach pracy aplikacji logiki, może być toocall interfejsów API, systemów i usług, które nie są dostępne jako łączniki. Możesz utworzyć własne niestandardowe interfejsów API, które zapewniają toouse działania i jest wyzwalane w aplikacjach logiki. W tym miejscu są też inne przyczyny, dlaczego warto toocreate własnych interfejsów API za pomocą łączników w aplikacjach logiki:

* Rozszerzanie bieżący system integracji i dane integrację przepływów pracy.
* Pomóc klientom Użyj zadań usługi toomanage professional lub osobiste.
* Rozwiń hello reach, odnajdywania i użycia dla usługi.

Zasadniczo łączników są interfejsów API REST na użytek podłączany interfejsów sieci web [format metadanych struktury Swagger](http://swagger.io/specification/) dla dokumentacji i dane JSON jako ich format wymiany danych. Ponieważ łączniki są interfejsów API REST, które komunikują się za pośrednictwem punktów końcowych HTTP, można użyć dowolnego języka, takich jak .NET, Java lub Node.js do tworzenia łączników. Można również udostępnić swoje interfejsy API na [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md), platformy jako — usługa (PaaS) oferta zapewnia sposoby najlepsze najprostszym i najbardziej skalowalny hello do obsługi interfejsu API. 

W przypadku niestandardowych interfejsów API toowork z usługą logic apps, interfejs API może zapewnić [ *akcje* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) który wykonywania określonych zadań w przepływach pracy aplikacji logiki. Interfejs API mogą również działać jako [ *wyzwalacza* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) zaczynającym się przepływu pracy aplikacji logiki w przypadku nowych danych lub zdarzeń spełnia określony warunek. W tym temacie opisano typowe wzorce, które możesz wykonać do tworzenia działań i wyzwalaczy interfejsu API, na podstawie zachowania hello, które mają tooprovide Twojego interfejsu API.

> [!TIP] 
> Mimo że można wdrożyć swoje interfejsy API jako [sieci web apps](../app-service-web/app-service-web-overview.md), warto wdrożyć swoje interfejsy API jako [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md), które mogą ułatwić zadania podczas kompilacji, hosta i korzystanie z interfejsów API w chmurze hello i lokalnie. Nie można znaleźć toochange dowolny kod swoje interfejsy API — wystarczy go wdrożyć aplikację interfejsu API tooan kodu. Dowiedz się, jak za [tworzenie aplikacji interfejsu API utworzone za pomocą programu ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), lub [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Przykłady aplikacji interfejsu API utworzony dla usługi logic apps, można znaleźć hello [repozytorium GitHub aplikacje logiki platformy Azure](http://github.com/logicappsio) lub [blogu](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Przydatne tools

Niestandardowy interfejs API, najlepiej z usługą logic apps ma również hello interfejsu API [dokumentu Swagger](http://swagger.io/specification/) opisujący operacji hello interfejsu API i parametry.
Wiele bibliotek, takich jak [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), można automatycznie generować hello plik struktury Swagger dla Ciebie. Plik struktury Swagger hello tooannotate dla nazw wyświetlanych, typy właściwości i tak dalej, można również użyć [TRex](https://github.com/nihaue/TRex) tak, aby plik struktury Swagger działa poprawnie z usługą logic apps.

<a name="actions"></a>

## <a name="action-patterns"></a>Wzorce akcji

Dla zadań tooperform aplikacji logiki, niestandardowego interfejsu API powinno dostarczyć [ *akcje*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Każdej operacji interfejsu API map tooan akcji. Podstawowe akcja jest kontrolera, który akceptuje żądania HTTP i zwraca odpowiedzi HTTP. Tak na przykład aplikacji logiki wysyła aplikacji interfejsu API lub aplikacji sieci web tooyour żądania HTTP. Aplikacja zwraca odpowiedź HTTP, wraz z zawartością, która hello logiki aplikacji może przetworzyć.

Działania standardowe możesz zapisać metoda żądania HTTP w interfejsie API i opis tej metody w pliku programu Swagger. Następnie można wywołać interfejsu API bezpośrednio z [akcji HTTP](../connectors/connectors-native-http.md) lub [HTTP + Swagger](../connectors/connectors-native-http-swagger.md) akcji. Domyślnie odpowiedzi musi zostać zwrócona w hello [limit czasu żądania](./logic-apps-limits-and-config.md). 

![Działania standardowe wzorca](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake aplikacji logiki Zaczekaj, aż interfejs API zakończy dłużej uruchomione zadania, interfejsu API można wykonać hello [wzorca asynchronicznego sondowania](#async-pattern) lub hello [wzorca asynchronicznego elementu webhook](#webhook-actions) opisanych w tym temacie. Dla odpowiednio, która pomaga zwizualizować różne zachowania tych wzorców Załóżmy procesu hello niestandardowych ciasto z bakery porządkowania. wzorzec sondowania Hello dubluje zachowanie hello, gdzie należy wywołać hello bakery toocheck co 20 minut czy ciasto hello jest gotowy. wzorzec elementu webhook Hello odzwierciedla zachowanie hello gdzie hello bakery monituje o numer telefonu, ich można wywołać, gdy ciasto hello jest gotowy.

Przykłady, można znaleźć hello [repozytorium GitHub aplikacje logiki](https://github.com/logicappsio). Ponadto Dowiedz się więcej o [zbierania danych użycia dla akcji](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Wykonywania długotrwałych zadań z hello sondowania wzorzec akcji

Interfejs API zadań, które można uruchomić dłuższy niż hello toohave [limit czasu żądania](./logic-apps-limits-and-config.md), można używać hello wzorca asynchronicznego sondowania. Ten wzorzec ma użytkownika interfejsu API działają w oddzielnym wątku, ale zachowaj aparat aktywnego połączenia toohello Logic Apps. W ten sposób aplikacji logiki hello nie nie upłynął limit czasu lub kontynuować hello następnego kroku w przepływie pracy hello zanim interfejsu API zakończy pracę.

Poniżej przedstawiono ogólne wzorzec hello:

1. Upewnij się, że który aparat hello wie, że Twój interfejs API zaakceptowano Żądanie hello i zaczął działać.
2. Gdy aparat hello sprawia, że kolejne żądania dotyczące stanu zadania, umożliwiają aparat hello wiedzieć, kiedy interfejsu API kończy zadanie hello.
3. Zwróć aparat toohello odpowiednie dane tak, aby kontynuować przepływ pracy aplikacji logiki hello.

<a name="bakery-polling-action"></a>Teraz zastosować hello wcześniejszego wzorca bakery odpowiednio toohello sondowania i Załóżmy, że należy wywołać bakery i kolejność ciasto niestandardowych w celu dostarczania. Hello procesu dokonywania ciasto hello jest czasochłonne i nie mają toowait w telefonie hello podczas hello bakery działa na powitania ciasto. Hello bakery potwierdzenie zamówienia i ma należy wywołać co 20 minut ciasto hello stanu. Po przekazać 20 minut, należy wywołać hello bakery, ale ich informujące, że nie jest wykonywane je i że należy wywołać w innym 20 minut. Ten proces Wstecz i w przód jest kontynuowany do momentu wywołania i hello bakery informuje, że Twoje zamówienie jest gotowa i dostarcza je. 

Więc warto Mapuj ponownie ten wzorzec sondowania. Hello bakery reprezentuje niestandardowego interfejsu API, gdy, powitania klienta ciasto, oświadczasz hello aplikacje logiki aparatu. Gdy aparat hello wywołuje interfejs API żądanie, interfejs API potwierdza Żądanie hello i reaguje z hello interwał czasu, gdy aparat hello można sprawdzić stan zadania. Aparat Hello kontynuuje sprawdzanie stanu zadania, dopóki Twój interfejs API odpowiada się, że odbywa się to zadanie hello i zwraca dane tooyour logikę aplikacji, która następnie jest kontynuowana przepływu pracy. 

![Wzorzec akcji sondowania](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Poniżej przedstawiono hello etapy toofollow Twojego interfejsu API, opisane z punktu widzenia hello interfejsu API:

1. Jeśli Twój interfejs API pobiera HTTP żądania toostart pracy, natychmiast zwracany HTTP `202 ACCEPTED` odpowiedzi z hello `location` nagłówka opisane w dalszej części tego kroku. Ta odpowiedź umożliwia hello aplikacje logiki aparatu wiedzieć, że Twój interfejs API uzyskano hello żądania, ładunku żądania akceptowane hello (dane wejściowe), a teraz przetwarza. 
   
   Witaj `202 ACCEPTED` odpowiedź powinna zawierać te nagłówki:
   
   * *Wymagane*: A `location` nagłówek, który określa hello ścieżkę bezwzględną tooa adresu URL, gdzie hello aparat Logic Apps można sprawdzić stan zadania Twój interfejs API

   * *Opcjonalne*: A `retry-after` nagłówek, który określa hello liczbę sekund, które hello aparat powinien zaczekać na sprawdzanie hello `location` adres URL dla stanu zadania. 

     Domyślnie aparat hello sprawdza co 20 sekund. toospecify inny interwał, obejmują hello `retry-after` nagłówka i hello liczbę sekund, aż do następnego sondowania hello.

2. Po hello określony upływu czasu, hello Logic Apps aparat hello sond `location` stan zadania toocheck adresu URL. Interfejs API należy te sprawdzania instalacji i zwracać tych odpowiedzi:
   
   * W przypadku pracę hello zwraca HTTP `200 OK` odpowiedzi, wraz z ładunku odpowiedzi hello (dane wejściowe dla następnego kroku hello).

   * Jeśli nadal przetwarza zadanie hello, zwróć inny HTTP `202 ACCEPTED` odpowiedzi, ale bez hello tego samego nagłówków odpowiedzi oryginalnego hello.

Kiedy interfejsu API ten wzorzec, nie masz toodo niczego w hello logiki aplikacji przepływu pracy definicji toocontinue sprawdzania stanu zadania. Gdy aparat hello pobiera HTTP `202 ACCEPTED` odpowiedzi i prawidłową `location` nagłówek, hello aparat względem hello asynchroniczny wzorzec i kontroli hello `location` nagłówka, dopóki Twój interfejs API zwraca odpowiedź z systemem innym niż 202.

> [!TIP]
> Na przykład wzorca asynchronicznego, przejrzyj [próbki odpowiedzi kontrolera asynchronicznego w serwisie GitHub](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Wykonywania długotrwałych zadań z wzorcem akcji elementu webhook hello

Alternatywnie można używać wzorca elementu webhook hello długotrwałych zadań i przetwarzania asynchronicznego. Ten wzorzec jest aplikacji logiki hello wstrzymać i poczekaj, aż "callback" z Twojej toofinish interfejsu API przetwarzania przed kontynuowaniem przepływu pracy. To wywołanie zwrotne jest HTTP POST, wysyłanej URL tooa wiadomości, gdy zdarzenie. 

<a name="bakery-webhook-action"></a>Teraz zastosować hello poprzedniego bakery odpowiednio toohello elementu webhook wzorca i Załóżmy, że należy wywołać bakery i kolejność ciasto niestandardowych w celu dostarczania. Hello procesu dokonywania ciasto hello jest czasochłonne i nie mają toowait w telefonie hello podczas hello bakery działa na powitania ciasto. Witaj bakery potwierdzenie zamówienia, ale teraz, możesz nadać im numer telefonu, ich można wywołać po zakończeniu ciasto hello. Teraz, hello bakery informuje, kiedy Twoje zamówienie jest gotowy, a następnie dostarcza je.

Gdy firma Microsoft mapować tego elementu webhook wzorca ponownie, hello bakery reprezentuje niestandardowego interfejsu API, podczas możesz powitania klienta ciasto, reprezentują hello aplikacje logiki aparatu. Aparat Hello wywołuje interfejs API żądanie i zawiera adres URL "wywołania zwrotnego".
Po zakończeniu zadania hello interfejsu API używa hello adresu URL toonotify hello aparatu i zwracać tooyour aplikacji logiki danych, który następnie jest kontynuowana przepływu pracy. 

Dla tego wzorca zdefiniować dwa punkty końcowe na kontrolerze: `subscribe` i`unsubscribe`

*  `subscribe`punkt końcowy: podczas wykonywania osiągnie Twój interfejs API działań w przepływie pracy hello, hello Logic Apps aparat hello wywołania `subscribe` punktu końcowego. Ten krok powoduje toocreate aplikacji logiki hello adresów URL wywołania zwrotnego, które interfejs API przechowuje i poczekaj wywołania zwrotnego hello z interfejsu API po zakończeniu pracy. Interfejs API, a następnie wywołuje z adresem URL HTTP POST toohello i przekazuje wszystkie zwrócone zawartości i nagłówków jako aplikacji logiki toohello wejściowego.

* `unsubscribe`punkt końcowy: Jeśli Uruchom aplikację logiki hello została anulowana, hello Logic Apps aparat hello wywołania `unsubscribe` punktu końcowego. Interfejs API można wyrejestrować adres URL wywołania zwrotnego hello i Zatrzymaj wszystkie procesy w razie potrzeby.

![Wzorzec akcji elementu Webhook](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Obecnie usługa hello projektanta aplikacji logiki nie obsługuje odnajdowania elementu webhook punktów końcowych za pośrednictwem struktury Swagger. Dlatego dla tego wzorca należy tooadd [ **Webhook** akcji](../connectors/connectors-native-webhook.md) i określ adres URL hello, nagłówki i treści żądania. Zobacz też [działania przepływu pracy i wyzwalaczy](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass w adresie URL wywołania zwrotnego hello, można użyć hello `@listCallbackUrl()` funkcji przepływu pracy w polach poprzedniej hello odpowiednio do potrzeb.

> [!TIP]
> Na przykład elementu webhook wzorzec, przejrzyj [próbki wyzwalacza elementu webhook w serwisie GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Wzorce wyzwalacza

Niestandardowy interfejs API może działać jako [ *wyzwalacza* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) zaczynającym się aplikacji logiki w przypadku nowych danych lub zdarzeń spełnia określony warunek. Wyzwalacz można regularnie, sprawdź lub poczekać i nasłuchiwania nowych danych lub zdarzeń na punkt końcowy usługi. Jeśli nowe dane lub zdarzenia spełnia hello określony warunek, wyzwalacz hello generowane i uruchamia hello logikę aplikacji, która nasłuchuje toothat wyzwalacza. aplikacje logiki toostart w ten sposób interfejsu API można wykonać hello [ *wyzwalacza sondowania* ](#polling-triggers) lub hello [ *wyzwalacza elementu webhook* ](#webhook-triggers) wzorca. Te wzorce są podobne odpowiednikami tootheir dla [sondowania akcje](#async-pattern) i [Akcje elementu webhook](#webhook-actions). Ponadto Dowiedz się więcej o [wyzwalaczy zbierania danych użycia](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Sprawdź, czy nowych danych lub zdarzeń regularnie o hello sondowania wzorzec wyzwalacza

A *wyzwalacza sondowania* działa podobnie hello [akcji sondowania](#async-pattern) opisanych wcześniej w tym temacie. Aparat Logic Apps Hello okresowo wywołuje i sprawdza hello wyzwalacza końcowy dla nowych danych lub zdarzeń. Jeśli aparat hello znajdzie nowych danych lub zdarzenia spełniającego określony warunek, hello wyzwalacza. Następnie aparat hello tworzy wystąpienie aplikacji logiki, który przetwarza dane hello jako dane wejściowe. 

![Sondowanie wzorzec wyzwalacza](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Każde żądanie sondowania jest traktowana jako wykonanie akcji, nawet wtedy, gdy jest tworzone żadne wystąpienie aplikacji logiki. Przetwarzanie tooprevent hello tych samych danych wiele razy, wyzwalacz należy wyczyścić dane, które już zostało odczytane i przekazane toohello aplikacji logiki.

Oto etapy wyzwalacz sondowania opisem z punktu widzenia hello interfejsu API:

| Znaleziono nowych danych lub zdarzeń?  | Odpowiedzi interfejsu API | 
| ------------------------- | ------------ |
| Znaleziono | Zwraca HTTP `200 OK` stan o ładunku odpowiedzi hello (dane wejściowe dla następnego kroku). <br/>Ta odpowiedź tworzy wystąpienie aplikacji logiki i uruchamia hello przepływu pracy. |
| Nie można odnaleźć | Zwraca HTTP `202 ACCEPTED` stan o `location` nagłówka i `retry-after` nagłówka. <br/>Wyzwalaczy, hello `location` nagłówka powinien również zawierać `triggerState` parametru zapytania, który zazwyczaj jest to "sygnatura czasowa". Interfejs API można użyć tego identyfikatora tootrack hello ostatniego hello logiki aplikacji zostało wyzwolone. |

Na przykład tooperiodically Sprawdzanie usługi dla nowych plików, może zbudować wyzwalacz sondowania, który ma następujące zachowania:

| Żądanie zawiera `triggerState`? | Odpowiedzi interfejsu API |
| -------------------------------- | -------------|
| Nie | Zwraca HTTP `202 ACCEPTED` stanu oraz `location` nagłówek o `triggerState` ustawić toohello bieżący czas i hello `retry-after` too15 interwał czasowy w sekundach. |
| Tak | Sprawdź usługi plików po hello dodaje `DateTime` dla `triggerState`. |

| Liczba znalezionych plików | Odpowiedzi interfejsu API |
| --------------------- | -------------|
| Pojedynczy plik | Zwraca HTTP `200 OK` stanu i hello ładunek zawartości, aktualizacja `triggerState` toohello `DateTime` hello pliku zwróconego i ustawić `retry-after` too15 interwał czasowy w sekundach. |
| Wiele plików | Zwróć jeden plik w czasie i HTTP `200 OK` stan, aktualizacja `triggerState`i ustaw hello `retry-after` too0 interwał czasowy w sekundach. </br>Te kroki let aparat hello dowiedzieć się, że dostępnych jest więcej danych i który aparat hello natychmiast powinien zażądać hello danych z adresu URL hello w hello `location` nagłówka. |
| Brak plików | Zwraca HTTP `202 ACCEPTED` stanu, nie zmieniaj `triggerState`i ustaw hello `retry-after` too15 interwał czasowy w sekundach. |

> [!TIP]
> Na przykład sondowania wzorzec wyzwalacza, przejrzyj to [próbki kontrolera wyzwalacza sondowania w serwisie GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Zaczekaj i nasłuchiwania nowych danych lub zdarzeń wzorem wyzwalacza hello elementu webhook

Wyzwalacz elementu webhook jest *wyzwalacz wypychania* czeka i nasłuchuje nowych danych lub zdarzeń na punktu końcowego usługi. Jeśli nowe dane lub zdarzenia spełnia hello określony warunek, uruchamiany wyzwalacza hello i tworzy wystąpienie aplikacji logiki, która następnie przetwarza hello danych jako dane wejściowe.
Wyzwalacze elementu Webhook działanie podobne jak w przypadku hello [Akcje elementu webhook](#webhook-actions) wcześniej w tym temacie opisano i skonfigurowano `subscribe` i `unsubscribe` punktów końcowych. 

* `subscribe`punkt końcowy: podczas dodawania i zapisać wyzwalacza elementu webhook w aplikacji logiki aplikacji logiki hello aparat hello wywołania `subscribe` punktu końcowego. Ten krok powoduje toocreate aplikacji logiki hello wywołania zwrotnego adresu URL, który przechowuje interfejsu API. Brak nowych danych lub zdarzenie, które spełnia hello określony warunek, interfejs API wywołuje z adresem URL toohello HTTP POST. ładunek zawartości Hello i nagłówków przekazać jako aplikacji logiki toohello wejściowego.

* `unsubscribe`punkt końcowy: usunięcie wyzwalacza elementu webhook hello lub całą logikę aplikacji hello Logic Apps aparat hello wywołania `unsubscribe` punktu końcowego. Interfejs API można wyrejestrować adres URL wywołania zwrotnego hello i Zatrzymaj wszystkie procesy w razie potrzeby.

![Wzorzec wyzwalacza elementu Webhook](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Obecnie usługa hello projektanta aplikacji logiki nie obsługuje odnajdowania elementu webhook punktów końcowych za pośrednictwem struktury Swagger. Dlatego dla tego wzorca należy tooadd [ **Webhook** wyzwalacza](../connectors/connectors-native-webhook.md) i określ adres URL hello, nagłówki i treści żądania. Zobacz też [wyzwalacza HTTPWebhook](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass w adresie URL wywołania zwrotnego hello, można użyć hello `@listCallbackUrl()` funkcji przepływu pracy w polach poprzedniej hello odpowiednio do potrzeb.
>
> Przetwarzanie tooprevent hello tych samych danych wiele razy, wyzwalacz należy wyczyścić dane, które już zostało odczytane i przekazane toohello aplikacji logiki.

> [!TIP]
> Na przykład elementu webhook wzorzec, przejrzyj [próbki kontrolera wyzwalacza elementu webhook w serwisie GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Wdrożenia, wywołaj i zabezpieczyć niestandardowych interfejsów API

Po utworzeniu sieci niestandardowych interfejsów API, skonfiguruj swoje interfejsy API dla wdrożenia, możesz je bezpiecznie wywołać. Dowiedz się, jak za[wdrażania, wywołaj i zabezpieczyć niestandardowych interfejsów API dla usługi logic apps](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Publikowanie niestandardowych tooAzure interfejsów API

toomake Twojego niestandardowych interfejsów API dostępne do użytku publicznego na platformie Azure, przesłać toohello Twojego nominacji [programu Microsoft Azure certyfikowane](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Uzyskiwanie pomocy

Aby uzyskać pomoc przy niestandardowych interfejsów API, skontaktuj się z [ customapishelp@microsoft.com ](mailto:customapishelp@microsoft.com).

pytania tooask, odpowiadanie na pytania i robią innych użytkowników usługi Azure Logic Apps, zobacz odwiedź hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników Logic Apps](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Następne kroki

* [Akcje i wyzwalaczy zbierania danych użycia](logic-apps-pricing.md)
* [Obsługa typów zawartości](./logic-apps-content-type.md)
* [Obsługa błędów i wyjątków](./logic-apps-exception-handling.md)
* [Bezpieczny dostęp do aplikacji logiki tooyour](./logic-apps-securing-a-logic-app.md)
* [Wywołaj wyzwalacz, lub zagnieżdżania logiki aplikacji za pomocą punktów końcowych HTTP](./logic-apps-http-endpoint.md)