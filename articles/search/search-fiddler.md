---
title: "Używanie narzędzia Fiddler do oceny i testowania interfejsów API REST usługi Azure Search | Microsoft Docs"
description: "Używanie narzędzia Fiddler bez korzystania z kodu, aby zweryfikować dostępność usługi Azure Search i wypróbować interfejsy API REST."
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
ms.openlocfilehash: c38b73fa69bee34ce2434c6274cb017c99ef3c35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="ac9fa-103">Używanie narzędzia Fiddler do oceny i testowania interfejsów API REST usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="ac9fa-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="ac9fa-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ac9fa-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="ac9fa-105">Eksplorator wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="ac9fa-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="ac9fa-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="ac9fa-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="ac9fa-107">.NET</span><span class="sxs-lookup"><span data-stu-id="ac9fa-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="ac9fa-108">REST</span><span class="sxs-lookup"><span data-stu-id="ac9fa-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="ac9fa-109">W tym artykule wyjaśniono, jak używać narzędzia Fiddler do wysyłania żądań HTTP i przeglądania odpowiedzi przy użyciu interfejsu API REST usługi Azure Search, bez konieczności pisania kodu. Narzędzie to można [bezpłatnie pobrać ze strony firmy Telerik](http://www.telerik.com/fiddler).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="ac9fa-110">Azure Search jest w pełni zarządzaną, hostowaną usługą wyszukiwania w chmurze na platformie Microsoft Azure, którą można łatwo zaprogramować za pomocą platformy .NET i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="ac9fa-111">Interfejsy API REST usługi Azure Search są opisane w witrynie [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="ac9fa-112">W poniższych krokach utworzysz indeks, przekażesz dokumenty, wykonasz zapytania względem indeksu, a następnie wykonasz zapytania względem systemu pod kątem informacji o usłudze.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="ac9fa-113">Aby móc wykonać te kroki, niezbędna będzie usługa Azure Search i klucz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="ac9fa-114">Aby uzyskać instrukcje dotyczące rozpoczęcia pracy, zobacz [Create an Azure Search service in the portal](search-create-service-portal.md) (Tworzenie usługi Azure Search w portalu).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="ac9fa-115">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="ac9fa-115">Create an index</span></span>
1. <span data-ttu-id="ac9fa-116">Uruchom narzędzie Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-116">Start Fiddler.</span></span> <span data-ttu-id="ac9fa-117">W menu **File** (Plik) wyłącz opcję **Capture Traffic** (Przechwyć ruch) w celu ukrycia dodatkowej aktywności protokołu HTTP, która nie ma wpływu na bieżące zadanie.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="ac9fa-118">Na karcie **Composer** (Kompozytor) sformułuj żądanie takie, jak to przedstawione na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="ac9fa-119">Wybierz pozycję **PUT**.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-119">Select **PUT**.</span></span>
4. <span data-ttu-id="ac9fa-120">Wprowadź adres URL, który określa adres URL usługi, atrybuty żądania i wersję interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="ac9fa-121">Kilka wskazówek, o których należy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="ac9fa-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="ac9fa-122">Używaj prefiksu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="ac9fa-123">Atrybutem żądania jest „/indexes/hotels”.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="ac9fa-124">Na tej podstawie usługa wyszukiwania utworzy indeks o nazwie „hotels”.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="ac9fa-125">Wersja interfejsu API jest pisana małymi literami i określana jako ciąg „?api-version=2016-09-01”.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="ac9fa-126">Wersje interfejsu API są ważne, ponieważ usługa Azure Search regularnie wdraża aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="ac9fa-127">W rzadkich przypadkach aktualizacja usługi może wprowadzić do interfejsu API istotną zmianę, która może powodować błędy.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="ac9fa-128">Z tego powodu usługa Azure Search wymaga podania parametru api-version dla każdego wysyłanego żądania, aby użytkownik miał pełną kontrolę nad tym, która wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="ac9fa-129">Pełny adres URL powinien wyglądać podobnie, jak przedstawiono w następującym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="ac9fa-130">Określ nagłówek żądania, zastępując nazwę hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="ac9fa-131">W obszarze Request Body (Treść żądania) wklej pola, które tworzą definicję indeksu.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-131">In Request Body, paste in the fields that make up the index definition.</span></span>

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
7. <span data-ttu-id="ac9fa-132">Kliknij polecenie **Execute** (Wykonaj).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-132">Click **Execute**.</span></span>

<span data-ttu-id="ac9fa-133">W ciągu kilku sekund na liście sesji powinna zostać wyświetlona odpowiedź 201 protokołu HTTP wskazująca, że indeks został pomyślnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="ac9fa-134">Jeśli otrzymasz odpowiedź 504 protokołu HTTP, sprawdź, czy adres URL określa protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="ac9fa-135">Jeśli zobaczysz odpowiedź 400 lub 404 protokołu HTTP, sprawdź treść żądania, aby zweryfikować, czy nie było żadnych błędów podczas kopiowania i wklejania.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="ac9fa-136">Odpowiedź 403 protokołu HTTP zazwyczaj wskazuje na problem z kluczem api-key (nieprawidłowy klucz lub problem ze składnią klucza api-key).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="ac9fa-137">Ładowanie dokumentów</span><span class="sxs-lookup"><span data-stu-id="ac9fa-137">Load documents</span></span>
<span data-ttu-id="ac9fa-138">Na karcie **Composer** (Kompozytor) Twoje żądanie opublikowania dokumentów będzie wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="ac9fa-139">Treść żądania zawiera dane wyszukiwania dla 4 hoteli.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="ac9fa-140">Wybierz pozycję **POST**.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-140">Select **POST**.</span></span>
2. <span data-ttu-id="ac9fa-141">Wprowadź adres URL, który rozpoczyna się od ciągu HTTPS, po którym następuje adres URL Twojej usługi, a następnie ciąg „/indexes/<nazwa_indeksu>/docs/index?api-version=2016-09-01”.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="ac9fa-142">Pełny adres URL powinien wyglądać podobnie, jak przedstawiono w następującym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="ac9fa-143">Nagłówek żądania powinien być taki jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-143">Request Header should be the same as before.</span></span> <span data-ttu-id="ac9fa-144">Pamiętaj, że nazwa hosta i klucz api-key zostały zastąpione wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="ac9fa-145">Obszar Request Body (Treść żądania) zawiera cztery dokumenty, które mają zostać dodane do indeksu hotels.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-145">The Request Body contains four documents to be added to the hotels index.</span></span>

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
             "description": "This could be the one",
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
5. <span data-ttu-id="ac9fa-146">Kliknij polecenie **Execute** (Wykonaj).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-146">Click **Execute**.</span></span>

<span data-ttu-id="ac9fa-147">W ciągu kilku sekund na liście sesji powinna zostać wyświetlona odpowiedź 200 protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="ac9fa-148">Oznacza to, że dokumenty zostały pomyślnie utworzone.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="ac9fa-149">Jeśli otrzymasz odpowiedź 207, przekazanie co najmniej jednego dokumentu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="ac9fa-150">Jeśli otrzymasz odpowiedź 404, wystąpił błąd składniowy w nagłówku lub w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="ac9fa-151">Wykonywanie zapytań względem indeksu</span><span class="sxs-lookup"><span data-stu-id="ac9fa-151">Query the index</span></span>
<span data-ttu-id="ac9fa-152">Teraz, gdy indeks i dokumenty są załadowane, możesz wykonywać zapytania względem nich.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="ac9fa-153">Na karcie **Composer** (Kompozytor) polecenie **GET**, które umożliwia wykonanie zapytania o usługę, będzie wyglądać podobnie jak na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="ac9fa-154">Wybierz pozycję **GET**.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-154">Select **GET**.</span></span>
2. <span data-ttu-id="ac9fa-155">Wprowadź adres URL, który rozpoczyna się od ciągu HTTPS, po którym następuje adres URL Twojej usługi, następnie ciąg „/indexes/<nazwa_indeksu>/docs?”, a na końcu parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="ac9fa-156">Możesz użyć następującego przykładowego adresu URL, zastępując przykładową nazwę hosta nazwą prawidłową dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="ac9fa-157">To zapytanie wyszukuje wystąpienia terminu „motel” i pobiera kategorie aspektów dla klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="ac9fa-158">Nagłówek żądania powinien być taki jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-158">Request Header should be the same as before.</span></span> <span data-ttu-id="ac9fa-159">Pamiętaj, że nazwa hosta i klucz api-key zostały zastąpione wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="ac9fa-160">Powinien zostać wyświetlony kod odpowiedzi 200, a dane wyjściowe odpowiedzi powinny wyglądać podobnie jak na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="ac9fa-161">Poniższe przykładowe zapytanie można znaleźć w [operacji wyszukiwania indeksu (interfejs API usługi Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="ac9fa-162">Wiele przykładowych zapytań w tym temacie zawiera spacje, które nie są dozwolone w narzędziu Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="ac9fa-163">Przed wklejeniem ciągu zapytania oraz podjęciem próby jego wykonania w narzędziu Fiddler zastąp każdą spację znakiem +.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="ac9fa-164">**Przed zastąpieniem spacji:**</span><span class="sxs-lookup"><span data-stu-id="ac9fa-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="ac9fa-165">**Po zastąpieniu spacji znakiem +:**</span><span class="sxs-lookup"><span data-stu-id="ac9fa-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="ac9fa-166">Wykonywanie zapytań względem systemu</span><span class="sxs-lookup"><span data-stu-id="ac9fa-166">Query the system</span></span>
<span data-ttu-id="ac9fa-167">Zapytania możesz także wykonywać względem systemu, aby uzyskać informacje o liczbie dokumentów i użyciu przestrzeni dyskowej.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="ac9fa-168">Na karcie **Composer** (Kompozytor) Twoje żądanie będzie wyglądało podobnie do poniższego, a odpowiedź zwróci liczbę dokumentów i ilość używanej przestrzeni dyskowej.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="ac9fa-169">Wybierz pozycję **GET**.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-169">Select **GET**.</span></span>
2. <span data-ttu-id="ac9fa-170">Wprowadź adres URL, który zawiera adres URL usługi, po którym następuje ciąg „/indexes/hotels/stats?api-version=2016-09-01”:</span><span class="sxs-lookup"><span data-stu-id="ac9fa-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="ac9fa-171">Określ nagłówek żądania, zastępując nazwę hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="ac9fa-172">Pozostaw treść żądania pustą.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="ac9fa-173">Kliknij polecenie **Execute** (Wykonaj).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-173">Click **Execute**.</span></span> <span data-ttu-id="ac9fa-174">Na liście sesji powinien zostać wyświetlony kod stanu 200 protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="ac9fa-175">Wybierz wpis opublikowany dla Twojego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="ac9fa-176">Kliknij kartę **Inspectors** (Inspektorzy), potem kliknij kartę **Headers** (Nagłówki), a następnie wybierz format JSON.</span><span class="sxs-lookup"><span data-stu-id="ac9fa-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="ac9fa-177">Powinny zostać wyświetlone informacje o liczbie dokumentów i rozmiarze magazynu (w KB).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac9fa-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac9fa-178">Next steps</span></span>
<span data-ttu-id="ac9fa-179">Aby uzyskać informacje o zarządzaniu i korzystaniu z usługi Azure Search bez konieczności pisania kodu, zobacz [Manage your Search service on Azure](search-manage.md) (Zarządzanie usługą wyszukiwania na platformie Azure).</span><span class="sxs-lookup"><span data-stu-id="ac9fa-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
