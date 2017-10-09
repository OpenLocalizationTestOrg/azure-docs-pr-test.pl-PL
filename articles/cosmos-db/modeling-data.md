---
title: dane dokumentu aaaModeling dla bazy danych NoSQL | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="99c99-104">Modelowanie danych dokumentów NoSQL baz danych</span><span class="sxs-lookup"><span data-stu-id="99c99-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="99c99-105">Gdy schematu baz danych bez, takich jak Azure DB rozwiązania Cosmos, ułatwiają super tooembrace zmiany tooyour danych modelu, należy nadal poświęcony niektóre razem analiza danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="99c99-106">Jak danych będzie przechowywane toobe?</span><span class="sxs-lookup"><span data-stu-id="99c99-106">How is data going toobe stored?</span></span> <span data-ttu-id="99c99-107">W jaki sposób będzie tooretrieve i zapytań dane aplikacji?</span><span class="sxs-lookup"><span data-stu-id="99c99-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="99c99-108">Jest duże aplikacji pogrubiona odczytu lub zapisu?</span><span class="sxs-lookup"><span data-stu-id="99c99-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="99c99-109">Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="99c99-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="99c99-110">Jak należy traktować dokumentu w bazie danych dokumentów?</span><span class="sxs-lookup"><span data-stu-id="99c99-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="99c99-111">Co to jest modelowania danych i dlaczego należy zależy?</span><span class="sxs-lookup"><span data-stu-id="99c99-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="99c99-112">W jaki sposób modelowania danych dokumentów bazy danych różnych tooa relacyjnej bazy danych?</span><span class="sxs-lookup"><span data-stu-id="99c99-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="99c99-113">Jak express relacji danych w bazie danych nierelacyjnych?</span><span class="sxs-lookup"><span data-stu-id="99c99-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="99c99-114">Gdy osadzanie danych i gdy łącze toodata?</span><span class="sxs-lookup"><span data-stu-id="99c99-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="99c99-115">Osadzanie danych</span><span class="sxs-lookup"><span data-stu-id="99c99-115">Embedding data</span></span>
<span data-ttu-id="99c99-116">Po uruchomieniu modelowania danych w magazynie dokumentu, takie jak bazy danych Azure rozwiązania Cosmos, spróbuj tootreat jednostki jako **niezależne dokumenty** reprezentowane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="99c99-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="99c99-117">Przed zajrzyj mamy dostęp zbyt dużo więcej Daj nam Zabierz kilka kroków i przyjrzeć jak firma Microsoft może coś relacyjnej bazy danych, temat, który wiele osób zna już modelu.</span><span class="sxs-lookup"><span data-stu-id="99c99-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="99c99-118">Witaj poniższy przykład przedstawia sposób osoby mogą być przechowywane w relacyjnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Model relacyjnej bazy danych](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="99c99-120">Podczas pracy z relacyjnych baz danych, został możemy nauczanych dla toonormalize lat normalizacji, normalizacji.</span><span class="sxs-lookup"><span data-stu-id="99c99-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="99c99-121">Zwykle normalizacji danych obejmuje pobranie jednostki, takie jak osoby i podzielenie go w toodiscrete fragmentów danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="99c99-122">W powyższym przykładzie hello osoba może mieć wiele rekordów szczegóły kontaktu, a także wiele rekordów adresów.</span><span class="sxs-lookup"><span data-stu-id="99c99-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="99c99-123">Firma Microsoft nawet wykonaj krok dalej i rozbić szczegóły dotyczące kontaktu wyodrębniając dalsze typowe pola, takich jak typu.</span><span class="sxs-lookup"><span data-stu-id="99c99-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="99c99-124">Tego samego adresu, w tym polu każdego rekordu ma typu like *Home* lub *biznesowa*</span><span class="sxs-lookup"><span data-stu-id="99c99-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="99c99-125">Witaj przeprowadzi lokalnych podczas normalizacji danych jest zbyt**nie należy przechowywać nadmiarowych danych** na wszystkich rekordów, a raczej odwoływać się toodata.</span><span class="sxs-lookup"><span data-stu-id="99c99-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="99c99-126">W tym przykładzie tooread osoby, ich szczegóły dotyczące kontaktu i adresy, należy toouse sprzężenia tooeffectively agregacji danych w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="99c99-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="99c99-127">Aktualizowanie jedna osoba ich szczegóły dotyczące kontaktu i adresy wymaga operacji zapisu w wielu poszczególnych tabel.</span><span class="sxs-lookup"><span data-stu-id="99c99-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="99c99-128">Teraz załóżmy podjęcia przyjrzeć się jak firma Microsoft będzie modelu hello takie same dane jako autonomiczną jednostkę w bazie danych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c99-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="99c99-129">Podejście hello powyżej mamy teraz **nieznormalizowany** hello rekord osoby gdzie możemy **osadzone** hello wszystkie informacje dotyczące osoby toothis, takie jak ich szczegóły dotyczące kontaktu i adresy w jednym tooa Dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="99c99-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="99c99-130">Ponadto ponieważ firma Microsoft nie jest ograniczone tooa ustalić schemat, który mamy hello elastyczność toodo np. konieczności skontaktowania się z różnych kształtów całkowicie.</span><span class="sxs-lookup"><span data-stu-id="99c99-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="99c99-131">Pobieranie rekordu pełną osoby z bazy danych hello jest teraz jeden odczytu operacji względem jednej kolekcji, a dla pojedynczego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c99-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="99c99-132">Aktualizacja rekordu osoby, ich szczegóły dotyczące kontaktu i adresy, jest również operacji zapisu pojedynczego dla pojedynczego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c99-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="99c99-133">Przez denormalizing danych, aplikacja może być konieczne tooissue mniejszej liczby zapytań i aktualizacje toocomplete typowych operacji.</span><span class="sxs-lookup"><span data-stu-id="99c99-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="99c99-134">Gdy tooembed</span><span class="sxs-lookup"><span data-stu-id="99c99-134">When tooembed</span></span>
<span data-ttu-id="99c99-135">Ogólnie rzecz biorąc, użyj osadzonych danych modeli, gdy:</span><span class="sxs-lookup"><span data-stu-id="99c99-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="99c99-136">Brak **zawiera** relacje między obiektami.</span><span class="sxs-lookup"><span data-stu-id="99c99-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="99c99-137">Brak **jeden do kilka** relacje między obiektami.</span><span class="sxs-lookup"><span data-stu-id="99c99-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="99c99-138">Brak dostępnych danych osadzonych który **zmienia się rzadko**.</span><span class="sxs-lookup"><span data-stu-id="99c99-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="99c99-139">Jest osadzony danych nie będzie rosnąć **bez powiązanych z**.</span><span class="sxs-lookup"><span data-stu-id="99c99-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="99c99-140">Brak osadzonych danych, która jest **integralną** toodata w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="99c99-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="99c99-141">Zwykle nieznormalizowane danych modele umożliwiają lepsze **odczytu** wydajności.</span><span class="sxs-lookup"><span data-stu-id="99c99-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="99c99-142">Jeśli nie tooembed</span><span class="sxs-lookup"><span data-stu-id="99c99-142">When not tooembed</span></span>
<span data-ttu-id="99c99-143">Witaj zasadą w bazie danych dokumentów wszystko, co jest toodenormalize i osadzone wszystkie dane w jednym dokumencie tooa, może to spowodować toosome sytuacji, w których należy unikać.</span><span class="sxs-lookup"><span data-stu-id="99c99-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="99c99-144">Zająć ta Wstawka kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="99c99-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="99c99-145">Może to być co podmiot post z komentarzami osadzone będzie wyglądała jeśli zostały możemy modelowania typowe blogu lub CMS, system.</span><span class="sxs-lookup"><span data-stu-id="99c99-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="99c99-146">Witaj problem z tym przykładem jest tym hello komentarze tablica jest **niepowiązany**, co oznacza, że są limit (praktyczne) nie toohello liczbę komentarzy może mieć żadnych pojedynczego post.</span><span class="sxs-lookup"><span data-stu-id="99c99-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="99c99-147">Problem będzie wzrostem rozmiaru hello hello dokumentu może znacznie.</span><span class="sxs-lookup"><span data-stu-id="99c99-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="99c99-148">Jako rozmiar hello hello dokumentu rozwoju hello możliwości tootransmit hello danych za pośrednictwem hello danych przesyłanych w sieci, a także odczytywania i aktualizowania dokumentu hello na dużą skalę, będzie to mieć wpływ na.</span><span class="sxs-lookup"><span data-stu-id="99c99-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="99c99-149">W takim przypadku byłoby lepsze hello tooconsider po modelu.</span><span class="sxs-lookup"><span data-stu-id="99c99-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
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

<span data-ttu-id="99c99-150">Ten model ma hello trzech najnowszych komentarzy osadzonych na powitania post siebie, który jest tablicą o stałej powiązane z tym czas.</span><span class="sxs-lookup"><span data-stu-id="99c99-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="99c99-151">Witaj komentarze są zgrupowane w toobatches 100 komentarze i przechowywane w oddzielnych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="99c99-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="99c99-152">Hello rozmiar wsadu hello została wybrana jako 100, ponieważ fikcyjne aplikacji umożliwia hello komentarze 100 tooload użytkownika w czasie.</span><span class="sxs-lookup"><span data-stu-id="99c99-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="99c99-153">Innym przypadku, gdy osadzanie danych nie jest dobrym rozwiązaniem jest hello osadzone w danych jest często używane w różnych dokumentach i będzie często zmieniana.</span><span class="sxs-lookup"><span data-stu-id="99c99-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="99c99-154">Zająć ta Wstawka kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="99c99-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="99c99-155">To może reprezentować portfolio standardowych osoby.</span><span class="sxs-lookup"><span data-stu-id="99c99-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="99c99-156">Wybraliśmy tooembed hello standardowych informacji w dokumencie portfolio tooeach.</span><span class="sxs-lookup"><span data-stu-id="99c99-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="99c99-157">W środowisku, w którym dane dotyczące zmienia się często, takich jak zasobu handlowymi aplikacji osadzanie danych, które zmieniają się często będzie toomean, czy są stale aktualizowane każdy dokument portfolio za każdym razem, gdy jest przedmiotem handlu zasobu.</span><span class="sxs-lookup"><span data-stu-id="99c99-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="99c99-158">Stock *zaza* mogą być przedmiotem handlu setki wiele razy w jednym dniu i tysięcy użytkowników może mieć *zaza* na ich portfolio.</span><span class="sxs-lookup"><span data-stu-id="99c99-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="99c99-159">Z modelem danych, takich jak hello powyżej czy mamy tooupdate wielu tysięcy dokumentów portfolio wiele razy każdego dnia wiodące tooa system, który nie jest bardzo dobrego skalowania.</span><span class="sxs-lookup"><span data-stu-id="99c99-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="99c99-160"><a id="Refer"></a>Odwołanie do danych</span><span class="sxs-lookup"><span data-stu-id="99c99-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="99c99-161">Tak osadzanie danych działa dobrze w wielu przypadkach, ale jest jasne, czy istnieją scenariusze, gdy problemy więcej niż warto denormalizing danych spowoduje przerwanie.</span><span class="sxs-lookup"><span data-stu-id="99c99-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="99c99-162">Dlatego co możemy zrobić teraz?</span><span class="sxs-lookup"><span data-stu-id="99c99-162">So what do we do now?</span></span> 

<span data-ttu-id="99c99-163">Relacyjnych baz danych nie są hello jedynym miejscem, w którym można utworzyć relacji między obiektami.</span><span class="sxs-lookup"><span data-stu-id="99c99-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="99c99-164">W bazie danych dokumentu może mieć informacji w jednym dokumencie, który faktycznie odnosi się toodata w innych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="99c99-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="99c99-165">Teraz I am nie postulować przez jedną minutę, nawet budujemy systemów, które jest lepiej dostosowane tooa relacyjnej bazy danych w usłudze Azure DB rozwiązania Cosmos lub wszelkie inne bazy danych dokumentów, że relacje proste jest uszkodzona i może być bardzo przydatne.</span><span class="sxs-lookup"><span data-stu-id="99c99-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="99c99-166">Przykład Witaj toouse standardowych portfolio z wcześniej, ale teraz określane toohello standardowych elementów na powitania portfolio zamiast osadzania Wybraliśmy w hello JSON poniżej.</span><span class="sxs-lookup"><span data-stu-id="99c99-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="99c99-167">W ten sposób element standardowych hello często zmienia się w całym hello dzień hello tylko dokument, który musi zaktualizować toobe po hello pojedynczego dokumentu standardowych.</span><span class="sxs-lookup"><span data-stu-id="99c99-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

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


<span data-ttu-id="99c99-168">Podejście toothis natychmiastowego wadą interfejsu jest jednak, jeśli aplikacja jest wymagana tooshow informacje o każdej akcji przechowywana podczas wyświetlania portfolio osoby; w takim przypadku trzeba toomake wiele rund toohello tooload hello informacje z bazy danych dla każdego dokumentu standardowych.</span><span class="sxs-lookup"><span data-stu-id="99c99-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="99c99-169">W tym miejscu wprowadziliśmy decyzji tooimprove hello wydajności operacji zapisu, które się zdarzyć, często w ciągu dnia hello, ale z kolei naruszenia zabezpieczeń na powitania operacje, które potencjalnie mają mniej wpływ na wydajność hello tego konkretnego systemu odczytu.</span><span class="sxs-lookup"><span data-stu-id="99c99-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="99c99-170">Znormalizowany modeli danych **może wymagać więcej rund** toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="99c99-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="99c99-171">Jakie klucze obce?</span><span class="sxs-lookup"><span data-stu-id="99c99-171">What about foreign keys?</span></span>
<span data-ttu-id="99c99-172">Ponieważ nie ma żadnych koncepcji ograniczenia, klucz obcy lub w inny sposób relacje między dokumentów zawierających w dokumentach skutecznej "powiązania" i nie są weryfikowane przez hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="99c99-173">Jeśli chcesz, aby tooensure, który hello dane, które odwołuje się dokument tooactually istnieje, a następnie toodo to konieczne w aplikacji lub przy użyciu hello wyzwalacze po stronie serwera lub procedur składowanych dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="99c99-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="99c99-174">Gdy tooreference</span><span class="sxs-lookup"><span data-stu-id="99c99-174">When tooreference</span></span>
<span data-ttu-id="99c99-175">Ogólnie rzecz biorąc, użyj danych znormalizowane modele, gdy:</span><span class="sxs-lookup"><span data-stu-id="99c99-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="99c99-176">Reprezentujący **jeden do wielu** relacji.</span><span class="sxs-lookup"><span data-stu-id="99c99-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="99c99-177">Reprezentujący **wiele do wielu** relacji.</span><span class="sxs-lookup"><span data-stu-id="99c99-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="99c99-178">Dane dotyczące **zmienia się często**.</span><span class="sxs-lookup"><span data-stu-id="99c99-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="99c99-179">Może być danych występujące w odwołaniu **niepowiązany**.</span><span class="sxs-lookup"><span data-stu-id="99c99-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="99c99-180">Zwykle normalizacji zapewnia lepsze **zapisu** wydajności.</span><span class="sxs-lookup"><span data-stu-id="99c99-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="99c99-181">Gdzie umieścić relacji hello?</span><span class="sxs-lookup"><span data-stu-id="99c99-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="99c99-182">rozwój Hello relacji hello pomoże określić, w których odwołanie hello toostore dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c99-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="99c99-183">Jeśli przyjrzymy się hello JSON poniżej modelujący wydawcy i książek.</span><span class="sxs-lookup"><span data-stu-id="99c99-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="99c99-184">Jeśli numer hello książek hello na wydawcy jest mały wzrost ograniczone, następnie przechowywanie hello książki odwołania w dokumencie wydawcy hello mogą być użyteczne.</span><span class="sxs-lookup"><span data-stu-id="99c99-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="99c99-185">Jednak w przypadku niepowiązanego numer hello książek na wydawcy, ten model danych doprowadziłoby toomutable rośnie tablic, tak jak dokument wydawcy przykład hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="99c99-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="99c99-186">Przełączanie rzeczy wokół bit czy wynik w modelu nadal reprezentuje ale teraz hello tych samych danych pozwala uniknąć dużych kolekcjach modyfikowalne.</span><span class="sxs-lookup"><span data-stu-id="99c99-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="99c99-187">W hello powyżej przykładzie, możemy porzucona hello niepowiązany kolekcji na powitania wydawcy dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c99-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="99c99-188">Zamiast tego po prostu mamy odwołanie wydawcy toohello na każdy dokument książki.</span><span class="sxs-lookup"><span data-stu-id="99c99-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="99c99-189">Jak model relacje wiele: wiele?</span><span class="sxs-lookup"><span data-stu-id="99c99-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="99c99-190">Relacyjnej bazy danych *wiele: wiele* relacje są często modelowane sprzężenie tabel, które właśnie ze sobą połączone rekordy z innych tabel.</span><span class="sxs-lookup"><span data-stu-id="99c99-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Dołącz do tabel](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="99c99-192">Może się wydawać tooreplicate hello przy użyciu tego samego operacją dokumenty i utworzyć model danych, która wygląda podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="99c99-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="99c99-193">Czy to pomoże.</span><span class="sxs-lookup"><span data-stu-id="99c99-193">This would work.</span></span> <span data-ttu-id="99c99-194">Jednak podczas ładowania albo autor z ich książki lub ładowania książkę z jego autorem zawsze wymagają co najmniej dwóch dodatkowych zapytań w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="99c99-195">Sprzęganie dokumentu i następnie innego zapytania toofetch hello rzeczywiste dokumentu jest dołączony toohello jednego zapytania.</span><span class="sxs-lookup"><span data-stu-id="99c99-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="99c99-196">Jeśli jest wszystkich zadań w tej tabeli sprzężenia przyklejanie ze sobą dwie części danych, dlaczego nie upuszczenie go całkowicie?</span><span class="sxs-lookup"><span data-stu-id="99c99-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="99c99-197">Należy wziąć pod uwagę następujące hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="99c99-198">Teraz gdyby Autor, niezwłocznie sprawdzić książki zostały one zapisane i odwrotnie gdyby załadować dokument książki czy wiem hello identyfikatory hello autora lub autorów.</span><span class="sxs-lookup"><span data-stu-id="99c99-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="99c99-199">Spowoduje to zapisanie tej pośredniczące zapytania dotyczącego tabeli sprzężenia hello zmniejszeniu liczby powitania serwera rund aplikacji ma toomake.</span><span class="sxs-lookup"><span data-stu-id="99c99-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="99c99-200"><a id="WrapUp"></a>Modele hybrydowe danych</span><span class="sxs-lookup"><span data-stu-id="99c99-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="99c99-201">Teraz analizujemy zostały osadzanie (lub denormalizing) i danych odwołującego się (lub normalizacji), o ich upsides, a każdy mieć dokonywania jako zaobserwowano.</span><span class="sxs-lookup"><span data-stu-id="99c99-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="99c99-202">Go nie zawsze są toobe albo lub, nie można rzeczy Przerażony toomix się nieco.</span><span class="sxs-lookup"><span data-stu-id="99c99-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="99c99-203">Na podstawie wzorców użycia określonych aplikacji i obciążeń, które może się zdarzyć, gdy mieszanie osadzonych danych występujące w odwołaniu ma sens i może logiki aplikacji toosimpler potencjalnego klienta z serwerem mniej przekazywanych zachowując dobrej poziomu wydajności .</span><span class="sxs-lookup"><span data-stu-id="99c99-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="99c99-204">Należy wziąć pod uwagę hello następującego formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="99c99-204">Consider hello following JSON.</span></span> 

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

<span data-ttu-id="99c99-205">W tym miejscu zostały (przeważnie) była hello osadzonego modelu, gdy dane z innych jednostek jest osadzony w dokumencie najwyższego poziomu hello, ale odwołuje się do innych danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="99c99-206">W dokumencie Podręcznik hello, firma Microsoft może zobaczyć kilka interesujące pola, jeśli przyjrzymy się tablicy hello autorów.</span><span class="sxs-lookup"><span data-stu-id="99c99-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="99c99-207">Brak *identyfikator* ma pola, które jest polem hello korzystamy również toorefer tooan wstecz autora dokumentu, standardową praktyką w znormalizowane modelu, ale następnie *nazwa* i *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="99c99-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="99c99-208">Firma Microsoft może po prostu wciąż z *identyfikator* i lewego tooget aplikacji hello jest potrzebne informacje dodatkowe z hello odpowiednich autora dokumentu za pomocą "link" hello, ale ponieważ naszej aplikacji Wyświetla nazwę autora hello i a Obraz miniatury z każdej książki wyświetlane można zapisać na książki serwera toohello obiegu na liście przez denormalizing **niektórych** danych z hello autora.</span><span class="sxs-lookup"><span data-stu-id="99c99-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="99c99-209">Na pewno zmienić imię i nazwisko autora hello lub chcieli tooupdate swoich zdjęć trzeba toogo aktualizacji co książki one kiedykolwiek opublikowany, ale dla aplikacji, oparte na założeniu hello czy autorów nie bardzo często, zmień ich nazwy to dopuszczalne projektu decyzji.</span><span class="sxs-lookup"><span data-stu-id="99c99-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="99c99-210">W przykładzie hello są **wstępnie obliczone wartości zagregowanych** wartości toosave kosztowne przetwarzania na operację odczytu.</span><span class="sxs-lookup"><span data-stu-id="99c99-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="99c99-211">W przykładzie hello dane hello osadzony w dokumencie autora hello jest dane, które jest obliczane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="99c99-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="99c99-212">Nowej książki zostanie opublikowana, tworzony jest dokument książki **i** hello countOfBooks pole jest ustawione na wartość tooa obliczana na podstawie liczby hello książki dokumentów, które istnieją dla konkretnego autora.</span><span class="sxs-lookup"><span data-stu-id="99c99-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="99c99-213">Tego rodzaju optymalizacji byłoby dobrej w systemach duże odczytu gdzie możemy sobie toodo obliczenia na zapisy w kolejności toooptimize odczytów.</span><span class="sxs-lookup"><span data-stu-id="99c99-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="99c99-214">Witaj toohave możliwości modelu z pól obliczeniowych wstępnie jest możliwe ponieważ obsługuje bazy danych Azure rozwiązania Cosmos **transakcji wielu dokumentów**.</span><span class="sxs-lookup"><span data-stu-id="99c99-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="99c99-215">Wiele magazynów NoSQL nie nie transakcji w dokumentach i w związku z tym wspierają decyzje dotyczące projektu, takie jak "zawsze osadzić wszystko", ze względu na ograniczenia toothis.</span><span class="sxs-lookup"><span data-stu-id="99c99-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="99c99-216">Z bazy danych rozwiązania Cosmos platformy Azure można użyć wyzwalacze po stronie serwera lub procedur składowanych, które Wstaw książki i zaktualizuj autorów wszystko w ramach transakcji ACID.</span><span class="sxs-lookup"><span data-stu-id="99c99-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="99c99-217">Teraz nie zostanie **ma** tooembed wszystko w tooone toobe tylko się upewnić, że dane pozostają spójne dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c99-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="99c99-218"><a name="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99c99-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="99c99-219">Witaj takeaways największych z tego artykułu jest toounderstand, że dane modelowania w świecie bez schematu są równie ważne jako kiedykolwiek.</span><span class="sxs-lookup"><span data-stu-id="99c99-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="99c99-220">Tak, ponieważ nie ma żadnych toorepresent jeden sposób element danych na ekranie, brak nie toomodel jeden sposób danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="99c99-221">Należy toounderstand aplikacji go i jak powoduje wygenerowanie używać i przetwarza dane hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="99c99-222">Następnie stosując niektóre hello wytycznych przedstawionych w tym miejscu możesz można ustawić o tworzeniu modelu, który dotyczy natychmiastowego wymagań aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="99c99-223">Jeśli aplikacje wymagają toochange, można wykorzystać elastyczność hello tooembrace bez schematu bazy danych zmiany i łatwo rozwijać modelu danych.</span><span class="sxs-lookup"><span data-stu-id="99c99-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="99c99-224">toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, można znaleźć usługi toohello [dokumentacji](https://azure.microsoft.com/documentation/services/cosmos-db/) strony.</span><span class="sxs-lookup"><span data-stu-id="99c99-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="99c99-225">toounderstand jak tooshard danych między wieloma partycjami odwoływać się za[partycjonowanie danych w usłudze Azure DB rozwiązania Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="99c99-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
