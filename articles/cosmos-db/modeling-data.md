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
# <a name="modeling-document-data-for-nosql-databases"></a>Modelowanie danych dokumentów NoSQL baz danych
Gdy schematu baz danych bez, takich jak Azure DB rozwiązania Cosmos, ułatwiają super tooembrace zmiany tooyour danych modelu, należy nadal poświęcony niektóre razem analiza danych. 

Jak danych będzie przechowywane toobe? W jaki sposób będzie tooretrieve i zapytań dane aplikacji? Jest duże aplikacji pogrubiona odczytu lub zapisu? 

Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:

* Jak należy traktować dokumentu w bazie danych dokumentów?
* Co to jest modelowania danych i dlaczego należy zależy? 
* W jaki sposób modelowania danych dokumentów bazy danych różnych tooa relacyjnej bazy danych?
* Jak express relacji danych w bazie danych nierelacyjnych?
* Gdy osadzanie danych i gdy łącze toodata?

## <a name="embedding-data"></a>Osadzanie danych
Po uruchomieniu modelowania danych w magazynie dokumentu, takie jak bazy danych Azure rozwiązania Cosmos, spróbuj tootreat jednostki jako **niezależne dokumenty** reprezentowane w formacie JSON.

Przed zajrzyj mamy dostęp zbyt dużo więcej Daj nam Zabierz kilka kroków i przyjrzeć jak firma Microsoft może coś relacyjnej bazy danych, temat, który wiele osób zna już modelu. Witaj poniższy przykład przedstawia sposób osoby mogą być przechowywane w relacyjnej bazie danych. 

![Model relacyjnej bazy danych](./media/documentdb-modeling-data/relational-data-model.png)

Podczas pracy z relacyjnych baz danych, został możemy nauczanych dla toonormalize lat normalizacji, normalizacji.

Zwykle normalizacji danych obejmuje pobranie jednostki, takie jak osoby i podzielenie go w toodiscrete fragmentów danych. W powyższym przykładzie hello osoba może mieć wiele rekordów szczegóły kontaktu, a także wiele rekordów adresów. Firma Microsoft nawet wykonaj krok dalej i rozbić szczegóły dotyczące kontaktu wyodrębniając dalsze typowe pola, takich jak typu. Tego samego adresu, w tym polu każdego rekordu ma typu like *Home* lub *biznesowa* 

Witaj przeprowadzi lokalnych podczas normalizacji danych jest zbyt**nie należy przechowywać nadmiarowych danych** na wszystkich rekordów, a raczej odwoływać się toodata. W tym przykładzie tooread osoby, ich szczegóły dotyczące kontaktu i adresy, należy toouse sprzężenia tooeffectively agregacji danych w czasie wykonywania.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

Aktualizowanie jedna osoba ich szczegóły dotyczące kontaktu i adresy wymaga operacji zapisu w wielu poszczególnych tabel. 

Teraz załóżmy podjęcia przyjrzeć się jak firma Microsoft będzie modelu hello takie same dane jako autonomiczną jednostkę w bazie danych dokumentu.

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

Podejście hello powyżej mamy teraz **nieznormalizowany** hello rekord osoby gdzie możemy **osadzone** hello wszystkie informacje dotyczące osoby toothis, takie jak ich szczegóły dotyczące kontaktu i adresy w jednym tooa Dokument JSON.
Ponadto ponieważ firma Microsoft nie jest ograniczone tooa ustalić schemat, który mamy hello elastyczność toodo np. konieczności skontaktowania się z różnych kształtów całkowicie. 

Pobieranie rekordu pełną osoby z bazy danych hello jest teraz jeden odczytu operacji względem jednej kolekcji, a dla pojedynczego dokumentu. Aktualizacja rekordu osoby, ich szczegóły dotyczące kontaktu i adresy, jest również operacji zapisu pojedynczego dla pojedynczego dokumentu.

Przez denormalizing danych, aplikacja może być konieczne tooissue mniejszej liczby zapytań i aktualizacje toocomplete typowych operacji. 

### <a name="when-tooembed"></a>Gdy tooembed
Ogólnie rzecz biorąc, użyj osadzonych danych modeli, gdy:

* Brak **zawiera** relacje między obiektami.
* Brak **jeden do kilka** relacje między obiektami.
* Brak dostępnych danych osadzonych który **zmienia się rzadko**.
* Jest osadzony danych nie będzie rosnąć **bez powiązanych z**.
* Brak osadzonych danych, która jest **integralną** toodata w dokumencie.

> [!NOTE]
> Zwykle nieznormalizowane danych modele umożliwiają lepsze **odczytu** wydajności.
> 
> 

### <a name="when-not-tooembed"></a>Jeśli nie tooembed
Witaj zasadą w bazie danych dokumentów wszystko, co jest toodenormalize i osadzone wszystkie dane w jednym dokumencie tooa, może to spowodować toosome sytuacji, w których należy unikać.

Zająć ta Wstawka kodu JSON.

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

Może to być co podmiot post z komentarzami osadzone będzie wyglądała jeśli zostały możemy modelowania typowe blogu lub CMS, system. Witaj problem z tym przykładem jest tym hello komentarze tablica jest **niepowiązany**, co oznacza, że są limit (praktyczne) nie toohello liczbę komentarzy może mieć żadnych pojedynczego post. Problem będzie wzrostem rozmiaru hello hello dokumentu może znacznie.

Jako rozmiar hello hello dokumentu rozwoju hello możliwości tootransmit hello danych za pośrednictwem hello danych przesyłanych w sieci, a także odczytywania i aktualizowania dokumentu hello na dużą skalę, będzie to mieć wpływ na.

W takim przypadku byłoby lepsze hello tooconsider po modelu.

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

Ten model ma hello trzech najnowszych komentarzy osadzonych na powitania post siebie, który jest tablicą o stałej powiązane z tym czas. Witaj komentarze są zgrupowane w toobatches 100 komentarze i przechowywane w oddzielnych dokumentów. Hello rozmiar wsadu hello została wybrana jako 100, ponieważ fikcyjne aplikacji umożliwia hello komentarze 100 tooload użytkownika w czasie.  

Innym przypadku, gdy osadzanie danych nie jest dobrym rozwiązaniem jest hello osadzone w danych jest często używane w różnych dokumentach i będzie często zmieniana. 

Zająć ta Wstawka kodu JSON.

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

To może reprezentować portfolio standardowych osoby. Wybraliśmy tooembed hello standardowych informacji w dokumencie portfolio tooeach. W środowisku, w którym dane dotyczące zmienia się często, takich jak zasobu handlowymi aplikacji osadzanie danych, które zmieniają się często będzie toomean, czy są stale aktualizowane każdy dokument portfolio za każdym razem, gdy jest przedmiotem handlu zasobu.

Stock *zaza* mogą być przedmiotem handlu setki wiele razy w jednym dniu i tysięcy użytkowników może mieć *zaza* na ich portfolio. Z modelem danych, takich jak hello powyżej czy mamy tooupdate wielu tysięcy dokumentów portfolio wiele razy każdego dnia wiodące tooa system, który nie jest bardzo dobrego skalowania. 

## <a id="Refer"></a>Odwołanie do danych
Tak osadzanie danych działa dobrze w wielu przypadkach, ale jest jasne, czy istnieją scenariusze, gdy problemy więcej niż warto denormalizing danych spowoduje przerwanie. Dlatego co możemy zrobić teraz? 

Relacyjnych baz danych nie są hello jedynym miejscem, w którym można utworzyć relacji między obiektami. W bazie danych dokumentu może mieć informacji w jednym dokumencie, który faktycznie odnosi się toodata w innych dokumentów. Teraz I am nie postulować przez jedną minutę, nawet budujemy systemów, które jest lepiej dostosowane tooa relacyjnej bazy danych w usłudze Azure DB rozwiązania Cosmos lub wszelkie inne bazy danych dokumentów, że relacje proste jest uszkodzona i może być bardzo przydatne. 

Przykład Witaj toouse standardowych portfolio z wcześniej, ale teraz określane toohello standardowych elementów na powitania portfolio zamiast osadzania Wybraliśmy w hello JSON poniżej. W ten sposób element standardowych hello często zmienia się w całym hello dzień hello tylko dokument, który musi zaktualizować toobe po hello pojedynczego dokumentu standardowych. 

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


Podejście toothis natychmiastowego wadą interfejsu jest jednak, jeśli aplikacja jest wymagana tooshow informacje o każdej akcji przechowywana podczas wyświetlania portfolio osoby; w takim przypadku trzeba toomake wiele rund toohello tooload hello informacje z bazy danych dla każdego dokumentu standardowych. W tym miejscu wprowadziliśmy decyzji tooimprove hello wydajności operacji zapisu, które się zdarzyć, często w ciągu dnia hello, ale z kolei naruszenia zabezpieczeń na powitania operacje, które potencjalnie mają mniej wpływ na wydajność hello tego konkretnego systemu odczytu.

> [!NOTE]
> Znormalizowany modeli danych **może wymagać więcej rund** toohello serwera.
> 
> 

### <a name="what-about-foreign-keys"></a>Jakie klucze obce?
Ponieważ nie ma żadnych koncepcji ograniczenia, klucz obcy lub w inny sposób relacje między dokumentów zawierających w dokumentach skutecznej "powiązania" i nie są weryfikowane przez hello bazy danych. Jeśli chcesz, aby tooensure, który hello dane, które odwołuje się dokument tooactually istnieje, a następnie toodo to konieczne w aplikacji lub przy użyciu hello wyzwalacze po stronie serwera lub procedur składowanych dla bazy danych Azure rozwiązania Cosmos.

### <a name="when-tooreference"></a>Gdy tooreference
Ogólnie rzecz biorąc, użyj danych znormalizowane modele, gdy:

* Reprezentujący **jeden do wielu** relacji.
* Reprezentujący **wiele do wielu** relacji.
* Dane dotyczące **zmienia się często**.
* Może być danych występujące w odwołaniu **niepowiązany**.

> [!NOTE]
> Zwykle normalizacji zapewnia lepsze **zapisu** wydajności.
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Gdzie umieścić relacji hello?
rozwój Hello relacji hello pomoże określić, w których odwołanie hello toostore dokumentu.

Jeśli przyjrzymy się hello JSON poniżej modelujący wydawcy i książek.

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

Jeśli numer hello książek hello na wydawcy jest mały wzrost ograniczone, następnie przechowywanie hello książki odwołania w dokumencie wydawcy hello mogą być użyteczne. Jednak w przypadku niepowiązanego numer hello książek na wydawcy, ten model danych doprowadziłoby toomutable rośnie tablic, tak jak dokument wydawcy przykład hello powyżej. 

Przełączanie rzeczy wokół bit czy wynik w modelu nadal reprezentuje ale teraz hello tych samych danych pozwala uniknąć dużych kolekcjach modyfikowalne.

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

W hello powyżej przykładzie, możemy porzucona hello niepowiązany kolekcji na powitania wydawcy dokumentu. Zamiast tego po prostu mamy odwołanie wydawcy toohello na każdy dokument książki.

### <a name="how-do-i-model-manymany-relationships"></a>Jak model relacje wiele: wiele?
Relacyjnej bazy danych *wiele: wiele* relacje są często modelowane sprzężenie tabel, które właśnie ze sobą połączone rekordy z innych tabel. 

![Dołącz do tabel](./media/documentdb-modeling-data/join-table.png)

Może się wydawać tooreplicate hello przy użyciu tego samego operacją dokumenty i utworzyć model danych, która wygląda podobnie następujące toohello.

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

Czy to pomoże. Jednak podczas ładowania albo autor z ich książki lub ładowania książkę z jego autorem zawsze wymagają co najmniej dwóch dodatkowych zapytań w bazie danych hello. Sprzęganie dokumentu i następnie innego zapytania toofetch hello rzeczywiste dokumentu jest dołączony toohello jednego zapytania. 

Jeśli jest wszystkich zadań w tej tabeli sprzężenia przyklejanie ze sobą dwie części danych, dlaczego nie upuszczenie go całkowicie?
Należy wziąć pod uwagę następujące hello.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Teraz gdyby Autor, niezwłocznie sprawdzić książki zostały one zapisane i odwrotnie gdyby załadować dokument książki czy wiem hello identyfikatory hello autora lub autorów. Spowoduje to zapisanie tej pośredniczące zapytania dotyczącego tabeli sprzężenia hello zmniejszeniu liczby powitania serwera rund aplikacji ma toomake. 

## <a id="WrapUp"></a>Modele hybrydowe danych
Teraz analizujemy zostały osadzanie (lub denormalizing) i danych odwołującego się (lub normalizacji), o ich upsides, a każdy mieć dokonywania jako zaobserwowano. 

Go nie zawsze są toobe albo lub, nie można rzeczy Przerażony toomix się nieco. 

Na podstawie wzorców użycia określonych aplikacji i obciążeń, które może się zdarzyć, gdy mieszanie osadzonych danych występujące w odwołaniu ma sens i może logiki aplikacji toosimpler potencjalnego klienta z serwerem mniej przekazywanych zachowując dobrej poziomu wydajności .

Należy wziąć pod uwagę hello następującego formatu JSON. 

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

W tym miejscu zostały (przeważnie) była hello osadzonego modelu, gdy dane z innych jednostek jest osadzony w dokumencie najwyższego poziomu hello, ale odwołuje się do innych danych. 

W dokumencie Podręcznik hello, firma Microsoft może zobaczyć kilka interesujące pola, jeśli przyjrzymy się tablicy hello autorów. Brak *identyfikator* ma pola, które jest polem hello korzystamy również toorefer tooan wstecz autora dokumentu, standardową praktyką w znormalizowane modelu, ale następnie *nazwa* i *thumbnailUrl*. Firma Microsoft może po prostu wciąż z *identyfikator* i lewego tooget aplikacji hello jest potrzebne informacje dodatkowe z hello odpowiednich autora dokumentu za pomocą "link" hello, ale ponieważ naszej aplikacji Wyświetla nazwę autora hello i a Obraz miniatury z każdej książki wyświetlane można zapisać na książki serwera toohello obiegu na liście przez denormalizing **niektórych** danych z hello autora.

Na pewno zmienić imię i nazwisko autora hello lub chcieli tooupdate swoich zdjęć trzeba toogo aktualizacji co książki one kiedykolwiek opublikowany, ale dla aplikacji, oparte na założeniu hello czy autorów nie bardzo często, zmień ich nazwy to dopuszczalne projektu decyzji.  

W przykładzie hello są **wstępnie obliczone wartości zagregowanych** wartości toosave kosztowne przetwarzania na operację odczytu. W przykładzie hello dane hello osadzony w dokumencie autora hello jest dane, które jest obliczane w czasie wykonywania. Nowej książki zostanie opublikowana, tworzony jest dokument książki **i** hello countOfBooks pole jest ustawione na wartość tooa obliczana na podstawie liczby hello książki dokumentów, które istnieją dla konkretnego autora. Tego rodzaju optymalizacji byłoby dobrej w systemach duże odczytu gdzie możemy sobie toodo obliczenia na zapisy w kolejności toooptimize odczytów.

Witaj toohave możliwości modelu z pól obliczeniowych wstępnie jest możliwe ponieważ obsługuje bazy danych Azure rozwiązania Cosmos **transakcji wielu dokumentów**. Wiele magazynów NoSQL nie nie transakcji w dokumentach i w związku z tym wspierają decyzje dotyczące projektu, takie jak "zawsze osadzić wszystko", ze względu na ograniczenia toothis. Z bazy danych rozwiązania Cosmos platformy Azure można użyć wyzwalacze po stronie serwera lub procedur składowanych, które Wstaw książki i zaktualizuj autorów wszystko w ramach transakcji ACID. Teraz nie zostanie **ma** tooembed wszystko w tooone toobe tylko się upewnić, że dane pozostają spójne dokumentu.

## <a name="NextSteps"></a>Następne kroki
Witaj takeaways największych z tego artykułu jest toounderstand, że dane modelowania w świecie bez schematu są równie ważne jako kiedykolwiek. 

Tak, ponieważ nie ma żadnych toorepresent jeden sposób element danych na ekranie, brak nie toomodel jeden sposób danych. Należy toounderstand aplikacji go i jak powoduje wygenerowanie używać i przetwarza dane hello. Następnie stosując niektóre hello wytycznych przedstawionych w tym miejscu możesz można ustawić o tworzeniu modelu, który dotyczy natychmiastowego wymagań aplikacji hello. Jeśli aplikacje wymagają toochange, można wykorzystać elastyczność hello tooembrace bez schematu bazy danych zmiany i łatwo rozwijać modelu danych. 

toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, można znaleźć usługi toohello [dokumentacji](https://azure.microsoft.com/documentation/services/cosmos-db/) strony. 

toounderstand jak tooshard danych między wieloma partycjami odwoływać się za[partycjonowanie danych w usłudze Azure DB rozwiązania Cosmos](documentdb-partition-data.md). 
