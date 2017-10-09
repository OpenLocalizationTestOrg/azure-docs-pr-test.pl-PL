---
title: "Wprowadzenie tooAzure DB rozwiązania Cosmos: interfejs API dla bazy danych MongoDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używasz bazy danych Azure rozwiązania Cosmos toostore i bardzo dużych woluminów dokumentów JSON z niskim opóźnieniem przy użyciu zapytania hello popularnych interfejsów API bazy danych MongoDB OSS."
keywords: Co to jest MongoDB
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Wprowadzenie tooAzure DB rozwiązania Cosmos: interfejs API dla bazy danych MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft do aplikacji o krytycznym znaczeniu. Udostępnia bazę danych systemu Azure rozwiązania Cosmos [dystrybucji globalne gotowe](distribute-data-globally.md), [elastyczne skalowanie przepływność i magazyn](partition-data.md) na całym świecie, jednocyfrowej milisekundy opóźnienia na powitania 99-ty percentyl [pięć dobrze zdefiniowane poziomy spójności](consistency-levels.md), zagwarantować wysokiej dostępności, wszystkie kopie przez [SLA branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB rozwiązania Cosmos [automatycznie indeksuje danych](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności toodeal z zarządzania schematu i indeksu. To usługa wielomodelowa, obsługująca modele dokumentowe, klucz-wartość, wykresy i kolumny. 

![Azure rozwiązania Cosmos bazy danych: Baza danych MongoDB interfejsu API](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Rozwiązania cosmos DB bazy danych może służyć jako hello magazynu danych dla aplikacji napisanych dla [MongoDB](https://docs.mongodb.com/manual/introduction/). Oznacza to, że przy użyciu istniejących [sterowniki](https://docs.mongodb.org/ecosystem/drivers/), aplikacji tworzonych na potrzeby bazy danych MongoDB mogą teraz komunikować się z rozwiązania Cosmos bazy danych i użyć bazy danych DB rozwiązania Cosmos zamiast bazy danych MongoDB. W wielu przypadkach można przełączać z przy użyciu bazy danych MongoDB tooCosmos bazy danych, zmieniając po prostu ciąg połączenia. Z tej funkcji, umożliwia łatwe tworzenie i uruchamianie aplikacji bazy danych MongoDB w hello Azure w chmurze z dystrybucji globalne DB rozwiązania Cosmos Azure i [kompleksowe branży SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), pozostawiając toouse znanych umiejętności i narzędzia bazy danych mongodb.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Co to jest hello korzyścią z używania bazy danych rozwiązania Cosmos Azure dla aplikacji bazy danych MongoDB?

**Elastycznie skalowalne przepływność i Magazyn:** łatwe skalowanie w górę lub w dół toomeet bazy danych z bazy danych MongoDB tę aplikację. Dane są przechowywane na dyskach półprzewodnikowych (SSD, solid-state drive) dla zapewnienia przewidywalnych, niskich opóźnień. Rozwiązania cosmos bazy danych obsługuje bazy danych MongoDB kolekcje, które mogą być skalowane toovirtually nieograniczonego rozmiaru magazynu i udostępnionej przepływności. Można też elastycznie skalować rozwiązania Cosmos DB z przewidywalną wydajnością bezproblemowo wraz z rozwojem aplikacji. 

**W przypadku replikacji:** DB rozwiązania Cosmos niewidocznie replikuje użytkownika jest skojarzony z Twoim kontem bazy danych MongoDB, umożliwiając aplikacji toodevelop, które wymagają dostępu globalny toodata zapewniając wady i zalety między regiony tooall danych spójności, dostępność i wydajność, wszystkie odpowiednie gwarancje. Rozwiązania cosmos DB zapewnia przezroczysty tryb failover regionalnych, z wielu interfejsów API, a hello możliwości tooelastically skali przepływność i Magazyn między Witaj świecie. Dowiedz się więcej w [globalnie dystrybucji danych](distribute-data-globally.md).

**Zgodność z bazy danych MongoDB**: korzystania z istniejącej bazy danych MongoDB wiedzy, kod aplikacji i narzędzi. Można tworzyć aplikacje przy użyciu bazy danych MongoDB i wdrażać je tooproduction przy użyciu hello w pełni zarządzane globalnie rozproszone usługi DB rozwiązania Cosmos.

**Nie zarządzania serwerem**: nie masz toomanage i skalowania bazy danych MongoDB. Rozwiązania cosmos bazy danych jest w pełni zarządzana usługa, co oznacza, że nie masz toomanage infrastruktury ani maszyn wirtualnych samodzielnie. Rozwiązania cosmos bazy danych jest dostępna w 30 + [regiony platformy Azure](https://azure.microsoft.com/regions/services/).

**Dostosowywalne poziomy spójności:** wybierz jedną z pięciu dobrze zdefiniowanych spójności poziomy tooachieve optymalnego kompromisu między wydajnością a spójnością. Dla zapytań i operacji odczytu bazy danych rozwiązania Cosmos oferuje pięć różne poziomy spójności: silne, nieaktualność, sesji, prefiks spójne i "ostateczna". Te poziomy spójności szczegółowe, dokładnie zdefiniowane pozwalają toomake dźwięku kompromis między spójności, dostępnością i opóźnieniem. Dowiedz się więcej w [przy użyciu spójności poziomy wydajności i dostępności toomaximize](consistency-levels.md).

**Automatyczne indeksowanie**: domyślnie DB rozwiązania Cosmos automatycznie indeksuje wszystkie właściwości hello w dokumentach bazy danych MongoDB i nie oczekiwać ani nie wymaga żadnego schematu lub tworzenia indeksów pomocniczych.

**Klasy Enterprise** -DB rozwiązania Cosmos Azure obsługuje wiele replik lokalnych toodeliver 99,99% dostępności i ochrony danych jest w fazie hello lokalnej i regionalnej awarii. Azure DB rozwiązania Cosmos ma klasy enterprise [certyfikaty zgodności](https://www.microsoft.com/trustcenter) i funkcje zabezpieczeń. 

Dowiedz się więcej, w tym Azure piątek wideo z Scott Hanselman i Azure rozwiązania Cosmos DB główny Engineering Menedżer Kirill Gavrylyuk.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Sposób uruchamiania tooget

Wykonaj toocreate Przewodniki Szybki Start bazy danych MongoDB hello konta rozwiązania Cosmos bazy danych i migrację z istniejącej aplikacji Mongo DB toouse DB rozwiązania Cosmos lub tworzenie nowego:

* [Migrowanie istniejących aplikacji sieci web Node.js bazy danych MongoDB](create-mongodb-nodejs.md).
* [Tworzenie aplikacji sieci web interfejsu API bazy danych MongoDB z usług .NET i hello portalu Azure](create-mongodb-dotnet.md)
* [Tworzenie aplikacji konsoli bazy danych MongoDB interfejsu API języka Java i hello portalu Azure](create-mongodb-java.md)

## <a name="next-steps"></a>Następne kroki

Informacji na temat interfejsu API bazy danych MongoDB DB rozwiązania Cosmos Azure została zintegrowana z hello Dokumentacja ogólna Azure rozwiązania Cosmos bazy danych, ale poniżej przedstawiono kilka tooget wskaźniki rozpoczętej:

* Wykonaj hello [połączyć konto bazy danych MongoDB tooa](connect-mongodb-account.md) toolearn samouczek jak tooget informacje o parametrach połączenia konta.
* Wykonaj hello [MongoChef użycia z bazy danych Azure rozwiązania Cosmos](mongodb-mongochef.md) toolearn samouczek jak toocreate połączenie między usługą Azure DB rozwiązania Cosmos bazy danych i aplikacji bazy danych MongoDB w MongoChef.
* Wykonaj hello [migracji danych tooAzure rozwiązania Cosmos bazy danych z obsługą protokołu bazy danych mongodb](mongodb-migrate.md) samouczka tooimport Twojego tooan danych interfejsu API dla bazy danych MongoDB.
* Połączenia bazy danych MongoDB konta przy użyciu interfejsu API tooan [Robomongo](mongodb-robomongo.md).
* Dowiedz się, jak wiele RUs operacji za pomocą hello [GetLastRequestStatistics poleceń i hello Azure metryki portalu](request-units.md#GetLastRequestStatistics).
* Dowiedz się, jak za[Konfigurowanie preferencji odczytu dla aplikacji rozproszonych globalnie](../cosmos-db/tutorial-global-distribution-mongodb.md).
