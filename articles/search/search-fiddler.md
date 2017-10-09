---
title: "aaaHow toouse Fiddler tooevaluate i testowania interfejsów API REST wyszukiwania Azure | Dokumentacja firmy Microsoft"
description: "Używanie narzędzia Fiddler o dostępności usługi Azure Search tooverifying podejście niekorzystające z kodu i wypróbować hello interfejsów API REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="f5f75-103">Użyj narzędzia Fiddler tooevaluate i testowania interfejsów API REST wyszukiwanie Azure</span><span class="sxs-lookup"><span data-stu-id="f5f75-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="f5f75-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f5f75-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="f5f75-105">Eksplorator wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="f5f75-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="f5f75-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="f5f75-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="f5f75-107">.NET</span><span class="sxs-lookup"><span data-stu-id="f5f75-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="f5f75-108">REST</span><span class="sxs-lookup"><span data-stu-id="f5f75-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="f5f75-109">W tym artykule opisano sposób toouse Fiddler dostępna jako [bezpłatnie pobrać ze strony firmy Telerik](http://www.telerik.com/fiddler), tooissue HTTP żądania tooand widoku odpowiedzi przy użyciu hello Azure interfejsu API REST Search, bez konieczności toowrite żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="f5f75-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="f5f75-110">Azure Search jest w pełni zarządzaną, hostowaną usługą wyszukiwania w chmurze na platformie Microsoft Azure, którą można łatwo zaprogramować za pomocą platformy .NET i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="f5f75-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="f5f75-111">Witaj usługi Azure Search interfejsów API REST są opisane w [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f75-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="f5f75-112">W hello następujące kroki możesz utworzyć indeks, przekazywanie dokumentów, indeks hello zapytania i system hello kwerendy informacji o usłudze.</span><span class="sxs-lookup"><span data-stu-id="f5f75-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="f5f75-113">toocomplete tych kroków, konieczne będzie usługi Azure Search i `api-key`.</span><span class="sxs-lookup"><span data-stu-id="f5f75-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="f5f75-114">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) instrukcje dotyczące sposobu uruchamiania tooget.</span><span class="sxs-lookup"><span data-stu-id="f5f75-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="f5f75-115">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="f5f75-115">Create an index</span></span>
1. <span data-ttu-id="f5f75-116">Uruchom narzędzie Fiddler.</span><span class="sxs-lookup"><span data-stu-id="f5f75-116">Start Fiddler.</span></span> <span data-ttu-id="f5f75-117">Na powitania **pliku** menu, wyłącz **przechwytywania ruchu** toohide dodatkowej aktywności protokołu HTTP będący niepowiązanych toohello bieżącego zadania.</span><span class="sxs-lookup"><span data-stu-id="f5f75-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="f5f75-118">Na powitania **Composer** karcie będzie sformułować żądania, która wygląda jak powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="f5f75-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="f5f75-119">Wybierz pozycję **PUT**.</span><span class="sxs-lookup"><span data-stu-id="f5f75-119">Select **PUT**.</span></span>
4. <span data-ttu-id="f5f75-120">Wprowadź adres URL, który określa adres URL usługi hello, atrybuty żądania i hello interfejsu api-version.</span><span class="sxs-lookup"><span data-stu-id="f5f75-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="f5f75-121">Kilka tookeep wskaźniki pamiętać:</span><span class="sxs-lookup"><span data-stu-id="f5f75-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="f5f75-122">Użyj protokołu HTTPS jako prefiksu hello.</span><span class="sxs-lookup"><span data-stu-id="f5f75-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="f5f75-123">Atrybutem żądania jest „/indexes/hotels”.</span><span class="sxs-lookup"><span data-stu-id="f5f75-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="f5f75-124">Ta wartość informuje toocreate wyszukiwania indeksu o nazwie "hotels".</span><span class="sxs-lookup"><span data-stu-id="f5f75-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="f5f75-125">Wersja interfejsu API jest pisana małymi literami i określana jako ciąg „?api-version=2016-09-01”.</span><span class="sxs-lookup"><span data-stu-id="f5f75-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="f5f75-126">Wersje interfejsu API są ważne, ponieważ usługa Azure Search regularnie wdraża aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="f5f75-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="f5f75-127">W rzadkich przypadkach aktualizacja usługi może powodować istotne zmiany toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f5f75-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="f5f75-128">Z tego powodu usługa Azure Search wymaga podania parametru api-version dla każdego wysyłanego żądania, aby użytkownik miał pełną kontrolę nad tym, która wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="f5f75-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="f5f75-129">Witaj pełny adres URL powinien wyglądać podobnie toohello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f5f75-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="f5f75-130">Określ nagłówek żądania hello, zastępując hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="f5f75-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="f5f75-131">W treści żądania Wklej hello pola, które tworzą definicję indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="f5f75-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="f5f75-132">Kliknij przycisk **Execute** (Wykonaj).</span><span class="sxs-lookup"><span data-stu-id="f5f75-132">Click **Execute**.</span></span>

<span data-ttu-id="f5f75-133">W ciągu kilku sekund powinna zostać wyświetlona odpowiedź 201 protokołu HTTP, na liście sesji hello, wskazujące hello indeks został pomyślnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="f5f75-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="f5f75-134">Jeśli otrzymasz odpowiedź 504 protokołu HTTP, sprawdź, czy adres URL hello Określa protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f5f75-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="f5f75-135">Jeśli zobaczysz HTTP 400 lub 404, sprawdź Żądanie hello tooverify treści nie było żadnych błędów kopiowania i wklejania.</span><span class="sxs-lookup"><span data-stu-id="f5f75-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="f5f75-136">Odpowiedź 403 protokołu HTTP zazwyczaj wskazuje na problem z hello klucz api-key (nieprawidłowy klucz lub problem składni z jak klucz interfejsu api hello jest określony).</span><span class="sxs-lookup"><span data-stu-id="f5f75-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="f5f75-137">Ładowanie dokumentów</span><span class="sxs-lookup"><span data-stu-id="f5f75-137">Load documents</span></span>
<span data-ttu-id="f5f75-138">Na powitania **Composer** karcie dokumentów toopost żądania będą wyglądać jak poniżej hello.</span><span class="sxs-lookup"><span data-stu-id="f5f75-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="f5f75-139">Witaj treści żądania hello zawiera hello dane wyszukiwania dla 4 hoteli.</span><span class="sxs-lookup"><span data-stu-id="f5f75-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="f5f75-140">Wybierz pozycję **POST**.</span><span class="sxs-lookup"><span data-stu-id="f5f75-140">Select **POST**.</span></span>
2. <span data-ttu-id="f5f75-141">Wprowadź adres URL, który rozpoczyna się od ciągu HTTPS, po którym następuje adres URL Twojej usługi, a następnie ciąg „/indexes/<nazwa_indeksu>/docs/index?api-version=2016-09-01”.</span><span class="sxs-lookup"><span data-stu-id="f5f75-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="f5f75-142">Witaj pełny adres URL powinien wyglądać podobnie toohello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f5f75-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="f5f75-143">Nagłówek żądania powinien być hello tego samego jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="f5f75-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="f5f75-144">Należy pamiętać, zastąpione hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="f5f75-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="f5f75-145">Witaj treść żądania zawiera cztery dokumenty toobe dodano toohello indeksu hotels.</span><span class="sxs-lookup"><span data-stu-id="f5f75-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="f5f75-146">Kliknij przycisk **Execute** (Wykonaj).</span><span class="sxs-lookup"><span data-stu-id="f5f75-146">Click **Execute**.</span></span>

<span data-ttu-id="f5f75-147">W ciągu kilku sekund powinna zostać wyświetlona odpowiedź 200 protokołu HTTP na liście sesji hello.</span><span class="sxs-lookup"><span data-stu-id="f5f75-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="f5f75-148">To ustawienie określa powitalne dokumenty zostały pomyślnie utworzone.</span><span class="sxs-lookup"><span data-stu-id="f5f75-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="f5f75-149">Jeśli otrzymasz odpowiedź 207, co najmniej jednego dokumentu nie powiodło się tooupload.</span><span class="sxs-lookup"><span data-stu-id="f5f75-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="f5f75-150">Jeśli otrzymasz odpowiedź 404, masz błąd składniowy w nagłówku hello lub treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="f5f75-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="f5f75-151">Indeks hello zapytania</span><span class="sxs-lookup"><span data-stu-id="f5f75-151">Query hello index</span></span>
<span data-ttu-id="f5f75-152">Teraz, gdy indeks i dokumenty są załadowane, możesz wykonywać zapytania względem nich.</span><span class="sxs-lookup"><span data-stu-id="f5f75-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="f5f75-153">Na powitania **Composer** karcie **UZYSKAĆ** polecenia, który wysyła zapytanie do usługi będzie wyglądać podobnie toohello po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="f5f75-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="f5f75-154">Wybierz pozycję **GET**.</span><span class="sxs-lookup"><span data-stu-id="f5f75-154">Select **GET**.</span></span>
2. <span data-ttu-id="f5f75-155">Wprowadź adres URL, który rozpoczyna się od ciągu HTTPS, po którym następuje adres URL Twojej usługi, następnie ciąg „/indexes/<nazwa_indeksu>/docs?”, a na końcu parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="f5f75-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="f5f75-156">Przykładowo Użyj hello następującego adresu URL, zastępując przykładową nazwę hosta hello jest prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="f5f75-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="f5f75-157">To zapytanie wyszukuje wystąpienia terminu "motel" hello i pobiera kategorie aspektów dla klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="f5f75-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="f5f75-158">Nagłówek żądania powinien być hello tego samego jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="f5f75-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="f5f75-159">Należy pamiętać, zastąpione hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="f5f75-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="f5f75-160">Kod odpowiedzi Hello powinien być 200, a dane wyjściowe odpowiedzi hello powinien wyglądać podobnie toohello po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="f5f75-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="f5f75-161">Witaj następujące przykładowe zapytanie jest z hello [operacji wyszukiwania indeksu (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="f5f75-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="f5f75-162">Wiele hello przykładowych zapytań w tym temacie zawiera spacje, które nie są dozwolone w narzędziu Fiddler.</span><span class="sxs-lookup"><span data-stu-id="f5f75-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="f5f75-163">Zastąp każdą spację znakiem + przed wklejeniem hello ciągu zapytania przed podjęciem próby wykonania kwerendy hello w narzędziu Fiddler.</span><span class="sxs-lookup"><span data-stu-id="f5f75-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="f5f75-164">**Przed zastąpieniem spacji:**</span><span class="sxs-lookup"><span data-stu-id="f5f75-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="f5f75-165">**Po zastąpieniu spacji znakiem +:**</span><span class="sxs-lookup"><span data-stu-id="f5f75-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="f5f75-166">system hello zapytania</span><span class="sxs-lookup"><span data-stu-id="f5f75-166">Query hello system</span></span>
<span data-ttu-id="f5f75-167">Możesz także zbadać hello systemu tooget liczby i magazynu użycie dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f5f75-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="f5f75-168">Na powitania **Composer** kartę, Twoje żądanie będzie wyglądało podobnie następujące toohello i hello odpowiedź zwróci liczbę hello dokumentów i miejsca.</span><span class="sxs-lookup"><span data-stu-id="f5f75-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="f5f75-169">Wybierz pozycję **GET**.</span><span class="sxs-lookup"><span data-stu-id="f5f75-169">Select **GET**.</span></span>
2. <span data-ttu-id="f5f75-170">Wprowadź adres URL, który zawiera adres URL usługi, po którym następuje ciąg „/indexes/hotels/stats?api-version=2016-09-01”:</span><span class="sxs-lookup"><span data-stu-id="f5f75-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="f5f75-171">Określ nagłówek żądania hello, zastępując hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="f5f75-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="f5f75-172">Treść żądania hello może pozostać puste.</span><span class="sxs-lookup"><span data-stu-id="f5f75-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="f5f75-173">Kliknij przycisk **Execute** (Wykonaj).</span><span class="sxs-lookup"><span data-stu-id="f5f75-173">Click **Execute**.</span></span> <span data-ttu-id="f5f75-174">Kod stanu HTTP 200 hello liście sesji powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="f5f75-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="f5f75-175">Wybierz wpis hello opublikowany dla Twojego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f5f75-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="f5f75-176">Kliknij przycisk hello **inspektorzy** , kliknij pozycję hello **nagłówki** kartę, a następnie wybierz hello formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="f5f75-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="f5f75-177">Powinny pojawić się hello dokumentu liczby i rozmiaru magazynu (w KB).</span><span class="sxs-lookup"><span data-stu-id="f5f75-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5f75-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5f75-178">Next steps</span></span>
<span data-ttu-id="f5f75-179">Zobacz [Zarządzanie usługą wyszukiwania na platformie Azure](search-manage.md) toomanaging podejście bez kodu i korzystania z usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="f5f75-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
