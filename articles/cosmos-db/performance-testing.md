---
title: "aaaAzure DB rozwiązania Cosmos skali i testowania wydajności | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować tooperform i testowania wydajności z bazy danych Azure rozwiązania Cosmos"
keywords: "Testowanie wydajności"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Wydajność i skalę testowania z bazy danych Azure rozwiązania Cosmos
Skala testowanie wydajności i jest klucza krok w rozwoju aplikacji. Dla wielu aplikacji hello warstwy bazy danych ma znaczący wpływ na hello ogólną wydajność i skalowalność i w związku z tym składnikiem krytycznym wydajności testuje. [Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest dedykowanym elastycznego skalowania przewidywalną wydajność i w związku z tym stanowi doskonałe dopasowanie dla aplikacji, które wymagają warstwy wysokiej wydajności bazy danych. 

W tym artykule jest odwołaniem dla deweloperów wykonania testów wydajności dla obciążeń DB rozwiązania Cosmos lub obliczenia DB rozwiązania Cosmos w scenariuszach wysokiej wydajności aplikacji. Skupiono się głównie na testowania wydajności izolowanego hello bazy danych, ale zawiera również najlepsze rozwiązania dotyczące aplikacji produkcyjnych.

Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:   

* Gdzie mogę znaleźć przykładowej aplikacji .NET klienta do testowania wydajności DB rozwiązania Cosmos 
* Jak osiągnięcia wysokiej przepływności poziomy DB rozwiązania Cosmos z mojej aplikacji klienta?

tooget wprowadzenie kodu, Pobierz hello projektu z [próbka testowania wydajności bazy danych rozwiązania Cosmos Azure](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> Celem tej aplikacji Hello jest toodemonstrate najlepsze rozwiązania dotyczące wyodrębniania lepszą wydajność poza DB rozwiązania Cosmos o niewielkiej liczby komputerów klienckich. Nie przeprowadzono toodemonstrate hello szczytu pojemności hello usługi, które można skalować nieograniczony.
> 
> 

Jeśli szukasz tooimprove opcje konfiguracji po stronie klienta DB rozwiązania Cosmos wydajności, zobacz [porady dotyczące wydajności bazy danych Azure rozwiązania Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Uruchom testowanie aplikacji hello wydajności
Witaj najszybszy sposób tooget uruchomiona jest toocompile i wykonywania hello .NET przykładowa poniżej, zgodnie z opisem w poniższych krokach hello. Można również przejrzeć kod źródłowy hello i wdrożenia podobnych konfiguracji tooyour klienta własnych aplikacji.

**Krok 1:** pobierania hello projektu z [próbka testowania wydajności bazy danych rozwiązania Cosmos Azure](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), lub repozytorium GitHub hello rozwidlenia.

**Krok 2:** zmodyfikować ustawienia hello EndpointUrl i AuthorizationKey, CollectionThroughput DocumentTemplate (opcjonalnie) w pliku App.config.

> [!NOTE]
> Przed zainicjowaniem obsługi administracyjnej kolekcje z wysokiej przepływności, zobacz toohello [stronie cennika](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate koszty hello na kolekcję. Azure DB rozwiązania Cosmos rachunków pamięci masowej i przepływność niezależnie co godzinę, więc można zmniejszyć koszty przez usunięcie lub zmniejszenie przepływności hello kolekcji bazy danych rozwiązania Cosmos Azure po zakończeniu testowania.
> 
> 

**Krok 3:** skompilować i uruchomić z wiersza polecenia hello hello aplikacji konsoli. Powinny pojawić się dane wyjściowe podobne do następujących hello:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Krok 4 (Jeśli to konieczne):** hello przepływności zgłoszone (RU/s) z narzędzia hello powinna być hello tego samego lub wyższego niż hello udostępnionej przepływności hello kolekcji. Jeśli nie, zwiększa hello DegreeOfParallelism w małych odstępach mogą pomóc w osiągnięciu limitu hello. Jeśli płaskowyżach przepływności hello z aplikacji klienta, uruchamianie wielu wystąpień aplikacji hello na hello takie same lub różnych maszyn mogą pomóc w osiągnięciu limitu hello udostępniane między hello różnymi wystąpieniami. Jeśli potrzebujesz pomocy w ramach tego kroku, napisz wiadomość e-mail tooaskcosmosdb@microsoft.com lub pliku biletu pomocy technicznej z hello [Azure Portal](https://portal.azure.com).

Po uruchomieniu aplikacji hello, możesz spróbować innego [zasady indeksowania](indexing-policies.md) i [poziomy spójności](consistency-levels.md) toounderstand ich wpływ na przepustowości i opóźnień. Można również przejrzeć kod źródłowy hello i implementować podobnych konfiguracji tooyour własnych testów lub aplikacje produkcyjne.

## <a name="next-steps"></a>Następne kroki
W tym artykule analizujemy sposobu wykonywania wydajności i skalowania testowanie za pomocą rozwiązania Cosmos bazy danych przy użyciu aplikacji konsoli .NET. Aby uzyskać dodatkowe informacje na temat pracy z bazy danych Azure rozwiązania Cosmos, zapoznaj się z łącza toohello poniżej.

* [Testowanie próbki Azure wydajności bazy danych rozwiązania Cosmos](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Tooimprove opcje konfiguracji klienta wydajności bazy danych Azure rozwiązania Cosmos](performance-tips.md)
* [Partycjonowanie po stronie serwera w usłudze Azure DB rozwiązania Cosmos](partition-data.md)


