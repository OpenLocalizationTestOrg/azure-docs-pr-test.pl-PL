---
title: "aaaAzure DB rozwiązania Cosmos — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące bazy danych z rozwiązania Cosmos platformy Azure, usługa globalnie rozproszone i wiele modeli bazy danych. Więcej informacji na temat pojemności, poziomów wydajności i skalowania."
keywords: "Pytania dotyczące bazy danych, często zadawane pytania, usługi documentdb, azure, platformy Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Często zadawane pytania dotyczące usługi Azure rozwiązania Cosmos bazy danych
## <a name="azure-cosmos-db-fundamentals"></a>Podstawowe informacje na temat usługi Azure DB rozwiązania Cosmos
### <a name="what-is-azure-cosmos-db"></a>Co to jest Azure DB rozwiązania Cosmos?
Azure DB rozwiązania Cosmos jest usługą bazy danych replikowany globalnie, wiele modeli, ułatwiająca oferująca zaawansowaną obsługę zapytań dane bez schematu oraz konfigurowalną i niezawodną wydajności i umożliwia szybkie opracowywanie. Jego wszystkich odbywa się za pośrednictwem platformy zarządzanej, która nie jest obsługiwana przez hello zasilania i połączyć systemu Microsoft Azure. 

Azure DB rozwiązania Cosmos jest hello odpowiednie rozwiązanie dla aplikacji sieci web, mobilnych, gier, i aplikacji IoT przewidywalnej przepływności, wysoką dostępność, małych opóźnień i model danych bez schematu są wymagania dotyczące klucza. Zapewnia elastyczność schematu i rozbudowane indeksowanie i zawiera obsługę transakcyjną wielu dokumentów dzięki zintegrowanemu środowisku JavaScript. 

Więcej pytań bazy danych, odpowiedzi i instrukcje dotyczące instalowania i korzystania z tej usługi można znaleźć hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Jakie happened tooDocumentDB?
Hello interfejsu API usługi DocumentDB jest jednym z interfejsów API i danych modeli hello obsługiwane dla bazy danych Azure rozwiązania Cosmos. Ponadto bazy danych rozwiązania Cosmos Azure obsługuje możesz przy użyciu interfejsu API programu Graph (wersja zapoznawcza), tabela interfejsu API (wersja zapoznawcza) i interfejsu API bazy danych MongoDB. Aby uzyskać więcej informacji, zobacz [pytania klientów usługi DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Jak uzyskać toomy konta usługi DocumentDB w portalu Azure hello?
W portalu Azure hello kliknij ikonę bazy danych Azure rozwiązania Cosmos hello w okienku po lewej stronie powitania. Jeśli masz konto usługi DocumentDB przed masz teraz konto bazy danych Azure rozwiązania Cosmos z rozliczeniami tooyour nie zmiany.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Co to są hello typowe zastosowania bazy danych rozwiązania Cosmos Azure?
Azure DB rozwiązania Cosmos jest dobrym rozwiązaniem w przypadku nowych sieci web, mobilnych, gier, i aplikacji IoT, gdzie szybkie kolejności czasów odpowiedzi milisekund skalowania automatycznego, przewidywalną wydajność i hello tooquery możliwości przez dane bez schematu jest ważne. Azure DB rozwiązania Cosmos jest przydatna toorapid opracowywanie i obsługę ciągłej iteracji modeli danych aplikacji hello. Zawartość wygenerowaną przez użytkowników i dane aplikacji są [typowe przypadki użycia bazy danych Azure rozwiązania Cosmos](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Jak bazy danych rozwiązania Cosmos Azure oferuje przewidywalną wydajność?
A [jednostki żądania](request-units.md) (RU) jest hello miara przepływności w usłudze Azure DB rozwiązania Cosmos. Przepływność 1 RU odpowiada przepływności toohello hello GET dokumentu 1 KB. Każdej operacji w usłudze Azure DB rozwiązania Cosmos, w tym odczytów, zapisy zapytania SQL i wykonywaniem procedur składowanych, ma wartość RU deterministyczna, która jest oparta na powitania przepływności wymaganej toocomplete hello operacji. Zamiast planowania procesora CPU, we/wy i pamięci oraz ich wpływ na przepływność aplikacji, można traktować pod względem jednej miary RU.

Istnieje możliwość rezerwowania każdego kontenera Azure DB rozwiązania Cosmos z aprowizowaną przepływnością wyrażoną jako RUs przepływności na sekundę. W przypadku aplikacji o dowolnej skali testu wydajności toomeasure poszczególnych żądań ich wartości RU i udostępnić łącznie hello toohandle kontenera jednostek żądania dla wszystkich żądań. Możesz też skalowanie w górę i skali z kontenera przepływności jako hello potrzeb aplikacji. Aby uzyskać więcej informacji na temat jednostek żądania i określania z kontenera musi zobacz [szacowanie potrzeb w zakresie przepustowości](request-units.md#estimating-throughput-needs) , a następnie spróbuj hello [Kalkulator przepływności](https://www.documentdb.com/capacityplanner). termin Hello *kontenera* odnosi się tutaj toorefers tooa interfejsu API usługi DocumentDB kolekcji, wykres interfejsu API programu Graph API bazy danych MongoDB kolekcji i tabeli tabeli interfejsu API. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Jak usługa Azure DB rozwiązania Cosmos obsługuje różne modele danych, takie jak klucz/wartość, kolumnowy, dokumentów i wykres

Klucz/wartość, tabela kolumnowy, dokumentów i danych wykresu modele są wszystkie obsługiwane ze względu na powitania ARS (atomami, rekordów i sekwencji) projektowania tej bazy danych rozwiązania Cosmos Azure jest wbudowany w program. Atomami, rekordów i sekwencji mogą być łatwo zamapowanych i planowanego toovarious modeli danych. Witaj interfejsów API dla podzbioru modeli są dostępne prawa teraz (usługi DocumentDB, bazy danych MongoDB, tabeli i interfejsów API Graph) i hello innym tooadditional określonych modeli danych będą dostępne w przyszłości.

Azure DB rozwiązania Cosmos ma niezależny schematu z funkcją automatycznego indeksowania wszystkie dane hello go wysyła strumień bez żadnego schematu lub indeksów pomocniczych z hello developer indeksowania aparatu. Aparat Hello zależy od zestawu układów logicznych indeksu (odwrócony, kolumnowy, drzewo), które oddziel hello układu magazynu z hello indeks i podsystemy przetwarzania zapytań. Rozwiązania cosmos DB również ma toosupport możliwości hello zestaw przewodowy protokołów i interfejsów API w sposób extensible i tłumaczyć je wydajnie toohello podstawowe dane modelu (1) hello logicznej indeksu układy i (2) co jednoznacznie może obsługiwać wiele modeli danych natywnie .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure rozwiązania Cosmos DB HIPAA jest zgodne?
Tak, bazy danych Azure rozwiązania Cosmos jest zgodny z ustawą HIPAA. Ustawa HIPAA określa korzystać wymagania dotyczące hello, ujawniania i ochrony informacji o kondycji umożliwiających indywidualną identyfikację osoby. Aby uzyskać więcej informacji, zobacz hello [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Jakie są limity magazynu hello Azure DB rozwiązania Cosmos?
Brak nie limit toohello łączną ilość danych, które kontener może przechowywać w usłudze Azure DB rozwiązania Cosmos.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Jakie są ograniczenia przepływności hello Azure DB rozwiązania Cosmos?
Brak nie limitu toohello całkowitej przepływności danych obsługujące przez kontener w usłudze Azure DB rozwiązania Cosmos. Witaj klucza rozwiązaniem jest toodistribute obciążenie przybliżeniu równomiernie między wystarczająco dużą liczbę kluczy partycji.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Ile kosztuje bazy danych Azure rozwiązania Cosmos
Aby uzyskać więcej informacji, zobacz toohello [Azure DB rozwiązania Cosmos szczegóły cennika](https://azure.microsoft.com/pricing/details/cosmos-db/) strony. Azure opłaty za użycie rozwiązania Cosmos bazy danych są określane przez hello liczbę kontenerów elastycznie, hello liczbę godzin kontenery hello były w trybie online i hello elastycznie przepływność dla każdego kontenera. termin Hello *kontenery* odnosi się tutaj toohello kolekcji interfejsu API usługi DocumentDB, wykres interfejsu API programu Graph API bazy danych MongoDB kolekcji i tabele tabeli interfejsu API. 

### <a name="is-a-free-account-available"></a>Jest dostępne bezpłatne konto?
W przypadku nowych tooAzure możesz zarejestrować się w celu [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/), które zapewnia 30 dni i i wszystkie tootry środki hello usług platformy Azure. Jeśli masz subskrypcję programu Visual Studio, przysługuje Ci również [kredytów systemu Azure w warstwie bezpłatna](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse z dowolnej usługi Azure. 

Można również użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toodevelop i testowania aplikacji lokalnie do zwolnienia, bez tworzenia subskrypcji platformy Azure. Po zakończeniu jak aplikacja działa na platformie hello Azure rozwiązania Cosmos DB emulatora, możesz przełączyć toousing konto bazy danych Azure rozwiązania Cosmos w chmurze hello.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Jak można uzyskać dodatkową pomoc dotyczącą bazy danych rozwiązania Cosmos Azure?
Jeśli potrzebujesz pomocy dotrzeć toous na [przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure-cosmosdb) lub hello [MSDN forum](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), lub zgodnie z harmonogramem Wykorzystaj rozmów z zespołu inżynieryjnego hello Azure DB rozwiązania Cosmos przez wysyłanie poczty zbyt[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Konfigurowanie bazy danych Azure rozwiązania Cosmos
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Jak tworzyć konta dla bazy danych rozwiązania Cosmos Azure?
Azure DB rozwiązania Cosmos jest dostępna w hello portalu Azure. Najpierw Utwórz subskrypcję platformy Azure. Po zarejestrowaniu się możesz dodać interfejs API usługi DocumentDB, interfejsu API programu Graph (wersja zapoznawcza), tabela interfejsu API (wersja zapoznawcza) lub bazy danych MongoDB API konta tooyour subskrypcji platformy Azure.

### <a name="what-is-a-master-key"></a>Co to jest klucz główny?
Klucz główny jest tooaccess tokenu zabezpieczeń wszystkich zasobów dla konta. Osób z kluczem hello ma zasobów tooall odczytu i zapisu w hello konta bazy danych. Podczas dystrybucji kluczy głównych należy zachować ostrożność. Witaj podstawowy klucz główny i pomocniczy klucz główny są dostępne na powitania **klucze** bloku hello [portalu Azure][azure-portal]. Aby uzyskać więcej informacji o kluczach, zobacz [wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>Co to są hello regionów, które można ustawić PreferredLocations? 
Witaj PreferredLocations wartość można ustawić tooany hello Azure regionów, w których są dostępne rozwiązania Cosmos bazy danych. Aby uzyskać listę dostępnych regionów, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>Czy jest coś I należy zwrócić uwagę podczas dystrybucję danych Witaj świecie za pośrednictwem hello centrach danych platformy Azure? 
Azure DB rozwiązania Cosmos jest obecny we wszystkich regionach platformy Azure, jak określono na powitania [regiony platformy Azure](https://azure.microsoft.com/regions/) strony. Co nowego centrum danych, ponieważ jest hello usługi podstawowej, ma obecności bazy danych Azure rozwiązania Cosmos. 

Po ustawieniu regionu, należy pamiętać, że bazy danych Azure rozwiązania Cosmos szanuje chmur suwerenne i dla instytucji rządowych. Oznacza to jeśli tworzysz konto w regionie suwerennych nie może replikować poza tym suwerennych regionie. Podobnie nie można włączyć replikacji w innych lokalizacjach suwerennych poza konta. 

## <a name="develop-against-hello-documentdb-api"></a>Opracowywanie przed hello interfejsu API usługi DocumentDB

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>Jak rozpocząć tworzenie oprogramowania dla hello interfejsu API usługi DocumentDB
Interfejs API usługi DocumentDB Microsoft jest dostępna w hello [portalu Azure][azure-portal]. Najpierw musisz zarejestrować subskrypcji platformy Azure. Po utworzeniu konta dla subskrypcji platformy Azure, możesz dodać interfejsu API usługi DocumentDB kontenera tooyour subskrypcji platformy Azure. Aby uzyskać instrukcje dotyczące dodawania konta bazy danych rozwiązania Cosmos platformy Azure, zobacz [Tworzenie konta bazy danych Azure DB rozwiązania Cosmos](create-documentdb-dotnet.md#create-account). Jeśli masz konto usługi DocumentDB w przeszłości hello masz teraz konto bazy danych Azure rozwiązania Cosmos. 

[Zestawy SDK](documentdb-sdk-dotnet.md) są dostępne dla języków .NET, Python, Node.js, JavaScript i Java. Deweloperzy mogą również używać hello [interfejsy API RESTful protokołu HTTP](/rest/api/documentdb/) toointeract z zasobami Azure DB rozwiązania Cosmos z różnych platform i języków.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>Można uzyskać dostęp do niektórych tooget gotowe do użycia przykłady ułatwiają rozpoczęcie?
Przykłady dotyczące interfejsu API usługi DocumentDB hello [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), i [Python](documentdb-python-samples.md) zestawów SDK są dostępne w serwisie GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Czy hello dane bez schematu obsługi bazy danych interfejsu API usługi DocumentDB?
Tak, hello interfejsu API usługi DocumentDB umożliwia aplikacji toostore dowolnych dokumentów JSON bez definicji schematu lub wskazówek. Dane są natychmiast dostępne dla zapytania dzięki interfejsowi zapytań hello Azure rozwiązania Cosmos bazy danych SQL.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Witaj interfejsu API usługi DocumentDB obsługuje transakcje ACID?
Tak, hello interfejsu API usługi DocumentDB obsługuje transakcje dla wielu dokumentów wyrażone jako procedury składowane JavaScript i wyzwalaczy. Transakcje są zakres tooa jednej partycji w ramach każdej kolekcji i wykonywane przy użyciu semantyki ACID jako "wszystkie lub żadne," odizolowana od innego współbieżnie wykonywanego kodu i żądań użytkownika. Jeśli istnieją wyjątki zgłaszane przez wykonanie po stronie serwera hello kodu aplikacji JavaScript, hello cała transakcja zostanie wycofana. Aby uzyskać więcej informacji na temat transakcji, zobacz [bazy danych programu transakcji](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Co to jest kolekcja?
Kolekcja jest grupą dokumentów i ich skojarzonej logiki aplikacji JavaScript. Kolekcja to płatna jednostka, gdzie hello [koszt](performance-levels.md) jest określana przez hello przepływności i użyto magazynu. Kolekcje mogą znajdować się na partycji lub serwerów i mogą być skalowane toohandle praktycznie nieograniczonej ilości magazynu lub przepływności.

Kolekcje są również jednostkami rozliczeniowymi powitania dla bazy danych Azure rozwiązania Cosmos. Każda kolekcja jest rozliczane godzinowo, oparta na powitania udostępnionej przepływności i używać miejsca do magazynowania. Aby uzyskać więcej informacji, zobacz [cennik usługi Azure rozwiązania Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Jak utworzyć bazę danych?
Bazy danych można tworzyć przy użyciu hello [portalu Azure](https://portal.azure.com), zgodnie z opisem w [dodania kolekcji](create-documentdb-dotnet.md#create-collection), jeden hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md), lub hello [interfejsów API REST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Jak skonfigurować użytkowników i uprawnienia?
Można utworzyć użytkowników i uprawnień przy użyciu jednej z hello [zestawów SDK interfejsu API DB rozwiązania Cosmos](documentdb-sdk-dotnet.md) lub hello [interfejsów API REST](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Witaj interfejsu API usługi DocumentDB obsługuje SQL?
język zapytań SQL Hello jest rozszerzonym podzbiorem funkcji zapytań hello obsługiwaną przez program SQL. Hello język zapytań SQL DB rozwiązania Cosmos Azure udostępnia sformatowanego hierarchiczna operatorów i rozszerzalność dzięki funkcji oparte na języku JavaScript, zdefiniowane przez użytkownika (UDF). Gramatyka JSON umożliwia modelowanie dokumentów JSON jako drzewa z etykietami węzły, które są używane zarówno przez techniki automatycznego indeksowania bazy danych Azure rozwiązania Cosmos hello i dialekt zapytań SQL hello Azure DB rozwiązania Cosmos. Informacje o używaniu gramatyki SQL, zobacz hello [QueryDocumentDB] [ query] artykułu.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Czy hello funkcje agregacji SQL obsługi interfejsu API usługi DocumentDB?
Witaj interfejsu API usługi DocumentDB obsługuje agregację małych opóźnieniach na dowolnym poziomie za pomocą funkcji agregujących `COUNT`, `MIN`, `MAX`, `AVG`, i `SUM` za pośrednictwem hello gramatyki SQL. Aby uzyskać więcej informacji, zobacz [funkcje agregujące](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>W jaki sposób hello interfejsu API usługi DocumentDB zapewnia współbieżność?
Witaj interfejsu API usługi DocumentDB obsługuje optymistycznej współbieżności sterowanie Współbieżnością za za pomocą tagów jednostki HTTP lub elementów ETag. Każdy zasób interfejsu API usługi DocumentDB ma element ETag i hello element ETag jest ustawiony na powitania serwera każdej aktualizacji dokumentu. nagłówek ETag Hello i bieżącą wartość hello są uwzględnione w wszystkie wiadomości odpowiedzi. Elementy etag można łączyć z hello If-Match nagłówka tooallow powitania serwera toodecide, czy zasób powinien zostać zaktualizowany. Witaj wartość If-Match jest toobe wartość ETag hello porównywane. Jeśli hello wartość ETag odpowiada powitania serwera wartość ETag, zasobów hello jest aktualizowana. Jeśli hello element ETag nie jest już aktualny, hello serwer odrzuca hello operację, podając "HTTP 412 niepowodzenie warunku wstępnego" Kod odpowiedzi. następnie powitania klienta pobiera ponownie hello zasobów tooacquire hello bieżącej wartości ETag dla zasobu hello. Ponadto elementy etag można z toodetermine nagłówka If-None-Match hello czy ponownie pobrać zasobu jest wymagana.

toouse optymistycznej współbieżności w programie .NET, użyj hello [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) klasy. Przykładowy .NET [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) w przykładowym DocumentManagement hello w witrynie GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Jak wykonywać transakcje w hello interfejsu API usługi DocumentDB?
Witaj interfejsu API usługi DocumentDB obsługuje transakcje zintegrowane z językiem za pomocą procedur składowanych JavaScript i wyzwalaczy. Wszystkie operacje bazy danych wewnątrz skryptów są wykonywane w ramach izolacji migawki. Jeśli jest to kolekcja jednej partycji, wykonanie hello jest toohello zakresami kolekcję. Jeśli kolekcja hello jest podzielona na partycje, wykonanie hello jest zakresem toodocuments z hello tę samą wartość klucza partycji w kolekcji hello. Migawka wersji dokumentów hello (elementy etag) jest podjęte na początku hello hello transakcji i zatwierdzone tylko wtedy, gdy hello skryptu zakończy się pomyślnie. Jeśli hello JavaScript zwraca błąd, hello transakcja zostanie wycofana. Aby uzyskać więcej informacji, zobacz [programowania w języku JavaScript po stronie serwera dla bazy danych Azure rozwiązania Cosmos](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Jak można I wstawiania zbiorczego dokumenty w bazie danych rozwiązania Cosmos?
Użytkownik może wstawiania zbiorczego dokumentów do bazy danych Azure rozwiązania Cosmos w jeden z dwóch sposobów:

* Witaj danych narzędzia migracji zgodnie z opisem w [narzędzie migracji bazy danych dla bazy danych Azure rozwiązania Cosmos](import-data.md).
* Procedury składowane, zgodnie z opisem w [programowania w języku JavaScript po stronie serwera dla bazy danych Azure rozwiązania Cosmos](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Witaj interfejsu API usługi DocumentDB obsługuje buforowanie linków zasobów?
Tak, ponieważ bazy danych rozwiązania Cosmos Azure jest usługą RESTful, linki zasobów są niezmienne i mogą być buforowane. Klienci usługi DocumentDB interfejsu API można określić nagłówek "If-None-Match" dla odczytów względem dowolnego zasobu typu dokumentu lub kolekcji, a następnie zaktualizuj ich lokalne kopie, po zmianie hello wersji serwera.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>Jest dostępne lokalne wystąpienie interfejsu API usługi DocumentDB?
Tak. Witaj [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) zapewnia emulację o wysokiej wierności hello rozwiązania Cosmos bazy danych usługi. Obsługuje funkcje, które są identyczne tooAzure rozwiązania Cosmos bazy danych, w tym obsługa tworzenia i badania dokumentów JSON, inicjowania obsługi administracyjnej i skalowanie kolekcje i wykonywania procedury składowane i wyzwalaczy. Mogą tworzyć i testować aplikacje przy użyciu hello Azure rozwiązania Cosmos DB emulatora i wdrażać je tooAzure w skali globalnej, tworząc pojedynczą konfiguracją zmienić toohello punktu końcowego połączenia dla bazy danych Azure rozwiązania Cosmos.

## <a name="develop-against-hello-api-for-mongodb"></a>Tworzenie przed hello interfejsu API dla bazy danych MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>Co to jest hello Azure rozwiązania Cosmos DB API bazy danych mongodb?
Hello Azure rozwiązania Cosmos DB API bazy danych mongodb jest warstwy zgodności, która umożliwia tooeasily aplikacji i niewidocznie komunikacji z hello natywnego aparatu bazy danych DB rozwiązania Cosmos Azure za pomocą istniejących, obsługiwane społeczności Apache bazy danych MongoDB z interfejsów API i sterowników. Deweloperzy mogą teraz używać bazy danych MongoDB narzędzie łańcuchów i umiejętności toobuild aplikacji korzystających z bazy danych Azure rozwiązania Cosmos. Deweloperom korzystać z hello unikatowych możliwości bazy danych rozwiązania Cosmos platformy Azure, w tym obsługi automatycznego indeksowania, tworzenia kopii zapasowej, umów dotyczących poziomu finansowo kopii zapasowej usług (SLA) i tak dalej.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Jak połączyć toomy interfejsu API dla bazy danych MongoDB?
Witaj najszybszy sposób toohello tooconnect interfejsu API Azure rozwiązania Cosmos bazy danych dla bazy danych MongoDB umieszczeniu toohello toohead [portalu Azure](https://portal.azure.com). Przejdź tooyour konta, a następnie w menu nawigacji po lewej stronie powitania kliknij **Szybki Start**. Szybki Start jest hello najlepsze sposób tooget kodu wstawki tooconnect tooyour bazy danych. 

Azure DB rozwiązania Cosmos wymusza wymogi ograniczeniami zabezpieczeń. Azure DB rozwiązania Cosmos kont wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem protokołu SSL, dlatego należy się toouse TLSv1.2.

Aby uzyskać więcej informacji, zobacz [połączenia interfejsu API tooyour dla bazy danych MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Czy istnieją dodatkowe kody błędów dla interfejsu API dla bazy danych MongoDB?
W dodatku toohello wspólnej bazy danych MongoDB kody błędów hello API bazy danych MongoDB ma własne kody błędu:


| Błąd               | Kod  | Opis  | Rozwiązanie  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | Całkowita liczba zużywane jednostki żądania Hello przekroczył wskaźnik elastycznie jednostka żądania hello hello kolekcji i został ograniczony. | Należy wziąć pod uwagę skalowanie hello przepływność kolekcji hello z hello portalu Azure lub podjęciem ponownej próby. |
| ExceededMemoryLimit | 16501 | Jako usługę wielodostępną hello operacja przekroczyła przydział pamięci powitania klienta. | Zmniejsz zakres hello hello operacji przy użyciu bardziej restrykcyjnego zapytania kryteria lub skontaktuj się z wsparciem hello [portalu Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Przykład:  *&nbsp; &nbsp; &nbsp; &nbsp;db.getCollection('users').aggregate ([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {Nazwa: "Adama"}}, <br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;{$sort: {wieku: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Opracowywania hello tabeli interfejsu API (wersja zapoznawcza)

### <a name="terms"></a>Warunki 
Hello Azure DB rozwiązania Cosmos: Tabela interfejsu API (wersja zapoznawcza) odwołuje się toohello premium oferty Azure DB rozwiązania Cosmos obsługi tabeli ogłoszenia na 2017 kompilacji. 

Tabela standardowe Hello zestawu SDK jest hello istniejącej tabeli magazynu Azure SDK. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Jak używać hello nową ofertę tabeli interfejsu API (wersja zapoznawcza)? 
Witaj interfejsu API Azure rozwiązania Cosmos DB tabeli są dostępne w hello [portalu Azure][azure-portal]. Najpierw musisz zarejestrować subskrypcji platformy Azure. Po zarejestrowaniu się możesz dodać interfejsu API Azure rozwiązania Cosmos DB tabeli tooyour konta subskrypcji platformy Azure, a następnie dodaj konto tooyour tabel. 

W okresie Podgląd hello podczas [zestawów SDK](../cosmos-db/table-sdk-dotnet.md) są dostępne dla platformy .NET, możesz rozpocząć pracę, wykonując hello [API tabeli](../cosmos-db/create-table-dotnet.md) artykułu szybki start.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>Należy nowego zestawu SDK toouse hello tabeli interfejsu API (wersja zapoznawcza)? 
Tak, hello [tabeli Premium magazynu systemu Windows Azure (wersja zapoznawcza) zestawu SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) jest dostępna w NuGet. Dodatkowe informacje są dostępne na powitania [interfejsu API Azure rozwiązania Cosmos DB tabeli .NET: Pobierz i informacje o wersji](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) strony. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Jak zgłosić opinię o hello zestawu SDK lub usterki?
Można udostępniać swoją opinię w żadnym hello następujące sposoby:

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Forum MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Witryna Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Co to jest hello parametry połączenia, czy potrzebuję toouse tooconnect toohello tabeli interfejsu API (wersja zapoznawcza)?
ciąg połączenia Hello jest:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Parametry połączenia hello można uzyskać ze strony klucze hello w hello portalu Azure. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Jak zastąpić ustawienia konfiguracji hello opcje żądania hello hello nowej tabeli interfejsu API (wersja zapoznawcza)?
Aby uzyskać informacje o ustawieniach konfiguracji, zobacz [możliwości bazy danych Azure rozwiązania Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Możesz zmienić ustawienia hello przez dodanie ich tooapp.config w sekcji appSettings hello powitania klienta aplikacji.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Dla klientów korzystających z istniejącej tabeli Standardowy zestaw SDK hello są wszystkie zmiany?
Brak. Brak zmian dla istniejących lub nowych klientów, którzy korzystają z hello istniejącej tabeli standardowego zestawu SDK. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Jak wyświetlić tabeli danych przechowywanych w usłudze Azure DB rozwiązania Cosmos do użytku z hello tabeli interfejsu API (Przegląd)? 
Można użyć hello Azure toobrowse portalu hello danych. Umożliwia także hello kodu interfejsu API tabeli (wersja zapoznawcza) lub narzędzi hello wspomnianego hello dalej odpowiedzi. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Narzędzia współpracuje z hello tabeli interfejsu API (wersja zapoznawcza)? 
Można użyć starszej wersji hello Azure Eksploratora (0.8.9).

Narzędzia z tootake elastyczność hello, które parametry połączenia w formacie hello określony wcześniej może obsługiwać hello nowy interfejs API tabeli (wersja zapoznawcza). Lista narzędzi tabeli są przekazywane w hello [narzędzi klienta magazynu Azure](../storage/common/storage-explorers.md) strony. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>Programu PowerShell lub interfejsu wiersza polecenia Azure działają z hello nowej tabeli interfejsu API (wersja zapoznawcza)?
Planujemy tooadd obsługę programu PowerShell i interfejsu wiersza polecenia Azure dla tabeli interfejsu API (wersja zapoznawcza). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>Jest hello współbieżności na operacje kontrolowane?
Tak, optymistycznej współbieżności zostaną przekazane za pośrednictwem hello użycie mechanizmu hello ETag. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>Czy hello model zapytań OData jest obsługiwane dla jednostek? 
Tak, hello tabeli interfejsu API (wersja zapoznawcza) obsługuje zapytania OData i zapytań LINQ. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>Można połączyć toohello standardowe tabeli platformy Azure i hello premium nowej tabeli API (wersja zapoznawcza) obok siebie w hello tej samej aplikacji? 
Tak, możesz połączyć przez utworzenie dwóch osobnych wystąpień hello CloudTableClient każdego wskazanie tooits własny identyfikator URI przy użyciu parametrów połączenia hello.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Jak przeprowadzić migrację istniejących tabel Azure magazynu aplikacji toothis nową ofertę?
Zaletą tootake hello nową ofertę tabeli interfejsu API w istniejącej tabeli magazynu danych, skontaktuj się z [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Co to jest plan powitania dla tej usługi, a kiedy zostanie oferujesz innych standardowych funkcji API tabeli?
Planujemy tooadd obsługę SAS tokenów, ServiceContext, statystykę, klienta szyfrowania po stronie, analizy i inne funkcje, jak możemy kontynuować kierunku po Użytkownik może Prześlij nam opinię na temat [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>W jaki sposób rozszerzania rozmiaru magazynu hello zrobić dla tej usługi, jeśli na przykład uruchomić z  *n*  GB danych i danych wzrośnie too1 TB wraz z upływem czasu? 
Azure DB rozwiązania Cosmos jest zaprojektowana tooprovide nieograniczony magazyn wykorzystaniem hello skalowanie w poziomie. Usługa Hello można monitorować i skutecznie zwiększyć magazynu. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Jak monitorować hello oferty tabeli interfejsu API (wersja zapoznawcza)?
Można użyć hello tabeli interfejsu API (wersja zapoznawcza) **metryki** okienko toomonitor żądań i wykorzystania magazynu. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>Sposób obliczania hello przepływności, który potrzebuję?
Możesz użyć hello pojemności narzędzia do szacowania toocalculate hello TableThroughput, które są wymagane dla operacji hello. Aby uzyskać więcej informacji, zobacz [szacowania jednostek żądania i przechowywanie danych](https://www.documentdb.com/capacityplanner). Ogólnie rzecz biorąc można reprezentować jednostki jako JSON i podaj numery hello operacje. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>Można użyć hello nowej tabeli interfejsu API zestawu SDK lokalnie w emulatorze hello (wersja zapoznawcza)?
Tak, można użyć hello tabeli interfejsu API (wersja zapoznawcza) z emulatora lokalne powitania korzystając z hello nowego zestawu SDK. Nowy emulator toodownload, przejdź zbyt[Użyj hello Azure rozwiązania Cosmos DB emulatora dla lokalnych projektowania i testowania](local-emulator.md). Witaj wartość StorageConnectionString w pliku app.config musi toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>Moja aplikacja istniejących może współpracować z hello tabeli interfejsu API (wersja zapoznawcza)? 
Witaj powierzchni hello nowy interfejs API tabeli (wersja zapoznawcza) jest zgodna z hello istniejącej tabeli standardowe platformy Azure SDK między hello tworzenie, usuwanie, aktualizowanie i zapytania operacje w hello interfejs API .NET. Upewnij się, czy masz klucz wiersza, ponieważ wymaga hello tabeli interfejsu API (wersja zapoznawcza), zarówno klucz partycji i klucz wiersza. Możemy również zaplanować tooadd więcej Obsługa zestawu SDK, jak możemy kontynuować kierunku GA tej oferty usługi.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>Należy toomigrate Mój istniejący toohello Azure aplikacji opartych na tabeli nowego zestawu SDK, jeśli nie chcesz toouse hello tabeli interfejsu API (wersja zapoznawcza) funkcje?
Nie można tworzyć i używać istniejących zasobów standardowej tabeli bez przeszkód dowolnego rodzaju. Jednak jeśli nie używasz hello nowej tabeli interfejsu API (wersja zapoznawcza), nie mogą korzystać z indeksu automatyczne hello, hello spójności dodatkowych opcji lub globalnego dystrybucji. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Jak dodać replikacji hello danych w warstwie premium hello tabeli interfejsu API (wersja zapoznawcza) w wielu regionach platformy Azure?
Przy użyciu portalu Azure DB rozwiązania Cosmos hello [ustawienia globalne replikacji](tutorial-global-distribution-documentdb.md#portal) tooadd regionów, które są odpowiednie dla twojej aplikacji. toodevelop aplikacji globalnie rozproszone, należy również dodać do aplikacji z hello PreferredLocation informacji zestawu toohello lokalny region zapewniające małych opóźnieniach odczytu. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Jak zmienić regionu podstawowego zapisu hello hello konta w warstwie premium hello tabeli interfejsu API (wersja zapoznawcza)?
Można użyć hello Azure DB rozwiązania Cosmos globalnej replikacji okienku portalu tooadd regionu i następnie przełączyć toohello wymagany region. Aby uzyskać instrukcje, zobacz [programowania z użyciem konta bazy danych Azure rozwiązania Cosmos w przypadku](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Jak skonfigurować Moje preferowanych regionów odczytu dla małych opóźnień I dystrybucji danych? 
w pliku app.config hello toohelp odczytywać hello lokalizacji lokalnej, za pomocą klawisza PreferredLocation hello. Istniejących aplikacji hello tabeli interfejsu API (wersja zapoznawcza) zgłasza błąd, jeśli ustawiono LocationMode. Ten kod, należy usunąć, ponieważ hello premium tabeli interfejsu API (wersja zapoznawcza) przejmuje te informacje z pliku app.config hello. Aby uzyskać więcej informacji, zobacz [możliwości bazy danych Azure rozwiązania Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Jak należy traktować poziomów spójności w hello tabeli interfejsu API (wersja zapoznawcza)? 
Azure DB rozwiązania Cosmos zapewnia dobrze uzasadnione kompromis między spójności, dostępnością i opóźnieniem. Azure DB rozwiązania Cosmos oferuje pięć poziomów spójności tooTable deweloperzy interfejsu API (wersja zapoznawcza), aby można było wybrać hello model prawo spójności na poziomie tabeli hello i tworzenie pojedynczych żądania podczas badania hello danych. Gdy klient nawiąże połączenie, może określać poziomu spójności. Można zmienić poziom hello za pośrednictwem hello app.config ustawienie dla wartości hello hello TableConsistencyLevel klucza. 

małe opóźnienia odczytuje z "odczytać własne zapisy" z spójność sesji jako domyślny hello zawiera Hello tabeli interfejsu API (wersja zapoznawcza). Aby uzyskać więcej informacji, zobacz [poziomy spójności](consistency-levels.md). 

Domyślnie Magazyn tabel Azure zapewnia wysoki poziom spójności w ramach regionu i spójność Eventual hello dodatkowej lokalizacji. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Bazy danych rozwiązania Cosmos Azure oferuje więcej poziomów spójności niż standardowe tabele?
Tak, aby dowiedzieć się, jak rozkład toobenefit z hello rodzaj bazy danych rozwiązania Cosmos platformy Azure, zobacz [poziomy spójności](consistency-levels.md). Ponieważ dla poziomy spójności hello podano gwarancji, można używać ich bez obaw. Aby uzyskać więcej informacji, zobacz [możliwości bazy danych Azure rozwiązania Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>Po włączeniu globalne dystrybucji, jak długo trwa tooreplicate hello danych?
Możemy przekazać danych hello trwałym w regionie lokalne powitania i push hello tooother obszarów danych natychmiast kwestią w milisekundach. Replikacja jest zależne tylko od czasu Rundy hello (RTT) hello centrum danych. toolearn więcej informacji na temat możliwości globalnego dystrybucji hello Azure rozwiązania Cosmos bazy danych, zobacz [bazy danych Azure rozwiązania Cosmos: globalnie rozproszoną bazę danych usługi Azure](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Można zmienić poziomu spójności żądanie odczytu hello?
Z bazy danych rozwiązania Cosmos platformy Azure można ustawić poziomu spójności hello na poziomie kontenera hello (na powitania tabeli). Za pomocą hello zestawu SDK, można zmienić poziom hello, podając wartość hello TableConsistencyLevel klucz w pliku app.config hello. Witaj możliwe wartości to: silne, ograniczone nieaktualności sesji, prefiks spójne i Eventual. Aby uzyskać więcej informacji, zobacz [danych dostosowywalne poziomy spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md). pomysł klucza Hello jest, że nie można ustawić spójności żądania hello poziomu więcej niż ustawienie hello hello tabeli. Na przykład nie można ustawić poziom spójności hello tabeli hello na Eventual i spójności żądania hello na silne. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Jak konta tabeli interfejsu API (wersja zapoznawcza) w wersji premium hello obsługuje tryb failover Jeśli region przestanie działać? 
Hello premium tabeli interfejsu API (wersja zapoznawcza) obiektowy hello globalnie rozproszone platformy Azure DB rozwiązania Cosmos. tooensure, że aplikacja może tolerować przestojami centrum danych, Włącz co najmniej jeden region więcej hello konta w portalu Azure DB rozwiązania Cosmos hello [programowania z użyciem konta bazy danych Azure rozwiązania Cosmos w przypadku](regional-failover.md). Można ustawić priorytet hello regionu hello przy użyciu portalu hello [programowania z użyciem konta bazy danych Azure rozwiązania Cosmos w przypadku](regional-failover.md). 

Możesz dodać dowolną liczbę regionów, jak dla konta hello i kontrolować, gdzie można przełączyć tooby dostarczanie priorytet trybu failover. Oczywiście toouse hello bazy danych, należy tooprovide aplikacji istnieje zbyt. Jeśli tak zrobisz, klienci nie wystąpi Przestój. powitania klienta SDK zostanie automatycznie homing. Oznacza to, że może wykryć regionu hello jest wyłączony i automatycznie w tryb failover toohello nowego regionu.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Premium hello tabeli interfejsu API (wersja zapoznawcza) jest włączona dla kopii zapasowych?
Tak, hello premium tabeli interfejsu API (wersja zapoznawcza) obiektowy hello platformy Azure DB rozwiązania Cosmos kopii zapasowych. Kopie zapasowe są wykonywane automatycznie. Aby uzyskać więcej informacji, zobacz [Online kopii zapasowej i przywracania bazy danych Azure rozwiązania Cosmos](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Powoduje hello tabeli interfejsu API (wersja zapoznawcza) indeksowania wszystkie atrybuty obiektu domyślnie
Tak, wszystkie atrybuty obiektu jest indeksowana domyślnie. Aby uzyskać więcej informacji, zobacz [bazy danych Azure rozwiązania Cosmos: zasady indeksowania](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Oznacza to, że jest nie ma toocreate wiele indeksów toosatisfy hello zapytania? 
Tak, bazy danych rozwiązania Cosmos Azure zapewnia automatyczne indeksowanie wszystkie atrybuty bez żadnych definicji schematu. Ta Automatyzacja zwalnia toofocus deweloperzy aplikacji hello, a nie na tworzenie indeksu i zarządzanie nimi. Aby uzyskać więcej informacji, zobacz [bazy danych Azure rozwiązania Cosmos: zasady indeksowania](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>Czy można zmienić zasady indeksowania hello?
Tak, można zmienić zasady indeksowania hello zapewniając hello definicję indeksu. Aby uzyskać więcej informacji, zobacz [możliwości bazy danych Azure rozwiązania Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Należy tooproperly kodowania i wprowadzić ustawienia hello. 

W formacie json ciąg w pliku app.config hello:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Azure DB rozwiązania Cosmos jako platforma prawdopodobnie toohave wiele możliwości, takie jak sortowanie, agregacje, hierarchii oraz innych funkcji. Będzie można dodanie tych możliwości toohello API tabeli? 
W wersji zapoznawczej, hello tabeli interfejs API udostępnia hello zapytania takie same funkcje co magazyn tabel Azure. Azure DB rozwiązania Cosmos obsługuje również sortowanie, agregacje, dane geograficzne zapytania hierarchii i szeroki zakres funkcji wbudowanych. Firma Microsoft udostępni dodatkowe funkcje w hello tabeli interfejsu API w przyszłej aktualizacji. Aby uzyskać więcej informacji, zobacz [kwerendy SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Podczas zmiany TableThroughput dla hello tabeli interfejsu API (wersja zapoznawcza)?
Należy zmienić TableThroughput, gdy hello następujące warunki mają zastosowanie:
* Przeprowadzasz wyodrębniania, przekształcania i ładowania (ETL) dane lub ma tooupload dużą ilość danych w krótkim czasie. 
* Potrzebujesz więcej przepustowości z kontenera hello na powitania zaplecza. Na przykład zobacz przepływności hello używany jest większa niż hello udostępnionej przepływności, czy możesz są pobierania ograniczane. Aby uzyskać więcej informacji, zobacz [przepływności zestawu dla kontenerów bazy danych Azure rozwiązania Cosmos](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>Można skalować lub dół hello przepływność tabeli tabeli interfejsu API (wersja zapoznawcza)? 
Tak, można użyć portalu Azure DB rozwiązania Cosmos hello skali okienku tooscale hello przepływności. Aby uzyskać więcej informacji, zobacz [przepływności zestawu](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Jest domyślnie ustawione dla nowo aprowizowanej tabel TableThroughput?
Tak, jeśli nie zastępują hello TableThroughput przy użyciu pliku app.config i nie należy używać kontenera utworzone wcześniej w usłudze Azure DB rozwiązania Cosmos usługi hello tworzy tabelę z przepływności 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>Istnieje już zmiany ceny dla istniejących klientów usługi interfejsu API hello standardowe tabeli?
Brak. Nie została zmieniona w cenie dla istniejących klientów usługi interfejsu API tabeli standardowa. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Jak cen hello jest obliczana dla hello tabeli interfejsu API (wersja zapoznawcza) 
Cena Hello zależy od hello przydzielone TableThroughput. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Jak obsługiwać żadnych ograniczania przepustowości w tabelach hello w tabeli interfejsu API (wersja zapoznawcza) oferty 
Współczynnik żądań hello przekracza pojemność hello hello udostępnionej przepływności dla kontenera podstawowej hello, wystąpi błąd i hello SDK ponowi próbę wywołania hello, stosując zasady ponawiania hello.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Dlaczego muszę toochoose przepływności oprócz PartitionKey i RowKey korzyści tootake hello premium tabeli interfejsu API (wersja zapoznawcza) oferty Azure DB rozwiązania Cosmos?
Azure DB rozwiązania Cosmos ustawia przepływności domyślnego kontenera sieci, jeśli nie zostanie określona w pliku app.config hello. 

Azure DB rozwiązania Cosmos zapewnia gwarancje wydajność i opóźnienia z górne granice operacji. Gwarancja jest możliwe, gdy aparat hello można wymusić ładu na operacje hello dzierżawy. Ustawienie TableThroughput zapewnia uzyskanie hello gwarantowanej przepustowości i opóźnień, ponieważ platforma hello rezerwuje tej pojemności i gwarantuje operacyjne Powodzenie. 

Przy użyciu specyfikacji przepływności hello, można elastycznie zmienić toobenefit sezonowości hello aplikacji, przepływności hello potrzeb i ograniczenia kosztów.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Zestawu SDK usługi Magazyn Azure została niedrogie dla mnie, ponieważ I Zapłać tylko toostore hello dane, a rzadko zapytania. Hello nową ofertę bazy danych Azure rozwiązania Cosmos jest prawdopodobnie toobe ładowania mnie, nawet jeśli nie ma I wykonać jednej transakcji lub niczego przechowywane. Sprawdź jakie?

Azure DB rozwiązania Cosmos jest zaprojektowana toobe globalnie rozproszone, na podstawie umowy SLA systemu z gwarancją dostępności, opóźnienia i przepływności. Podczas rezerwowania przepustowości w usłudze Azure DB rozwiązania Cosmos gwarantowane, w odróżnieniu od przepustowości hello innych systemów. Azure DB rozwiązania Cosmos zapewnia dodatkowe funkcje, które żądane klientów, takie jak indeksów pomocniczych i dystrybucji globalnego. W okresie Podgląd hello udostępniamy modelu zoptymalizowanych pod kątem przepływności i po pewnym czasie planujemy tooprovide toomeet storage zoptymalizowana modelu potrzeby klientów. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Nigdy nie pojawia się powiadomienie "przydział pełna" (co oznacza, że partycji jest pełny) po pozyskiwania danych do magazynu tabel. Z hello tabeli interfejsu API (wersja zapoznawcza) I ten komunikat. Jest to oferta ograniczenie mnie i wymuszanie mnie toochange mojej istniejącej aplikacji?

Azure DB rozwiązania Cosmos jest system na podstawie umowy SLA zawiera nieograniczone skali gwarancje opóźnień, przepustowości, dostępności i spójności. tooensure gwarantowane wydajności premium, upewnij się, że rozmiar danych i indeks są łatwe w zarządzaniu i skalowalność. limit 10 GB Hello hello liczby jednostek lub elementów na klucz partycji to tooensure czy udostępniamy doskonałą wydajność wyszukiwania i zapytania. tooensure, która aplikacja może obsłużyć dobrze nawet w przypadku usługi Azure Storage, zalecamy, aby użytkownik *nie* utworzyć partycję gorących wszystkie informacje są przechowywane w jednej partycji i badając ją. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>Dzięki PartitionKey i RowKey są nadal wymagane z hello nowy interfejs API tabeli (wersja zapoznawcza)? 
Tak. Ponieważ hello powierzchni hello tabeli interfejsu API (wersja zapoznawcza) jest podobne toothat z hello magazynu tabel zestawu SDK, klucz partycji hello zapewnia danych hello toodistribute wydajny sposób. klucz wiersza Hello jest unikatowy w ramach tej partycji. Witaj obecny toobe potrzeb klucza wiersza i nie może mieć wartości null jako w hello standardowego zestawu SDK. Długość Hello RowKey wynosi 255 bajtów i długość hello PartitionKey wynosi 100 bajtów (wkrótce toobe zwiększyć too1 KB). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Co to są hello komunikaty o błędach dla hello tabeli interfejsu API (wersja zapoznawcza)?
Ta wersja zapoznawcza jest niezgodna z tabelą standardowe hello, większość błędów hello przypisze toohello błędy hello standardowej tabeli. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Dlaczego I pobrać ograniczany podczas toocreate wiele tabel jeden po drugim hello tabeli interfejsu API (wersja zapoznawcza)?
Azure DB rozwiązania Cosmos jest system na podstawie umowy SLA zawiera czas oczekiwania, przepływności i dostępności gwarancje spójności. Ponieważ jest inicjowana systemu zastrzega sobie tooguarantee zasobów tych wymagań. Wykryto Hello szybkość szybkie tworzenie tabel i ograniczany. Firma Microsoft zaleca przyjrzeć się hello częstotliwość tworzenia tabel i obniżyć go tooless niż 5 na minutę. Należy pamiętać, że tego hello tabeli interfejsu API (wersja zapoznawcza) jest inicjowana systemu. obecnie Hello go udostępnić, zostanie rozpoczęta toopay dla niego. 

## <a name="develop-against-hello-graph-api-preview"></a>Opracowywanie przed hello interfejsu API programu Graph (wersja zapoznawcza)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Jak można stosować funkcje hello tooAzure interfejsu API programu Graph (wersja zapoznawcza) DB rozwiązania Cosmos
Umożliwia rozszerzenie biblioteki tooapply hello funkcje interfejsu API programu Graph (wersja zapoznawcza). Ta biblioteka jest nazywana Microsoft Azure wykresy, i jest dostępny na NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Wygląda na to, obsługuje hello Gremlin wykres przechodzenie języka. Czy firma planuje tooadd więcej formularzy zapytania?
Tak, planujemy tooadd innych mechanizmów dla zapytania w przyszłości hello. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Jak używać hello nową ofertę interfejsu API programu Graph (wersja zapoznawcza)? 
hello pełną, wprowadzenie tooget [interfejsu API programu Graph](../cosmos-db/create-graph-dotnet.md) artykułu szybki start.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Pytania klientów usługi DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Dlaczego należy przenieść tooAzure DB rozwiązania Cosmos? 

Azure DB rozwiązania Cosmos jest dalej przestępnego big hello w rozproszonych globalnie, baz danych z chmury na dużą skalę. Jako klient usługi DocumentDB masz teraz dostęp toohello przełomowe systemu i możliwości oferowane przez bazy danych Azure rozwiązania Cosmos.

Azure DB rozwiązania Cosmos jest uruchomiona jako usługa "Projektu Florencji" w 2010 tooaddress hello słabe punkty napotykają deweloperom tworzenie aplikacji na dużą skalę w firmie Microsoft. wyzwania Hello tworzenia globalnie rozproszone aplikacje nie są unikatowe tooMicrosoft, więc firma Microsoft dostępnych hello pierwszej generacji tej technologii w 2015 tooAzure deweloperów w formie hello Azure DocumentDB. 

Od tego czasu dodane nowe funkcje i wprowadzono istotne nowe funkcje. Azure DB rozwiązania Cosmos jest wynikiem hello. W ramach tej wersji, klienci usługi DocumentDB, z danymi, automatycznie i bezproblemowo stają się klientów z bazy danych Azure rozwiązania Cosmos. Te możliwości są w obszarach hello hello core aparatu bazy danych, a także dystrybucji globalne, elastyczną skalowalność i branży, kompleksowe umów SLA. W szczególności usprawnionych firma Microsoft hello Azure DB rozwiązania Cosmos bazy danych aparatu tooefficiently mapy wszystkie modeli danych popularnych systemów typu i interfejsów API toohello właściwego modelu danych z bazy danych Azure rozwiązania Cosmos. 

Witaj bieżącego reprezentację developer uwzględniającym tej pracy jest hello nowa funkcja obsługi [Gremlin](../cosmos-db/graph-introduction.md) i [tabeli interfejsów API magazynu](../cosmos-db/table-introduction.md). I to tylko hello początku. Planujemy tooadd innych popularnych interfejsów API i nowszych modelach danych w czasie z więcej poprawę wydajności i magazynu w skali globalnej. 

Jest ważne toopoint się, że hello DocumentDB [dialekt SQL](../documentdb/documentdb-sql-query.md) zawsze odbywało się co najmniej jeden hello wiele interfejsów API tego hello podstawowej bazy danych rozwiązania Cosmos Azure może obsługiwać. Dla deweloperów korzystających z pełni zarządzana usługa, takie jak bazy danych Azure rozwiązania Cosmos hello tylko interfejs toohello usługa jest hello interfejsów API, które są udostępniane przez usługę hello. Naprawdę żadne zmiany dla istniejących klientów usługi DocumentDB. W usłudze Azure DB rozwiązania Cosmos możesz uzyskać dokładnie powitalne oferuje SQL tego samego interfejsu API tej usługi DocumentDB. Teraz (i w przyszłości hello) można uzyskać dostęp innych funkcji wcześniej niedostępny 

Inny reprezentację naszych ciągłość pracy jest hello rozszerzony podstawę globalne i elastyczną skalowalność przepływność i magazyn. Wprowadzono kilka ulepszeń podstawowych toohello globalne dystrybucji podsystemu. Jedną z hello hello spójne prefiksu spójności modelu, który sprawia, że całkowita pięć modeli spójności dobrze zdefiniowany jest wiele takich funkcji uwzględniającym dla deweloperów. Firma Microsoft opublikuje wiele możliwości bardziej interesujące ich. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>Czego potrzebuję tooensure toodo, że zasoby usługi DocumentDB nadal toorun dla bazy danych rozwiązania Cosmos Azure?

Należy toomake żadnych zmian w ogóle. Zasoby usługi DocumentDB są teraz zasobów bazy danych Azure rozwiązania Cosmos, i nie było żadnych przerwy w działaniu hello usługi podczas przenoszenia tego wystąpienia.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>Zmiany są potrzebne toomake toowork mojej aplikacji z bazy danych rozwiązania Cosmos Azure?

Nie ma żadnych toomake zmiany. Nie zmieniono nazw klas, obszary nazw i NuGet w pakiecie. Zawsze firma Microsoft zaleca zachowywanie z zestawów SDK się toodate tootake zaletą hello najnowsze funkcje i ulepszenia. 

### <a name="whats-changed-in-hello-azure-portal"></a>Co się zmieniło w portalu Azure hello?

Usługa DocumentDB nie jest już widoczna w portalu hello jako usługi Azure. W tym miejscu jest nową ikonę bazy danych Azure rozwiązania Cosmos, pokazane na powitania po obrazu. Dostępnych wszystkich kolekcji, które znajdowały się przed i nadal można skalować przepływność, Zmień poziomy spójności i monitora umów SLA. zostały rozszerzone możliwości Hello Eksploratora danych (wersja zapoznawcza). Można teraz wyświetlać i edycji dokumentów, tworzenie i uruchamianie zapytań i pracować z procedur składowanych, wyzwalaczy i funkcji zdefiniowanej przez użytkownika z jednej strony, jak pokazano w powitania po obrazu: 

![Blok Azure rozwiązania Cosmos DB kolekcje Hello](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Czy istnieją toopricing zmiany?

Nie, kosztów hello uruchamiania aplikacji dla bazy danych Azure rozwiązania Cosmos jest hello sam sprzed.

### <a name="are-there-changes-toohello-slas"></a>Czy istnieją zmiany toohello umów SLA?

Nie, hello umowy SLA dla dostępności, spójności, opóźnienia i przepływności nie uległy zmianie i wciąż są wyświetlane w portalu hello. Aby uzyskać więcej informacji, zobacz [umowy SLA dla bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![Zadania do wykonania aplikacji z przykładowymi danymi](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
