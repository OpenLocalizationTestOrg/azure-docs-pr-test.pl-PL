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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Wzorzec wielu globalnie zreplikowany architektury bazy danych z bazy danych Azure rozwiązania Cosmos
Azure DB rozwiązania Cosmos obsługuje gotowe [globalnej replikacji](distribute-data-globally.md), co pozwala toodistribute danych toomultiple regionach o małych opóźnieniach dostępu w dowolnym miejscu hello obciążenia. Ten model jest najczęściej używany w przypadku obciążeń wydawcy/konsumenta przypadku zapisywania w jednym regionie geograficznym i czytników globalnie rozproszone w różnych regionach (odczytu). 

Umożliwia także Azure rozwiązania Cosmos DB globalnej replikacji obsługuje toobuild aplikacji w których autorzy i czytników są globalnie rozproszone. W tym dokumencie przedstawiono wzorzec, która umożliwia uzyskanie lokalnego zapisu i lokalne dostęp do odczytu autorzy rozproszonego przy użyciu bazy danych Azure rozwiązania Cosmos.

## <a id="ExampleScenario"></a>Publikowanie — przykładowy scenariusz zawartości
Przyjrzyjmy się toodescribe scenariusza rzeczywistych wykorzystania wzorce globalnie rozproszone kilku-region/kilku-główny odczytu zapisu z bazy danych Azure rozwiązania Cosmos. Należy wziąć pod uwagę zawartości platformy publikowania oparte na usłudze Azure DB rozwiązania Cosmos. Poniżej przedstawiono niektóre wymagania, które musi spełniać ta platforma obsługi użytkowników dla konsumentów i wydawców.

* Zarówno twórcy, jak i subskrybentów są rozkładane Witaj świecie 
* Autorzy należy opublikować lokalny region (najbliższego) (Zapisz) artykuły tootheir
* Autorzy mają czytników/użytkownikom ich artykułów są rozproszone na Witaj świecie. 
* Subskrybenci należy uzyskać powiadomienie, gdy nowe artykuły są publikowane.
* Subskrybenci musi być możliwe tooread artykuły z ich lokalnego regionu. Powinny być również artykuły toothese przeglądami tooadd stanie. 
* Każda osoba, która tym autora hello artykułów hello powinna być stanie widoku hello wszystkie przeglądy dołączonych tooarticles z lokalnego regionu. 

Zakładając, że miliony konsumentów i wydawców z miliardów artykułów, wkrótce mamy problemy hello tooconfront skali wraz z gwarantujących miejscowości dostępu. Podobnie jak w przypadku większości problemów skalowalności, hello rozwiązanie znajduje się w skutecznej strategii partycjonowania. Następnie możemy przyjrzeć się jak artykuły toomodel, przejrzyj i powiadomienia jako dokumentów, skonfiguruj konta bazy danych Azure rozwiązania Cosmos oraz implementował Warstwa dostępu do danych. 

Jeśli chcesz toolearn więcej informacji na temat partycjonowania i kluczy partycji, zobacz [partycjonowania i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).

## <a id="ModelingNotifications"></a>Modelowanie powiadomienia
Powiadomienia są użytkownika tooa określonego źródła danych. W związku z tym hello wzorce dostępu do dokumentów powiadomienia są zawsze w kontekście hello jednego użytkownika. Czy na przykład "post użytkownik tooa powiadomienia" lub "Pobierz wszystkie powiadomienia dla danego użytkownika". Witaj, optymalny wybór partycjonowania klucza dla tego typu może być `UserId`.

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

## <a id="ModelingSubscriptions"></a>Modelowanie subskrypcji
Subskrypcje mogą być tworzone dla różnych kryteriów, takich jak określonej kategorii artykułów odsetek lub określonego wydawcy. Dlatego hello `SubscriptionFilter` jest dobrym rozwiązaniem dla klucza partycji.

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

## <a id="ModelingArticles"></a>Artykuły modelowania
Po artykułu jest identyfikowane za pomocą powiadomień, kolejne zapytania są zwykle oparte na hello `Article.Id`. Wybieranie `Article.Id` jako partycja hello klucza w związku z tym zapewnia hello najlepsze dystrybucji do przechowywania artykułów w kolekcji usługi Azure DB rozwiązania Cosmos. 

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

## <a id="ModelingReviews"></a>Przegląda modelowania
Podobne artykuły recenzje przede wszystkim są zapisywane i do odczytu w kontekście hello artykułu. Wybieranie `ArticleId` jako partycja klucz zapewnia najlepsze dystrybucji i wydajny dostęp przeglądów skojarzone z artykułu. 

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

## <a id="DataAccessMethods"></a>Metody warstwy dostępu do danych
Teraz Przyjrzyjmy się dane główne hello potrzebujemy tooimplement metody dostępu. Oto lista hello metod, które hello `ContentPublishDatabase` musi:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Konfiguracja konta w usłudze Azure DB rozwiązania Cosmos
tooguarantee lokalnego operacji odczytu i zapisu, firma Microsoft musi partycjonowania danych nie tylko na klucz partycji, ale również na podstawie wzorca dostępu geograficzne hello w regionach. Hello model zależy od tego, mając konto bazy danych Azure DB rozwiązania Cosmos replikacją geograficzną dla każdego regionu. Na przykład z dwóch regionach, w tym miejscu jest konfiguracji w przypadku zapisów:

| Nazwa konta | Zapis regionu | Region odczytu |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Witaj poniższym diagramie przedstawiono sposób odczyty i zapisy są wykonywane w typowej aplikacji z tej konfiguracji:

![Azure architektura wieloma serwerami głównymi DB rozwiązania Cosmos](./media/multi-region-writers/multi-master.png)

Oto fragment kodu będący jak tooinitialize hello klientów w DAL, uruchomionych w hello `West US` regionu.
    
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

Z hello poprzedzających Instalatora Warstwa dostępu do danych hello może przekazywać wszystkie zapisy toohello lokalnego konta na podstawie których jest wdrożona. Odczyty są wykonywane przez odczyt z obu kont tooget hello globalne widoku danych. Ta metoda może być rozszerzony tooas w wielu regionach, zgodnie z wymaganiami. Na przykład poniżej przedstawiono ustawienia z trzech regionów geograficznych:

| Nazwa konta | Zapis regionu | Region odczytu 1 | Region odczytu 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Implementacja warstwy dostępu do danych
Teraz Przyjrzyjmy się implementacja hello Warstwa dostępu do danych hello (DAL) dla aplikacji z dwóch regionach zapisywalny. Witaj DAL musi implementować hello następujące kroki:

* Tworzenie wielu wystąpień `DocumentClient` dla poszczególnych kont. Z dwóch regionach, każde wystąpienie warstwy DAL ma jeden `writeClient` i jeden `readClient`. 
* Oparte na region hello wdrożonych aplikacji hello, skonfiguruj punkty końcowe powitania dla `writeclient` i `readClient`. Na przykład hello DAL wdrożone w `West US` używa `contentpubdatabase-usa.documents.azure.com` do wykonywania operacji zapisu. Witaj DAL wdrożone w `NorthEurope` używa `contentpubdatabase-europ.documents.azure.com` dla operacji zapisu.

Z hello powyższej konfiguracji można zaimplementować metody dostępu do danych hello. Zapis operacji przekazywania hello zapisu toohello odpowiadającego `writeClient`.

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

Do odczytywania powiadomienia i recenzji, musi przeczytanie z regiony i wyniki Unii hello pokazane na powitania po fragment kodu:

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

W związku z tym, wybierając odpowiednim kluczem partycjonowania i partycjonowania statycznego na podstawie konta, można osiągnąć w przypadku lokalnego zapisy i odczyty przy użyciu bazy danych Azure rozwiązania Cosmos.

## <a id="NextSteps"></a>Następne kroki
W tym artykule opisano możemy wykorzystania wzorce globalnie rozproszone w przypadku zapisu odczytu z bazy danych rozwiązania Cosmos Azure przy użyciu publikowania zawartości jako przykładowy scenariusz.

* Dowiedz się więcej o sposobie obsługi bazy danych Azure rozwiązania Cosmos [dystrybucji globalne](distribute-data-globally.md)
* Dowiedz się więcej o [automatycznej i ręcznej pracy awaryjnej w usłudze Azure DB rozwiązania Cosmos](regional-failover.md)
* Dowiedz się więcej o [globalne spójności z bazy danych Azure rozwiązania Cosmos](consistency-levels.md)
* Tworzenie z wielu regionach, przy użyciu hello [DB rozwiązania Cosmos Azure - DocumentDB interfejsu API](tutorial-global-distribution-documentdb.md)
* Tworzenie z wielu regionach, przy użyciu hello [Azure DB rozwiązania Cosmos - API bazy danych MongoDB](tutorial-global-distribution-MongoDB.md)
* Tworzenie z wielu regionach, przy użyciu hello [Azure DB rozwiązania Cosmos - API tabeli](tutorial-global-distribution-table.md)
