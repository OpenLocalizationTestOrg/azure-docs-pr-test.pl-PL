---
title: "Modelowanie dokumentów danych dla bazy danych NoSQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o modelowania danych dla bazy danych NoSQL"
keywords: modelowanie danych
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="9ec0f-104">Modelowanie danych dokumentów NoSQL baz danych</span><span class="sxs-lookup"><span data-stu-id="9ec0f-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="9ec0f-105">Podczas schematu baz danych bez, takich jak Azure DB rozwiązania Cosmos, stał się bardzo łatwe obejmuje zmiany w modelu danych powinien nadal spędzonego niektórych planowania czasu dotyczące danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="9ec0f-106">Jak danych ma być przechowywany?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-106">How is data going to be stored?</span></span> <span data-ttu-id="9ec0f-107">Jak będzie aplikację do pobierania i zapytania na danych</span><span class="sxs-lookup"><span data-stu-id="9ec0f-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="9ec0f-108">Jest duże aplikacji pogrubiona odczytu lub zapisu?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="9ec0f-109">Po przeczytaniu tego artykułu, będzie mógł odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="9ec0f-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="9ec0f-110">Jak należy traktować dokumentu w bazie danych dokumentów?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="9ec0f-111">Co to jest modelowania danych i dlaczego należy zależy?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="9ec0f-112">Czym różni się modelowania danych w bazie danych dokumentów relacyjnej bazy danych?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="9ec0f-113">Jak express relacji danych w bazie danych nierelacyjnych?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="9ec0f-114">Gdy osadzanie danych i gdy połączyć z danych?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="9ec0f-115">Osadzanie danych</span><span class="sxs-lookup"><span data-stu-id="9ec0f-115">Embedding data</span></span>
<span data-ttu-id="9ec0f-116">Po uruchomieniu modelowania danych w magazynie dokumentu, takie jak bazy danych Azure rozwiązania Cosmos, spróbuj traktowanie jednostek jako **niezależne dokumenty** reprezentowane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="9ec0f-117">Przed zajrzyj mamy dostęp zbyt dużo więcej Daj nam Zabierz kilka kroków i przyjrzeć jak firma Microsoft może coś relacyjnej bazy danych, temat, który wiele osób zna już modelu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="9ec0f-118">W poniższym przykładzie pokazano, jak osoby mogą być przechowywane w relacyjnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Model relacyjnej bazy danych](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="9ec0f-120">Podczas pracy z relacyjnych baz danych, firma Microsoft już został nauczanych lat do normalizacji normalizacji, normalizacji.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="9ec0f-121">Zwykle normalizacji danych obejmuje pobranie jednostki, takie jak osoby i podzielenie go celu odrębny fragmentów danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="9ec0f-122">W powyższym przykładzie osoba może mieć wiele rekordów szczegóły kontaktu, a także wiele rekordów adresów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="9ec0f-123">Firma Microsoft nawet wykonaj krok dalej i rozbić szczegóły dotyczące kontaktu wyodrębniając dalsze typowe pola, takich jak typu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="9ec0f-124">Tego samego adresu, w tym polu każdego rekordu ma typu like *Home* lub *biznesowa*</span><span class="sxs-lookup"><span data-stu-id="9ec0f-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="9ec0f-125">Przeprowadzi lokalnych podczas normalizacji danych **nie należy przechowywać nadmiarowych danych** na każdym Rejestruj i zamiast odwoływania się do danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="9ec0f-126">W tym przykładzie można odczytać osoby, ich szczegóły dotyczące kontaktu i adresy, należy użyć SPRZĘŻEŃ skutecznie agregacji danych w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="9ec0f-127">Aktualizowanie jedna osoba ich szczegóły dotyczące kontaktu i adresy wymaga operacji zapisu w wielu poszczególnych tabel.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="9ec0f-128">Teraz Spójrzmy na jak możemy modelu tych samych danych jako autonomiczną jednostkę w bazie danych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="9ec0f-129">Powyżej podejście mamy teraz **nieznormalizowany** osoby rejestrowania gdzie możemy **osadzonych** wszystkie informacje dotyczące tej osobie, takie jak ich szczegóły dotyczące kontaktu i adresów, w jednym JSON dokument.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="9ec0f-130">Ponadto ponieważ firma Microsoft nie jest ograniczone do stałego schematu mamy może wykonywać następujące czynności mających całkowicie skontaktowania się z różnych kształtów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="9ec0f-131">Pobieranie rekordu pełną osoby z bazy danych jest teraz jeden odczytu operacji względem jednej kolekcji, a dla pojedynczego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="9ec0f-132">Aktualizacja rekordu osoby, ich szczegóły dotyczące kontaktu i adresy, jest również operacji zapisu pojedynczego dla pojedynczego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="9ec0f-133">Denormalizing danych, aplikacja może być konieczne wystawiać mniej zapytania i na zakończenie typowych operacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="9ec0f-134">Aby można było osadzić</span><span class="sxs-lookup"><span data-stu-id="9ec0f-134">When to embed</span></span>
<span data-ttu-id="9ec0f-135">Ogólnie rzecz biorąc, użyj osadzonych danych modeli, gdy:</span><span class="sxs-lookup"><span data-stu-id="9ec0f-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="9ec0f-136">Brak **zawiera** relacje między obiektami.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="9ec0f-137">Brak **jeden do kilka** relacje między obiektami.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="9ec0f-138">Brak dostępnych danych osadzonych który **zmienia się rzadko**.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="9ec0f-139">Jest osadzony danych nie będzie rosnąć **bez powiązanych z**.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="9ec0f-140">Brak osadzonych danych, która jest **integralną** z danymi w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="9ec0f-141">Zwykle nieznormalizowane danych modele umożliwiają lepsze **odczytu** wydajności.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="9ec0f-142">Kiedy nie można osadzić</span><span class="sxs-lookup"><span data-stu-id="9ec0f-142">When not to embed</span></span>
<span data-ttu-id="9ec0f-143">Chociaż zasadą w bazie danych dokumentów do denormalize wszystko i osadzone wszystkie dane do pojedynczego dokumentu, może to prowadzić do niektórych sytuacjach, w których należy unikać.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="9ec0f-144">Zająć ta Wstawka kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="9ec0f-145">Może to być co podmiot post z komentarzami osadzone będzie wyglądała jeśli zostały możemy modelowania typowe blogu lub CMS, system.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="9ec0f-146">Problem z tym przykładzie jest to tablica komentarze **niepowiązany**, co oznacza, że nie ma żadnego limitu (praktyczne), liczba komentarze może mieć żadnych pojedynczego post.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="9ec0f-147">Problem będzie wzrostem rozmiaru dokumentu może znacznie.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="9ec0f-148">Ucierpi w miarę zwiększania się możliwość przesyłania danych za pośrednictwem danych przesyłanych w sieci, a także odczytywanie i aktualizowanie dokumentu, na dużą skalę, rozmiar dokumentu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="9ec0f-149">W takim przypadku byłoby lepiej wziąć pod uwagę następujące modelu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="9ec0f-150">Ten model ma trzy najnowsze komentarze osadzone w post, który jest tablicą o stałym powiązany teraz.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="9ec0f-151">Inne komentarze są grupowane w partiach 100 komentarze i przechowywane w oddzielnych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="9ec0f-152">Rozmiar partii została wybrana jako 100, ponieważ fikcyjne aplikacji zezwala użytkownikowi na załadować 100 komentarze naraz.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="9ec0f-153">Innym przypadku, gdy osadzanie danych nie jest dobrym rozwiązaniem jest, gdy dane osadzone jest często używane w różnych dokumentach i będzie często zmieniana.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="9ec0f-154">Zająć ta Wstawka kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="9ec0f-155">To może reprezentować portfolio standardowych osoby.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="9ec0f-156">Wybraliśmy osadzanie standardowych informacji w do każdego dokumentu portfolio.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="9ec0f-157">W środowisku, gdzie dane dotyczące zmienia się często takich jak giełdowych handlowymi aplikacji, osadzanie danych, które zmieniają się często będzie oznaczać, że stale aktualizowany każdy dokument portfolio za każdym razem, gdy jest przedmiotem handlu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="9ec0f-158">Stock *zaza* mogą być przedmiotem handlu setki wiele razy w jednym dniu i tysięcy użytkowników może mieć *zaza* na ich portfolio.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="9ec0f-159">Z modelem danych, takich jak powyżej czy konieczne jest uaktualnienie wielu tysięcy dokumentów portfolio wielokrotnie codziennie, co może prowadzić do systemu który nie będzie bardzo dobrego skalowania.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="9ec0f-160"><a id="Refer"></a>Odwołanie do danych</span><span class="sxs-lookup"><span data-stu-id="9ec0f-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="9ec0f-161">Tak osadzanie danych działa dobrze w wielu przypadkach, ale jest jasne, czy istnieją scenariusze, gdy problemy więcej niż warto denormalizing danych spowoduje przerwanie.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="9ec0f-162">Dlatego co możemy zrobić teraz?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-162">So what do we do now?</span></span> 

<span data-ttu-id="9ec0f-163">Relacyjnych baz danych nie są jedynym miejscem, w którym można utworzyć relacji między obiektami.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="9ec0f-164">W bazie danych dokumentu może mieć informacji w jednym dokumencie, który faktycznie odnosi się do danych w innych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="9ec0f-165">Teraz I am nie postulować przez jedną minutę, nawet budujemy systemów, które mogłyby być lepiej dostosowane do relacyjnej bazy danych w usłudze Azure DB rozwiązania Cosmos lub wszelkie inne bazy danych dokumentów, że relacje proste jest uszkodzona i może być bardzo przydatne.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="9ec0f-166">W poniższych JSON wybraliśmy do użycia w przykładzie standardowych portfolio z wcześniej, ale tym razem możemy odnosi się do standardowych elementów na wchodzących w skład zestawu zamiast osadzania.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="9ec0f-167">W ten sposób element standardowych zmienia się często w ciągu dnia tylko dokument, który musi zostać zaktualizowany jest pojedynczego dokumentu standardowych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="9ec0f-168">Wadą tego podejścia natychmiastowego interfejsu jest jednak, jeśli aplikacja jest wymagane, aby wyświetlić informacje o każdej akcji przechowywana podczas wyświetlania portfolio osoby; w takim przypadku należy wprowadzić wiele rund do bazy danych można załadować danych dla każdego dokumentu standardowych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="9ec0f-169">W tym miejscu wprowadziliśmy decyzji, aby zwiększyć wydajność operacji zapisu, które się zdarzyć, często w ciągu dnia, ale z kolei naruszenia zabezpieczeń na operacje odczytu, potencjalnie mające mniej wpływ na wydajność tej konkretnej systemu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="9ec0f-170">Znormalizowany modeli danych **może wymagać więcej rund** do serwera.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="9ec0f-171">Jakie klucze obce?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-171">What about foreign keys?</span></span>
<span data-ttu-id="9ec0f-172">Ponieważ nie ma żadnych koncepcji ograniczenia, klucz obcy lub w inny sposób relacje między dokumentów zawierających w dokumentach skutecznej "powiązania" i nie są weryfikowane przez sama baza danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="9ec0f-173">Jeśli chcesz upewnij się, że dane, które dokument odwołuje się do faktycznie istnieje, należy to zrobić w aplikacji lub przy użyciu wyzwalaczy po stronie serwera lub procedur składowanych dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="9ec0f-174">Kiedy do odwołania</span><span class="sxs-lookup"><span data-stu-id="9ec0f-174">When to reference</span></span>
<span data-ttu-id="9ec0f-175">Ogólnie rzecz biorąc, użyj danych znormalizowane modele, gdy:</span><span class="sxs-lookup"><span data-stu-id="9ec0f-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="9ec0f-176">Reprezentujący **jeden do wielu** relacji.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="9ec0f-177">Reprezentujący **wiele do wielu** relacji.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="9ec0f-178">Dane dotyczące **zmienia się często**.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="9ec0f-179">Może być danych występujące w odwołaniu **niepowiązany**.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="9ec0f-180">Zwykle normalizacji zapewnia lepsze **zapisu** wydajności.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="9ec0f-181">Gdzie umieścić relacji?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-181">Where do I put the relationship?</span></span>
<span data-ttu-id="9ec0f-182">Rozwój relacji pomoże określić, w których dokumentu do przechowywania odwołanie.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="9ec0f-183">Jeśli przyjrzymy się poniżej JSON modelujący wydawcy i książek.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="9ec0f-184">W przypadku małych wzrost ograniczona liczba książek na wydawcy mogą być przydatne następnie przechowywanie odwołanie książki w dokumencie wydawcy.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="9ec0f-185">Jednak w przypadku niepowiązanego liczba książek na wydawcy tego modelu danych może spowodować modyfikowalna, rosnącym tablic, tak jak na przykład dokument wydawcy powyżej.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="9ec0f-186">Przełączanie rzeczy wokół bit spowoduje modelu, który nadal reprezentuje tych samych danych, ale teraz pozwala uniknąć dużych kolekcjach modyfikowalne.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="9ec0f-187">W powyższym przykładzie mamy porzucona niepowiązany kolekcji w dokumencie wydawcy.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="9ec0f-188">Zamiast tego po prostu mamy odwołanie do wydawcy na każdy dokument książki.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="9ec0f-189">Jak model relacje wiele: wiele?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="9ec0f-190">Relacyjnej bazy danych *wiele: wiele* relacje są często modelowane sprzężenie tabel, które właśnie ze sobą połączone rekordy z innych tabel.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Dołącz do tabel](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="9ec0f-192">Może się wydawać do replikowania samo używanie dokumentów oraz tworzenia modelu danych, która wygląda podobnie do następującego.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="9ec0f-193">Czy to pomoże.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-193">This would work.</span></span> <span data-ttu-id="9ec0f-194">Jednak podczas ładowania albo autor z ich książki lub ładowania książkę z jego autorem zawsze wymagają co najmniej dwóch dodatkowych zapytań w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="9ec0f-195">Jedno zapytanie do łącząca dokumentu, a następnie inne zapytanie, aby pobrać rzeczywiste dokumentu jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="9ec0f-196">Jeśli jest wszystkich zadań w tej tabeli sprzężenia przyklejanie ze sobą dwie części danych, dlaczego nie upuszczenie go całkowicie?</span><span class="sxs-lookup"><span data-stu-id="9ec0f-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="9ec0f-197">Rozważ następujące opcje.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="9ec0f-198">Teraz gdyby Autor, niezwłocznie sprawdzić książki zostały one zapisane i odwrotnie gdyby załadować dokument książki I wiedział, identyfikatory autora lub autorów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="9ec0f-199">Spowoduje to zapisanie tej pośredniczące zapytanie sprzężenia zmniejszenie tabeli numer serwera przekazywanych aplikacja ma być.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="9ec0f-200"><a id="WrapUp"></a>Modele hybrydowe danych</span><span class="sxs-lookup"><span data-stu-id="9ec0f-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="9ec0f-201">Teraz analizujemy zostały osadzanie (lub denormalizing) i danych odwołującego się (lub normalizacji), o ich upsides, a każdy mieć dokonywania jako zaobserwowano.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="9ec0f-202">Nie zawsze musi być lub nie można Przerażony do nieco pomylone rzeczy.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="9ec0f-203">Na podstawie wzorców użycia określonych aplikacji i obciążeń, które może się zdarzyć, gdy mieszanie osadzonych i danych występujące w odwołaniu ma sens, i może prowadzić do prostsze logiki aplikacji z serwerem mniej przekazywanych zachowując dobrej poziomu wydajności.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="9ec0f-204">Należy wziąć pod uwagę następujące JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-204">Consider the following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="9ec0f-205">W tym miejscu zostały (przeważnie) była osadzonego modelu, gdy dane z innych jednostek są osadzone w dokumencie najwyższego poziomu, ale odwołuje się do innych danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="9ec0f-206">W dokumencie Podręcznik, firma Microsoft może zobaczyć kilka interesujące pola, jeśli przyjrzymy się tablicy autorów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="9ec0f-207">Brak *identyfikator* pola, które jest polem używamy odwołują się do dokumentu autora standardową praktyką w modelu znormalizowane, ale następnie mamy także *nazwa* i *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="9ec0f-208">Firma Microsoft może po prostu wciąż z *identyfikator* i aplikacji w celu uzyskania ono potrzebne informacje dodatkowe z odpowiednich autora dokumentu za pomocą "link", ale ponieważ naszej aplikacji jest wyświetlana nazwa autora i obraz z każdym książką wyświetlane można zapisać podróż serwer na książki na liście przez denormalizing **niektórych** danych od autora.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="9ec0f-209">Na pewno zmienić imię i nazwisko autora lub chcieli zaktualizować ich fotografii, firma Microsoft będzie musiał przejść aktualizacji co książki one kiedykolwiek opublikowany, ale dla aplikacji, na podstawie założenia, że autorów nie zmieniaj nazwy bardzo często jest to dopuszczalne decyzję.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="9ec0f-210">W tym przykładzie są **wstępnie obliczone wartości zagregowanych** wartości do zapisania kosztowne przetwarzania na operację odczytu.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="9ec0f-211">W tym przykładzie dane osadzony w dokumencie autora jest dane, które jest obliczane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="9ec0f-212">Nowej książki zostanie opublikowana, tworzony jest dokument książki **i** pola countOfBooks ma ustawioną wartość obliczana na podstawie liczby dokumentów książki, które istnieją dla konkretnego autora.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="9ec0f-213">Tego rodzaju optymalizacji byłoby dobrej w systemach duże odczytu gdzie możemy akceptowalny wykonać obliczenia na zapisy w celu zoptymalizowania odczytów.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="9ec0f-214">Możliwość modelu z pól obliczeniowych wstępnie jest możliwe ponieważ obsługuje bazy danych Azure rozwiązania Cosmos **transakcji wielu dokumentów**.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="9ec0f-215">Wiele magazynów NoSQL nie nie transakcji w dokumentach i w związku z tym wspierają decyzje dotyczące projektu, takie jak "zawsze osadzić wszystko", z powodu tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="9ec0f-216">Z bazy danych rozwiązania Cosmos platformy Azure można użyć wyzwalacze po stronie serwera lub procedur składowanych, które Wstaw książki i zaktualizuj autorów wszystko w ramach transakcji ACID.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="9ec0f-217">Teraz nie zostanie **ma** do osadzenia wszystkie elementy z jednym dokumentem tak, aby mieć pewność, spójność danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="9ec0f-218"><a name="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ec0f-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="9ec0f-219">Największych takeaways z tego artykułu jest zrozumienie, że modelowania w świecie bez schematu danych jest równie ważne co kiedykolwiek.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="9ec0f-220">Podobnie jak nie istnieje jeden sposób reprezentujący element danych na ekranie, nie istnieje jeden sposób do modelu danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="9ec0f-221">Możesz muszą zrozumieć i aplikacji, jak powoduje wygenerowanie, korzystać z, a przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="9ec0f-222">Następnie przez zastosowanie niektórych wytycznych przedstawionych w tym miejscu można ustawić o tworzeniu modelu, który dotyczy natychmiastowego wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="9ec0f-223">Jeśli aplikacje potrzebne zmiany, można wykorzystać elastyczność bez schematu bazy danych obejmuje zmiany i łatwo rozwijać modelu danych.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="9ec0f-224">Aby dowiedzieć się więcej o usłudze Azure DB rozwiązania Cosmos, należy zapoznać się z usługi [dokumentacji](https://azure.microsoft.com/documentation/services/cosmos-db/) strony.</span><span class="sxs-lookup"><span data-stu-id="9ec0f-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="9ec0f-225">Aby zrozumieć, jak do niezależnego fragmentu danych między wieloma partycjami się [partycjonowanie danych w usłudze Azure DB rozwiązania Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="9ec0f-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
