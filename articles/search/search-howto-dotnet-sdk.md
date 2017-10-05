---
title: "Jak używać usługi Azure Search z aplikacji .NET | Dokumentacja firmy Microsoft"
description: "Jak używać usługi Azure Search z aplikacji .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="74329-103">Jak używać usługi Azure Search z aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="74329-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="74329-104">Ten artykuł zawiera wskazówki ułatwiające rozpoczęcie działa z [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="74329-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="74329-105">Zestaw .NET SDK umożliwia wdrożenie zaawansowane wyszukiwanie w aplikacji przy użyciu usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="74329-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="74329-106">Co to jest Azure wyszukiwania zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="74329-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="74329-107">Zestaw SDK składa się z biblioteki klienta, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="74329-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="74329-108">Umożliwia ona zarządzanie indeksów, indeksatorów oraz źródeł danych, a także przekazywanie i zarządzania dokumentami i wykonywać zapytania, bez konieczności postępowania w przypadku szczegóły HTTP i JSON.</span><span class="sxs-lookup"><span data-stu-id="74329-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="74329-109">Biblioteka klienta definiuje klas takich jak `Index`, `Field`, i `Document`, jak również operacji, takich jak `Indexes.Create` i `Documents.Search` na `SearchServiceClient` i `SearchIndexClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="74329-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="74329-110">Te klasy są podzielone na następujące obszary nazw:</span><span class="sxs-lookup"><span data-stu-id="74329-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="74329-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="74329-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="74329-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="74329-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="74329-113">Bieżąca wersja zestawu .NET SDK usługi Azure Search teraz jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="74329-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="74329-114">Jeśli chcesz przekazać opinię firmie Microsoft w celu uwzględnienia w następnej wersji, skontaktuj się z odwiedziny naszych [strony](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="74329-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="74329-115">Zestaw .NET SDK obsługuje wersję `2016-09-01` z [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="74329-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="74329-116">Ta wersja zawiera teraz obsługę niestandardowych analizatory i obiektów Blob platformy Azure i tabel Azure indeksatorze obsługi.</span><span class="sxs-lookup"><span data-stu-id="74329-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="74329-117">Funkcji, które są w wersji zapoznawczej *nie* są częścią tej wersji, takie jak Obsługa indeksowania JSON i woluminów CSV, [Podgląd](search-api-2015-02-28-preview.md) i dostępne za pośrednictwem starszej [2.0 — wersja zapoznawcza zestawu .NET SDK](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="74329-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="74329-118">Zestaw SDK nie obsługuje [operacji zarządzania](https://docs.microsoft.com/rest/api/searchmanagement/) takich jak tworzenie i skalowanie usługi wyszukiwania i zarządzanie nimi klucze interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="74329-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="74329-119">Jeśli trzeba zarządzać zasobami wyszukiwania z aplikacji .NET, możesz użyć [zestawu SDK usługi Azure Search .NET zarządzania](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="74329-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="74329-120">Uaktualnianie do najnowszej wersji zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="74329-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="74329-121">Jeśli już używasz starszej wersji zestawu .NET SDK usługi Azure Search i chcesz uaktualnić do nowej wersji ogólnie dostępna, [w tym artykule](search-dotnet-sdk-migration.md) wyjaśniono sposób.</span><span class="sxs-lookup"><span data-stu-id="74329-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="74329-122">Wymagania dotyczące zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="74329-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="74329-123">Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="74329-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="74329-124">Własne usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="74329-124">Your own Azure Search service.</span></span> <span data-ttu-id="74329-125">Aby korzystać z zestawu SDK, należy uzyskać nazwę usługi i co najmniej jeden klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="74329-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="74329-126">[Tworzenie usługi w portalu](search-create-service-portal.md) pomoże Ci tych kroków.</span><span class="sxs-lookup"><span data-stu-id="74329-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="74329-127">Pobierz zestaw .NET SDK usługi Azure Search [pakietu NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) za pomocą "Manage NuGet Packages" programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74329-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="74329-128">Po prostu wyszukać nazwę pakietu `Microsoft.Azure.Search` na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="74329-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="74329-129">Zestaw .NET SDK usługi Azure Search obsługuje aplikacji przeznaczonych dla platformy .NET Framework 4.6 i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="74329-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="74329-130">Podstawowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="74329-130">Core scenarios</span></span>
<span data-ttu-id="74329-131">Istnieje kilka kwestii, które należy wykonać w aplikacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74329-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="74329-132">W tym samouczku omówione zostaną następujące czynności te podstawowe scenariusze:</span><span class="sxs-lookup"><span data-stu-id="74329-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="74329-133">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="74329-133">Creating an index</span></span>
* <span data-ttu-id="74329-134">Podczas wypełniania indeksu z dokumentami</span><span class="sxs-lookup"><span data-stu-id="74329-134">Populating the index with documents</span></span>
* <span data-ttu-id="74329-135">Wyszukiwanie dokumentów za pomocą wyszukiwania pełnotekstowego oraz filtry</span><span class="sxs-lookup"><span data-stu-id="74329-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="74329-136">Przykładowy kod, który jest zgodny ilustruje każdą z nich.</span><span class="sxs-lookup"><span data-stu-id="74329-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="74329-137">Możesz także użyć wstawki kodu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74329-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="74329-138">Omówienie</span><span class="sxs-lookup"><span data-stu-id="74329-138">Overview</span></span>
<span data-ttu-id="74329-139">Tworzy nową aplikację przykładową, firma Microsoft będzie można badać indeksu o nazwie "hotels" wypełnia kilku dokumentów, a następnie wykonuje kilka zapytań wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74329-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="74329-140">Oto główne programu, przedstawiający ogólny przepływ:</span><span class="sxs-lookup"><span data-stu-id="74329-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="74329-141">Możesz znaleźć pełny kod źródłowy przykładowej aplikacji używanej w tym poradniku w portalu [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="74329-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="74329-142">Zostanie omówiony ten krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="74329-142">We'll walk through this step by step.</span></span> <span data-ttu-id="74329-143">Najpierw należy utworzyć nowy `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="74329-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="74329-144">Ten obiekt umożliwia zarządzanie indeksów.</span><span class="sxs-lookup"><span data-stu-id="74329-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="74329-145">Aby można było utworzyć jedną, musisz podać nazwę usługi Azure Search, a także klucz interfejsu API administratora.</span><span class="sxs-lookup"><span data-stu-id="74329-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="74329-146">Możesz wprowadzić te informacje w `appsettings.json` pliku [Przykładowa aplikacja](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="74329-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="74329-147">Jeśli podasz nieprawidłowy klucz (na przykład klucz zapytania gdy był wymagany klucz administratora), `SearchServiceClient` zgłosi `CloudException` z powodu błędu komunikatu "Dostęp zabroniony" po raz pierwszy metoda jest wywoływana operacji, takich jak `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="74329-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="74329-148">W takim przypadku do Ciebie należy dokładnie sprawdzić naszych klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="74329-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="74329-149">Następnych kilku wierszy wywołania metody, aby utworzyć indeks o nazwie "hotels", usuwając go najpierw, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="74329-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="74329-150">Firma Microsoft przeprowadzi tych metod nieco później.</span><span class="sxs-lookup"><span data-stu-id="74329-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="74329-151">Następnie indeks musi być wypełnione.</span><span class="sxs-lookup"><span data-stu-id="74329-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="74329-152">Aby to zrobić, firma Microsoft będzie `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="74329-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="74329-153">Istnieją dwa sposoby uzyskania: tworząc go lub poprzez wywołanie `Indexes.GetClient` na `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="74329-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="74329-154">Używamy jego dla wygody.</span><span class="sxs-lookup"><span data-stu-id="74329-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="74329-155">W typowej aplikacji wyszukującej wypełnianie indeksu i zarządzanie nim jest obsługiwane przez inny składnik niż zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74329-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="74329-156">`Indexes.GetClient` jest wygodną metodą wypełniania indeksu, ponieważ nie wymaga dostarczenia kolejnej klasy `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="74329-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="74329-157">Dzieje się tak dzięki przekazaniu klucza administratora, który został użyty w celu utworzenia klasy `SearchServiceClient` do nowej klasy `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="74329-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="74329-158">Jednak w tej części aplikacji, która wykonuje zapytania, zaleca się utworzenie klasy `SearchIndexClient` bezpośrednio, dzięki czemu można przekazać klucz zapytania zamiast klucza administratora.</span><span class="sxs-lookup"><span data-stu-id="74329-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="74329-159">To jest zgodna z zasadą najniższych uprawnień i pomoże zapewnić bardziej bezpieczne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74329-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="74329-160">Można dowiedzieć się więcej o kluczach administratora i kluczach zapytań [tutaj](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="74329-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="74329-161">Teraz, gdy mamy `SearchIndexClient`, firma Microsoft może wypełnić indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="74329-162">Jest to realizowane przy użyciu innej metody, które firma Microsoft przeprowadzi później.</span><span class="sxs-lookup"><span data-stu-id="74329-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="74329-163">Ponadto możemy wykonać kilka zapytań wyszukiwania i wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="74329-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="74329-164">Teraz możemy użyć innego `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="74329-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="74329-165">Firma Microsoft podejmie bliższe spojrzenie na `RunQueries` metody później.</span><span class="sxs-lookup"><span data-stu-id="74329-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="74329-166">Oto kod, aby utworzyć nowy `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="74329-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="74329-167">Teraz możemy użyć klucza zapytania, ponieważ firma Microsoft nie musi uzyskać dostęp do indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="74329-168">Możesz wprowadzić te informacje w `appsettings.json` pliku [Przykładowa aplikacja](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="74329-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="74329-169">Po uruchomieniu tej aplikacji z prawidłową nazwę usługi i klucze interfejsu API, dane wyjściowe powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="74329-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="74329-170">Kodu źródłowego aplikacji znajduje się na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="74329-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="74329-171">Następnie będzie trwać bliższe spojrzenie na każdej z metod wywoływane przez `Main`.</span><span class="sxs-lookup"><span data-stu-id="74329-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="74329-172">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="74329-172">Creating an index</span></span>
<span data-ttu-id="74329-173">Po utworzeniu `SearchServiceClient`, co dalej `Main` jest jest usuwania indeksu "hotels", jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="74329-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="74329-174">Który odbywa się następującymi metodami:</span><span class="sxs-lookup"><span data-stu-id="74329-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="74329-175">Ta metoda używa danej `SearchServiceClient` do sprawdzenia, jeśli istnieje indeks, a jeśli tak, usuń go.</span><span class="sxs-lookup"><span data-stu-id="74329-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-176">Przykład kodu przedstawiony w tym artykule używa metod synchronicznych zestawu .NET SDK usługi Azure Search dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="74329-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="74329-177">Zalecamy użycie metod asynchronicznych w aplikacjach, aby pozostały skalowalne i szybko reagowały.</span><span class="sxs-lookup"><span data-stu-id="74329-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="74329-178">Na przykład w powyższej metodzie możesz użyć `ExistsAsync` i `DeleteAsync` zamiast `Exists` i `Delete`.</span><span class="sxs-lookup"><span data-stu-id="74329-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="74329-179">Następnie `Main` powoduje utworzenie nowego indeksu "hotels" przez wywołanie tej metody:</span><span class="sxs-lookup"><span data-stu-id="74329-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="74329-180">Ta metoda tworzy nowy `Index` obiektu z listy `Field` obiektów, które definiuje schemat nowego indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="74329-181">Każde pole ma nazwę, typ danych i kilka atrybutów, które określają zachowanie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74329-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="74329-182">`FieldBuilder` Klasy używa odbicia w celu utworzenia listy `Field` obiektów dla indeksu przez sprawdzenie właściwości publiczne i atrybuty danego `Hotel` klasa modelu.</span><span class="sxs-lookup"><span data-stu-id="74329-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="74329-183">Przeniesiemy bliższe spojrzenie na `Hotel` klasy później.</span><span class="sxs-lookup"><span data-stu-id="74329-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-184">Zawsze można utworzyć listę `Field` obiektów bezpośrednio zamiast `FieldBuilder` w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="74329-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="74329-185">Na przykład nie można używać klasy modelu lub może być konieczne użycie istniejącej klasy modelu, który chcesz zmodyfikować przez dodanie atrybutów.</span><span class="sxs-lookup"><span data-stu-id="74329-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="74329-186">Oprócz pól można również dodać do indeksu (te zostaną pominięte próbkę do skrócenia) oceniania profile, sugestorów lub opcji CORS.</span><span class="sxs-lookup"><span data-stu-id="74329-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="74329-187">Można znaleźć więcej informacji o obiekcie indeksu i jego elementów składowych w [odwołania do zestawu SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), oraz w [dokumentacji interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="74329-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="74329-188">Podczas wypełniania indeksu</span><span class="sxs-lookup"><span data-stu-id="74329-188">Populating the index</span></span>
<span data-ttu-id="74329-189">Następny krok `Main` jest do wypełniania indeksu nowo utworzona.</span><span class="sxs-lookup"><span data-stu-id="74329-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="74329-190">Można to zrobić w następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="74329-190">This is done in the following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="74329-191">Ta metoda ma cztery części.</span><span class="sxs-lookup"><span data-stu-id="74329-191">This method has four parts.</span></span> <span data-ttu-id="74329-192">Pierwszy tworzy tablicę `Hotel` obiektów, które będzie służyć jako danych wejściowych do przekazania do indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="74329-193">Te dane są stałe dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="74329-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="74329-194">W aplikacji danych prawdopodobnie będzie pochodził z zewnętrznego źródła danych takie jak bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="74329-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="74329-195">Druga część tworzy `IndexBatch` zawierającego dokumenty.</span><span class="sxs-lookup"><span data-stu-id="74329-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="74329-196">Określ działanie, które chcesz zastosować do wykonywania zadania wsadowego w czasie tworzenia, w tym przypadku przez wywołanie metody `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="74329-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="74329-197">Partii są następnie przekazywane do indeksu usługi Azure Search przez `Documents.Index` metody.</span><span class="sxs-lookup"><span data-stu-id="74329-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-198">W tym przykładzie mamy tylko przekazywania dokumentów.</span><span class="sxs-lookup"><span data-stu-id="74329-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="74329-199">Jeśli chcesz scalić zmian w istniejących dokumentów lub usuwanie dokumentów, możesz utworzyć partie przez wywołanie metody `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, lub `IndexBatch.Delete` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="74329-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="74329-200">Możesz łączyć różnych operacji w pojedynczej partii przez wywołanie metody `IndexBatch.New`, który przyjmuje Kolekcja `IndexAction` obiektów, które informują usługę Azure Search do wykonywania określonej operacji w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="74329-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="74329-201">Można utworzyć każdego `IndexAction` z działaniem przez wywołanie metody odpowiedniej metody, takie jak `IndexAction.Merge`, `IndexAction.Upload`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="74329-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="74329-202">Trzeci część tej metody jest blok catch obsługuje ważny przypadek błędu indeksowania.</span><span class="sxs-lookup"><span data-stu-id="74329-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="74329-203">Jeśli usługa Azure Search nie może zindeksować niektórych dokumentów w partii, metoda `Documents.Index` zgłasza wyjątek `IndexBatchException`.</span><span class="sxs-lookup"><span data-stu-id="74329-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="74329-204">Może to nastąpić, jeśli indeksujesz dokumenty w czasie, gdy usługa jest mocno obciążona.</span><span class="sxs-lookup"><span data-stu-id="74329-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="74329-205">**Zdecydowanie zalecamy jawną obsługę tego przypadku w kodzie.**</span><span class="sxs-lookup"><span data-stu-id="74329-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="74329-206">Możesz opóźnić, a następnie ponowić indeksowanie dokumentów, których przetwarzanie zakończyło się niepowodzeniem, lub możesz zarejestrować błąd i kontynuować, tak jak w prezentowanym przykładzie. Możesz też wykonać inną akcję w zależności od wymagań spójności danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74329-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-207">Można użyć `FindFailedActionsToRetry` metodę, aby utworzyć nową instancję zawierający tylko akcje, których nie powiodła się podczas poprzedniego wywołania `Index`.</span><span class="sxs-lookup"><span data-stu-id="74329-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="74329-208">Metoda jest udokumentowany [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) i znajduje się omówienie sposobu jego używania prawidłowo [w witrynie StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="74329-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="74329-209">Na koniec `UploadDocuments` umieszczono dwusekundowe opóźnienie metody.</span><span class="sxs-lookup"><span data-stu-id="74329-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="74329-210">Indeksowanie w usłudze Azure Search jest asynchroniczne, więc przykładowa aplikacja musi czekać przez krótki czas, aby upewnić się, że dokumenty można wyszukiwać.</span><span class="sxs-lookup"><span data-stu-id="74329-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="74329-211">Tego typu opóźnienia są zazwyczaj konieczne tylko w przypadku pokazów, testów i przykładowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74329-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="74329-212">Jak zestaw .NET SDK obsługuje dokumenty</span><span class="sxs-lookup"><span data-stu-id="74329-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="74329-213">Możesz się zastanawiać, jak zestaw .NET SDK usługi Azure Search jest w stanie przekazać wystąpienia klasy zdefiniowanej przez użytkownika, np. `Hotel`, do indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="74329-214">Aby odpowiedzieć na to pytanie, Przyjrzyjmy się `Hotel` klasy:</span><span class="sxs-lookup"><span data-stu-id="74329-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="74329-215">Przede wszystkim należy zauważyć, że każda właściwość publiczna klasy `Hotel` odpowiada polu w definicji indeksu, ale z jedną istotną różnicą: nazwa każdego pola rozpoczyna się małą literą (camelCase), podczas gdy nazwa każdej właściwości publicznej klasy `Hotel` rozpoczyna się wielką literą (PascalCase).</span><span class="sxs-lookup"><span data-stu-id="74329-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="74329-216">Jest to częsty przypadek w aplikacjach platformy .NET, które tworzą powiązania danych, gdzie schemat docelowy jest poza kontrolą dewelopera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74329-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="74329-217">Zamiast naruszać zasady nazewnictwa platformy .NET przez używanie notacji camelCase dla nazw właściwości, za pomocą atrybutu `[SerializePropertyNamesAsCamelCase]` można określić, że zestaw SDK ma mapować nazwy właściwości na notację camelCase automatycznie.</span><span class="sxs-lookup"><span data-stu-id="74329-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-218">Zestaw .NET SDK usługi Azure Search korzysta z biblioteki [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) w celu serializacji i deserializacji niestandardowych obiektów modelu do i z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="74329-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="74329-219">W razie potrzeby możesz dostosować serializację.</span><span class="sxs-lookup"><span data-stu-id="74329-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="74329-220">Aby uzyskać więcej informacji, zobacz [niestandardowe serializacji z struktury JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="74329-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="74329-221">Drugi wszystkim należy zauważyć są atrybuty, takie jak `IsFilterable`, `IsSearchable`, `Key`, i `Analyzer` który dekoracji każda właściwość publiczna.</span><span class="sxs-lookup"><span data-stu-id="74329-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="74329-222">Te atrybuty bezpośrednio do mapy [odpowiednie atrybuty indeksu usługi Azure Search](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="74329-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="74329-223">`FieldBuilder` Klasy wykorzystuje te do skonstruowania definicje pól dla indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="74329-224">Trzeci ważną kwestią dotyczącą `Hotel` klasy są typy danych właściwości publicznych.</span><span class="sxs-lookup"><span data-stu-id="74329-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="74329-225">Typy .NET tych właściwości są mapowane na odpowiadające im typy pól w definicji indeksu.</span><span class="sxs-lookup"><span data-stu-id="74329-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="74329-226">Na przykład właściwość ciągu `Category` jest mapowana na pole `category` mające typ `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="74329-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="74329-227">Podobne mapowania typów występują między typami `bool?` i `Edm.Boolean`, `DateTimeOffset?` i `Edm.DateTimeOffset` itp. Dokładne zasady mapowania typów znajdują się w dokumentacji metody `Documents.Get` w [dokumentacji zestawu .NET SDK usługi Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="74329-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="74329-228">`FieldBuilder` Klasy zajmuje się to mapowanie dla Ciebie, ale nadal można zrozumieć, w razie potrzeby można rozwiązać wszelkie napotkane problemy serializacji.</span><span class="sxs-lookup"><span data-stu-id="74329-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="74329-229">Ta możliwość używania własnych klas jako dokumentów działa w obu kierunkach; Można również pobrać wyniki wyszukiwania i mieć automatycznie je na typ wybranym deserializacji zestawu SDK, które zostanie wyświetlone w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="74329-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-230">Zestaw .NET SDK usługi Azure Search obsługuje również dynamiczne typowanie dokumentów za pomocą klasy `Document`, która stanowi mapowanie klucz/wartość nazw pól na wartości pól.</span><span class="sxs-lookup"><span data-stu-id="74329-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="74329-231">Jest to przydatne, jeśli nie znasz schematu indeksu w czasie projektowania lub jeśli powiązanie z określonymi klasami modelu jest niedogodne.</span><span class="sxs-lookup"><span data-stu-id="74329-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="74329-232">Wszystkie metody w zestawie SDK, które obsługują dokumenty, mają przeciążenia działające z klasą `Document`, a także przeciążenia o silnych typach przyjmujące parametr typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="74329-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="74329-233">Tylko te ostatnie są używane w przykładowym kodzie w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="74329-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="74329-234">`Document` Klasa dziedziczy `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="74329-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="74329-235">Inne szczegółowe informacje można znaleźć [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="74329-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="74329-236">**Dlaczego należy używać typów danych dopuszczających wartość null**</span><span class="sxs-lookup"><span data-stu-id="74329-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="74329-237">Jeśli projektujesz własne klasy modeli na potrzeby mapowania na indeks usługi Azure Search, zalecamy deklarowanie właściwości typów wartości, takich jak `bool` i `int`, aby dopuszczały możliwość użycia wartości null (na przykład `bool?` zamiast `bool`).</span><span class="sxs-lookup"><span data-stu-id="74329-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="74329-238">W przypadku użycia właściwości niedopuszczającej wartości null musisz **zagwarantować**, że żaden dokument w indeksie nie zawiera wartości null w odpowiednim polu.</span><span class="sxs-lookup"><span data-stu-id="74329-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="74329-239">Ani zestaw SDK, ani usługa Azure Search nie pomoże Ci tego wymusić.</span><span class="sxs-lookup"><span data-stu-id="74329-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="74329-240">Nie jest to czysto hipotetyczny problem: wyobraź sobie scenariusz, w którym dodajesz nowe pole do istniejącego indeksu typu `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="74329-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="74329-241">Po zaktualizowaniu definicji indeksu wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy w usłudze Azure Search dopuszczają wartość null).</span><span class="sxs-lookup"><span data-stu-id="74329-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="74329-242">Jeśli następnie dla tego pola użyjesz klasy modelu z właściwością `int` niedopuszczającą wartości null, podczas próby pobrania dokumentów otrzymasz wyjątek `JsonSerializationException` podobny do poniższego:</span><span class="sxs-lookup"><span data-stu-id="74329-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="74329-243">Z tego powodu najlepszym i zalecanym rozwiązaniem jest używanie w klasach modeli typów dopuszczających wartość null.</span><span class="sxs-lookup"><span data-stu-id="74329-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="74329-244">Niestandardowej serializacji z struktury JSON.NET</span><span class="sxs-lookup"><span data-stu-id="74329-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="74329-245">Zestaw SDK używa struktury JSON.NET do serializacji i deserializacji dokumentów.</span><span class="sxs-lookup"><span data-stu-id="74329-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="74329-246">Można dostosować serializacji i deserializacji w razie potrzeby, definiując własne `JsonConverter` lub `IContractResolver` (zobacz [dokumentacji struktury JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) więcej szczegółów).</span><span class="sxs-lookup"><span data-stu-id="74329-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="74329-247">Może to być przydatne, jeśli chcesz dostosować istniejącej klasy modelu z aplikacji do użycia z usługi Azure Search i innych bardziej zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="74329-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="74329-248">Na przykład za pomocą niestandardowej serializacji można:</span><span class="sxs-lookup"><span data-stu-id="74329-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="74329-249">Uwzględnić lub wykluczyć pewne właściwości klasy modelu są przechowywane jako pól dokumentu.</span><span class="sxs-lookup"><span data-stu-id="74329-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="74329-250">Mapowania nazw właściwości w kodzie i nazw pól w indeksie.</span><span class="sxs-lookup"><span data-stu-id="74329-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="74329-251">Tworzenie atrybutów niestandardowych, które mogą być używane do mapowania właściwości pól dokumentu.</span><span class="sxs-lookup"><span data-stu-id="74329-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="74329-252">Można znaleźć przykłady stosowania niestandardowej serializacji w testy jednostek dla zestawu SDK .NET wyszukiwanie Azure w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="74329-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="74329-253">Dobry punkt wyjścia jest [ten folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="74329-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="74329-254">Zawiera klasy, które są używane przez testy niestandardowej serializacji.</span><span class="sxs-lookup"><span data-stu-id="74329-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="74329-255">Wyszukiwanie dokumentów w indeksie</span><span class="sxs-lookup"><span data-stu-id="74329-255">Searching for documents in the index</span></span>
<span data-ttu-id="74329-256">Ostatnim krokiem w przykładowej aplikacji jest do wyszukiwania niektórych dokumentów w indeksie.</span><span class="sxs-lookup"><span data-stu-id="74329-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="74329-257">Następująca metoda robi to:</span><span class="sxs-lookup"><span data-stu-id="74329-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
    Console.WriteLine("and return the hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take the top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search the entire index for the term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="74329-258">Każdy czasu wykonywania zapytania, najpierw ta metoda tworzy nowy `SearchParameters` obiektu.</span><span class="sxs-lookup"><span data-stu-id="74329-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="74329-259">Umożliwia określenie dodatkowych opcji zapytania, takie jak sortowanie, filtrowanie, stronicowania i tworzenie aspektów.</span><span class="sxs-lookup"><span data-stu-id="74329-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="74329-260">W przypadku tej metody jest firma Microsoft ustawienie `Filter`, `Select`, `OrderBy`, i `Top` właściwości dla różnych zapytań.</span><span class="sxs-lookup"><span data-stu-id="74329-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="74329-261">Wszystkie `SearchParameters` właściwości są udokumentowane [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="74329-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="74329-262">Następnym krokiem jest rzeczywiście wykonać kwerendy wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74329-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="74329-263">Jest to realizowane przy użyciu `Documents.Search` metody.</span><span class="sxs-lookup"><span data-stu-id="74329-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="74329-264">Dla każdego zapytania jest przekazywana szukany tekst do użycia jako ciąg (lub `"*"` , jeśli nie ma żadnego tekstu wyszukiwania), oraz parametry wyszukiwania utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="74329-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="74329-265">Również określić `Hotel` jako parametr typu dla `Documents.Search`, który określa, że zestaw SDK, aby deserializować dokumentów w wynikach wyszukiwania w obiektach typu `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="74329-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="74329-266">Można znaleźć więcej informacji na temat składni wyrażeń zapytania wyszukiwania [tutaj](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="74329-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="74329-267">Na koniec po każdym zapytaniem tej metody iteruje wszystkie dopasowania w wynikach wyszukiwania, drukowania każdego dokumentu do konsoli:</span><span class="sxs-lookup"><span data-stu-id="74329-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="74329-268">Z kolei wytłumaczone bliższe spojrzenie na każdym z zapytania.</span><span class="sxs-lookup"><span data-stu-id="74329-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="74329-269">Oto kod do wykonania pierwszej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="74329-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="74329-270">W takim przypadku możemy Cię szukające hoteli, zgodne słowo "budget" i chcemy, aby odzyskać tylko nazwy hoteli, określony przez `Select` parametru.</span><span class="sxs-lookup"><span data-stu-id="74329-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="74329-271">Poniżej przedstawiono wyniki:</span><span class="sxs-lookup"><span data-stu-id="74329-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="74329-272">Następnie chcemy znaleźć hotele co noc szybkość wynosi mniej niż 150 USD i zwróć tylko identyfikator hoteli i opis:</span><span class="sxs-lookup"><span data-stu-id="74329-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="74329-273">To zapytanie używa OData `$filter` wyrażenie `baseRate lt 150`, aby filtrować dokumenty w indeksie.</span><span class="sxs-lookup"><span data-stu-id="74329-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="74329-274">Można dowiedzieć się więcej o składni OData, który obsługuje usługę Azure Search [tutaj](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="74329-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="74329-275">Poniżej przedstawiono wyniki zapytania:</span><span class="sxs-lookup"><span data-stu-id="74329-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="74329-276">Następnie chcemy się znaleźć górny dwóch hotele, które zostały ostatnio renovated i zawierają nazwę hoteli i datę ostatniej odnawianie.</span><span class="sxs-lookup"><span data-stu-id="74329-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="74329-277">Oto kod:</span><span class="sxs-lookup"><span data-stu-id="74329-277">Here is the code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="74329-278">W takim przypadku ponownie używamy składni OData do określenia `OrderBy` parametr jako `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="74329-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="74329-279">Możemy również ustawić `Top` 2, aby upewnić się, uzyskujemy tylko dokumenty dwóch pierwszych.</span><span class="sxs-lookup"><span data-stu-id="74329-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="74329-280">Jak wcześniej, możemy ustawić `Select` do określenia pola, które ma zostać zwrócony.</span><span class="sxs-lookup"><span data-stu-id="74329-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="74329-281">Poniżej przedstawiono wyniki:</span><span class="sxs-lookup"><span data-stu-id="74329-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="74329-282">Wreszcie chcemy mieć Znajdź wszystkie hotele, zgodne słowo "motel":</span><span class="sxs-lookup"><span data-stu-id="74329-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="74329-283">A Oto wyniki, które obejmują wszystkie pola, ponieważ firma Microsoft nie określono `Select` właściwości:</span><span class="sxs-lookup"><span data-stu-id="74329-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="74329-284">Ten krok jest wykonywany samouczek, ale nie zatrzymuje tutaj.</span><span class="sxs-lookup"><span data-stu-id="74329-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="74329-285">**Następne kroki** przedstawiono dodatkowe zasoby, aby uzyskać więcej informacji na temat usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="74329-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74329-286">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74329-286">Next steps</span></span>
* <span data-ttu-id="74329-287">Przeglądaj odwołania do [zestawu SDK .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) oraz [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="74329-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="74329-288">Pogłębić swoją wiedzę za pośrednictwem [wideo i inne przykłady i samouczki](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="74329-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="74329-289">Przegląd [konwencje nazewnictwa](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) Aby dowiedzieć się reguły nazewnictwa różnych obiektów.</span><span class="sxs-lookup"><span data-stu-id="74329-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="74329-290">Przegląd [obsługiwane typy danych](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="74329-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
