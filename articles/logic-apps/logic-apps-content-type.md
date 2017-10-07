---
title: "typy zawartości aaaHandle - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sposób obsługi usługi Azure Logic Apps z typami zawartości projektu i środowiska wykonawczego"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Dojście do typów zawartości w aplikacji logiki

Wiele różnych typów zawartości mogą przepływać przez aplikację logiki, w tym JSON, XML, plików prostych i danych binarnych. Gdy hello aparat aplikacje logiki obsługuje wszystkie typy zawartości, są niektóre natywnie zrozumiałe hello aparat aplikacji logiki. Inne osoby mogą wymagać rzutowania lub konwersji w razie potrzeby. W tym artykule opisano, jak aparat hello obsługuje różne typy zawartości i jak toocorrectly obsługiwać te typy, gdy jest to konieczne.

## <a name="content-type-header"></a>Nagłówek Content-Type

toostart zasadniczo Przyjrzyjmy się hello dwa `Content-Types` wymagają konwersji lub Rzutowanie używanego w aplikacji logiki: `application/json` i `text/plain`.

## <a name="applicationjson"></a>Application/JSON

Witaj aparatu przepływu pracy polega na powitania `Content-Type` obsługa odpowiedniego hello toodetermine wywołuje nagłówka z protokołu HTTP. Każde żądanie o typie zawartości hello `application/json` są przechowywane i obsługiwane jako obiekt JSON. Ponadto zawartość JSON można przeanalizować domyślnie bez konieczności żadnych rzutowania. 

Na przykład, można przeanalizować żądanie ma nagłówek typu zawartości hello `application/json ` w przepływie pracy przy użyciu wyrażeń, takich jak `@body('myAction')['foo'][0]` tooget hello wartość `bar` w takim przypadku:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Nie dodatkowe rzutowanie jest niezbędne. Podczas pracy z danymi, które jest JSON, ale nie ma określonego nagłówka, można ręcznie rzutować go przy użyciu hello tooJSON `@json()` funkcji, na przykład: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Schemat i generator schematu

Witaj wyzwalacza żądania umożliwia tooenter schematu JSON dla ładunku hello spodziewasz się tooreceive. Ten schemat umożliwia projektanta hello generowania tokenów, więc będzie można korzystać z zawartości hello hello żądania. Jeśli nie masz schematu gotowe, wybierz **Użyj przykładowy ładunek toogenerate schematu**, więc można wygenerować schematu JSON z ładunku próbki.

![Schemat](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Akcja "Parse JSON"

Witaj `Parse JSON` pozwala analizować zawartość JSON w tokenach przyjazną wykorzystania aplikacji logiki. Podobne wyzwalacza żądania toohello, ta akcja umożliwia wprowadź lub wygenerować schematu JSON dla zawartości, które chcesz tooparse hello. To narzędzie ułatwia danych korzystanie z usługi Service Bus, bazy danych Azure rozwiązania Cosmos i tak dalej, znacznie.

![Przeanalizować składni JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>zwykły tekst

Podobne zbyt`application/json`, wiadomości HTTP odebrane z hello `Content-Type` nagłówek `text/plain` są przechowywane w postaci raw. Ponadto komunikaty te są zawarte w kolejne czynności bez rzutowania, te żądania przejść z `Content-Type`: `text/plain` nagłówka. Na przykład podczas pracy z pliku prostego, można uzyskać ten HTTP zawartości jako `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

W następnej akcji hello, w przypadku wysłania żądania hello jako hello treści żądania innego (`@body('flatfile')`), musi żądania hello `text/plain` nagłówka Content-Type. Podczas pracy z danymi, które jest w formacie zwykłego tekstu, ale nie ma określonego nagłówka, można ręcznie rzutować hello tootext danych przy użyciu hello `@string()` funkcji, na przykład: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Aplikacja/xml i funkcji Application/octet-stream i konwertera

Hello aparat aplikacje logiki zawsze zachowuje hello `Content-Type` który został odebrany w hello HTTP żądania lub odpowiedzi. Dlatego jeśli aparat hello odbiera zawartość z hello `Content-Type` z `application/octet-stream`, i obejmują, że zawartość w kolejnych akcji bez rzutowania, żądania wychodzącego hello ma `Content-Type`: `application/octet-stream`. W ten sposób aparat hello można zagwarantować, że utratę danych podczas przenoszenia za pomocą hello przepływu pracy. Jednak stan akcji hello (wejścia i wyjścia) jest przechowywana w obiekt JSON, ponieważ hello przenosi stan za pomocą hello przepływu pracy. Dlatego toopreserve konwertuje niektórych typów danych aparatu hello hello tooa zawartości binary base64 zakodowany ciąg z odpowiednie metadane, która zachowuje zarówno `$content` i `$content-type`, które są automatycznie przekonwertować. 

* `@json()`-zbyt rzutuje danych`application/json`
* `@xml()`-zbyt rzutuje danych`application/xml`
* `@binary()`-zbyt rzutuje danych`application/octet-stream`
* `@string()`-zbyt rzutuje danych`text/plain`
* `@base64()`-Konwertuje ciąg base64 tooa zawartości
* `@base64toString()`-zbyt konwertuje ciąg kodowany w standardzie base64`text/plain`
* `@base64toBinary()`-zbyt konwertuje ciąg kodowany w standardzie base64`application/octet-stream`
* `@encodeDataUri()`-koduje ciągiem w postaci tablicy bajtów dataUri
* `@decodeDataUri()`-dekoduje dataUri do tablicy typu byte

Na przykład w przypadku otrzymania żądania HTTP z `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Można rzutować i później użyć przypominać `@xml(triggerBody())`, lub w funkcji, takich jak `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Inne typy zawartości

Inne typy zawartości są obsługiwane i pracy z usługą logic apps, ale może wymagać ręcznego pobierania treści wiadomości powitania przez dekodowania hello `$content`. Na przykład, załóżmy, że użytkownik zainicjuje `application/x-www-url-formencoded` żądania where `$content` jest ładunku hello zakodowane jako toopreserve ciąg base64 wszystkich danych:

```
CustomerName=Frank&Address=123+Avenue
```

Ponieważ hello żądania nie jest w postaci zwykłego tekstu lub JSON, Żądanie hello są przechowywane w akcji hello w następujący sposób:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Obecnie nie ma funkcji macierzystej dla danych formularza, więc można nadal używać tych danych w przepływie pracy, przez ręcznie podczas uzyskiwania dostępu do danych hello za pomocą funkcji, takich jak `@string(body('formdataAction'))`. Jeśli potrzebujesz hello żądania wychodzącego tooalso ma hello `application/x-www-url-formencoded` nagłówek typu zawartości, można dodać treści hello żądania toohello akcji bez żadnych rzutowania, takich jak `@body('formdataAction')`. Jednak ta metoda działa tylko, jeśli treść hello jest tylko parametr hello w hello `body` wejściowego. Jeśli spróbujesz toouse `@body('formdataAction')` w `application/json` żądania, pobrać błąd w czasie wykonywania, ponieważ treść hello zakodowane są wysyłane.

