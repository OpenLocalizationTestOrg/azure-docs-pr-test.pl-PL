---
title: "tryb failover aaaRegional w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o sposobie ręcznego i automatycznego działania trybu failover z bazy danych Azure rozwiązania Cosmos."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Automatyczne regionalnej pracy w trybie failover ciągłość prowadzenia działalności biznesowej w usłudze Azure DB rozwiązania Cosmos
Azure DB rozwiązania Cosmos upraszcza rozkład danych globalnych hello oferując do pełnego zarządzania, [konta bazy danych w przypadku](distribute-data-globally.md) zawierających wyczyść wady i zalety między spójności, dostępność i wydajność, wszystkie z odpowiednimi gwarancje. Rozwiązania cosmos DB kont oferują wysoką dostępność, opóźnienia ms w pojedynczą cyfrą [dobrze zdefiniowane poziomy spójności](consistency-levels.md), przezroczysty regionalnej pracy awaryjnej z wielu interfejsów API, a hello możliwości tooelastically skali przepływność i Magazyn między Witaj świecie. 

Rozwiązania cosmos bazy danych obsługuje zarówno jawnego i praca awaryjna zasad zmiennych umożliwiającą zachowanie systemu end-to-end hello toocontrol w zdarzeniu hello błędów. W tym artykule opisano:

* Jak działają ręcznej pracy awaryjnej w bazie danych rozwiązania Cosmos
* Jak pracy automatycznego przechodzenia w tryb failover do rozwiązania Cosmos bazy danych i co się dzieje, gdy dane Centrum umieszczane w dół?
* Jak można użyć ręcznej pracy awaryjnej w architekturach aplikacji?

Można również zapoznać się regionalnej pracy w trybie Failover w tym Azure piątek wideo Scott Hanselman i Ramana Karthik główny Menedżer zespołu inżynieryjnego.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Konfigurowanie aplikacji w przypadku
Zanim firma Microsoft Poznaj tryby pracy awaryjnej przyjrzymy się jak skonfigurować zaletą tootake aplikacji w przypadku dostępności i zapewnienie odporności w powierzchnię hello regionalnej pracy w trybie Failover.

* Najpierw należy wdrożyć aplikację w wielu regionach
* Skonfiguruj tooensure małych opóźnieniach dostępu z każdego regionu, wdrażania aplikacji hello odpowiadającego [listy regiony preferowanych](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) dla każdego regionu, za pomocą jednego z hello obsługiwanych zestawów SDK.

powitania po fragment kodu przedstawia sposób tooinitialize aplikacji w przypadku. W tym miejscu hello konta bazy danych Azure rozwiązania Cosmos `contoso.documents.azure.com` jest skonfigurowany z dwóch regionach - zachodnie stany USA, Europa Północna, Europa a. 

* Aplikacja Hello jest wdrażana regionu zachodnie stany USA hello (na przykład przy użyciu usługi aplikacji Azure) 
* Skonfigurowany z użyciem `West US` jako pierwszy preferowanego regionu powitania dla małych opóźnieniach odczytuje
* Skonfigurowany z użyciem `North Europe` jako drugi preferowanego regionu hello (wysokiej dostępności podczas regionalnej awarii)

W hello interfejsu API usługi DocumentDB ta konfiguracja wygląda powitania po fragment kodu:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

Aplikacja Hello również jest wdrażana w regionie Europa Północna, Europa hello z kolejnością hello preferowanych regionów wycofane. Oznacza to hello Europa Północna, Europa region jest określony jako pierwszy dla odczytów małe opóźnienia. Następnie regionu zachodnie stany USA hello jest określony jako hello drugi preferowanego regionu wysokiej dostępności podczas regionalnej awarii.

Hello poniższy architektura diagram przedstawia wdrożenia aplikacji w przypadku których rozwiązania Cosmos bazę danych i aplikacji hello są skonfigurowane toobe dostępne w czterech Azure regionach geograficznych.  

![Wdrożenie aplikacji rozproszonych globalnie z bazy danych Azure rozwiązania Cosmos](./media/regional-failover/app-deployment.png)

Teraz Przyjrzyjmy się jak hello DB rozwiązania Cosmos usługi obsługuje regionalnymi awariami za pomocą automatycznej pracy awaryjnej. 

## <a id="AutomaticFailovers"></a>Automatycznego przechodzenia w tryb failover
W rzadkich hello Azure regionalnej awarii lub awarii centrum danych bazy danych rozwiązania Cosmos automatyczne wyzwolenie procesu przechodzenia w tryb failover wszystkich kont DB rozwiązania Cosmos obecności w regionie hello, których to dotyczy. 

**Co się stanie, jeśli region odczytu ma awarii?**

Konta rozwiązania cosmos bazy danych za pomocą obszaru odczytu w jednym z regionów hello wpływ automatycznie są odłączone od ich region zapisu i oznaczone w trybie offline. Implementowanie rozwiązania Cosmos DB SDK Hello protokołu odnajdowania regionalnych, który umożliwia im tooautomatically Wykryj, kiedy region jest dostępny i Przekierowanie do odczytu wywołania toohello następny dostępny region hello preferowanego regionu liście. Jeśli brak regionów hello w hello preferowanego regionu lista jest dostępna, wywołania automatycznie wrócić toohello bieżący obszar zapisu. W Twojej aplikacji kod toohandle regionalnej pracy w trybie Failover nie są konieczne nie zmiany. W trakcie tego procesu całego gwarancje spójności nadal toobe honorowane przez DB rozwiązania Cosmos.

![Błędy region odczytu w usłudze Azure DB rozwiązania Cosmos](./media/regional-failover/read-region-failures.png)

Gdy region hello dotyczy odzyskiwania z hello awarii, wszystkie konta DB rozwiązania Cosmos hello wpływ w regionie hello są automatycznie odzyskiwane przez usługę hello. Rozwiązania cosmos bazy danych konta, które ma odczytu regionu w regionie hello, których dotyczy problem, a następnie automatycznie synchronizacji z bieżącego obszaru do zapisu i włączyć online. zestawy SDK DB rozwiązania Cosmos Hello odnajdywanie hello dostępność hello nowy region i ocenić, czy należy wybrać hello region jako hello bieżący obszar odczytu na podstawie listy preferowanego regionu hello konfigurowane za pomocą aplikacji hello. Kolejne odczyty są przekierowane toohello region odzyskane bez konieczności zmiany kodu aplikacji tooyour.

**Co się stanie, jeśli region zapisu ma awarii?**

Jeśli region dotyczy hello jest hello bieżący obszar zapisu dla danego konta rozwiązania Cosmos DB, następnie hello region zostaną automatycznie oznaczone w trybie offline. Następnie alternatywne region jest podwyższany pisania hello region wszystkich odpowiednich kont DB rozwiązania Cosmos. Można w pełni kontrolować kolejność zaznaczania region powitania dla kont rozwiązania Cosmos bazy danych za pośrednictwem portalu Azure hello lub [programowo](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Priorytetów trybu failover dla bazy danych Azure rozwiązania Cosmos](./media/regional-failover/failover-priorities.png)

Podczas automatycznego przechodzenia w tryb failover, DB rozwiązania Cosmos automatycznie wybiera następny region zapisu hello na dla danego DB rozwiązania Cosmos konto oparte na powitania określone priorytetu. 

![Zakończone niepowodzeniem regionu w usłudze Azure DB rozwiązania Cosmos](./media/regional-failover/write-region-failures.png)

Gdy region hello dotyczy odzyskiwania z hello awarii, wszystkie konta DB rozwiązania Cosmos hello wpływ w regionie hello są automatycznie odzyskiwane przez usługę hello. 

* Rozwiązania cosmos DB kont z ich poprzednich region zapisu w regionie hello, których to dotyczy, pozostanie w trybie offline o dostępności odczytu nawet po odzyskaniu hello hello regionu. 
* Można zbadać toocompute tego regionu wszelkie niezreplikowane zapisy podczas awarii hello porównując z dostępnych danych hello w hello bieżący obszar zapisu. Oparte na powitania wymagania dotyczące aplikacji, można wykonywać scalania i/lub konflikt rozpoznawania i zapisać hello ostatecznego zestawu zmian wstecz toohello bieżący obszar zapisu. 
* Po ukończeniu scalania zmian, będzie można przełączyć region hello wpływ na powrót online przez usunięcie i ponowne dodawanie hello region tooyour DB rozwiązania Cosmos konta. Po hello region jest dodany ponownie, można skonfigurować go jako regionu zapisu hello, wykonując ręcznego przełączania trybu failover za pośrednictwem portalu Azure hello lub [programowo](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a>Ręczne praca awaryjna

Ponadto tooautomatic przełączenia do trybu failover, hello bieżącego zapisu regionu danego konta rozwiązania Cosmos bazy danych może być zmieniony ręcznie dynamicznie tooone hello istniejących regionów odczytu. Ręczne przechodzenia w tryb failover może być inicjowane za pośrednictwem portalu Azure hello lub [programowo](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

Zapewnienia ręcznej pracy awaryjnej **zero utraty danych** i **zero dostępności** utratą i bezpiecznie stanu zapisu transferu z hello starego zapisać region toohello nową hello określone konto bazy danych rozwiązania Cosmos. Jak automatycznego przechodzenia w tryb failover hello rozwiązania Cosmos DB SDK automatycznie uchwytów zapisu region zmiany podczas ręcznej pracy awaryjnej i zapewnia, że połączenia są automatycznie przekierowane toohello nowy region zapisu. Twojej aplikacji toomanage przechodzenia w tryb failover nie są konieczne nie zmiany kodu lub konfiguracji. 

![Ręcznej pracy awaryjnej w usłudze Azure DB rozwiązania Cosmos](./media/regional-failover/manual-failovers.png)

Typowe scenariusze hello, gdzie ręcznego przełączania trybu failover może być przydatne, należą:

**Postępuj zgodnie z modelu zegara hello**: Jeśli wzorce ruchu przewidywalną na podstawie czasu dnia hello hello aplikacji, można zmienić okresowo hello zapisu stanu toohello Najaktywniejsze regionu geograficznego na podstawie czasu dnia hello.

**Aktualizacja usługi**: niektóre wdrożenia aplikacji rozproszonych globalnie może obejmować ponownego routingu ruchu toodifferent regionu za pośrednictwem Menedżera ruchu podczas ich aktualizacji planowane usługi. Teraz takie wdrożenie aplikacji można użyć gdzie będzie toobe active ruchu w oknie aktualizacji usługi hello ręcznego przełączania trybu failover tookeep hello zapisu stanu toohello regionu.

**Ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii (BCDR) i rozwija wysokiej dostępności i odzyskiwania po awarii (HADR)**: większość aplikacji przedsiębiorstwa obejmują testy ciągłości biznesowej jako część procesu projektowania i wersji. BCDR i testowania HADR często jest ważnym krokiem w certyfikatach zgodności i gwarantujących dostępności usługi w przypadku hello regionalnej awarii. Można przetestować hello gotowości BCDR aplikacji korzystających z rozwiązania Cosmos bazy danych dla magazynu przez wyzwalania ręcznego przełączania trybu failover konta rozwiązania Cosmos bazy danych i/lub dodawanie i usuwanie region dynamicznie.

W tym artykule firma Microsoft przeglądowi sposób ręcznego i automatycznego pracy trybu failover do rozwiązania Cosmos bazy danych oraz sposobu konfigurowania Twojego rozwiązania Cosmos DB konta i aplikacje toobe dostępnego globalnie. Przy użyciu funkcji obsługi replikacji globalne rozwiązania Cosmos DB, można zwiększyć czas oczekiwania na trasie i zapewnienia wysokiej dostępności, nawet w przypadku hello niepowodzeń regionu. 

## <a id="NextSteps"></a>Następne kroki
* Dowiedz się więcej o sposobie obsługi DB rozwiązania Cosmos [dystrybucji globalne](distribute-data-globally.md)
* Dowiedz się więcej o [globalne spójności z bazy danych Azure rozwiązania Cosmos](consistency-levels.md)
* Tworzenie z wielu regionach, przy użyciu usługi Azure rozwiązania Cosmos DB [interfejsu API usługi DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md)
* Dowiedz się, jak toobuild [architektury w przypadku zapisywania](multi-region-writers.md) za pomocą usługi Azure DocumentDB

