---
title: "Przykłady Python aaaDocumentDB interfejsu API dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Znaleźć przykłady Python w usłudze github dla typowych zadań w usłudze Azure DB rozwiązania Cosmos, w tym operacji CRUD."
keywords: "Przykłady dla języka Python"
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Przykłady rozwiązania Cosmos DB Python platformy Azure
> [!div class="op_single_selector"]
> * [Przykłady .NET](documentdb-dotnet-samples.md)
> * [Przykłady środowiska node.js](documentdb-nodejs-samples.md)
> * [Przykłady dla języka Python](documentdb-python-samples.md)
> * [Galeria próbki kodu platformy Azure](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

Przykładowe rozwiązania, wykonujących operacje CRUD i innymi typowymi operacjami zasobów bazy danych Azure rozwiązania Cosmos znajdują się w hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) repozytorium GitHub. Ten artykuł zawiera:

* Zadania toohello łącza w każdym przykładzie Python hello pliki projektu. 
* Toohello łącza powiązane zawartości referencyjnej interfejsu API.

**Wymagania wstępne**

1. Należy toouse konto platformy Azure w tych przykładach Python:
   * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/): otrzymasz kredyt płatnej usług platformy Azure można użyć tootry wychodzących, a nawet po wyczerpaniu kredytu możesz zachować konto hello i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web. Karty kredytowej nigdy nie zostanie obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.
     * Możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
2. Należy również hello [zestaw SDK Python](documentdb-sdk-python.md). 
   
   > [!NOTE]
   > Każda próbka jest autonomicznym środowiskiem, konfiguruje się i czyści po samej siebie. Tak, przykłady hello wystawiać wielu wywołań zbyt[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Zawsze, gdy jest to realizowane subskrypcji będą naliczane za godzinę użycia na powitania warstwę wydajności kolekcji hello tworzona. 
   > 
   > 

## <a name="database-examples"></a>Przykłady bazy danych
Witaj [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) pliku hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) projektu pokazuje, jak hello tooperform następujące zadania.

| Zadanie | Dokumentacja interfejsu API |
| --- | --- |
| [Tworzenie bazy danych](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client. Metody CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Zapytania konta bazy danych](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client. QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Przeczytaj przez identyfikator bazy danych](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client. ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Lista baz danych, konta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client. ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Usuwanie bazy danych](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client. Metody DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Przykłady kolekcji
Witaj [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) pliku hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) projektu pokazuje, jak hello tooperform następujące zadania.

| Zadanie | Dokumentacja interfejsu API |
| --- | --- |
| [Tworzenie kolekcji](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Odczytaj listę wszystkich kolekcji w bazie danych](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client. ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Pobierz kolekcję według identyfikatora](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client. ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Pobierz warstwę wydajności kolekcji](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Zmień warstwę wydajności kolekcji](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client. ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Usuwanie kolekcji](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client. DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

