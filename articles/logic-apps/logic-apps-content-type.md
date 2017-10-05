---
title: "Obsługa typów zawartości — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="cc222-103">Dojście do typów zawartości w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="cc222-103">Handle content types in logic apps</span></span>

<span data-ttu-id="cc222-104">Wiele różnych typów zawartości mogą przepływać przez aplikację logiki, w tym JSON, XML, plików prostych i danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="cc222-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="cc222-105">Gdy aparat aplikacje logiki obsługuje wszystkie typy zawartości, niektóre natywnie zrozumiane przez aparat aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="cc222-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="cc222-106">Inne osoby mogą wymagać rzutowania lub konwersji w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="cc222-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="cc222-107">W tym artykule opisano sposób aparat obsługi różnych typów zawartości oraz sposób prawidłowej obsługi tych typów, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cc222-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="cc222-108">Nagłówek Content-Type</span><span class="sxs-lookup"><span data-stu-id="cc222-108">Content-Type Header</span></span>

<span data-ttu-id="cc222-109">Aby uruchomić zasadniczo, Przyjrzyjmy się dwa `Content-Types` wymagają konwersji lub Rzutowanie używanego w aplikacji logiki: `application/json` i `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="cc222-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="cc222-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="cc222-110">Application/JSON</span></span>

<span data-ttu-id="cc222-111">Aparatu przepływu pracy polega na `Content-Type` nagłówka z protokołu HTTP wymaga aby określić odpowiednią obsługę.</span><span class="sxs-lookup"><span data-stu-id="cc222-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="cc222-112">Wszystkie żądania z typem zawartości `application/json` są przechowywane i obsługiwane jako obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="cc222-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="cc222-113">Ponadto zawartość JSON można przeanalizować domyślnie bez konieczności żadnych rzutowania.</span><span class="sxs-lookup"><span data-stu-id="cc222-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="cc222-114">Na przykład, można przeanalizować żądanie ma nagłówek typu zawartości `application/json ` w przepływie pracy przy użyciu wyrażeń, takich jak `@body('myAction')['foo'][0]` można uzyskać wartość `bar` w takim przypadku:</span><span class="sxs-lookup"><span data-stu-id="cc222-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="cc222-115">Nie dodatkowe rzutowanie jest niezbędne.</span><span class="sxs-lookup"><span data-stu-id="cc222-115">No additional casting is needed.</span></span> <span data-ttu-id="cc222-116">Podczas pracy z danymi, które jest JSON, ale nie ma określonego nagłówka, należy go ręcznie rzutowania JSON przy użyciu `@json()` funkcji, na przykład: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="cc222-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="cc222-117">Schemat i generator schematu</span><span class="sxs-lookup"><span data-stu-id="cc222-117">Schema and schema generator</span></span>

<span data-ttu-id="cc222-118">Wyzwalacz żądania umożliwia wprowadzenie schematu JSON dla ładunku, który powinien być wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="cc222-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="cc222-119">Ten schemat umożliwia projektanta Generowanie tokenów, może korzystać z zawartości żądania.</span><span class="sxs-lookup"><span data-stu-id="cc222-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="cc222-120">Jeśli nie masz schematu gotowe, wybierz **ładunku próbki używany do generowania schematu**, więc można wygenerować schematu JSON z ładunku próbki.</span><span class="sxs-lookup"><span data-stu-id="cc222-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schemat](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="cc222-122">Akcja "Parse JSON"</span><span class="sxs-lookup"><span data-stu-id="cc222-122">'Parse JSON' action</span></span>

<span data-ttu-id="cc222-123">`Parse JSON` Pozwala analizować zawartość JSON w tokenach przyjazną wykorzystania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="cc222-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="cc222-124">Podobnie jak wyzwalacza żądania, ta akcja umożliwia wprowadź lub wygenerować schematu JSON dla zawartości, który chcesz przeanalizować.</span><span class="sxs-lookup"><span data-stu-id="cc222-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="cc222-125">To narzędzie ułatwia danych korzystanie z usługi Service Bus, bazy danych Azure rozwiązania Cosmos i tak dalej, znacznie.</span><span class="sxs-lookup"><span data-stu-id="cc222-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Przeanalizować składni JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="cc222-127">zwykły tekst</span><span class="sxs-lookup"><span data-stu-id="cc222-127">Text/plain</span></span>

<span data-ttu-id="cc222-128">Podobnie jak `application/json`, wiadomości HTTP odebrane z `Content-Type` nagłówek `text/plain` są przechowywane w postaci raw.</span><span class="sxs-lookup"><span data-stu-id="cc222-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="cc222-129">Ponadto komunikaty te są zawarte w kolejne czynności bez rzutowania, te żądania przejść z `Content-Type`: `text/plain` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="cc222-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="cc222-130">Na przykład podczas pracy z pliku prostego, można uzyskać ten HTTP zawartości jako `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="cc222-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="cc222-131">W następnej akcji w przypadku wysłania żądania jako treść inne żądanie (`@body('flatfile')`), żądanie będzie mieć `text/plain` nagłówka Content-Type.</span><span class="sxs-lookup"><span data-stu-id="cc222-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="cc222-132">Podczas pracy z danymi, które jest w formacie zwykłego tekstu, ale nie ma określonego nagłówka ręcznie można rzutować danych przy użyciu tekstu `@string()` funkcji, na przykład: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="cc222-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="cc222-133">Aplikacja/xml i funkcji Application/octet-stream i konwertera</span><span class="sxs-lookup"><span data-stu-id="cc222-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="cc222-134">Aparat aplikacji logiki zawsze zachowuje `Content-Type` który otrzymano na żądanie lub odpowiedź HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc222-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="cc222-135">Dlatego jeśli aparat odbiera zawartość z `Content-Type` z `application/octet-stream`, i obejmują, że zawartość w kolejnych akcji bez rzutowania, żądania wychodzącego został `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="cc222-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="cc222-136">W ten sposób aparat można zagwarantować, że utratę danych podczas przenoszenia przez przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="cc222-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="cc222-137">Jednak stan akcji (wejścia i wyjścia) jest przechowywana w obiekcie JSON, ponieważ stan przechodzi przez przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="cc222-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="cc222-138">Tak, aby zachować niektóre typy danych, aparat Konwertuje zawartość na ciąg kodowany w standardzie binary base64 odpowiednie metadane, która zachowuje zarówno `$content` i `$content-type`, które są automatycznie przekonwertować.</span><span class="sxs-lookup"><span data-stu-id="cc222-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="cc222-139">`@json()`-rzutuje danych`application/json`</span><span class="sxs-lookup"><span data-stu-id="cc222-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="cc222-140">`@xml()`-rzutuje danych`application/xml`</span><span class="sxs-lookup"><span data-stu-id="cc222-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="cc222-141">`@binary()`-rzutuje danych`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="cc222-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="cc222-142">`@string()`-rzutuje danych`text/plain`</span><span class="sxs-lookup"><span data-stu-id="cc222-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="cc222-143">`@base64()`-Konwertuje zawartość na ciąg w formacie base64</span><span class="sxs-lookup"><span data-stu-id="cc222-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="cc222-144">`@base64toString()`-Konwertuje ciąg kodowany w standardzie base64`text/plain`</span><span class="sxs-lookup"><span data-stu-id="cc222-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="cc222-145">`@base64toBinary()`-Konwertuje ciąg kodowany w standardzie base64`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="cc222-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="cc222-146">`@encodeDataUri()`-koduje ciągiem w postaci tablicy bajtów dataUri</span><span class="sxs-lookup"><span data-stu-id="cc222-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="cc222-147">`@decodeDataUri()`-dekoduje dataUri do tablicy typu byte</span><span class="sxs-lookup"><span data-stu-id="cc222-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="cc222-148">Na przykład w przypadku otrzymania żądania HTTP z `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="cc222-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="cc222-149">Można rzutować i później użyć przypominać `@xml(triggerBody())`, lub w funkcji, takich jak `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="cc222-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="cc222-150">Inne typy zawartości</span><span class="sxs-lookup"><span data-stu-id="cc222-150">Other content types</span></span>

<span data-ttu-id="cc222-151">Inne typy zawartości są obsługiwane i pracy z usługą logic apps, ale może wymagać ręcznego pobierania treść komunikatu przez dekodowania `$content`.</span><span class="sxs-lookup"><span data-stu-id="cc222-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="cc222-152">Na przykład, załóżmy, że użytkownik zainicjuje `application/x-www-url-formencoded` żądania where `$content` jest ładunku zakodowany jako ciąg base64, aby zachować wszystkie dane:</span><span class="sxs-lookup"><span data-stu-id="cc222-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="cc222-153">Ponieważ żądanie nie jest w postaci zwykłego tekstu lub JSON, żądanie jest przechowywane w akcji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cc222-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Obecnie nie ma funkcji macierzystej dla danych formularza, więc można nadal używać tych danych w przepływie pracy, przez ręcznie podczas uzyskiwania dostępu do danych przy użyciu funkcji, takich jak `@string(body('formdataAction'))`. Jeśli potrzebujesz żądania wychodzącego musi mieć również `application/x-www-url-formencoded` nagłówek typu zawartości żądania można dodać do treści akcji bez żadnych rzutowania, takich jak `@body('formdataAction')`. Jednak ta metoda działa tylko, jeśli treść jest to jedyny parametr w `body` wejściowego. <span data-ttu-id="cc222-157">Jeśli spróbujesz użyć `@body('formdataAction')` w `application/json` żądania, pobrać błąd w czasie wykonywania, ponieważ jest wysyłany zakodowanej treści.</span><span class="sxs-lookup"><span data-stu-id="cc222-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

