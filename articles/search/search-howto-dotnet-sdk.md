---
title: "toouse aaaHow usługi Azure Search z aplikacji .NET | Dokumentacja firmy Microsoft"
description: "W jaki sposób toouse Azure wyszukiwanie od aplikacji .NET"
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
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="24201-103">W jaki sposób toouse Azure wyszukiwanie od aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="24201-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="24201-104">W tym artykule jest tooget wskazówki można do pracy z hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="24201-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="24201-105">Można użyć tooimplement zestawu .NET SDK hello wzbogaconej wyszukiwania doświadczenie w aplikacji przy użyciu usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="24201-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="24201-106">Nowości w hello wyszukiwanie Azure SDK</span><span class="sxs-lookup"><span data-stu-id="24201-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="24201-107">Witaj zestaw SDK składa się z biblioteki klienta, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="24201-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="24201-108">Go umożliwia toomanage można z indeksów, źródła danych i indeksatorów, oraz przekazywanie i zarządzania dokumentami i wykonywać zapytania, bez konieczności toodeal ze szczegółami hello HTTP i JSON.</span><span class="sxs-lookup"><span data-stu-id="24201-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="24201-109">Biblioteka klienta Hello definiuje klas takich jak `Index`, `Field`, i `Document`, jak również operacji, takich jak `Indexes.Create` i `Documents.Search` na powitania `SearchServiceClient` i `SearchIndexClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="24201-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="24201-110">Te klasy są podzielone na następujące obszary nazw hello:</span><span class="sxs-lookup"><span data-stu-id="24201-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="24201-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="24201-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="24201-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="24201-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="24201-113">Bieżąca wersja hello zestawu .NET SDK usługi Azure Search Hello teraz jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="24201-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="24201-114">Jeśli chcesz opinii tooprovide nam tooincorporate hello następnej wersji, można znaleźć na naszych [strony](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="24201-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="24201-115">Witaj zestawu .NET SDK obsługuje wersję `2016-09-01` z hello [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="24201-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="24201-116">Ta wersja zawiera teraz obsługę niestandardowych analizatory i obiektów Blob platformy Azure i tabel Azure indeksatorze obsługi.</span><span class="sxs-lookup"><span data-stu-id="24201-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="24201-117">Funkcji, które są w wersji zapoznawczej *nie* są częścią tej wersji, takie jak Obsługa indeksowania JSON i woluminów CSV, [Podgląd](search-api-2015-02-28-preview.md) i dostępne za pośrednictwem hello starsze [2.0 — wersja zapoznawcza hello zestawu .NET SDK ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="24201-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="24201-118">Zestaw SDK nie obsługuje [operacji zarządzania](https://docs.microsoft.com/rest/api/searchmanagement/) takich jak tworzenie i skalowanie usługi wyszukiwania i zarządzanie nimi klucze interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24201-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="24201-119">Jeśli potrzebujesz toomanage wyszukiwania zasobów z poziomu aplikacji .NET, można użyć hello [zestawu SDK usługi Azure Search .NET zarządzania](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="24201-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="24201-120">Uaktualnianie toohello najnowszą wersję hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="24201-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="24201-121">Jeśli już używasz starszej wersji hello zestawu .NET SDK usługi Azure Search i chcesz tooupgrade toohello ogólnie dostępna wersja nowego, [w tym artykule](search-dotnet-sdk-migration.md) wyjaśniono sposób.</span><span class="sxs-lookup"><span data-stu-id="24201-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="24201-122">Wymagania dotyczące hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="24201-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="24201-123">Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="24201-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="24201-124">Własne usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="24201-124">Your own Azure Search service.</span></span> <span data-ttu-id="24201-125">W kolejności toouse hello zestawu SDK konieczne będzie hello nazwę usługi i co najmniej jeden klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24201-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="24201-126">[Tworzenie usługi w portalu hello](search-create-service-portal.md) pomoże Ci tych kroków.</span><span class="sxs-lookup"><span data-stu-id="24201-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="24201-127">Pobierz hello zestawu .NET SDK usługi Azure Search [pakietu NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) za pomocą "Manage NuGet Packages" programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24201-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="24201-128">Po prostu wyszukać nazwę pakietu hello `Microsoft.Azure.Search` na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="24201-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="24201-129">Witaj zestawu .NET SDK usługi Azure Search obsługuje aplikacji hello .NET Framework 4.6 i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="24201-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="24201-130">Podstawowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="24201-130">Core scenarios</span></span>
<span data-ttu-id="24201-131">Istnieje kilka czynności, będziesz potrzebować toodo w aplikacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24201-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="24201-132">W tym samouczku omówione zostaną następujące czynności te podstawowe scenariusze:</span><span class="sxs-lookup"><span data-stu-id="24201-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="24201-133">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="24201-133">Creating an index</span></span>
* <span data-ttu-id="24201-134">Podczas wypełniania indeksu hello z dokumentami</span><span class="sxs-lookup"><span data-stu-id="24201-134">Populating hello index with documents</span></span>
* <span data-ttu-id="24201-135">Wyszukiwanie dokumentów za pomocą wyszukiwania pełnotekstowego oraz filtry</span><span class="sxs-lookup"><span data-stu-id="24201-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="24201-136">Hello przykładowy kod, który następuje ilustruje każdą z tych.</span><span class="sxs-lookup"><span data-stu-id="24201-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="24201-137">Możesz wstawki kodu hello wolnego toouse w swojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24201-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="24201-138">Omówienie</span><span class="sxs-lookup"><span data-stu-id="24201-138">Overview</span></span>
<span data-ttu-id="24201-139">Witaj przykładowej aplikacji, firma Microsoft będzie można badać tworzy nowy indeks o nazwie "hotels" wypełnia kilku dokumentów, a następnie wykonuje kilka zapytań wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24201-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="24201-140">Oto główne programu hello, przedstawiający hello ogólny przepływ:</span><span class="sxs-lookup"><span data-stu-id="24201-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="24201-141">Można znaleźć hello pełny kod źródłowy hello przykładowej aplikacji używane w tym krokach związanych z na [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="24201-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="24201-142">Zostanie omówiony ten krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="24201-142">We'll walk through this step by step.</span></span> <span data-ttu-id="24201-143">Najpierw musimy toocreate nowy `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="24201-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="24201-144">Ten obiekt umożliwia toomanage indeksów.</span><span class="sxs-lookup"><span data-stu-id="24201-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="24201-145">W kolejności tooconstruct jedną należy tooprovide nazwę usługi Azure Search, a także klucz interfejsu API administratora.</span><span class="sxs-lookup"><span data-stu-id="24201-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="24201-146">Te informacje można wprowadzić w hello `appsettings.json` pliku hello [Przykładowa aplikacja](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="24201-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="24201-147">Jeśli podasz nieprawidłowy klucz (na przykład klucz zapytania gdzie klucz administratora nie jest wymagana) hello `SearchServiceClient` zgłosi `CloudException` z hello błąd komunikat "Zabronione" hello po raz pierwszy należy wywołać metody operacji, takich jak `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="24201-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="24201-148">W takim przypadku tooyou dokładnie sprawdzić naszych klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24201-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="24201-149">Witaj następnych kilku wierszy wywołania metody toocreate indeksu o nazwie "hotels", usuwając go najpierw, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="24201-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="24201-150">Firma Microsoft przeprowadzi tych metod nieco później.</span><span class="sxs-lookup"><span data-stu-id="24201-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="24201-151">Następnie hello indeks musi toobe wypełnione.</span><span class="sxs-lookup"><span data-stu-id="24201-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="24201-152">toodo, firma Microsoft będzie `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="24201-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="24201-153">Istnieją dwa sposoby tooobtain, jedną: tworząc go lub poprzez wywołanie `Indexes.GetClient` na powitania `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="24201-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="24201-154">Używamy hello drugie dla wygody.</span><span class="sxs-lookup"><span data-stu-id="24201-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="24201-155">W typowej aplikacji wyszukującej wypełnianie indeksu i zarządzanie nim jest obsługiwane przez inny składnik niż zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24201-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="24201-156">`Indexes.GetClient`jest wygodną metodą wypełniania indeksu, ponieważ wymaga dostarczenia kolejnej hello `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="24201-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="24201-157">Robi to przez przekazanie klucza administratora hello tego możesz używane toocreate hello `SearchServiceClient` toohello nowe `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="24201-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="24201-158">Jednak w hello część aplikacji, która wykonuje zapytania jest lepsze hello toocreate `SearchIndexClient` bezpośrednio, aby można przekazać klucz zapytania zamiast klucza administratora.</span><span class="sxs-lookup"><span data-stu-id="24201-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="24201-159">To jest zgodna z zasadą najniższych uprawnień hello i pomoże toomake aplikacji bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="24201-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="24201-160">Można dowiedzieć się więcej o kluczach administratora i kluczach zapytań [tutaj](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="24201-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="24201-161">Teraz, gdy mamy `SearchIndexClient`, firma Microsoft może wypełnić hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="24201-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="24201-162">Jest to realizowane przy użyciu innej metody, które firma Microsoft przeprowadzi później.</span><span class="sxs-lookup"><span data-stu-id="24201-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="24201-163">Na koniec możemy wykonać kilka zapytań wyszukiwania i wyświetlić wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="24201-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="24201-164">Teraz możemy użyć innego `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="24201-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="24201-165">Firma Microsoft podejmie bliższe spojrzenie na powitania `RunQueries` metody później.</span><span class="sxs-lookup"><span data-stu-id="24201-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="24201-166">Poniżej przedstawiono nowe hello kodu toocreate hello `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="24201-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="24201-167">Teraz firma Microsoft używa klucza zapytania, ponieważ nie potrzebujemy indeksu toohello dostęp do zapisu.</span><span class="sxs-lookup"><span data-stu-id="24201-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="24201-168">Te informacje można wprowadzić w hello `appsettings.json` pliku hello [Przykładowa aplikacja](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="24201-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="24201-169">Po uruchomieniu tej aplikacji z prawidłową nazwę usługi i klucze interfejsu API hello dane wyjściowe powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="24201-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="24201-170">Witaj pełny kod źródłowy aplikacji hello znajduje się na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="24201-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="24201-171">Następnie będzie trwać bliższe spojrzenie na każdej z metod hello wywoływane przez `Main`.</span><span class="sxs-lookup"><span data-stu-id="24201-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="24201-172">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="24201-172">Creating an index</span></span>
<span data-ttu-id="24201-173">Po utworzeniu `SearchServiceClient`, co dalej hello `Main` jest jest delete hello indeksu "hotels", jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="24201-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="24201-174">Który odbywa się przez hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="24201-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="24201-175">Ta metoda używa hello podane `SearchServiceClient` toocheck Jeśli indeks hello istnieje, a jeśli tak, usuń go.</span><span class="sxs-lookup"><span data-stu-id="24201-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-176">Witaj przykładowy kod w tym artykule używa metod synchronicznych hello hello zestawu .NET SDK usługi Azure Search dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="24201-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="24201-177">Firma Microsoft zaleca używanie metod asynchronicznych hello w tookeep własne aplikacje ich skalowalne i szybko reagowały.</span><span class="sxs-lookup"><span data-stu-id="24201-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="24201-178">Na przykład w hello metody powyżej, które można użyć `ExistsAsync` i `DeleteAsync` zamiast `Exists` i `Delete`.</span><span class="sxs-lookup"><span data-stu-id="24201-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="24201-179">Następnie `Main` powoduje utworzenie nowego indeksu "hotels" przez wywołanie tej metody:</span><span class="sxs-lookup"><span data-stu-id="24201-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="24201-180">Ta metoda tworzy nowy `Index` obiektu z listy `Field` obiektów, które definiuje schemat hello hello nowego indeksu.</span><span class="sxs-lookup"><span data-stu-id="24201-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="24201-181">Każde pole ma nazwę, typ danych i kilka atrybutów, które określają zachowanie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24201-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="24201-182">Witaj `FieldBuilder` klasy używa toocreate odbicia listę `Field` obiektów dla indeksu hello, sprawdzając hello publicznej właściwości i atrybutów hello podane `Hotel` klasa modelu.</span><span class="sxs-lookup"><span data-stu-id="24201-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="24201-183">Przeniesiemy bliższe spojrzenie na powitania `Hotel` klasy później.</span><span class="sxs-lookup"><span data-stu-id="24201-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-184">Zawsze można utworzyć listy hello `Field` obiektów bezpośrednio zamiast `FieldBuilder` w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="24201-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="24201-185">Na przykład możesz nie chcieć toouse klasę modelu lub może być konieczne toouse istniejącej klasy modelu użytkownik chce toomodify przez dodanie atrybutów.</span><span class="sxs-lookup"><span data-stu-id="24201-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="24201-186">Ponadto toofields, można również dodać oceniania profile, sugestorów lub CORS toohello opcji indeksu (te zostaną pominięte próbki hello w celu jego skrócenia).</span><span class="sxs-lookup"><span data-stu-id="24201-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="24201-187">Więcej informacji na temat hello indeksu obiekt i jego elementów składowych można znaleźć w hello [odwołania do zestawu SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), jak również w hello [dokumentacji interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="24201-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="24201-188">Podczas wypełniania indeksu hello</span><span class="sxs-lookup"><span data-stu-id="24201-188">Populating hello index</span></span>
<span data-ttu-id="24201-189">następnym krokiem Hello w `Main` toopopulate hello nowo utworzony indeks.</span><span class="sxs-lookup"><span data-stu-id="24201-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="24201-190">Można to zrobić w hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="24201-190">This is done in hello following method:</span></span>

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
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="24201-191">Ta metoda ma cztery części.</span><span class="sxs-lookup"><span data-stu-id="24201-191">This method has four parts.</span></span> <span data-ttu-id="24201-192">Witaj najpierw tworzy tablicę `Hotel` obiektów, które będzie służyć jako dane wejściowe tooupload toohello indeksu.</span><span class="sxs-lookup"><span data-stu-id="24201-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="24201-193">Te dane są stałe dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="24201-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="24201-194">W aplikacji danych prawdopodobnie będzie pochodził z zewnętrznego źródła danych takie jak bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="24201-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="24201-195">druga część Hello tworzy `IndexBatch` zawierających hello dokumenty.</span><span class="sxs-lookup"><span data-stu-id="24201-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="24201-196">Określ operację hello ma tooapply toohello partii w czasie hello należy utworzyć ją, w tym przypadku przez wywołanie metody `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="24201-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="24201-197">Hello partii jest następnie przekazane toohello usługi Azure Search index przez hello `Documents.Index` metody.</span><span class="sxs-lookup"><span data-stu-id="24201-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-198">W tym przykładzie mamy tylko przekazywania dokumentów.</span><span class="sxs-lookup"><span data-stu-id="24201-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="24201-199">Jeśli potrzebujesz toomerge zmian do istniejących dokumentów lub usuwanie dokumentów, możesz utworzyć partie przez wywołanie metody `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, lub `IndexBatch.Delete` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="24201-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="24201-200">Możesz łączyć różnych operacji w pojedynczej partii przez wywołanie metody `IndexBatch.New`, który przyjmuje Kolekcja `IndexAction` obiektów, z których każdy określa, że usługi Azure Search tooperform określonej operacji w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="24201-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="24201-201">Można utworzyć każdego `IndexAction` z działaniem wywołując hello odpowiedniej metody, takie jak `IndexAction.Merge`, `IndexAction.Upload`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="24201-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="24201-202">Witaj trzeci część tej metody jest blok catch obsługuje ważny przypadek błędu indeksowania.</span><span class="sxs-lookup"><span data-stu-id="24201-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="24201-203">Jeśli usługi Azure Search nie powiedzie się tooindex niektóre hello dokumentów w partii hello `IndexBatchException` jest generowany przez `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="24201-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="24201-204">Może to nastąpić, jeśli indeksujesz dokumenty w czasie, gdy usługa jest mocno obciążona.</span><span class="sxs-lookup"><span data-stu-id="24201-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="24201-205">**Zdecydowanie zalecamy jawną obsługę tego przypadku w kodzie.**</span><span class="sxs-lookup"><span data-stu-id="24201-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="24201-206">Można opóźnić, a następnie ponów próbę indeksowania hello dokumentów, których nie powiodła się lub zaloguj się i kontynuować jak w prezentowanym przykładzie hello, lub możesz też wykonać inną akcję w zależności od wymagań spójności danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24201-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-207">Można użyć hello `FindFailedActionsToRetry` tooconstruct metody, zawierający nowe partii hello tylko akcje, których nie powiodła się w poprzednie wywołanie za`Index`.</span><span class="sxs-lookup"><span data-stu-id="24201-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="24201-208">Metoda Hello jest udokumentowany [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) i uzyskać informacje dotyczące sposobu używania go tooproperly [w witrynie StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="24201-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="24201-209">Na koniec hello `UploadDocuments` umieszczono dwusekundowe opóźnienie metody.</span><span class="sxs-lookup"><span data-stu-id="24201-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="24201-210">Indeksowanie odbywa się asynchronicznie w usłudze Azure Search tak hello Przykładowa aplikacja musi toowait tooensure krótki czas, że hello dokumenty można wyszukiwać.</span><span class="sxs-lookup"><span data-stu-id="24201-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="24201-211">Tego typu opóźnienia są zazwyczaj konieczne tylko w przypadku pokazów, testów i przykładowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24201-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="24201-212">Jak hello zestawu .NET SDK obsługuje dokumenty</span><span class="sxs-lookup"><span data-stu-id="24201-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="24201-213">Możesz się zastanawiać, jak hello zestawu .NET SDK usługi Azure Search jest tooupload stanie wystąpienia klasy zdefiniowanej przez użytkownika, jak `Hotel` toohello indeksu.</span><span class="sxs-lookup"><span data-stu-id="24201-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="24201-214">toohelp odpowiedzi na to pytanie, Przyjrzyjmy się hello `Hotel` klasy:</span><span class="sxs-lookup"><span data-stu-id="24201-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
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

<span data-ttu-id="24201-215">Witaj po pierwsze toonotice jest to, że każda właściwość publiczna klasy `Hotel` odpowiada tooa pola w definicji indeksu hello, ale z jedną istotną różnicą: hello nazwę każdego pola rozpoczyna się małą literą (camelcase"), podczas hello nazwę każdego publicznego Właściwość `Hotel` rozpoczyna się wielką literą ("Pascal litery").</span><span class="sxs-lookup"><span data-stu-id="24201-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="24201-216">To typowy scenariusz w aplikacjach .NET, które tworzą powiązania danych, gdzie schemat docelowy hello jest poza hello kontroli Deweloper aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="24201-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="24201-217">Zamiast tooviolate hello zasady nazewnictwa platformy .NET dokonując camelcase nazwy właściwości, można ustalić hello SDK toomap hello właściwość nazwy toocamel przypadku automatycznie z hello `[SerializePropertyNamesAsCamelCase]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="24201-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-218">Witaj zestawu .NET SDK usługi Azure Search korzysta hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize biblioteki i deserializacji tooand obiekty z modelu niestandardowych z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="24201-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="24201-219">W razie potrzeby możesz dostosować serializację.</span><span class="sxs-lookup"><span data-stu-id="24201-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="24201-220">Aby uzyskać więcej informacji, zobacz [niestandardowe serializacji z struktury JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="24201-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="24201-221">Hello drugi element toonotice to hello atrybutów, takich jak `IsFilterable`, `IsSearchable`, `Key`, i `Analyzer` który dekoracji każda właściwość publiczna.</span><span class="sxs-lookup"><span data-stu-id="24201-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="24201-222">Te atrybuty bezpośrednio mapy toohello [odpowiednie atrybuty indeksu usługi Azure Search hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="24201-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="24201-223">Witaj `FieldBuilder` klasy używa tych definicji pola tooconstruct hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="24201-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="24201-224">Witaj trzeci ważną kwestią dotyczącą hello `Hotel` hello typy danych właściwości publicznych hello są klasy.</span><span class="sxs-lookup"><span data-stu-id="24201-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="24201-225">Hello typy .NET tych właściwości mapy typy pól równoważne tootheir w definicji indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="24201-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="24201-226">Na przykład Witaj `Category` toohello mapy właściwości ciągu `category` pola, które jest typu `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="24201-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="24201-227">Istnieją podobne mapowania typów między `bool?` i `Edm.Boolean`, `DateTimeOffset?` i `Edm.DateTimeOffset`, itp. hello dokładne zasady mapowania typu hello są udokumentowane hello `Documents.Get` metoda hello [zestawu .NET SDK usługi Azure Search Odwołanie](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="24201-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="24201-228">Witaj `FieldBuilder` klasy zajmuje się to mapowanie dla Ciebie, ale nadal może być przydatne toounderstand w razie potrzeby tootroubleshoot problemy serializacji.</span><span class="sxs-lookup"><span data-stu-id="24201-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="24201-229">Ta toouse możliwości własnych klas jako dokumentów działa w obu kierunkach; Można również pobrać wyniki wyszukiwania i hello zestawu SDK dokonać ich automatycznej deserializacji typu tooa wybranych przez użytkownika, jak zostanie wyświetlone w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="24201-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-230">Witaj zestawu .NET SDK usługi Azure Search obsługuje również dynamiczne typowanie dokumentów za pomocą hello `Document` klasy, która jest mapowanie klucz/wartość, wartości toofield nazw pól.</span><span class="sxs-lookup"><span data-stu-id="24201-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="24201-231">Jest to przydatne w scenariuszach, jeśli nie znasz schematu indeksu hello w czasie projektowania lub gdy byłoby niewygodne toobind toospecific modelu klasy.</span><span class="sxs-lookup"><span data-stu-id="24201-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="24201-232">Wszystkie metody hello w hello zestawu SDK, które obsługują dokumenty mają przeciążenia działające z hello `Document` klasy, a także przeciążenia o silnych typach, które przyjmują parametr typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="24201-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="24201-233">Tylko hello te ostatnie są używane w hello przykładowy kod w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="24201-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="24201-234">Witaj `Document` klasa dziedziczy `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="24201-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="24201-235">Inne szczegółowe informacje można znaleźć [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="24201-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="24201-236">**Dlaczego należy używać typów danych dopuszczających wartość null**</span><span class="sxs-lookup"><span data-stu-id="24201-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="24201-237">Podczas projektowania indeksu własne modelu klasy toomap tooan usługi Azure Search, zalecamy deklarowanie właściwości typów wartości, takich jak `bool` i `int` toobe wartości null (na przykład `bool?` zamiast `bool`).</span><span class="sxs-lookup"><span data-stu-id="24201-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="24201-238">Użycie wartości null właściwość masz zbyt**zagwarantować** że żaden dokument w indeksie nie zawiera wartości null dla odpowiednich pól hello.</span><span class="sxs-lookup"><span data-stu-id="24201-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="24201-239">Hello zestawu SDK ani hello usługi Azure Search nie pomoże tooenforce należy to.</span><span class="sxs-lookup"><span data-stu-id="24201-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="24201-240">To nie jest to czysto hipotetyczny problem: Wyobraź sobie scenariusz, w którym dodajesz nowe pole tooan istniejącego indeksu typu `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="24201-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="24201-241">Po zaktualizowaniu definicji indeksu hello, wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy dopuszczają wartości null w usłudze Azure Search).</span><span class="sxs-lookup"><span data-stu-id="24201-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="24201-242">Jeśli następnie użyjesz klasy modelu z niedopuszczającą `int` właściwości dla tego pola, otrzymasz `JsonSerializationException` podobny podczas próby tooretrieve dokumentów:</span><span class="sxs-lookup"><span data-stu-id="24201-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="24201-243">Z tego powodu najlepszym i zalecanym rozwiązaniem jest używanie w klasach modeli typów dopuszczających wartość null.</span><span class="sxs-lookup"><span data-stu-id="24201-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="24201-244">Niestandardowej serializacji z struktury JSON.NET</span><span class="sxs-lookup"><span data-stu-id="24201-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="24201-245">Witaj SDK używa struktury JSON.NET do serializacji i deserializacji dokumentów.</span><span class="sxs-lookup"><span data-stu-id="24201-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="24201-246">Można dostosować serializacji i deserializacji w razie potrzeby, definiując własne `JsonConverter` lub `IContractResolver` (zobacz hello [dokumentacji struktury JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) więcej szczegółów).</span><span class="sxs-lookup"><span data-stu-id="24201-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="24201-247">Może to być przydatne, jeśli chcesz tooadapt istniejącej klasy modelu z aplikacji do użycia z usługi Azure Search i innych bardziej zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="24201-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="24201-248">Na przykład za pomocą niestandardowej serializacji można:</span><span class="sxs-lookup"><span data-stu-id="24201-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="24201-249">Uwzględnić lub wykluczyć pewne właściwości klasy modelu są przechowywane jako pól dokumentu.</span><span class="sxs-lookup"><span data-stu-id="24201-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="24201-250">Mapowania nazw właściwości w kodzie i nazw pól w indeksie.</span><span class="sxs-lookup"><span data-stu-id="24201-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="24201-251">Tworzenie atrybutów niestandardowych, które mogą być używane do mapowania pól toodocument właściwości.</span><span class="sxs-lookup"><span data-stu-id="24201-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="24201-252">Można znaleźć przykłady stosowania niestandardowej serializacji w hello testów jednostkowych dla hello Azure Search .NET SDK w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="24201-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="24201-253">Dobry punkt wyjścia jest [ten folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="24201-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="24201-254">Zawiera klasy, które są używane przez hello niestandardowej serializacji testy.</span><span class="sxs-lookup"><span data-stu-id="24201-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="24201-255">Wyszukiwanie dokumentów w indeksie hello</span><span class="sxs-lookup"><span data-stu-id="24201-255">Searching for documents in hello index</span></span>
<span data-ttu-id="24201-256">Ostatnim krokiem hello Przykładowa aplikacja Hello jest toosearch dla niektórych dokumentów w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="24201-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="24201-257">następujące metody Hello robi to:</span><span class="sxs-lookup"><span data-stu-id="24201-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
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

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="24201-258">Każdy czasu wykonywania zapytania, najpierw ta metoda tworzy nowy `SearchParameters` obiektu.</span><span class="sxs-lookup"><span data-stu-id="24201-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="24201-259">Jest to dodatkowe opcje używane toospecify hello zapytania, takie jak sortowanie, filtrowanie, stronicowania i tworzenie aspektów.</span><span class="sxs-lookup"><span data-stu-id="24201-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="24201-260">W przypadku tej metody, firma Microsoft jest ustawienie hello `Filter`, `Select`, `OrderBy`, i `Top` właściwości dla różnych zapytań.</span><span class="sxs-lookup"><span data-stu-id="24201-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="24201-261">Wszystkie hello `SearchParameters` właściwości są udokumentowane [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="24201-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="24201-262">Witaj, następnym krokiem jest tooactually wykonać hello zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24201-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="24201-263">Jest to realizowane przy użyciu hello `Documents.Search` metody.</span><span class="sxs-lookup"><span data-stu-id="24201-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="24201-264">Dla każdego zapytania hello wyszukiwania tekstu toouse przekazywana jako ciąg (lub `"*"` , jeśli nie ma żadnego tekstu wyszukiwania), oraz hello wyszukiwania parametry utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="24201-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="24201-265">Również określić `Hotel` jako parametr typu hello `Documents.Search`, który informuje hello SDK toodeserialize dokumentów w wynikach wyszukiwania hello w obiektach typu `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="24201-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="24201-266">Można znaleźć więcej informacji na temat składni wyrażeń zapytania wyszukiwania hello [tutaj](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="24201-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="24201-267">Na koniec po każdym zapytaniem tej metody iteruje wszystkie dopasowania hello w wynikach wyszukiwania hello, drukowanie każdego dokumentu toohello konsoli:</span><span class="sxs-lookup"><span data-stu-id="24201-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

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

<span data-ttu-id="24201-268">Z kolei wytłumaczone bliższe spojrzenie na każdym hello zapytań.</span><span class="sxs-lookup"><span data-stu-id="24201-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="24201-269">Oto hello kodu tooexecute hello pierwszego zapytania:</span><span class="sxs-lookup"><span data-stu-id="24201-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="24201-270">W takim przypadku możemy Cię szukające hoteli, zgodne hello word "budget" i chcemy tooget ponownie tylko hello hoteli nazwy, określony przez hello `Select` parametru.</span><span class="sxs-lookup"><span data-stu-id="24201-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="24201-271">Poniżej przedstawiono wyniki hello:</span><span class="sxs-lookup"><span data-stu-id="24201-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="24201-272">Następnie możemy mają hotels hello toofind co noc szybkość wynosi mniej niż 150 USD i zwracać tylko identyfikator hoteli hello i opis:</span><span class="sxs-lookup"><span data-stu-id="24201-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

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

<span data-ttu-id="24201-273">To zapytanie używa OData `$filter` wyrażenie `baseRate lt 150`, toofilter hello dokumenty w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="24201-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="24201-274">Można dowiedzieć się więcej o składni OData, który obsługuje usługę Azure Search hello [tutaj](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="24201-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="24201-275">Poniżej przedstawiono wyniki hello hello zapytania:</span><span class="sxs-lookup"><span data-stu-id="24201-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="24201-276">Następnie chcemy toofind hello top dwóch hotels został ostatnio renovated, które zawierają nazwę hoteli hello i odnawianie Data.</span><span class="sxs-lookup"><span data-stu-id="24201-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="24201-277">Oto kod hello:</span><span class="sxs-lookup"><span data-stu-id="24201-277">Here is hello code:</span></span> 

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

<span data-ttu-id="24201-278">W takim przypadku ponownie używamy OData składni toospecify hello `OrderBy` parametr jako `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="24201-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="24201-279">Możemy również ustawić `Top` too2 tooensure tylko uzyskujemy hello dwa dokumenty.</span><span class="sxs-lookup"><span data-stu-id="24201-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="24201-280">Jak wcześniej, możemy ustawić `Select` toospecify pola, które ma zostać zwrócony.</span><span class="sxs-lookup"><span data-stu-id="24201-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="24201-281">Poniżej przedstawiono wyniki hello:</span><span class="sxs-lookup"><span data-stu-id="24201-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="24201-282">Wreszcie chcemy mieć toofind wszystkie hotele, zgodne hello słowo "motel":</span><span class="sxs-lookup"><span data-stu-id="24201-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="24201-283">A Oto hello wyników, które obejmują wszystkie pola, ponieważ nie określono firma Microsoft hello `Select` właściwości:</span><span class="sxs-lookup"><span data-stu-id="24201-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="24201-284">Ten krok jest wykonywany hello samouczek, ale nie zatrzymuje tutaj.</span><span class="sxs-lookup"><span data-stu-id="24201-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="24201-285">**Następne kroki** przedstawiono dodatkowe zasoby, aby uzyskać więcej informacji na temat usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="24201-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24201-286">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24201-286">Next steps</span></span>
* <span data-ttu-id="24201-287">Przeglądaj hello odwołań dla hello [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) i [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="24201-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="24201-288">Pogłębić swoją wiedzę za pośrednictwem [wideo i inne przykłady i samouczki](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="24201-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="24201-289">Przegląd [konwencje nazewnictwa](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello reguły nazewnictwa różnych obiektów.</span><span class="sxs-lookup"><span data-stu-id="24201-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="24201-290">Przegląd [obsługiwane typy danych](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="24201-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
