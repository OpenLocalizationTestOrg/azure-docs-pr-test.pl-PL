---
title: aaaEnable w trybie offline synchronizowanie z aplikacji mobilnych systemu iOS | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse usłudze Azure App Service aplikacje mobilne toocache i synchronizacji danych w trybie offline w aplikacjach systemu iOS."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Włącz synchronizację w trybie offline z aplikacji mobilnych systemu iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Omówienie
Ten samouczek obejmuje synchronizacji w trybie offline z funkcji Mobile Apps hello Azure App Service dla systemu iOS. Z trybu offline synchronizowania użytkowników końcowych może interakcyjnie tooview aplikacji mobilnej, dodać lub modyfikować danych, nawet w przypadku, gdy mają oni połączenia sieciowego. Zmiany są przechowywane w lokalnej bazie danych. Po powrocie do trybu online urządzenia hello hello zmiany są zsynchronizowane z hello zdalnego wewnętrzna.

Jeśli jest to usprawnić pierwszy Mobile Apps, najpierw należy wykonać samouczek hello [tworzenie aplikacji systemu iOS]. Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać hello dostęp do danych rozszerzenia pakietów tooyour projektu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

Zobacz toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello [synchronizacji danych w trybie Offline w aplikacjach mobilnych].

## <a name="review-sync"></a>Przejrzyj powitania klienta synchronizacji kodu
Projekt klienta Hello pobranego hello [tworzenie aplikacji systemu iOS] samouczek już zawiera kod, który obsługuje synchronizacji w trybie offline przy użyciu lokalnej bazy danych na podstawie danych podstawowych. Ta sekcja zawiera podsumowanie, co to jest już uwzględniony w hello samouczek kodu. Omówienie koncepcji hello funkcji, zobacz [synchronizacji danych w trybie Offline w aplikacjach mobilnych].

Za pomocą funkcji synchronizacji danych w trybie offline hello Mobile Apps, użytkownicy końcowi mogą współdziałać z lokalnej bazy danych nawet wtedy, gdy sieć hello jest niedostępny. toouse te funkcje w aplikacji należy zainicjować kontekstu synchronizacji hello `MSClient` i referencyjne Magazyn lokalny. Następnie odwołania tabeli za pomocą hello **MSSyncTable** interfejsu.

W **QSTodoService.m** (Objective-C) lub **ToDoTableViewController.swift** (Swift), zwróć uwagę, że typ elementu członkowskiego hello hello **syncTable** jest  **MSSyncTable**. Synchronizacja w trybie offline używa tego interfejsu tabeli synchronizacji zamiast **MSTable**. W przypadku tabeli synchronizacji wszystkie operacje Przejdź toohello lokalnego magazynu i są synchronizowane tylko z hello zdalnego zaplecza z jawnym wypychania i ściągania operacji.

 tooget tabeli odwołań tooa synchronizacji, użyj hello **syncTableWithName** metoda `MSClient`. tooremove funkcji synchronizacji w trybie offline, użyj **tableWithName** zamiast tego.

Aby można było wykonać wszystkie operacje tabeli, muszą zostać zainicjowane hello lokalnego magazynu. Oto hello odpowiedni kod:

* **Objective-C**. W hello **QSTodoService.init** metody:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Kod SWIFT**. W hello **ToDoTableViewController.viewDidLoad** metody:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Ta metoda tworzy magazynu lokalnego przy użyciu hello `MSCoreDataStore` udostępnia interfejs, który hello zestaw SDK usługi Mobile Apps. Alternatywnie można udostępnić inny magazyn lokalny zaimplementowanie hello `MSSyncContextDataSource` protokołu. Ponadto hello pierwszy parametr **MSSyncContext** jest używane toospecify obsługi konfliktu. Ponieważ firma Microsoft przekazanego `nil`, uzyskujemy hello domyślne konflikt obsługi, który zakończy się niepowodzeniem w przypadku dowolnego konfliktu.

Teraz załóżmy operacji synchronizacji rzeczywiste hello i Pobierz dane z zdalnego zaplecza hello:

* **Objective-C**. `syncData`najpierw wypchnięcia nowych zmian, a następnie wywołuje **pullData** tooget danych z hello zdalnego systemu wewnętrznego. Z kolei hello **pullData** — metoda pobiera nowe dane, odpowiadający kwerendy:

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* **Kod SWIFT**:
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

W wersji hello Objective-C w `syncData`, pierwsze wywołanie **pushWithCompletion** hello kontekstu synchronizacji. Ta metoda jest elementem członkowskim `MSSyncContext` (i nie hello synchronizacji samej tabeli), ponieważ wypycha dane zmiany we wszystkich tabel. Tylko te rekordy, które zostały zmodyfikowane w sposób lokalnie (za pośrednictwem operacji CUD) są wysyłane toohello serwera. Następnie hello Pomocnika **pullData** zostanie wywołany, które wywołuje **MSSyncTable.pullWithQuery** tooretrieve danych zdalnych i zapisz go w hello lokalnej bazy danych.

W wersji Swift hello, hello operacji push nie jest niezbędne, nie istnieje żadne wywołanie za**pushWithCompletion**. Jeśli istnieją oczekujące zmiany w kontekście synchronizacji hello hello tabeli, która wykonuje operację push, ściągania zawsze wystawia wypychanej najpierw. Jednak jeśli masz więcej niż jednej tabeli synchronizacji jest najlepsze tooensure tooexplicitly wywołania wypychania, że wszystko jest spójne w tabelach pokrewnych.

W hello Objective-C i wersje Swift, można użyć hello **pullWithQuery** rekordów, które mają tooretrieve hello toospecify metody toofilter zapytania. W tym przykładzie hello zapytanie pobiera wszystkie rekordy w hello zdalnego `TodoItem` tabeli.

drugi parametr funkcji Hello **pullWithQuery** jest identyfikator zapytania, który służy do *synchronizacja przyrostowa*. Synchronizacja przyrostowa pobiera tylko te rekordy, które zostały zmodyfikowane od momentu ostatniej synchronizacji hello, przy użyciu rekordu hello `UpdatedAt` sygnaturę czasową (nazywane `updatedAt` w hello lokalnym magazynie.) identyfikator zapytania hello powinny być opisowe ciąg, który jest unikatowy dla każdego zapytania logicznych w aplikacji. tooopt Brak synchronizacji przyrostowej, Przekaż `nil` jako hello identyfikator zapytania. Takie podejście może być potencjalnie nieefektywne, ponieważ pobiera on wszystkie rekordy na każdej operacji ściągania.

Witaj synchronizacje aplikacji w języku Objective-C, podczas modyfikowania lub dodawanie danych, gdy użytkownik wykona hello gestu odświeżania i uruchamiania.

Swift aplikacji Hello synchronizacji, gdy użytkownik hello wykonuje hello gestu odświeżania i uruchamiania.

Ponieważ hello synchronizacje aplikacji zawsze, gdy dane są zmodyfikowany (Objective-C) lub przy każdym uruchomieniu aplikacji hello (Objective-C i Swift), aplikacji hello przyjęto założenie, że użytkownik hello jest w trybie online. W dalszej części artykułu spowoduje zaktualizowanie aplikacji hello, dzięki czemu użytkownicy mogą edytować nawet wtedy, gdy są one w trybie offline.

## <a name="review-core-data"></a>Model danych podstawowych hello przeglądu
Korzystając z magazynu offline hello podstawowych danych, należy zdefiniować określonego tabel i pól w modelu danych. Hello Przykładowa aplikacja już zawiera model danych z hello w prawidłowym formacie. W tej sekcji możemy przeprowadzenie tooshow te tabele korzystania z nich.

Otwórz **QSDataModel.xcdatamodeld**. Cztery tabele są zdefiniowane — Witaj trzech, które są używane przez zestaw SDK i używany dla zadania do wykonania hello się elementy:
  * MS_TableOperations: Śledzi hello elementy toobe zsynchronizowane z serwerem hello.
  * MS_TableOperationErrors: Śledzi wszystkie błędy, które mają miejsce podczas synchronizacji w trybie offline.
  * MS_TableConfig: Śledzi hello hello ostatniej operacji synchronizacji dla wszystkich operacji ściągania godziny ostatniej aktualizacji.
  * TodoItem: Przechowuje hello elementów do wykonania. Witaj kolumny systemowe **createdAt**, **updatedAt**, i **wersji** są właściwości opcjonalne systemu.

> [!NOTE]
> Witaj zestaw SDK usługi Mobile Apps rezerwuje nazwy kolumn, które zaczynają się od "**``**". Nie należy używać tego prefiksu z innym niż system kolumn. W przeciwnym razie nazwy kolumny są modyfikowane, gdy używasz hello zdalnego wewnętrznej bazy.
>
>

Gdy funkcja hello synchronizacji w trybie offline, zdefiniuj hello trzy tabele systemowe i hello danych tabeli.

### <a name="system-tables"></a>Tabele systemowe

**MS_TableOperations**  

![Atrybuty tabeli MS_TableOperations][defining-core-data-tableoperations-entity]

| Atrybut | Typ |
| --- | --- |
| id | Liczba całkowita 64 |
| Identyfikator elementu | Ciąg |
| properties | Dane binarne |
| Tabela | Ciąg |
| tableKind | Liczba całkowita 16 |


**MS_TableOperationErrors**

 ![Atrybuty tabeli MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| Atrybut | Typ |
| --- | --- |
| id |Ciąg |
| operationId |Liczba całkowita 64 |
| properties |Dane binarne |
| tableKind |Liczba całkowita 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Atrybut | Typ |
| --- | --- |
| id |Ciąg |
| key |Ciąg |
| Właściwość KeyType |Liczba całkowita 64 |
| Tabela |Ciąg |
| wartość |Ciąg |

### <a name="data-table"></a>Tabela danych

**TodoItem**

| Atrybut | Typ | Uwaga |
| --- | --- | --- |
| id | Ciąg, oznaczona jako wymagana |klucz podstawowy w magazynie zdalnym |
| Zakończenie | Wartość logiczna | Pole elementu zadań do wykonania |
| Tekst |Ciąg |Pole elementu zadań do wykonania |
| CreatedAt | Date | (opcjonalnie) Mapuje zbyt**createdAt** właściwości systemu |
| updatedAt | Date | (opcjonalnie) Mapuje zbyt**updatedAt** właściwości systemu |
| Wersja | Ciąg | (opcjonalnie) Używane toodetect konflikty, tooversion mapy |

## <a name="setup-sync"></a>Należy zmienić to zachowanie synchronizacji hello aplikacji hello
W tej sekcji możesz zmodyfikować aplikacji hello tak, aby nie synchronizuje się na początku aplikacji lub podczas wstawiania i aktualizowania elementów. Synchronizuje tylko wtedy, gdy przycisk gestu Odśwież hello jest wykonywana.

**Objective-C**:

1. W **QSTodoListViewController.m**, zmień hello **viewDidLoad** tooremove metody hello wywołanie za`[self refresh]` na końcu hello hello metody. Teraz hello danych nie jest zsynchronizowane z serwerem powitania po uruchomieniu aplikacji. Zamiast tego jest synchronizowany z zawartością hello hello magazynu lokalnego.
2. W **QSTodoService.m**, zmodyfikuj definicję hello `addItem` tak, aby nie synchronizacji, po wstawieniu elementu hello. Usuń hello `self syncData` zablokować i zastąp go hello poniżej:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Modyfikowanie definicji hello `completeItem` jak wspomniano powyżej. Usuń blok hello `self syncData` i zastąp go hello poniżej:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Kod SWIFT**:

W `viewDidLoad`w **ToDoTableViewController.swift**, komentarz dwa wiersze hello pokazane toostop synchronizowanie po uruchomieniu aplikacji. W czasie hello pisania tego dokumentu aplikacji Swift Todo hello nie aktualizowania usługi hello, gdy ktoś dodaje lub zakończeniu elementu. Aktualizuje usługę hello tylko po uruchomieniu aplikacji.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Aplikacja hello testu
W tej sekcji możesz połączyć tooan nieprawidłowy adres URL toosimulate scenariusz w trybie offline. Po dodaniu elementów danych są przechowywane w hello przechowywać dane lokalne Core, ale nie są one zsynchronizowane z zaplecza aplikacji mobilnej hello.

1. Zmień adres URL aplikacji mobilnej hello w **QSTodoService.m** tooan nieprawidłowy adres URL i ponownie uruchom hello aplikacji:

   **Objective-C**. W QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Kod SWIFT**. W ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Dodać niektóre elementy zadań do wykonania. Zamknij symulator hello (lub hello wymuszanie zamknięcia aplikacji), a następnie uruchom go ponownie. Sprawdź, czy zachować zmiany.

3. Wyświetl zawartość hello hello zdalnego **TodoItem** tabeli:
   * Dla środowiska Node.js zaplecze, przejdź toohello [portalu Azure](https://portal.azure.com/) i w Twojej aplikacji mobilnej wewnętrznej, kliknij przycisk **łatwe tabel** > **TodoItem**.  
   * Dla programu .NET w ponownie zakończyć, użyj narzędzia SQL, takich jak SQL Server Management Studio lub klienta REST, takiego jak Fiddler lub Postman.  

4. Sprawdź, czy nowe elementy hello *nie* zostały zsynchronizowane z serwerem hello.

5. Zmiany hello adresu URL wstecz toohello Popraw jedną w **QSTodoService.m**i uruchom ponownie hello aplikacji.

6. Wykonaj hello odświeżania gestu przez ściąganie dół hello listy elementów.  
Pokrętła postępu jest wyświetlana.

7. Widok hello **TodoItem** danych ponownie. Witaj nowe i zmienione wykonania powinna być teraz wyświetlana.

## <a name="summary"></a>Podsumowanie
Funkcja synchronizacji w trybie offline hello toosupport, użyliśmy hello `MSSyncTable` interfejsu i zainicjować `MSClient.syncContext` z lokalnego magazynu. W takim przypadku Magazyn lokalny hello został bazy danych opartej na danych podstawowych.

Korzystając z lokalnego magazynu danych podstawowe, należy zdefiniować wiele tabel o hello [Popraw właściwości systemu](#review-core-data).

Normalny Hello tworzenia, odczytu, aktualizacji i usuwania operacji (CRUD) do pracy aplikacji mobilnych tak, jakby aplikacji hello jest nadal połączony, ale wszystkie operacje hello są wykonywane przed hello magazynu lokalnego.

Witaj w lokalnym magazynie firma Microsoft synchronizowane z serwerem hello, użyliśmy hello **MSSyncTable.pullWithQuery** metody.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [synchronizacji danych w trybie Offline w aplikacjach mobilnych]
* [Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services] \(jest hello wideo dotyczące usługi Mobile Services, ale działa synchronizacja Mobile Apps w tryb offline w podobny sposób.\)

<!-- URLs. -->


[tworzenie aplikacji systemu iOS]: app-service-mobile-ios-get-started.md
[synchronizacji danych w trybie Offline w aplikacjach mobilnych]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
