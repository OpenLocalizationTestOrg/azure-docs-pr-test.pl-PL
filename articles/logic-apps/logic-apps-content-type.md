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
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="6ef3f-103">Dojście do typów zawartości w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="6ef3f-103">Handle content types in logic apps</span></span>

<span data-ttu-id="6ef3f-104">Wiele różnych typów zawartości mogą przepływać przez aplikację logiki, w tym JSON, XML, plików prostych i danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="6ef3f-105">Gdy hello aparat aplikacje logiki obsługuje wszystkie typy zawartości, są niektóre natywnie zrozumiałe hello aparat aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="6ef3f-106">Inne osoby mogą wymagać rzutowania lub konwersji w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="6ef3f-107">W tym artykule opisano, jak aparat hello obsługuje różne typy zawartości i jak toocorrectly obsługiwać te typy, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="6ef3f-108">Nagłówek Content-Type</span><span class="sxs-lookup"><span data-stu-id="6ef3f-108">Content-Type Header</span></span>

<span data-ttu-id="6ef3f-109">toostart zasadniczo Przyjrzyjmy się hello dwa `Content-Types` wymagają konwersji lub Rzutowanie używanego w aplikacji logiki: `application/json` i `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="6ef3f-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="6ef3f-110">Application/JSON</span></span>

<span data-ttu-id="6ef3f-111">Witaj aparatu przepływu pracy polega na powitania `Content-Type` obsługa odpowiedniego hello toodetermine wywołuje nagłówka z protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="6ef3f-112">Każde żądanie o typie zawartości hello `application/json` są przechowywane i obsługiwane jako obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="6ef3f-113">Ponadto zawartość JSON można przeanalizować domyślnie bez konieczności żadnych rzutowania.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="6ef3f-114">Na przykład, można przeanalizować żądanie ma nagłówek typu zawartości hello `application/json ` w przepływie pracy przy użyciu wyrażeń, takich jak `@body('myAction')['foo'][0]` tooget hello wartość `bar` w takim przypadku:</span><span class="sxs-lookup"><span data-stu-id="6ef3f-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="6ef3f-115">Nie dodatkowe rzutowanie jest niezbędne.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-115">No additional casting is needed.</span></span> <span data-ttu-id="6ef3f-116">Podczas pracy z danymi, które jest JSON, ale nie ma określonego nagłówka, można ręcznie rzutować go przy użyciu hello tooJSON `@json()` funkcji, na przykład: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="6ef3f-117">Schemat i generator schematu</span><span class="sxs-lookup"><span data-stu-id="6ef3f-117">Schema and schema generator</span></span>

<span data-ttu-id="6ef3f-118">Witaj wyzwalacza żądania umożliwia tooenter schematu JSON dla ładunku hello spodziewasz się tooreceive.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="6ef3f-119">Ten schemat umożliwia projektanta hello generowania tokenów, więc będzie można korzystać z zawartości hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="6ef3f-120">Jeśli nie masz schematu gotowe, wybierz **Użyj przykładowy ładunek toogenerate schematu**, więc można wygenerować schematu JSON z ładunku próbki.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schemat](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="6ef3f-122">Akcja "Parse JSON"</span><span class="sxs-lookup"><span data-stu-id="6ef3f-122">'Parse JSON' action</span></span>

<span data-ttu-id="6ef3f-123">Witaj `Parse JSON` pozwala analizować zawartość JSON w tokenach przyjazną wykorzystania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="6ef3f-124">Podobne wyzwalacza żądania toohello, ta akcja umożliwia wprowadź lub wygenerować schematu JSON dla zawartości, które chcesz tooparse hello.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="6ef3f-125">To narzędzie ułatwia danych korzystanie z usługi Service Bus, bazy danych Azure rozwiązania Cosmos i tak dalej, znacznie.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Przeanalizować składni JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="6ef3f-127">zwykły tekst</span><span class="sxs-lookup"><span data-stu-id="6ef3f-127">Text/plain</span></span>

<span data-ttu-id="6ef3f-128">Podobne zbyt`application/json`, wiadomości HTTP odebrane z hello `Content-Type` nagłówek `text/plain` są przechowywane w postaci raw.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="6ef3f-129">Ponadto komunikaty te są zawarte w kolejne czynności bez rzutowania, te żądania przejść z `Content-Type`: `text/plain` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="6ef3f-130">Na przykład podczas pracy z pliku prostego, można uzyskać ten HTTP zawartości jako `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="6ef3f-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="6ef3f-131">W następnej akcji hello, w przypadku wysłania żądania hello jako hello treści żądania innego (`@body('flatfile')`), musi żądania hello `text/plain` nagłówka Content-Type.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="6ef3f-132">Podczas pracy z danymi, które jest w formacie zwykłego tekstu, ale nie ma określonego nagłówka, można ręcznie rzutować hello tootext danych przy użyciu hello `@string()` funkcji, na przykład: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="6ef3f-133">Aplikacja/xml i funkcji Application/octet-stream i konwertera</span><span class="sxs-lookup"><span data-stu-id="6ef3f-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="6ef3f-134">Hello aparat aplikacje logiki zawsze zachowuje hello `Content-Type` który został odebrany w hello HTTP żądania lub odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="6ef3f-135">Dlatego jeśli aparat hello odbiera zawartość z hello `Content-Type` z `application/octet-stream`, i obejmują, że zawartość w kolejnych akcji bez rzutowania, żądania wychodzącego hello ma `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="6ef3f-136">W ten sposób aparat hello można zagwarantować, że utratę danych podczas przenoszenia za pomocą hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="6ef3f-137">Jednak stan akcji hello (wejścia i wyjścia) jest przechowywana w obiekt JSON, ponieważ hello przenosi stan za pomocą hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="6ef3f-138">Dlatego toopreserve konwertuje niektórych typów danych aparatu hello hello tooa zawartości binary base64 zakodowany ciąg z odpowiednie metadane, która zachowuje zarówno `$content` i `$content-type`, które są automatycznie przekonwertować.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="6ef3f-139">`@json()`-zbyt rzutuje danych`application/json`</span><span class="sxs-lookup"><span data-stu-id="6ef3f-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="6ef3f-140">`@xml()`-zbyt rzutuje danych`application/xml`</span><span class="sxs-lookup"><span data-stu-id="6ef3f-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="6ef3f-141">`@binary()`-zbyt rzutuje danych`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="6ef3f-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="6ef3f-142">`@string()`-zbyt rzutuje danych`text/plain`</span><span class="sxs-lookup"><span data-stu-id="6ef3f-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="6ef3f-143">`@base64()`-Konwertuje ciąg base64 tooa zawartości</span><span class="sxs-lookup"><span data-stu-id="6ef3f-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="6ef3f-144">`@base64toString()`-zbyt konwertuje ciąg kodowany w standardzie base64`text/plain`</span><span class="sxs-lookup"><span data-stu-id="6ef3f-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="6ef3f-145">`@base64toBinary()`-zbyt konwertuje ciąg kodowany w standardzie base64`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="6ef3f-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="6ef3f-146">`@encodeDataUri()`-koduje ciągiem w postaci tablicy bajtów dataUri</span><span class="sxs-lookup"><span data-stu-id="6ef3f-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="6ef3f-147">`@decodeDataUri()`-dekoduje dataUri do tablicy typu byte</span><span class="sxs-lookup"><span data-stu-id="6ef3f-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="6ef3f-148">Na przykład w przypadku otrzymania żądania HTTP z `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="6ef3f-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="6ef3f-149">Można rzutować i później użyć przypominać `@xml(triggerBody())`, lub w funkcji, takich jak `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="6ef3f-150">Inne typy zawartości</span><span class="sxs-lookup"><span data-stu-id="6ef3f-150">Other content types</span></span>

<span data-ttu-id="6ef3f-151">Inne typy zawartości są obsługiwane i pracy z usługą logic apps, ale może wymagać ręcznego pobierania treści wiadomości powitania przez dekodowania hello `$content`.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="6ef3f-152">Na przykład, załóżmy, że użytkownik zainicjuje `application/x-www-url-formencoded` żądania where `$content` jest ładunku hello zakodowane jako toopreserve ciąg base64 wszystkich danych:</span><span class="sxs-lookup"><span data-stu-id="6ef3f-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="6ef3f-153">Ponieważ hello żądania nie jest w postaci zwykłego tekstu lub JSON, Żądanie hello są przechowywane w akcji hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6ef3f-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Obecnie nie ma funkcji macierzystej dla danych formularza, więc można nadal używać tych danych w przepływie pracy, przez ręcznie podczas uzyskiwania dostępu do danych hello za pomocą funkcji, takich jak `@string(body('formdataAction'))`. Jeśli potrzebujesz hello żądania wychodzącego tooalso ma hello `application/x-www-url-formencoded` nagłówek typu zawartości, można dodać treści hello żądania toohello akcji bez żadnych rzutowania, takich jak `@body('formdataAction')`. Jednak ta metoda działa tylko, jeśli treść hello jest tylko parametr hello w hello `body` wejściowego. <span data-ttu-id="6ef3f-157">Jeśli spróbujesz toouse `@body('formdataAction')` w `application/json` żądania, pobrać błąd w czasie wykonywania, ponieważ treść hello zakodowane są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="6ef3f-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

