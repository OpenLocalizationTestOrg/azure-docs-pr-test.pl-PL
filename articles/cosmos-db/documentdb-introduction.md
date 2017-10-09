---
title: "Azure Cosmos DB: interfejs API usługi DocumentDB | Microsoft Docs"
description: "Dowiedz się, jak skorzystać z bazy danych Azure rozwiązania Cosmos toostore i zapytań bardzo dużych woluminów dokumentów JSON z niskim opóźnieniem przy użyciu programu SQL i JavaScript."
keywords: "baza danych json, baza danych dokumentów"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Wprowadzenie tooAzure DB rozwiązania Cosmos: interfejs API usługi DocumentDB

[Azure Cosmos DB](introduction.md) to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft do aplikacji o krytycznym znaczeniu. Udostępnia bazę danych systemu Azure rozwiązania Cosmos [dystrybucji globalne gotowe](distribute-data-globally.md), [elastyczne skalowanie przepływność i magazyn](partition-data.md) na całym świecie, jednocyfrowej milisekundy opóźnienia na powitania 99-ty percentyl [pięć dobrze zdefiniowane poziomy spójności](consistency-levels.md), zagwarantować wysokiej dostępności, wszystkie kopie przez [SLA branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB rozwiązania Cosmos [automatycznie indeksuje danych](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności toodeal z zarządzania schematu i indeksu. To usługa wielomodelowa, obsługująca modele dokumentowe, klucz-wartość, wykresy i kolumny. 

![Interfejs API usługi Azure DocumentDB](./media/documentdb-introduction/cosmosdb-documentdb.png) 

W ramach hello interfejsu API usługi DocumentDB, bazy danych rozwiązania Cosmos Azure zapewnia sformatowany i znanym [możliwość wykonywania kwerend SQL](documentdb-sql-query.md) z stale małe opóźnienia na dane JSON bez schematu. W tym artykule firma Microsoft udostępnia przegląd DB hello Azure rozwiązania Cosmos interfejsu API usługi DocumentDB i jak można używany toostore bardzo dużych woluminów danych JSON, wyszukiwać w nich w kolejności w milisekundach czas oczekiwania i łatwo rozwijać hello schematu. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Jakie możliwości i kluczowe funkcje oferuje usługa Azure Cosmos DB?
Rozwiązania Cosmos bazę danych systemu Azure, za pośrednictwem hello API usługi DocumentDB oferuje następujące kluczowe funkcje i korzyści hello:

* **Elastycznie skalowalne przepływność i Magazyn:** łatwe skalowanie w górę lub skali z toomeet bazy danych JSON aplikacji wymaga. Dane są przechowywane na dyskach półprzewodnikowych (SSD, solid-state drive) dla zapewnienia przewidywalnych, niskich opóźnień. Azure DB rozwiązania Cosmos obsługuje kontenery do przechowywania danych JSON zwane kolekcjami, które mogą być skalowane toovirtually nieograniczonego rozmiaru magazynu i udostępnionej przepływności. W miarę wzrostu aplikacji usługę Azure Cosmos DB można bezproblemowo elastycznie skalować z przewidywalną wydajnością. 


* **W przypadku replikacji:** bazy danych Azure rozwiązania Cosmos niewidocznie replikuje użytkownika jest skojarzony z Twoim kontem platformy Azure DB rozwiązania Cosmos umożliwiając aplikacji toodevelop, które wymagają dostępu globalny toodata zapewniając regiony tooall danych wady i zalety między spójności, dostępność i wydajność, wszystkie odpowiednie gwarancje. Azure DB rozwiązania Cosmos zapewnia przezroczysty tryb failover regionalnych, z wielu interfejsów API, a hello możliwości tooelastically skali przepływność i Magazyn między Witaj świecie. Więcej informacji zawiera artykuł [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md) (Globalna dystrybucja danych przy użyciu usługi Azure Cosmos DB).

* **Zapytania ad hoc z użyciem dobrze znanej składni SQL**: przechowywanie heterogenicznych dokumentów JSON i wykonywanie względem nich zapytań przy użyciu dobrze znanej składni SQL. Azure DB rozwiązania Cosmos wykorzystuje wysoce współbieżną, nieblokującą, opartą na strukturze dziennika indeksowania indeksu tooautomatically technologii całej zawartości dokumentu. Dzięki temu zaawansowanych zapytań w czasie rzeczywistym bez wskazówek schematu toospecify potrzeby hello, indeksów pomocniczych czy widoków. Więcej informacji zawiera temat [Tworzenie zapytań względem usługi Azure Cosmos DB](documentdb-sql-query.md). 
* **Wykonywanie skryptów JavaScript w bazie danych hello:** wyrażanie logiki aplikacji jako procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika (UDF) przy użyciu standardowego języka JavaScript. Dzięki temu Twojej aplikacji logiki toooperate nad danymi bez obaw o hello niezgodność aplikacji hello hello schematu bazy danych. Witaj interfejsu API usługi DocumentDB zapewnia pełne transakcyjne wykonywanie logiki aplikacji JavaScript bezpośrednio wewnątrz aparatu bazy danych hello. Witaj głęboka integracja języka JavaScript umożliwia wykonywanie hello INSERT, REPLACE, DELETE i wybierz operacji z poziomu programu JavaScript jako izolowanych transakcji. Aby dowiedzieć się więcej, zobacz [Programowanie po stronie serwera w usłudze DocumentDB](programming.md).

* **Dostosowywalne poziomy spójności:** wybierz jedną z pięciu dobrze zdefiniowanych spójności poziomy tooachieve optymalnego kompromisu między wydajnością a spójnością. Dla zapytań i operacji odczytu usługa Azure Cosmos DB oferuje pięć różnych poziomów spójności: „silna”, „powiązana nieaktualność”, „sesja”, „spójny prefiks” i „ostateczna”. Te poziomy spójności szczegółowe, dokładnie zdefiniowane pozwalają toomake dźwięku kompromis między spójności, dostępnością i opóźnieniem. Dowiedz się więcej w [przy użyciu spójności poziomy wydajności i dostępności toomaximize](consistency-levels.md).

* **Pełna:** wyeliminować hello potrzeby toomanage maszyn i bazy danych zasobów. Jako pełni zarządzaną usługę Microsoft Azure możesz nie nie potrzeba maszyn wirtualnych toomanage, wdrażanie i konfigurowanie oprogramowania, zarządzać skalowaniem lub postępowania w przypadku uaktualnienia złożonych warstwy danych. Dla każdej bazy danych jest automatycznie tworzona kopia zapasowa i jest ona chroniona przed regionalnymi awariami. Możesz łatwo dodać konto bazy danych Azure rozwiązania Cosmos i aprowizować pojemność odpowiednio do potrzeb, co pozwoli toofocus na aplikacji zamiast pracy i zarządzania bazą danych. 

* **Celowa ogólnodostępność**: można szybko rozpocząć pracę, wykorzystując posiadane umiejętności i narzędzia. Programowanie w odniesieniu do hello interfejsu API usługi DocumentDB jest łatwe, przystępne, nie wymagają tooadopt nowe narzędzia i stosować tooJSON rozszerzenia toocustom lub JavaScript. Możesz uzyskać dostęp do wszystkich funkcji bazy danych hello tym CRUD, zapytań i przetwarzania języka JavaScript przy użyciu prostego interfejsu RESTful protokołu HTTP. Witaj interfejsu API usługi DocumentDB obejmuje istniejące formaty, języki i standardy, jednocześnie zapewniając wysoką wartość możliwości bazy danych oparte na nich.

* **Automatyczne indeksowanie:** domyślnie bazy danych Azure rozwiązania Cosmos automatycznie indeksuje wszystkie dokumenty hello hello bazy danych i nie oczekują lub wymaga żadnego schematu lub tworzenia indeksów pomocniczych. Nie chcesz tooindex wszystko? Nie martw się, możesz również [zrezygnować ze ścieżki plików JSON](indexing-policies.md).

* **Zmiana źródła pomocy technicznej:** zmiany źródła danych zawiera posortowaną listę dokumentów w kolekcji bazy danych Azure rozwiązania Cosmos w kolejności hello, w którym zostały zmodyfikowane. To źródło można toolisten używane dla toodata zmian w kolejności tooreplicate danych, wyzwolenia wywołań interfejsu API lub przetwarzają strumienia aktualizacji. Zmiany źródła danych jest automatycznie włączone i łatwe toouse: [Dowiedz się więcej na temat zmiany źródła strumieniowego](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>Jak zarządzać danych za pomocą hello interfejsu API usługi DocumentDB?
Hello interfejsu API usługi DocumentDB ułatwia zarządzanie dane JSON za pomocą dobrze zdefiniowanych zasobów bazy danych. Te zasoby są replikowane w celu zapewnienia wysokiej dostępności i unikatowo adresowane przez ich logiczny identyfikator URI. Witaj interfejsu API usługi DocumentDB oferuje prosty HTTP na podstawie model programowania RESTful dla wszystkich zasobów. 


konto bazy danych Azure DB rozwiązania Cosmos Hello jest unikatową przestrzenią nazw, który zapewnia dostęp do tooAzure DB rozwiązania Cosmos. Przed utworzeniem konta bazy danych musi mieć subskrypcję platformy Azure, która umożliwia dostęp do różnych tooa usług platformy Azure. 

Wszystkie zasoby w usłudze Azure Cosmos DB są modelowane i przechowywane jako dokumenty JSON. Zasoby są zarządzane jako elementy, które są dokumentami JSON zawierającymi metadane, oraz jako źródła danych, które są kolekcjami elementów. Zestawy elementów są zawarte w odpowiednich źródłach danych.

Obraz powitania poniżej przedstawia hello relacje między zasobami Azure DB rozwiązania Cosmos hello:

![Witaj hierarchiczną relację między zasobami w usłudze Azure DB rozwiązania Cosmos][1] 

Konto bazy danych składa się z zestawu baz danych, każda z nich zawiera wiele kolekcji, a każda kolekcja może zawierać procedury składowane, wyzwalacze, funkcje UDF, dokumenty i powiązane załączniki. Bazy danych ma również skojarzonych użytkowników, każdy z zestawem uprawnień tooaccess różnych innych kolekcji, procedur składowanych, wyzwalaczy, funkcji UDF, dokumentów lub załączników. Bazy danych, użytkownicy, uprawnienia i kolekcje są zasobami zdefiniowanymi przez system za pomocą dobrze znanych schematów, natomiast dokumenty, procedury składowane, wyzwalacze, funkcje UDF i załączniki zawierają dowolną, zdefiniowaną przez użytkownika zawartość JSON.  

> [!NOTE]
> Ponieważ hello interfejsu API usługi DocumentDB wcześniej była dostępna jako hello usługi Azure DocumentDB, można kontynuować tooprovision, monitorowanie i zarządzanie nimi kont utworzonych za pomocą interfejsu API REST zarządzania zasobów Azure hello, lub za pomocą narzędzia hello Azure DocumentDB lub bazy danych Azure rozwiązania Cosmos nazwy zasobów. Używamy nazwy hello zamiennie podczas odwoływania się toohello interfejsów API usługi Azure DocumentDB. 

## <a name="develop"></a>Jak można programować aplikacje z hello interfejsu API usługi DocumentDB?

Azure DB rozwiązania Cosmos udostępnia zasoby za pośrednictwem hello interfejsów API REST, który można wywołać za pomocą dowolnego języka realizującego żądania HTTP i HTTPS. Ponadto firma Microsoft oferuje biblioteki programistyczne dla kilku popularnych języków dla hello interfejsu API usługi DocumentDB. powitania klienta biblioteki upraszczają wiele aspektów pracy z interfejsu API hello dzięki obsłudze szczegółów takich jak buforowanie adresów, Zarządzanie wyjątkami, Automatyczne ponawianie prób i tak dalej. Biblioteki są obecnie dostępne dla hello następujących języków i platform:  

| Do pobrania | Dokumentacja |
| --- | --- |
| [Zestaw SDK platformy .NET](http://go.microsoft.com/fwlink/?LinkID=402989) |[Biblioteka języka .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Zestaw SDK dla platformy Node.js](http://go.microsoft.com/fwlink/?LinkID=402990) |[Biblioteka języka Node.js](http://azure.github.io/azure-documentdb-node/) |
| [Zestaw SDK Java](http://go.microsoft.com/fwlink/?LinkID=402380) |[Biblioteka języka Java](/java/api/com.microsoft.azure.documentdb) |
| [Zestaw SDK dla języka JavaScript](http://go.microsoft.com/fwlink/?LinkID=402991) |[Biblioteka języka JavaScript](http://azure.github.io/azure-documentdb-js/) |
| Nie dotyczy |[Zestaw SDK dla języka JavaScript po stronie serwera](http://azure.github.io/azure-documentdb-js-server/) |
| [Zestaw SDK dla języka Python](https://pypi.python.org/pypi/pydocumentdb) |[Biblioteka języka Python](http://azure.github.io/azure-documentdb-python/) |
| Nie dotyczy | [Interfejs API dla usługi MongoDB](mongodb-introduction.md)


Przy użyciu hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md), mogą tworzyć i przetestować aplikację lokalnie z hello interfejsu API usługi DocumentDB, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów. Po zakończeniu jak aplikacja działa w emulatorze hello, możesz przełączyć toousing konto bazy danych Azure rozwiązania Cosmos w chmurze hello.

Poza basic tworzenia, odczytu, aktualizacji i usuwania działań, powitalne interfejsu API usługi DocumentDB udostępnia interfejs zaawansowanych zapytań SQL do pobierania dokumentów JSON oraz obsługę po stronie serwera dla transakcyjnego wykonywania logiki aplikacji JavaScript. interfejsy wykonywania zapytań i skryptów Hello są dostępne za pośrednictwem bibliotek wszystkich platform także hello interfejsów API REST. 

### <a name="sql-query"></a>Zapytanie SQL
Hello interfejsu API usługi DocumentDB obsługiwanych badania dokumentów przy użyciu języka SQL, osadzonego w hello JavaScript wpisz systemu oraz wyrażenia z obsługą zapytań relacyjnych, hierarchicznych i przestrzennych. język zapytań usługi DocumentDB Hello jest proste, ale dokumentów JSON tooquery interfejsu. Witaj język obsługuje podzbiór gramatyki ANSI SQL i dodaje głęboką integrację obiektów, tablic, konstrukcji obiektów i wywołania funkcji JavaScript. Hello interfejsu API usługi DocumentDB udostępnia swój model zapytań bez żadnego jawnego schematu lub wskazówek indeksowania od dewelopera hello.

Funkcje zdefiniowane przez użytkownika (UDF) można zarejestrowany hello interfejsu API usługi DocumentDB i określany jako część zapytania SQL, rozszerzając w ten sposób hello gramatyki toosupport niestandardowej logiki aplikacji. Te funkcje UDF są zapisywane jako programy JavaScript i wykonywane w ramach hello bazy danych. 

Deweloperom platformy .NET hello interfejsu API usługi DocumentDB [zestawu .NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) oferuje również dostawcę zapytań LINQ. 

### <a name="transactions-and-javascript-execution"></a>Transakcje i wykonywanie kodu JavaScript
Witaj interfejsu API usługi DocumentDB umożliwia toowrite logiki aplikacji jako nazwanych programów napisanych w całości w języku JavaScript. Te programy są rejestrowane dla kolekcji i mogą wyzwalać operacje bazy danych na dokumentach hello w ramach danej kolekcji. Kod JavaScript można zarejestrować do wykonania jako wyzwalacz, procedurę składowaną lub funkcję zdefiniowaną przez użytkownika. Wyzwalacze i procedury składowane można tworzenia, odczytu, aktualizacji i usuwać dokumenty, natomiast funkcje zdefiniowane przez użytkownika wykonywane jako część logiki wykonywania zapytania hello bez kolekcji toohello dostęp do zapisu.

Wykonywanie skryptów JavaScript w hello DB rozwiązania Cosmos jest modelowane hello koncepcjami obsługiwanymi przez systemy relacyjnych baz danych, z użyciem języka JavaScript jako nowoczesnego zamiennika języka Transact-SQL. Cała logika JavaScript jest wykonywana w ramach transakcji ACID otoczenia z izolacją migawki. W trakcie hello jego wykonywania Jeśli powitalne JavaScript zgłasza wyjątek, następnie hello cała transakcja została przerwana.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Czy są jakieś kursy online na temat usługi Azure Cosmos DB?

Tak, jest kurs [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) dotyczący usługi Azure DocumentDB. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Następne kroki
Masz już konto platformy Azure? Następnie można rozpocząć pracę z usługą Azure Cosmos DB, wykonując zadania opisane w przewodnikach [Szybki start](../cosmos-db/create-documentdb-dotnet.md), które poprowadzą Cię przez proces tworzenia konta i rozpoczynania pracy z usługą Cosmos DB.

[1]: ./media/documentdb-introduction/json-database-resources1.png

