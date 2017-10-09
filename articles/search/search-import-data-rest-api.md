---
title: "AAA \"przekazywanie danych (interfejsu API REST - usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Dowiedz się, jak tooupload indeks tooan danych za pomocą usługi Azure Search hello interfejsu API REST."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="e6fc5-103">Przekazywanie danych tooAzure wyszukiwania przy użyciu hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="e6fc5-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="e6fc5-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e6fc5-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="e6fc5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e6fc5-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="e6fc5-106">REST</span><span class="sxs-lookup"><span data-stu-id="e6fc5-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="e6fc5-107">W tym artykule opisano, jak toouse hello [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport danych do indeksu usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="e6fc5-108">Przed rozpoczęciem pracy z tym przewodnikiem powinien zostać [utworzony indeks usługi Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="e6fc5-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="e6fc5-109">W kolejności toopush dokumenty do indeksu przy użyciu hello interfejsu API REST należy wysłać punktu końcowego adresu URL HTTP POST żądania tooyour indeksu.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="e6fc5-110">Treść Hello hello żądania HTTP, że treść jest obiekt JSON zawierający dokumenty hello toobe dodane, zmodyfikowane lub usunięte.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="e6fc5-111">Identyfikowanie klucza api-key administratora usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="e6fc5-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="e6fc5-112">Podczas wystawiania żądania HTTP wysyłane do usługi przy użyciu interfejsu API REST, hello *każdego* żądania interfejsu API musi zawierać hello klucz api-key wygenerowany dla aprowizowanej usługi wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="e6fc5-113">Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="e6fc5-114">toofind z usługą api Key, możesz zalogować się toohello [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="e6fc5-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="e6fc5-115">Przejdź do bloku usługi Azure Search tooyour</span><span class="sxs-lookup"><span data-stu-id="e6fc5-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="e6fc5-116">Kliknij ikonę "Klucze" hello</span><span class="sxs-lookup"><span data-stu-id="e6fc5-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="e6fc5-117">Usługa będzie dysponować *kluczami administratora* i *kluczami zapytań*.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="e6fc5-118">Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="e6fc5-119">Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="e6fc5-120">Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="e6fc5-121">Dla celów hello importowanie danych do indeksu, możesz użyć dowolnej z podstawowego i pomocniczego klucza administratora.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="e6fc5-122">Zdecyduj, które indeksowania toouse akcji</span><span class="sxs-lookup"><span data-stu-id="e6fc5-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="e6fc5-123">Podczas korzystania z interfejsu API REST hello, należy wysłać żądania HTTP POST z JSON żądania organów tooyour indeksu usługi Azure Search na adres URL punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="e6fc5-124">Witaj obiekt JSON w treści żądania HTTP będzie zawierał pojedynczą tablicę danych JSON o nazwie "wartość" z obiektami JSON reprezentującymi dokumenty, które chcesz tooadd tooyour indeksu, update lub delete.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="e6fc5-125">Poszczególne obiekty JSON w tablicy "wartość" hello reprezentuje toobe dokumentu, indeksowane.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="e6fc5-126">Każdy z tych obiektów zawiera klucz dokumentu hello i określa hello wymaganą akcję indeksowania (przekazywania, scalania, delete itd.).</span><span class="sxs-lookup"><span data-stu-id="e6fc5-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="e6fc5-127">W zależności od tego, który hello poniższych akcji, którą wybierzesz tylko niektóre pola muszą być uwzględnione w danym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="e6fc5-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="e6fc5-128">Opis</span><span class="sxs-lookup"><span data-stu-id="e6fc5-128">Description</span></span> | <span data-ttu-id="e6fc5-129">Wymagane pola dla każdego dokumentu</span><span class="sxs-lookup"><span data-stu-id="e6fc5-129">Necessary fields for each document</span></span> | <span data-ttu-id="e6fc5-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e6fc5-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="e6fc5-131">`upload` Akcji jest podobne tooan "upsert", gdzie hello dokument zostanie wstawiony, jeśli jest nowy albo zaktualizowany/zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="e6fc5-132">pole klucza oraz inne pola mają toodefine</span><span class="sxs-lookup"><span data-stu-id="e6fc5-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="e6fc5-133">Podczas aktualizowania/zastępowania istniejącego dokumentu, wszystkie pola, które nie jest określony w żądaniu hello ma ustawione zbyt`null`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="e6fc5-134">Dzieje się tak nawet wtedy, gdy hello pole było wcześniej ustawione tooa wartość inną niż null.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="e6fc5-135">Aktualizacje istniejący dokument o hello określone pola.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="e6fc5-136">Jeśli hello dokument nie istnieje w indeksie hello, hello scalanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="e6fc5-137">pole klucza oraz inne pola mają toodefine</span><span class="sxs-lookup"><span data-stu-id="e6fc5-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="e6fc5-138">Wszystkie pola, które określisz w żądaniu scalania zastąpi istniejące pole hello w dokumencie hello.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="e6fc5-139">Obejmuje to również pola typu `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="e6fc5-140">Na przykład, jeśli hello dokument zawiera pole `tags` z wartością `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` dla `tags`, końcowa wartość hello hello `tags` pole będzie `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="e6fc5-141">Nie będzie to `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="e6fc5-142">Ta akcja działa jak `merge` Jeśli dokument o hello podany klucz już istnieje w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="e6fc5-143">Jeśli dokument hello nie istnieje, działa jak akcja `upload` dla nowego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="e6fc5-144">pole klucza oraz inne pola mają toodefine</span><span class="sxs-lookup"><span data-stu-id="e6fc5-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="e6fc5-145">Usuwa określony dokument hello z hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="e6fc5-146">tylko pole klucza</span><span class="sxs-lookup"><span data-stu-id="e6fc5-146">key only</span></span> |<span data-ttu-id="e6fc5-147">Wszystkie pola, które określisz oprócz pola klucza hello zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="e6fc5-148">Tooremove pojedyncze pole z dokumentu, należy użyć `merge` zamiast i po prostu jawnie ustaw pola hello toonull.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="e6fc5-149">Konstruowania żądania HTTP i treści żądania</span><span class="sxs-lookup"><span data-stu-id="e6fc5-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="e6fc5-150">Teraz, po zebraniu wartości pól wymaganych powitania dla akcji indeksu są gotowe tooconstruct hello rzeczywistego żądania HTTP i tooimport treści żądania JSON, dane.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="e6fc5-151">Żądanie i nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="e6fc5-151">Request and Request Headers</span></span>
<span data-ttu-id="e6fc5-152">W adresie URL hello, konieczne będzie tooprovide Twojego nazwy usługi, nazwę indeksu ("hotels" w tym przypadku), a także hello odpowiednią wersję interfejsu API (bieżąca wersja interfejsu API hello jest `2016-09-01` w czasie hello publikowania tego dokumentu).</span><span class="sxs-lookup"><span data-stu-id="e6fc5-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="e6fc5-153">Konieczne będzie toodefine hello `Content-Type` i `api-key` nagłówki żądań.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="e6fc5-154">Dla hello później należy użyć jednego z kluczy administratora usługi.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="e6fc5-155">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e6fc5-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="e6fc5-156">W tym przypadku jako akcje wyszukiwania są używane akcje `upload`, `mergeOrUpload` i `delete`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="e6fc5-157">Załóżmy, że przedstawiony w przykładzie indeks „hotels” jest już wypełniony różnymi dokumentami.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="e6fc5-158">Należy zwrócić uwagę, jak firma Microsoft nie miał toospecify wszystkich hello możliwych pól dokumentu przy użyciu `mergeOrUpload` tylko określony klucz dokumentu hello (`hotelId`) przy użyciu `delete`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="e6fc5-159">Ponadto należy pamiętać, że może zawierać too1000 dokumentów (lub 16 MB) w pojedyncze żądanie indeksowania.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="e6fc5-160">Opisy kodów odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="e6fc5-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="e6fc5-161">200</span><span class="sxs-lookup"><span data-stu-id="e6fc5-161">200</span></span>
<span data-ttu-id="e6fc5-162">Po pomyślnym przesłaniu żądania indeksowania zostanie zwrócona odpowiedź HTTP z kodem stanu `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="e6fc5-163">Witaj treść kodu JSON hello odpowiedzi HTTP będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e6fc5-163">hello JSON body of hello HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="e6fc5-164">207</span><span class="sxs-lookup"><span data-stu-id="e6fc5-164">207</span></span>
<span data-ttu-id="e6fc5-165">Kod stanu `207` jest zwracany, gdy co najmniej jeden element nie został pomyślnie umieszczony w indeksie.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="e6fc5-166">Treść kodu JSON odpowiedzi HTTP hello Hello zawierają informacje na temat hello dokumentów nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="e6fc5-167">Często oznacza to, że obciążenia hello na wyszukiwanie usługi wkrótce osiągnie punkt, w którym żądania indeksowania zaczną tooreturn `503` odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="e6fc5-168">W takim przypadku zdecydowanie zaleca się wycofanie kodu klienta i odczekanie przed ponownym wysłaniem żądania.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="e6fc5-169">Zapewni systemu hello niektórych toorecover czasu, zwiększa prawdopodobieństwo hello, które powiedzie przyszłych żądań.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="e6fc5-170">Szybkie ponawianie żądań tylko wydłuży hello sytuacji.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="e6fc5-171">429</span><span class="sxs-lookup"><span data-stu-id="e6fc5-171">429</span></span>
<span data-ttu-id="e6fc5-172">Kod stanu `429` zostanie zwrócony w przypadku przekroczenia limitu przydziału na powitania liczby dokumentów w indeksie.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="e6fc5-173">503</span><span class="sxs-lookup"><span data-stu-id="e6fc5-173">503</span></span>
<span data-ttu-id="e6fc5-174">Kod stanu `503` zostanie zwrócony, jeśli żaden z elementów hello w żądaniu hello zostały pomyślnie umieszczony w indeksie.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="e6fc5-175">Ten błąd oznacza, że hello system jest mocno obciążony i w tej chwili nie można przetworzyć żądania.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="e6fc5-176">W takim przypadku zdecydowanie zaleca się wycofanie kodu klienta i odczekanie przed ponownym wysłaniem żądania.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="e6fc5-177">Zapewni systemu hello niektórych toorecover czasu, zwiększa prawdopodobieństwo hello, które powiedzie przyszłych żądań.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="e6fc5-178">Szybkie ponawianie żądań tylko wydłuży hello sytuacji.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="e6fc5-179">Aby uzyskać więcej informacji na temat akcji dla dokumentów oraz odpowiedzi oznaczających powodzenie lub błąd, zobacz [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) (Dodawanie, aktualizowanie lub usuwanie dokumentów).</span><span class="sxs-lookup"><span data-stu-id="e6fc5-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="e6fc5-180">Aby uzyskać więcej informacji o innych kodach stanów HTTP, które mogą być zwracane w przypadku niepowodzenia, zobacz [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) (Usługa Azure Search — kody stanów HTTP).</span><span class="sxs-lookup"><span data-stu-id="e6fc5-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6fc5-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6fc5-181">Next steps</span></span>
<span data-ttu-id="e6fc5-182">Po wypełnieniu indeksu usługi Azure Search, będzie gotowy toostart wystawiania toosearch zapytań dla dokumentów.</span><span class="sxs-lookup"><span data-stu-id="e6fc5-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="e6fc5-183">Aby uzyskać szczegóły, zobacz [Query Your Azure Search Index](search-query-overview.md) (Tworzenie zapytań względem indeksu usługi Azure Search).</span><span class="sxs-lookup"><span data-stu-id="e6fc5-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
