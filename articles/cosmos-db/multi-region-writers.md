---
title: "architektury aaaMulti główny bazy danych z bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toodesign architekturach aplikacji lokalnych odczytuje i zapisuje w różnych regionach geograficznych z bazy danych Azure rozwiązania Cosmos."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="80730-103">Wzorzec wielu globalnie zreplikowany architektury bazy danych z bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="80730-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="80730-104">Azure DB rozwiązania Cosmos obsługuje gotowe [globalnej replikacji](distribute-data-globally.md), co pozwala toodistribute danych toomultiple regionach o małych opóźnieniach dostępu w dowolnym miejscu hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="80730-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="80730-105">Ten model jest najczęściej używany w przypadku obciążeń wydawcy/konsumenta przypadku zapisywania w jednym regionie geograficznym i czytników globalnie rozproszone w różnych regionach (odczytu).</span><span class="sxs-lookup"><span data-stu-id="80730-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="80730-106">Umożliwia także Azure rozwiązania Cosmos DB globalnej replikacji obsługuje toobuild aplikacji w których autorzy i czytników są globalnie rozproszone.</span><span class="sxs-lookup"><span data-stu-id="80730-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="80730-107">W tym dokumencie przedstawiono wzorzec, która umożliwia uzyskanie lokalnego zapisu i lokalne dostęp do odczytu autorzy rozproszonego przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80730-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="80730-108"><a id="ExampleScenario"></a>Publikowanie — przykładowy scenariusz zawartości</span><span class="sxs-lookup"><span data-stu-id="80730-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="80730-109">Przyjrzyjmy się toodescribe scenariusza rzeczywistych wykorzystania wzorce globalnie rozproszone kilku-region/kilku-główny odczytu zapisu z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80730-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="80730-110">Należy wziąć pod uwagę zawartości platformy publikowania oparte na usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80730-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="80730-111">Poniżej przedstawiono niektóre wymagania, które musi spełniać ta platforma obsługi użytkowników dla konsumentów i wydawców.</span><span class="sxs-lookup"><span data-stu-id="80730-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="80730-112">Zarówno twórcy, jak i subskrybentów są rozkładane Witaj świecie</span><span class="sxs-lookup"><span data-stu-id="80730-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="80730-113">Autorzy należy opublikować lokalny region (najbliższego) (Zapisz) artykuły tootheir</span><span class="sxs-lookup"><span data-stu-id="80730-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="80730-114">Autorzy mają czytników/użytkownikom ich artykułów są rozproszone na Witaj świecie.</span><span class="sxs-lookup"><span data-stu-id="80730-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="80730-115">Subskrybenci należy uzyskać powiadomienie, gdy nowe artykuły są publikowane.</span><span class="sxs-lookup"><span data-stu-id="80730-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="80730-116">Subskrybenci musi być możliwe tooread artykuły z ich lokalnego regionu.</span><span class="sxs-lookup"><span data-stu-id="80730-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="80730-117">Powinny być również artykuły toothese przeglądami tooadd stanie.</span><span class="sxs-lookup"><span data-stu-id="80730-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="80730-118">Każda osoba, która tym autora hello artykułów hello powinna być stanie widoku hello wszystkie przeglądy dołączonych tooarticles z lokalnego regionu.</span><span class="sxs-lookup"><span data-stu-id="80730-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="80730-119">Zakładając, że miliony konsumentów i wydawców z miliardów artykułów, wkrótce mamy problemy hello tooconfront skali wraz z gwarantujących miejscowości dostępu.</span><span class="sxs-lookup"><span data-stu-id="80730-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="80730-120">Podobnie jak w przypadku większości problemów skalowalności, hello rozwiązanie znajduje się w skutecznej strategii partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="80730-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="80730-121">Następnie możemy przyjrzeć się jak artykuły toomodel, przejrzyj i powiadomienia jako dokumentów, skonfiguruj konta bazy danych Azure rozwiązania Cosmos oraz implementował Warstwa dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="80730-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="80730-122">Jeśli chcesz toolearn więcej informacji na temat partycjonowania i kluczy partycji, zobacz [partycjonowania i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="80730-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="80730-123"><a id="ModelingNotifications"></a>Modelowanie powiadomienia</span><span class="sxs-lookup"><span data-stu-id="80730-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="80730-124">Powiadomienia są użytkownika tooa określonego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="80730-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="80730-125">W związku z tym hello wzorce dostępu do dokumentów powiadomienia są zawsze w kontekście hello jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80730-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="80730-126">Czy na przykład "post użytkownik tooa powiadomienia" lub "Pobierz wszystkie powiadomienia dla danego użytkownika".</span><span class="sxs-lookup"><span data-stu-id="80730-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="80730-127">Witaj, optymalny wybór partycjonowania klucza dla tego typu może być `UserId`.</span><span class="sxs-lookup"><span data-stu-id="80730-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="80730-128"><a id="ModelingSubscriptions"></a>Modelowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="80730-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="80730-129">Subskrypcje mogą być tworzone dla różnych kryteriów, takich jak określonej kategorii artykułów odsetek lub określonego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="80730-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="80730-130">Dlatego hello `SubscriptionFilter` jest dobrym rozwiązaniem dla klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="80730-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <span data-ttu-id="80730-131"><a id="ModelingArticles"></a>Artykuły modelowania</span><span class="sxs-lookup"><span data-stu-id="80730-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="80730-132">Po artykułu jest identyfikowane za pomocą powiadomień, kolejne zapytania są zwykle oparte na hello `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="80730-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="80730-133">Wybieranie `Article.Id` jako partycja hello klucza w związku z tym zapewnia hello najlepsze dystrybucji do przechowywania artykułów w kolekcji usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80730-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="80730-134"><a id="ModelingReviews"></a>Przegląda modelowania</span><span class="sxs-lookup"><span data-stu-id="80730-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="80730-135">Podobne artykuły recenzje przede wszystkim są zapisywane i do odczytu w kontekście hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="80730-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="80730-136">Wybieranie `ArticleId` jako partycja klucz zapewnia najlepsze dystrybucji i wydajny dostęp przeglądów skojarzone z artykułu.</span><span class="sxs-lookup"><span data-stu-id="80730-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <span data-ttu-id="80730-137"><a id="DataAccessMethods"></a>Metody warstwy dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="80730-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="80730-138">Teraz Przyjrzyjmy się dane główne hello potrzebujemy tooimplement metody dostępu.</span><span class="sxs-lookup"><span data-stu-id="80730-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="80730-139">Oto lista hello metod, które hello `ContentPublishDatabase` musi:</span><span class="sxs-lookup"><span data-stu-id="80730-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="80730-140"><a id="Architecture"></a>Konfiguracja konta w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="80730-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="80730-141">tooguarantee lokalnego operacji odczytu i zapisu, firma Microsoft musi partycjonowania danych nie tylko na klucz partycji, ale również na podstawie wzorca dostępu geograficzne hello w regionach.</span><span class="sxs-lookup"><span data-stu-id="80730-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="80730-142">Hello model zależy od tego, mając konto bazy danych Azure DB rozwiązania Cosmos replikacją geograficzną dla każdego regionu.</span><span class="sxs-lookup"><span data-stu-id="80730-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="80730-143">Na przykład z dwóch regionach, w tym miejscu jest konfiguracji w przypadku zapisów:</span><span class="sxs-lookup"><span data-stu-id="80730-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="80730-144">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="80730-144">Account Name</span></span> | <span data-ttu-id="80730-145">Zapis regionu</span><span class="sxs-lookup"><span data-stu-id="80730-145">Write Region</span></span> | <span data-ttu-id="80730-146">Region odczytu</span><span class="sxs-lookup"><span data-stu-id="80730-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="80730-147">Witaj poniższym diagramie przedstawiono sposób odczyty i zapisy są wykonywane w typowej aplikacji z tej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="80730-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure architektura wieloma serwerami głównymi DB rozwiązania Cosmos](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="80730-149">Oto fragment kodu będący jak tooinitialize hello klientów w DAL, uruchomionych w hello `West US` regionu.</span><span class="sxs-lookup"><span data-stu-id="80730-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="80730-150">Z hello poprzedzających Instalatora Warstwa dostępu do danych hello może przekazywać wszystkie zapisy toohello lokalnego konta na podstawie których jest wdrożona.</span><span class="sxs-lookup"><span data-stu-id="80730-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="80730-151">Odczyty są wykonywane przez odczyt z obu kont tooget hello globalne widoku danych.</span><span class="sxs-lookup"><span data-stu-id="80730-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="80730-152">Ta metoda może być rozszerzony tooas w wielu regionach, zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="80730-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="80730-153">Na przykład poniżej przedstawiono ustawienia z trzech regionów geograficznych:</span><span class="sxs-lookup"><span data-stu-id="80730-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="80730-154">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="80730-154">Account Name</span></span> | <span data-ttu-id="80730-155">Zapis regionu</span><span class="sxs-lookup"><span data-stu-id="80730-155">Write Region</span></span> | <span data-ttu-id="80730-156">Region odczytu 1</span><span class="sxs-lookup"><span data-stu-id="80730-156">Read Region 1</span></span> | <span data-ttu-id="80730-157">Region odczytu 2</span><span class="sxs-lookup"><span data-stu-id="80730-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="80730-158"><a id="DataAccessImplementation"></a>Implementacja warstwy dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="80730-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="80730-159">Teraz Przyjrzyjmy się implementacja hello Warstwa dostępu do danych hello (DAL) dla aplikacji z dwóch regionach zapisywalny.</span><span class="sxs-lookup"><span data-stu-id="80730-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="80730-160">Witaj DAL musi implementować hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="80730-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="80730-161">Tworzenie wielu wystąpień `DocumentClient` dla poszczególnych kont.</span><span class="sxs-lookup"><span data-stu-id="80730-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="80730-162">Z dwóch regionach, każde wystąpienie warstwy DAL ma jeden `writeClient` i jeden `readClient`.</span><span class="sxs-lookup"><span data-stu-id="80730-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="80730-163">Oparte na region hello wdrożonych aplikacji hello, skonfiguruj punkty końcowe powitania dla `writeclient` i `readClient`.</span><span class="sxs-lookup"><span data-stu-id="80730-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="80730-164">Na przykład hello DAL wdrożone w `West US` używa `contentpubdatabase-usa.documents.azure.com` do wykonywania operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="80730-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="80730-165">Witaj DAL wdrożone w `NorthEurope` używa `contentpubdatabase-europ.documents.azure.com` dla operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="80730-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="80730-166">Z hello powyższej konfiguracji można zaimplementować metody dostępu do danych hello.</span><span class="sxs-lookup"><span data-stu-id="80730-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="80730-167">Zapis operacji przekazywania hello zapisu toohello odpowiadającego `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="80730-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="80730-168">Do odczytywania powiadomienia i recenzji, musi przeczytanie z regiony i wyniki Unii hello pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="80730-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="80730-169">W związku z tym, wybierając odpowiednim kluczem partycjonowania i partycjonowania statycznego na podstawie konta, można osiągnąć w przypadku lokalnego zapisy i odczyty przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80730-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="80730-170"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80730-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="80730-171">W tym artykule opisano możemy wykorzystania wzorce globalnie rozproszone w przypadku zapisu odczytu z bazy danych rozwiązania Cosmos Azure przy użyciu publikowania zawartości jako przykładowy scenariusz.</span><span class="sxs-lookup"><span data-stu-id="80730-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="80730-172">Dowiedz się więcej o sposobie obsługi bazy danych Azure rozwiązania Cosmos [dystrybucji globalne](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="80730-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="80730-173">Dowiedz się więcej o [automatycznej i ręcznej pracy awaryjnej w usłudze Azure DB rozwiązania Cosmos](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="80730-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="80730-174">Dowiedz się więcej o [globalne spójności z bazy danych Azure rozwiązania Cosmos](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="80730-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="80730-175">Tworzenie z wielu regionach, przy użyciu hello [DB rozwiązania Cosmos Azure - DocumentDB interfejsu API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="80730-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="80730-176">Tworzenie z wielu regionach, przy użyciu hello [Azure DB rozwiązania Cosmos - API bazy danych MongoDB](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="80730-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="80730-177">Tworzenie z wielu regionach, przy użyciu hello [Azure DB rozwiązania Cosmos - API tabeli](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="80730-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
