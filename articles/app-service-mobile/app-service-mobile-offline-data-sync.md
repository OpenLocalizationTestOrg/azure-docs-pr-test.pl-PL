---
title: "aaaOffline synchronizacji danych w usłudze Azure Mobile Apps | Dokumentacja firmy Microsoft"
description: "Odwołanie koncepcyjne i przegląd hello funkcja synchronizacji danych w trybie offline dla usługi Azure Mobile Apps"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Synchronizowanie danych w trybie offline w usłudze Azure Mobile Apps
## <a name="what-is-offline-data-sync"></a>Co to jest synchronizacja danych w trybie offline?
Synchronizacja danych w trybie offline jest klientem i serwerem funkcji zestawu SDK usługi Azure Mobile Apps, która ułatwia deweloperom toocreate aplikacje, które działają bez połączenia sieciowego.

Gdy aplikacja jest w trybie offline, można nadal tworzyć i modyfikować danych, które są zapisywane w lokalnym magazynie tooa. Po powrocie do trybu online aplikacji hello lokalne zmiany można było synchronizować z zaplecza aplikacji mobilnej Azure. Funkcja Hello obejmuje również obsługę wykrywania konfliktów powitalne sam rekord jest zmieniany na obu hello klienta i hello wewnętrznej bazy danych. Następnie można obsłużyć konfliktów na powitania serwera lub powitania klienta.

Synchronizacja w trybie offline ma wiele zalet:

* Zwiększyć czas odpowiedzi aplikacji przez buforowanie danych serwera lokalnie na urządzeniu hello
* Tworzenie niezawodnych aplikacji, które pozostają przydatne, gdy istnieją problemy z siecią
* Zezwalaj na toocreate użytkowników końcowych i modyfikować danych, nawet wtedy, gdy nie dostępu do sieci, obsługujące scenariusze niewielkiego lub żadnego łączności z
* Synchronizowanie danych na wielu urządzeniach i wykrywania konfliktów podczas hello sam rekord jest modyfikowany przez dwa urządzenia
* Ogranicz użycie sieci w sieciach dużymi opóźnieniami lub naliczane

następujące samouczki Hello pokazują, jak w trybie offline tooadd synchronizacji tooyour klientów mobilnych za pomocą usługi Azure Mobile Apps:

* [System android: Włączanie synchronizacji w trybie offline]
* [Apache Cordova: Włączanie synchronizacji w trybie offline](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: Włączanie synchronizacji w trybie offline]
* [Xamarin iOS: Włączanie synchronizacji w trybie offline]
* [Dla systemu Xamarin Android: Włączanie synchronizacji w trybie offline]
* [Platformy Xamarin.Forms: Synchronizacja w trybie offline Włącz](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [platformy uniwersalnej systemu Windows: Włączanie synchronizacji w trybie offline]

## <a name="what-is-a-sync-table"></a>Co to jest tabela synchronizacji?
Witaj tooaccess "/ tabel" punktu końcowego, powitania klienta usługi Azure Mobile zestawów SDK Podaj interfejsów, taki jak `IMobileServiceTable` (klient .NET SDK) lub `MSTable` (klient z systemem iOS). Te interfejsy API Połącz bezpośrednio zaplecza aplikacji mobilnej Azure toohello i zakończyć się niepowodzeniem, jeśli powitania klienta urządzenia nie ma połączenia sieciowego.

toosupport użycia w trybie offline, aplikacji zamiast tego należy użyć hello *synchronizacji tabeli* interfejsów API, takich jak `IMobileServiceSyncTable` (klient .NET SDK) lub `MSSyncTable` (klient z systemem iOS). Hello wszystkich operacji CRUD (tworzenia, odczytu, aktualizacji, usuwania) pracy projektowej synchronizacji tabeli interfejsów API, z wyjątkiem teraz są odczytywane lub napisz tooa *lokalnego magazynu*. Aby można było wykonać wszystkie operacje tabeli synchronizacji, musi zostać zainicjowany hello magazynu lokalnego.

## <a name="what-is-a-local-store"></a>Co to jest Magazyn lokalny?
Magazyn lokalny jest warstwę trwałości danych hello na powitania klienta urządzenia. klienta usługi Azure Mobile Apps Hello, zestawy SDK zapewniają domyślnego lokalnego magazynu implementacji. W systemach Windows, Xamarin i Android jest on oparty na SQLite. W systemach iOS jest on oparty na danych podstawowych.

toouse hello SQLite wdrożeniem opartym na Windows Phone lub Sklepu Windows 8.1, trzeba tooinstall rozszerzenia SQLite. Aby uzyskać więcej informacji, zobacz [platformy uniwersalnej systemu Windows: Włączanie synchronizacji w trybie offline]. Android i iOS są dostarczane z wersją bazy danych SQLite w urządzeniu hello systemu operacyjnego, więc nie jest konieczne tooreference własną wersję bazy danych SQLite.

Deweloperzy mogą także implementować własnych magazynu lokalnego. Na przykład w razie potrzeby toostore dane w postaci zaszyfrowanej na powitania klienta mobilnego, można zdefiniować magazynu lokalnego, który używa SQLCipher szyfrowania.

## <a name="what-is-a-sync-context"></a>Co to jest kontekst synchronizacji?
A *kontekstu synchronizacji* jest skojarzony z obiektem klientów urządzeń przenośnych (takich jak `IMobileServiceClient` lub `MSClient`) i śledzi zmiany wprowadzone w tabelach synchronizacji. kontekst synchronizacji Hello przechowuje *kolejka operację*, co pozwala uporządkowaną listę operacji CUD (tworzenia, aktualizacji, usuwania), zostanie wysłana toohello serwera.

Magazyn lokalny jest skojarzona z kontekstu synchronizacji hello za pomocą metody initialize, takich jak `IMobileServicesSyncContext.InitializeAsync(localstore)` w hello [klienta .NET SDK].

## <a name="how-sync-works"></a>Jak w trybie offline działania synchronizacji
Korzystając z tabel synchronizacji, kod klienta określa, kiedy lokalne zmiany są synchronizowane z zaplecza aplikacji mobilnej Azure. Nic nie są wysyłane toohello wewnętrznej bazy danych, do momentu wywołania zbyt*wypychania* zmian lokalnych. Podobnie magazynu lokalnego hello jest wypełniane przy użyciu nowych danych tylko wtedy, gdy wywołanie za*ściągania* danych.

* **Wypychania**: operacja jest w kontekście synchronizacji hello i wysyła wszystkie zmiany CUD od czasu ostatniego wypychania hello. Należy pamiętać, że nie toosend nie jest możliwe tylko pojedynczej tabeli zmian, ponieważ w przeciwnym razie operacje mógł zostać wysłany poza kolejnością. Wypychania wykonuje szereg zaplecza aplikacji mobilnej Azure tooyour wywołań REST, który z kolei modyfikuje bazy danych serwera.
* **Ściąganie**: ściągania odbywa się na konkretnych tabel i można dostosować za pomocą tooretrieve zapytania tylko podzestaw danych serwera hello. Witaj zestawów SDK klienta usługi Azure Mobile, a następnie wstawianie danych wynikowy hello w lokalnym magazynie hello.
* **Niejawne Wypchnięć**: w przypadku ściąganie jest wykonywane względem tabeli, która ma oczekujące aktualizacje lokalnej, ściągania hello najpierw wykonuje `push()` hello kontekstu synchronizacji. To zamówienie minimalizuje konfliktów między zmiany, które już są umieszczane w kolejce i nowych danych z serwera hello.
* **Synchronizacja przyrostowa**: operacja ściągania toohello pierwszy parametr hello *nazwa zapytania* używany tylko na powitania klienta. Jeśli używasz nazwę inną niż null kwerendy hello zestaw SDK usługi Azure Mobile wykonuje *synchronizacja przyrostowa*. Zawsze operacji ściągania zwraca zestaw wyników, najnowsza wersja hello `updatedAt` sygnatury czasowej z tego zestawu wyników jest przechowywany w hello zestawu SDK systemu lokalnego tabel. Ściągania kolejnych operacji pobierania rekordów tylko po tym sygnatury czasowej.

  Synchronizacja przyrostowa toouse, serwer musi zwracać znaczący `updatedAt` wartości i muszą również obsługiwać sortowania według tego pola. Jednak ponieważ hello SDK dodaje własny sortowania na powitania updatedAt pola, nie można użyć ściągania kwerendę, która ma własną `orderBy` klauzuli.

  Nazwa zapytania Hello może być dowolnym ciągiem, wybrane, ale musi być unikatowa dla każdej logicznej kwerendy w aplikacji.
  W przeciwnym razie ściągania różne operacje można zastąpić hello tą samą sygnaturą czasową synchronizacji przyrostowej i zapytania mogą zwracać niepoprawne wyniki.

  Jeśli zapytanie hello ma parametr, jednokierunkowej toocreate nazwę unikatową kwerendy jest wartość parametru hello tooincorporate.
  Na przykład jeśli filtrowania na userid, nazwę kwerendy można w następujący sposób (w języku C#):

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Jeśli chcesz tooopt poza synchronizacja przyrostowa przekazuj `null` jako hello identyfikator zapytania. W takim przypadku wszystkie rekordy są pobierane przy każdym wywołaniu zbyt`PullAsync`, który jest potencjalnie nieefektywne.
* **Przeczyszczanie**: można wyczyścić zawartość hello hello magazynu lokalnego przy użyciu `IMobileServiceSyncTable.PurgeAsync`.
  Przeczyszczanie może być konieczne, jeśli masz stare dane w powitania klienta w bazie danych lub w razie potrzeby toodiscard wszystkie oczekujące zmiany.

  Przeczyszczanie usuwa tabelę z lokalnego magazynu hello. W przypadku operacji oczekiwanie na synchronizację z bazy danych z serwera hello, hello przeczyszczania zgłasza wyjątek, który występuje, chyba że hello *wymusić przeczyszczania* ustawiono parametr.

  Na przykład stare dane na powitania klienta Załóżmy, że w przykładzie "Lista czynności do wykonania" hello, Device1 pobiera tylko elementy, które nie zostały zakończone. Czynność do wykonania "Kup mleka" jest oznaczona jako zakończona na powitania serwera przez inne urządzenie. Device1 ma nadal powitalne "Kup mleka" todoitem w lokalnym magazynie, ponieważ jest on tylko ściąganie elementy, które nie są oznaczone jako ukończone. Przeczyszczanie usuwa ten element stare.

## <a name="next-steps"></a>Następne kroki
* [iOS: Włączanie synchronizacji w trybie offline]
* [Xamarin iOS: Włączanie synchronizacji w trybie offline]
* [Dla systemu Xamarin Android: Włączanie synchronizacji w trybie offline]
* [platformy uniwersalnej systemu Windows: Włączanie synchronizacji w trybie offline]

<!-- Links -->
[klienta .NET SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[System android: Włączanie synchronizacji w trybie offline]: app-service-mobile-android-get-started-offline-data.md
[iOS: Włączanie synchronizacji w trybie offline]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: Włączanie synchronizacji w trybie offline]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Dla systemu Xamarin Android: Włączanie synchronizacji w trybie offline]: app-service-mobile-xamarin-android-get-started-offline-data.md
[platformy uniwersalnej systemu Windows: Włączanie synchronizacji w trybie offline]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
