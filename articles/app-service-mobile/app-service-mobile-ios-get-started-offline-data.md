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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="963dd-103">Włącz synchronizację w trybie offline z aplikacji mobilnych systemu iOS</span><span class="sxs-lookup"><span data-stu-id="963dd-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="963dd-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="963dd-104">Overview</span></span>
<span data-ttu-id="963dd-105">Ten samouczek obejmuje synchronizacji w trybie offline z funkcji Mobile Apps hello Azure App Service dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="963dd-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="963dd-106">Z trybu offline synchronizowania użytkowników końcowych może interakcyjnie tooview aplikacji mobilnej, dodać lub modyfikować danych, nawet w przypadku, gdy mają oni połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="963dd-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="963dd-107">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="963dd-107">Changes are stored in a local database.</span></span> <span data-ttu-id="963dd-108">Po powrocie do trybu online urządzenia hello hello zmiany są zsynchronizowane z hello zdalnego wewnętrzna.</span><span class="sxs-lookup"><span data-stu-id="963dd-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="963dd-109">Jeśli jest to usprawnić pierwszy Mobile Apps, najpierw należy wykonać samouczek hello [tworzenie aplikacji systemu iOS].</span><span class="sxs-lookup"><span data-stu-id="963dd-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="963dd-110">Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać hello dostęp do danych rozszerzenia pakietów tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="963dd-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="963dd-111">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="963dd-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="963dd-112">Zobacz toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello [synchronizacji danych w trybie Offline w aplikacjach mobilnych].</span><span class="sxs-lookup"><span data-stu-id="963dd-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="963dd-113"><a name="review-sync"></a>Przejrzyj powitania klienta synchronizacji kodu</span><span class="sxs-lookup"><span data-stu-id="963dd-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="963dd-114">Projekt klienta Hello pobranego hello [tworzenie aplikacji systemu iOS] samouczek już zawiera kod, który obsługuje synchronizacji w trybie offline przy użyciu lokalnej bazy danych na podstawie danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="963dd-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="963dd-115">Ta sekcja zawiera podsumowanie, co to jest już uwzględniony w hello samouczek kodu.</span><span class="sxs-lookup"><span data-stu-id="963dd-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="963dd-116">Omówienie koncepcji hello funkcji, zobacz [synchronizacji danych w trybie Offline w aplikacjach mobilnych].</span><span class="sxs-lookup"><span data-stu-id="963dd-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="963dd-117">Za pomocą funkcji synchronizacji danych w trybie offline hello Mobile Apps, użytkownicy końcowi mogą współdziałać z lokalnej bazy danych nawet wtedy, gdy sieć hello jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="963dd-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="963dd-118">toouse te funkcje w aplikacji należy zainicjować kontekstu synchronizacji hello `MSClient` i referencyjne Magazyn lokalny.</span><span class="sxs-lookup"><span data-stu-id="963dd-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="963dd-119">Następnie odwołania tabeli za pomocą hello **MSSyncTable** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="963dd-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="963dd-120">W **QSTodoService.m** (Objective-C) lub **ToDoTableViewController.swift** (Swift), zwróć uwagę, że typ elementu członkowskiego hello hello **syncTable** jest  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="963dd-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="963dd-121">Synchronizacja w trybie offline używa tego interfejsu tabeli synchronizacji zamiast **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="963dd-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="963dd-122">W przypadku tabeli synchronizacji wszystkie operacje Przejdź toohello lokalnego magazynu i są synchronizowane tylko z hello zdalnego zaplecza z jawnym wypychania i ściągania operacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="963dd-123">tooget tabeli odwołań tooa synchronizacji, użyj hello **syncTableWithName** metoda `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="963dd-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="963dd-124">tooremove funkcji synchronizacji w trybie offline, użyj **tableWithName** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="963dd-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="963dd-125">Aby można było wykonać wszystkie operacje tabeli, muszą zostać zainicjowane hello lokalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="963dd-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="963dd-126">Oto hello odpowiedni kod:</span><span class="sxs-lookup"><span data-stu-id="963dd-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="963dd-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="963dd-127">**Objective-C**.</span></span> <span data-ttu-id="963dd-128">W hello **QSTodoService.init** metody:</span><span class="sxs-lookup"><span data-stu-id="963dd-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="963dd-129">**Kod SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="963dd-129">**Swift**.</span></span> <span data-ttu-id="963dd-130">W hello **ToDoTableViewController.viewDidLoad** metody:</span><span class="sxs-lookup"><span data-stu-id="963dd-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="963dd-131">Ta metoda tworzy magazynu lokalnego przy użyciu hello `MSCoreDataStore` udostępnia interfejs, który hello zestaw SDK usługi Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="963dd-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="963dd-132">Alternatywnie można udostępnić inny magazyn lokalny zaimplementowanie hello `MSSyncContextDataSource` protokołu.</span><span class="sxs-lookup"><span data-stu-id="963dd-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="963dd-133">Ponadto hello pierwszy parametr **MSSyncContext** jest używane toospecify obsługi konfliktu.</span><span class="sxs-lookup"><span data-stu-id="963dd-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="963dd-134">Ponieważ firma Microsoft przekazanego `nil`, uzyskujemy hello domyślne konflikt obsługi, który zakończy się niepowodzeniem w przypadku dowolnego konfliktu.</span><span class="sxs-lookup"><span data-stu-id="963dd-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="963dd-135">Teraz załóżmy operacji synchronizacji rzeczywiste hello i Pobierz dane z zdalnego zaplecza hello:</span><span class="sxs-lookup"><span data-stu-id="963dd-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="963dd-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="963dd-136">**Objective-C**.</span></span> <span data-ttu-id="963dd-137">`syncData`najpierw wypchnięcia nowych zmian, a następnie wywołuje **pullData** tooget danych z hello zdalnego systemu wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="963dd-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="963dd-138">Z kolei hello **pullData** — metoda pobiera nowe dane, odpowiadający kwerendy:</span><span class="sxs-lookup"><span data-stu-id="963dd-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

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
* <span data-ttu-id="963dd-139">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="963dd-139">**Swift**:</span></span>
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

<span data-ttu-id="963dd-140">W wersji hello Objective-C w `syncData`, pierwsze wywołanie **pushWithCompletion** hello kontekstu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="963dd-141">Ta metoda jest elementem członkowskim `MSSyncContext` (i nie hello synchronizacji samej tabeli), ponieważ wypycha dane zmiany we wszystkich tabel.</span><span class="sxs-lookup"><span data-stu-id="963dd-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="963dd-142">Tylko te rekordy, które zostały zmodyfikowane w sposób lokalnie (za pośrednictwem operacji CUD) są wysyłane toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="963dd-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="963dd-143">Następnie hello Pomocnika **pullData** zostanie wywołany, które wywołuje **MSSyncTable.pullWithQuery** tooretrieve danych zdalnych i zapisz go w hello lokalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="963dd-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="963dd-144">W wersji Swift hello, hello operacji push nie jest niezbędne, nie istnieje żadne wywołanie za**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="963dd-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="963dd-145">Jeśli istnieją oczekujące zmiany w kontekście synchronizacji hello hello tabeli, która wykonuje operację push, ściągania zawsze wystawia wypychanej najpierw.</span><span class="sxs-lookup"><span data-stu-id="963dd-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="963dd-146">Jednak jeśli masz więcej niż jednej tabeli synchronizacji jest najlepsze tooensure tooexplicitly wywołania wypychania, że wszystko jest spójne w tabelach pokrewnych.</span><span class="sxs-lookup"><span data-stu-id="963dd-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="963dd-147">W hello Objective-C i wersje Swift, można użyć hello **pullWithQuery** rekordów, które mają tooretrieve hello toospecify metody toofilter zapytania.</span><span class="sxs-lookup"><span data-stu-id="963dd-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="963dd-148">W tym przykładzie hello zapytanie pobiera wszystkie rekordy w hello zdalnego `TodoItem` tabeli.</span><span class="sxs-lookup"><span data-stu-id="963dd-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="963dd-149">drugi parametr funkcji Hello **pullWithQuery** jest identyfikator zapytania, który służy do *synchronizacja przyrostowa*. Synchronizacja przyrostowa pobiera tylko te rekordy, które zostały zmodyfikowane od momentu ostatniej synchronizacji hello, przy użyciu rekordu hello `UpdatedAt` sygnaturę czasową (nazywane `updatedAt` w hello lokalnym magazynie.) identyfikator zapytania hello powinny być opisowe ciąg, który jest unikatowy dla każdego zapytania logicznych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="963dd-150">tooopt Brak synchronizacji przyrostowej, Przekaż `nil` jako hello identyfikator zapytania.</span><span class="sxs-lookup"><span data-stu-id="963dd-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="963dd-151">Takie podejście może być potencjalnie nieefektywne, ponieważ pobiera on wszystkie rekordy na każdej operacji ściągania.</span><span class="sxs-lookup"><span data-stu-id="963dd-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="963dd-152">Witaj synchronizacje aplikacji w języku Objective-C, podczas modyfikowania lub dodawanie danych, gdy użytkownik wykona hello gestu odświeżania i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="963dd-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="963dd-153">Swift aplikacji Hello synchronizacji, gdy użytkownik hello wykonuje hello gestu odświeżania i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="963dd-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="963dd-154">Ponieważ hello synchronizacje aplikacji zawsze, gdy dane są zmodyfikowany (Objective-C) lub przy każdym uruchomieniu aplikacji hello (Objective-C i Swift), aplikacji hello przyjęto założenie, że użytkownik hello jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="963dd-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="963dd-155">W dalszej części artykułu spowoduje zaktualizowanie aplikacji hello, dzięki czemu użytkownicy mogą edytować nawet wtedy, gdy są one w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="963dd-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="963dd-156"><a name="review-core-data"></a>Model danych podstawowych hello przeglądu</span><span class="sxs-lookup"><span data-stu-id="963dd-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="963dd-157">Korzystając z magazynu offline hello podstawowych danych, należy zdefiniować określonego tabel i pól w modelu danych.</span><span class="sxs-lookup"><span data-stu-id="963dd-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="963dd-158">Hello Przykładowa aplikacja już zawiera model danych z hello w prawidłowym formacie.</span><span class="sxs-lookup"><span data-stu-id="963dd-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="963dd-159">W tej sekcji możemy przeprowadzenie tooshow te tabele korzystania z nich.</span><span class="sxs-lookup"><span data-stu-id="963dd-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="963dd-160">Otwórz **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="963dd-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="963dd-161">Cztery tabele są zdefiniowane — Witaj trzech, które są używane przez zestaw SDK i używany dla zadania do wykonania hello się elementy:</span><span class="sxs-lookup"><span data-stu-id="963dd-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="963dd-162">MS_TableOperations: Śledzi hello elementy toobe zsynchronizowane z serwerem hello.</span><span class="sxs-lookup"><span data-stu-id="963dd-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="963dd-163">MS_TableOperationErrors: Śledzi wszystkie błędy, które mają miejsce podczas synchronizacji w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="963dd-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="963dd-164">MS_TableConfig: Śledzi hello hello ostatniej operacji synchronizacji dla wszystkich operacji ściągania godziny ostatniej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="963dd-165">TodoItem: Przechowuje hello elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="963dd-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="963dd-166">Witaj kolumny systemowe **createdAt**, **updatedAt**, i **wersji** są właściwości opcjonalne systemu.</span><span class="sxs-lookup"><span data-stu-id="963dd-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="963dd-167">Witaj zestaw SDK usługi Mobile Apps rezerwuje nazwy kolumn, które zaczynają się od "**``**".</span><span class="sxs-lookup"><span data-stu-id="963dd-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="963dd-168">Nie należy używać tego prefiksu z innym niż system kolumn.</span><span class="sxs-lookup"><span data-stu-id="963dd-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="963dd-169">W przeciwnym razie nazwy kolumny są modyfikowane, gdy używasz hello zdalnego wewnętrznej bazy.</span><span class="sxs-lookup"><span data-stu-id="963dd-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="963dd-170">Gdy funkcja hello synchronizacji w trybie offline, zdefiniuj hello trzy tabele systemowe i hello danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="963dd-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="963dd-171">Tabele systemowe</span><span class="sxs-lookup"><span data-stu-id="963dd-171">System tables</span></span>

<span data-ttu-id="963dd-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="963dd-172">**MS_TableOperations**</span></span>  

![Atrybuty tabeli MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="963dd-174">Atrybut</span><span class="sxs-lookup"><span data-stu-id="963dd-174">Attribute</span></span> | <span data-ttu-id="963dd-175">Typ</span><span class="sxs-lookup"><span data-stu-id="963dd-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="963dd-176">id</span><span class="sxs-lookup"><span data-stu-id="963dd-176">id</span></span> | <span data-ttu-id="963dd-177">Liczba całkowita 64</span><span class="sxs-lookup"><span data-stu-id="963dd-177">Integer 64</span></span> |
| <span data-ttu-id="963dd-178">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="963dd-178">itemId</span></span> | <span data-ttu-id="963dd-179">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-179">String</span></span> |
| <span data-ttu-id="963dd-180">properties</span><span class="sxs-lookup"><span data-stu-id="963dd-180">properties</span></span> | <span data-ttu-id="963dd-181">Dane binarne</span><span class="sxs-lookup"><span data-stu-id="963dd-181">Binary Data</span></span> |
| <span data-ttu-id="963dd-182">Tabela</span><span class="sxs-lookup"><span data-stu-id="963dd-182">table</span></span> | <span data-ttu-id="963dd-183">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-183">String</span></span> |
| <span data-ttu-id="963dd-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="963dd-184">tableKind</span></span> | <span data-ttu-id="963dd-185">Liczba całkowita 16</span><span class="sxs-lookup"><span data-stu-id="963dd-185">Integer 16</span></span> |


<span data-ttu-id="963dd-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="963dd-186">**MS_TableOperationErrors**</span></span>

 ![Atrybuty tabeli MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="963dd-188">Atrybut</span><span class="sxs-lookup"><span data-stu-id="963dd-188">Attribute</span></span> | <span data-ttu-id="963dd-189">Typ</span><span class="sxs-lookup"><span data-stu-id="963dd-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="963dd-190">id</span><span class="sxs-lookup"><span data-stu-id="963dd-190">id</span></span> |<span data-ttu-id="963dd-191">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-191">String</span></span> |
| <span data-ttu-id="963dd-192">operationId</span><span class="sxs-lookup"><span data-stu-id="963dd-192">operationId</span></span> |<span data-ttu-id="963dd-193">Liczba całkowita 64</span><span class="sxs-lookup"><span data-stu-id="963dd-193">Integer 64</span></span> |
| <span data-ttu-id="963dd-194">properties</span><span class="sxs-lookup"><span data-stu-id="963dd-194">properties</span></span> |<span data-ttu-id="963dd-195">Dane binarne</span><span class="sxs-lookup"><span data-stu-id="963dd-195">Binary Data</span></span> |
| <span data-ttu-id="963dd-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="963dd-196">tableKind</span></span> |<span data-ttu-id="963dd-197">Liczba całkowita 16</span><span class="sxs-lookup"><span data-stu-id="963dd-197">Integer 16</span></span> |

 <span data-ttu-id="963dd-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="963dd-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="963dd-199">Atrybut</span><span class="sxs-lookup"><span data-stu-id="963dd-199">Attribute</span></span> | <span data-ttu-id="963dd-200">Typ</span><span class="sxs-lookup"><span data-stu-id="963dd-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="963dd-201">id</span><span class="sxs-lookup"><span data-stu-id="963dd-201">id</span></span> |<span data-ttu-id="963dd-202">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-202">String</span></span> |
| <span data-ttu-id="963dd-203">key</span><span class="sxs-lookup"><span data-stu-id="963dd-203">key</span></span> |<span data-ttu-id="963dd-204">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-204">String</span></span> |
| <span data-ttu-id="963dd-205">Właściwość KeyType</span><span class="sxs-lookup"><span data-stu-id="963dd-205">keyType</span></span> |<span data-ttu-id="963dd-206">Liczba całkowita 64</span><span class="sxs-lookup"><span data-stu-id="963dd-206">Integer 64</span></span> |
| <span data-ttu-id="963dd-207">Tabela</span><span class="sxs-lookup"><span data-stu-id="963dd-207">table</span></span> |<span data-ttu-id="963dd-208">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-208">String</span></span> |
| <span data-ttu-id="963dd-209">wartość</span><span class="sxs-lookup"><span data-stu-id="963dd-209">value</span></span> |<span data-ttu-id="963dd-210">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="963dd-211">Tabela danych</span><span class="sxs-lookup"><span data-stu-id="963dd-211">Data table</span></span>

<span data-ttu-id="963dd-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="963dd-212">**TodoItem**</span></span>

| <span data-ttu-id="963dd-213">Atrybut</span><span class="sxs-lookup"><span data-stu-id="963dd-213">Attribute</span></span> | <span data-ttu-id="963dd-214">Typ</span><span class="sxs-lookup"><span data-stu-id="963dd-214">Type</span></span> | <span data-ttu-id="963dd-215">Uwaga</span><span class="sxs-lookup"><span data-stu-id="963dd-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="963dd-216">id</span><span class="sxs-lookup"><span data-stu-id="963dd-216">id</span></span> | <span data-ttu-id="963dd-217">Ciąg, oznaczona jako wymagana</span><span class="sxs-lookup"><span data-stu-id="963dd-217">String, marked required</span></span> |<span data-ttu-id="963dd-218">klucz podstawowy w magazynie zdalnym</span><span class="sxs-lookup"><span data-stu-id="963dd-218">Primary key in remote store</span></span> |
| <span data-ttu-id="963dd-219">Zakończenie</span><span class="sxs-lookup"><span data-stu-id="963dd-219">complete</span></span> | <span data-ttu-id="963dd-220">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="963dd-220">Boolean</span></span> | <span data-ttu-id="963dd-221">Pole elementu zadań do wykonania</span><span class="sxs-lookup"><span data-stu-id="963dd-221">To-do item field</span></span> |
| <span data-ttu-id="963dd-222">Tekst</span><span class="sxs-lookup"><span data-stu-id="963dd-222">text</span></span> |<span data-ttu-id="963dd-223">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-223">String</span></span> |<span data-ttu-id="963dd-224">Pole elementu zadań do wykonania</span><span class="sxs-lookup"><span data-stu-id="963dd-224">To-do item field</span></span> |
| <span data-ttu-id="963dd-225">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="963dd-225">createdAt</span></span> | <span data-ttu-id="963dd-226">Date</span><span class="sxs-lookup"><span data-stu-id="963dd-226">Date</span></span> | <span data-ttu-id="963dd-227">(opcjonalnie) Mapuje zbyt**createdAt** właściwości systemu</span><span class="sxs-lookup"><span data-stu-id="963dd-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="963dd-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="963dd-228">updatedAt</span></span> | <span data-ttu-id="963dd-229">Date</span><span class="sxs-lookup"><span data-stu-id="963dd-229">Date</span></span> | <span data-ttu-id="963dd-230">(opcjonalnie) Mapuje zbyt**updatedAt** właściwości systemu</span><span class="sxs-lookup"><span data-stu-id="963dd-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="963dd-231">Wersja</span><span class="sxs-lookup"><span data-stu-id="963dd-231">version</span></span> | <span data-ttu-id="963dd-232">Ciąg</span><span class="sxs-lookup"><span data-stu-id="963dd-232">String</span></span> | <span data-ttu-id="963dd-233">(opcjonalnie) Używane toodetect konflikty, tooversion mapy</span><span class="sxs-lookup"><span data-stu-id="963dd-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="963dd-234"><a name="setup-sync"></a>Należy zmienić to zachowanie synchronizacji hello aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="963dd-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="963dd-235">W tej sekcji możesz zmodyfikować aplikacji hello tak, aby nie synchronizuje się na początku aplikacji lub podczas wstawiania i aktualizowania elementów.</span><span class="sxs-lookup"><span data-stu-id="963dd-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="963dd-236">Synchronizuje tylko wtedy, gdy przycisk gestu Odśwież hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="963dd-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="963dd-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="963dd-237">**Objective-C**:</span></span>

1. <span data-ttu-id="963dd-238">W **QSTodoListViewController.m**, zmień hello **viewDidLoad** tooremove metody hello wywołanie za`[self refresh]` na końcu hello hello metody.</span><span class="sxs-lookup"><span data-stu-id="963dd-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="963dd-239">Teraz hello danych nie jest zsynchronizowane z serwerem powitania po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="963dd-240">Zamiast tego jest synchronizowany z zawartością hello hello magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="963dd-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="963dd-241">W **QSTodoService.m**, zmodyfikuj definicję hello `addItem` tak, aby nie synchronizacji, po wstawieniu elementu hello.</span><span class="sxs-lookup"><span data-stu-id="963dd-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="963dd-242">Usuń hello `self syncData` zablokować i zastąp go hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="963dd-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="963dd-243">Modyfikowanie definicji hello `completeItem` jak wspomniano powyżej.</span><span class="sxs-lookup"><span data-stu-id="963dd-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="963dd-244">Usuń blok hello `self syncData` i zastąp go hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="963dd-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="963dd-245">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="963dd-245">**Swift**:</span></span>

<span data-ttu-id="963dd-246">W `viewDidLoad`w **ToDoTableViewController.swift**, komentarz dwa wiersze hello pokazane toostop synchronizowanie po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="963dd-247">W czasie hello pisania tego dokumentu aplikacji Swift Todo hello nie aktualizowania usługi hello, gdy ktoś dodaje lub zakończeniu elementu.</span><span class="sxs-lookup"><span data-stu-id="963dd-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="963dd-248">Aktualizuje usługę hello tylko po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="963dd-249"><a name="test-app"></a>Aplikacja hello testu</span><span class="sxs-lookup"><span data-stu-id="963dd-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="963dd-250">W tej sekcji możesz połączyć tooan nieprawidłowy adres URL toosimulate scenariusz w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="963dd-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="963dd-251">Po dodaniu elementów danych są przechowywane w hello przechowywać dane lokalne Core, ale nie są one zsynchronizowane z zaplecza aplikacji mobilnej hello.</span><span class="sxs-lookup"><span data-stu-id="963dd-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="963dd-252">Zmień adres URL aplikacji mobilnej hello w **QSTodoService.m** tooan nieprawidłowy adres URL i ponownie uruchom hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="963dd-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="963dd-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="963dd-253">**Objective-C**.</span></span> <span data-ttu-id="963dd-254">W QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="963dd-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="963dd-255">**Kod SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="963dd-255">**Swift**.</span></span> <span data-ttu-id="963dd-256">W ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="963dd-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="963dd-257">Dodać niektóre elementy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="963dd-257">Add some to-do items.</span></span> <span data-ttu-id="963dd-258">Zamknij symulator hello (lub hello wymuszanie zamknięcia aplikacji), a następnie uruchom go ponownie.</span><span class="sxs-lookup"><span data-stu-id="963dd-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="963dd-259">Sprawdź, czy zachować zmiany.</span><span class="sxs-lookup"><span data-stu-id="963dd-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="963dd-260">Wyświetl zawartość hello hello zdalnego **TodoItem** tabeli:</span><span class="sxs-lookup"><span data-stu-id="963dd-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="963dd-261">Dla środowiska Node.js zaplecze, przejdź toohello [portalu Azure](https://portal.azure.com/) i w Twojej aplikacji mobilnej wewnętrznej, kliknij przycisk **łatwe tabel** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="963dd-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="963dd-262">Dla programu .NET w ponownie zakończyć, użyj narzędzia SQL, takich jak SQL Server Management Studio lub klienta REST, takiego jak Fiddler lub Postman.</span><span class="sxs-lookup"><span data-stu-id="963dd-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="963dd-263">Sprawdź, czy nowe elementy hello *nie* zostały zsynchronizowane z serwerem hello.</span><span class="sxs-lookup"><span data-stu-id="963dd-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="963dd-264">Zmiany hello adresu URL wstecz toohello Popraw jedną w **QSTodoService.m**i uruchom ponownie hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="963dd-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="963dd-265">Wykonaj hello odświeżania gestu przez ściąganie dół hello listy elementów.</span><span class="sxs-lookup"><span data-stu-id="963dd-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="963dd-266">Pokrętła postępu jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="963dd-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="963dd-267">Widok hello **TodoItem** danych ponownie.</span><span class="sxs-lookup"><span data-stu-id="963dd-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="963dd-268">Witaj nowe i zmienione wykonania powinna być teraz wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="963dd-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="963dd-269">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="963dd-269">Summary</span></span>
<span data-ttu-id="963dd-270">Funkcja synchronizacji w trybie offline hello toosupport, użyliśmy hello `MSSyncTable` interfejsu i zainicjować `MSClient.syncContext` z lokalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="963dd-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="963dd-271">W takim przypadku Magazyn lokalny hello został bazy danych opartej na danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="963dd-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="963dd-272">Korzystając z lokalnego magazynu danych podstawowe, należy zdefiniować wiele tabel o hello [Popraw właściwości systemu](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="963dd-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="963dd-273">Normalny Hello tworzenia, odczytu, aktualizacji i usuwania operacji (CRUD) do pracy aplikacji mobilnych tak, jakby aplikacji hello jest nadal połączony, ale wszystkie operacje hello są wykonywane przed hello magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="963dd-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="963dd-274">Witaj w lokalnym magazynie firma Microsoft synchronizowane z serwerem hello, użyliśmy hello **MSSyncTable.pullWithQuery** metody.</span><span class="sxs-lookup"><span data-stu-id="963dd-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="963dd-275">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="963dd-275">Additional resources</span></span>
* <span data-ttu-id="963dd-276">[synchronizacji danych w trybie Offline w aplikacjach mobilnych]</span><span class="sxs-lookup"><span data-stu-id="963dd-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="963dd-277">[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services] \(jest hello wideo dotyczące usługi Mobile Services, ale działa synchronizacja Mobile Apps w tryb offline w podobny sposób.\)</span><span class="sxs-lookup"><span data-stu-id="963dd-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[tworzenie aplikacji systemu iOS]: app-service-mobile-ios-get-started.md
[synchronizacji danych w trybie Offline w aplikacjach mobilnych]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
