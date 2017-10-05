---
title: "Włącz synchronizację w trybie offline z aplikacji mobilnych systemu iOS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać aplikacji mobilnych w usłudze Azure App Service na potrzeby pamięci podręcznej i synchronizacji danych w trybie offline w aplikacjach systemu iOS."
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
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="b9ffe-103">Włącz synchronizację w trybie offline z aplikacji mobilnych systemu iOS</span><span class="sxs-lookup"><span data-stu-id="b9ffe-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="b9ffe-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b9ffe-104">Overview</span></span>
<span data-ttu-id="b9ffe-105">Ten samouczek obejmuje synchronizacji w trybie offline z funkcji Mobile Apps w usłudze Azure App Service dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="b9ffe-106">Z synchronizacji w trybie offline w użytkownicy końcowi mogą współdziałać z aplikacji mobilnej, aby wyświetlić, dodawanie lub modyfikowanie danych, nawet w przypadku, gdy mają oni połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="b9ffe-107">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-107">Changes are stored in a local database.</span></span> <span data-ttu-id="b9ffe-108">Gdy urządzenie jest w trybie online, zmiany są synchronizowane z zdalnego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="b9ffe-109">Jeśli jest to usprawnić pierwszy Mobile Apps, należy najpierw Ukończ samouczek [tworzenie aplikacji systemu iOS].</span><span class="sxs-lookup"><span data-stu-id="b9ffe-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="b9ffe-110">Jeśli projekt pobrany szybki start serwera nie jest używany, należy dodać pakietów rozszerzenia dostępu do danych do projektu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="b9ffe-111">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="b9ffe-112">Aby dowiedzieć się więcej na temat funkcji synchronizacji w trybie offline, zobacz [synchronizacji danych w trybie Offline w aplikacjach mobilnych].</span><span class="sxs-lookup"><span data-stu-id="b9ffe-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="b9ffe-113"><a name="review-sync"></a>Przegląd kodu klienta synchronizacji</span><span class="sxs-lookup"><span data-stu-id="b9ffe-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="b9ffe-114">Projekt klienta, który został pobrany dla [tworzenie aplikacji systemu iOS] samouczek już zawiera kod, który obsługuje synchronizacji w trybie offline przy użyciu lokalnej bazy danych na podstawie danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="b9ffe-115">Ta sekcja zawiera podsumowanie, co jest już uwzględniony w kodzie samouczka.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="b9ffe-116">Omówienie koncepcji funkcji, zobacz [synchronizacji danych w trybie Offline w aplikacjach mobilnych].</span><span class="sxs-lookup"><span data-stu-id="b9ffe-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="b9ffe-117">Za pomocą funkcji synchronizacji danych w trybie offline Mobile Apps, użytkownicy końcowi mogą współdziałać z lokalnej bazy danych nawet wtedy, gdy sieć jest niedostępna.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="b9ffe-118">Aby używać tych funkcji w aplikacji, zainicjować kontekstu synchronizacji z `MSClient` i referencyjne Magazyn lokalny.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="b9ffe-119">Odwołania do tabeli, a następnie **MSSyncTable** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="b9ffe-120">W **QSTodoService.m** (Objective-C) lub **ToDoTableViewController.swift** (Swift), zwróć uwagę, że typ elementu członkowskiego **syncTable** jest **MSSyncTable** .</span><span class="sxs-lookup"><span data-stu-id="b9ffe-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="b9ffe-121">Synchronizacja w trybie offline używa tego interfejsu tabeli synchronizacji zamiast **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="b9ffe-122">W przypadku tabeli synchronizacji wszystkie operacje przejdź do lokalnego magazynu i są synchronizowane tylko w przypadku zdalnego wewnętrznej z jawnym operacje wypychania i ściągania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="b9ffe-123">Aby pobrać odwołanie do tabeli synchronizacji, użyj **syncTableWithName** metoda `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="b9ffe-124">Aby usunąć funkcji synchronizacji w trybie offline, użyj **tableWithName** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="b9ffe-125">Aby można było wykonać wszystkie operacje tabeli, muszą zostać zainicjowane magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="b9ffe-126">W tym miejscu jest odpowiedni kod:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-126">Here is the relevant code:</span></span>

* <span data-ttu-id="b9ffe-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-127">**Objective-C**.</span></span> <span data-ttu-id="b9ffe-128">W **QSTodoService.init** metody:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="b9ffe-129">**Kod SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-129">**Swift**.</span></span> <span data-ttu-id="b9ffe-130">W **ToDoTableViewController.viewDidLoad** metody:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="b9ffe-131">Ta metoda tworzy magazynu lokalnego przy użyciu `MSCoreDataStore` interfejs, który zawiera zestaw SDK usługi Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="b9ffe-132">Alternatywnie można udostępnić inny magazyn lokalny zaimplementowanie `MSSyncContextDataSource` protokołu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="b9ffe-133">Ponadto pierwszy parametr **MSSyncContext** służy do określania obsługi konfliktu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="b9ffe-134">Ponieważ firma Microsoft przekazanego `nil`, uzyskujemy domyślne obsługi konfliktu, który zakończy się niepowodzeniem w przypadku dowolnego konfliktu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="b9ffe-135">Teraz załóżmy operacji synchronizacji rzeczywiste i Pobierz dane z zdalnego zaplecza:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="b9ffe-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-136">**Objective-C**.</span></span> <span data-ttu-id="b9ffe-137">`syncData`najpierw wypchnięcia nowych zmian, a następnie wywołuje **pullData** można pobrać danych z zdalnego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="b9ffe-138">Z kolei **pullData** — metoda pobiera nowe dane, odpowiadający kwerendy:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="b9ffe-139">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="b9ffe-140">W wersji języka Objective-C w `syncData`, pierwsze wywołanie **pushWithCompletion** w kontekście synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="b9ffe-141">Ta metoda jest elementem członkowskim `MSSyncContext` (i nie w tabeli synchronizacji, sam), ponieważ wypycha dane zmiany we wszystkich tabel.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="b9ffe-142">Tylko te rekordy, które zostały zmodyfikowane w sposób lokalnie (za pośrednictwem operacji CUD) są wysyłane do serwera.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="b9ffe-143">Następnie Pomocnika **pullData** zostanie wywołany, które wywołuje **MSSyncTable.pullWithQuery** pobierania zdalnych danych i zapisz go w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="b9ffe-144">W wersji Swift operacji push nie jest bezwzględnie konieczne, nie istnieje żadne wywołanie **pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="b9ffe-145">Jeśli istnieją oczekujące zmiany w kontekście synchronizacji dla tabeli, która wykonuje operację push, ściągania zawsze wystawia wypychanej najpierw.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="b9ffe-146">Jeśli masz więcej niż jednej tabeli synchronizacji, najlepiej jawnie wywołać wypychania upewnij się, że wszystko jest spójne w tabelach pokrewnych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="b9ffe-147">W języku Objective C i wersje Swift, można użyć **pullWithQuery** metodę, aby określić kwerendy do filtrowania rekordów do pobrania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="b9ffe-148">W tym przykładzie zapytanie pobiera wszystkie rekordy w obiekcie zdalnym `TodoItem` tabeli.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="b9ffe-149">Drugi parametr funkcji **pullWithQuery** jest identyfikator zapytania, który służy do *synchronizacja przyrostowa*.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="b9ffe-150">Synchronizacja przyrostowa pobiera tylko te rekordy, które zostały zmodyfikowane od ostatniej synchronizacji, przy użyciu rekordu `UpdatedAt` sygnaturę czasową (nazywane `updatedAt` w magazynie lokalnym.) Identyfikator kwerendy powinna być opisowe ciąg, który jest unikatowy dla każdego zapytania logicznych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="b9ffe-151">Aby zrezygnować z synchronizacji przyrostowej, należy przekazać `nil` jako identyfikator zapytania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="b9ffe-152">Takie podejście może być potencjalnie nieefektywne, ponieważ pobiera on wszystkie rekordy na każdej operacji ściągania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="b9ffe-153">Aplikacji języka Objective C jest synchronizowane podczas modyfikowania lub dodawanie danych, gdy użytkownik wykona gestu odświeżania i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="b9ffe-154">Przeprowadza synchronizację Swift aplikacji, gdy użytkownik wykonuje gestu odświeżania i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="b9ffe-155">Synchronizacje aplikacji zawsze, gdy dane są zmodyfikowana (Objective-C) lub przy każdym uruchomieniu aplikacji (Objective-C i Swift), aplikacji przyjęto założenie, że użytkownik jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="b9ffe-156">W dalszej części artykułu spowoduje zaktualizowanie aplikacji, dzięki czemu użytkownicy mogą edytować nawet wtedy, gdy są one w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="b9ffe-157"><a name="review-core-data"></a>Przegląd modelu danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="b9ffe-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="b9ffe-158">Korzystając z magazynu offline podstawowych danych, należy zdefiniować określonego tabel i pól w modelu danych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="b9ffe-159">Przykładowa aplikacja już zawiera model danych z prawidłowym formacie.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="b9ffe-160">W tej sekcji możemy przeprowadzenie te tabele, aby pokazać, jak są one używane.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="b9ffe-161">Otwórz **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="b9ffe-162">Cztery tabele są zdefiniowane — trzech, które są używane przez zestaw SDK i używany dla zadania do wykonania elementy się:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="b9ffe-163">MS_TableOperations: Śledzi elementy, które muszą zostać zsynchronizowane z serwerem.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="b9ffe-164">MS_TableOperationErrors: Śledzi wszystkie błędy, które mają miejsce podczas synchronizacji w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="b9ffe-165">MS_TableConfig: Śledzi ostatniej aktualizacji czas ostatniej operacji synchronizacji dla wszystkich operacji ściągania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="b9ffe-166">TodoItem: Przechowuje elementy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="b9ffe-167">Kolumny systemowe **createdAt**, **updatedAt**, i **wersji** są właściwości opcjonalne systemu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="b9ffe-168">Zestaw SDK usługi Mobile Apps rezerwuje nazwy kolumn, które zaczynają się od "**``**".</span><span class="sxs-lookup"><span data-stu-id="b9ffe-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="b9ffe-169">Nie należy używać tego prefiksu z innym niż system kolumn.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="b9ffe-170">W przeciwnym razie wartość nazwy kolumny są modyfikowane, gdy używasz zdalnego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="b9ffe-171">Korzystając z funkcji synchronizacji w trybie offline, zdefiniuj tabel systemowych trzy i tabelę danych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="b9ffe-172">Tabele systemowe</span><span class="sxs-lookup"><span data-stu-id="b9ffe-172">System tables</span></span>

<span data-ttu-id="b9ffe-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-173">**MS_TableOperations**</span></span>  

![Atrybuty tabeli MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="b9ffe-175">Atrybut</span><span class="sxs-lookup"><span data-stu-id="b9ffe-175">Attribute</span></span> | <span data-ttu-id="b9ffe-176">Typ</span><span class="sxs-lookup"><span data-stu-id="b9ffe-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="b9ffe-177">id</span><span class="sxs-lookup"><span data-stu-id="b9ffe-177">id</span></span> | <span data-ttu-id="b9ffe-178">Liczba całkowita 64</span><span class="sxs-lookup"><span data-stu-id="b9ffe-178">Integer 64</span></span> |
| <span data-ttu-id="b9ffe-179">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="b9ffe-179">itemId</span></span> | <span data-ttu-id="b9ffe-180">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-180">String</span></span> |
| <span data-ttu-id="b9ffe-181">properties</span><span class="sxs-lookup"><span data-stu-id="b9ffe-181">properties</span></span> | <span data-ttu-id="b9ffe-182">Dane binarne</span><span class="sxs-lookup"><span data-stu-id="b9ffe-182">Binary Data</span></span> |
| <span data-ttu-id="b9ffe-183">Tabela</span><span class="sxs-lookup"><span data-stu-id="b9ffe-183">table</span></span> | <span data-ttu-id="b9ffe-184">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-184">String</span></span> |
| <span data-ttu-id="b9ffe-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="b9ffe-185">tableKind</span></span> | <span data-ttu-id="b9ffe-186">Liczba całkowita 16</span><span class="sxs-lookup"><span data-stu-id="b9ffe-186">Integer 16</span></span> |


<span data-ttu-id="b9ffe-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-187">**MS_TableOperationErrors**</span></span>

 ![Atrybuty tabeli MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="b9ffe-189">Atrybut</span><span class="sxs-lookup"><span data-stu-id="b9ffe-189">Attribute</span></span> | <span data-ttu-id="b9ffe-190">Typ</span><span class="sxs-lookup"><span data-stu-id="b9ffe-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="b9ffe-191">id</span><span class="sxs-lookup"><span data-stu-id="b9ffe-191">id</span></span> |<span data-ttu-id="b9ffe-192">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-192">String</span></span> |
| <span data-ttu-id="b9ffe-193">operationId</span><span class="sxs-lookup"><span data-stu-id="b9ffe-193">operationId</span></span> |<span data-ttu-id="b9ffe-194">Liczba całkowita 64</span><span class="sxs-lookup"><span data-stu-id="b9ffe-194">Integer 64</span></span> |
| <span data-ttu-id="b9ffe-195">properties</span><span class="sxs-lookup"><span data-stu-id="b9ffe-195">properties</span></span> |<span data-ttu-id="b9ffe-196">Dane binarne</span><span class="sxs-lookup"><span data-stu-id="b9ffe-196">Binary Data</span></span> |
| <span data-ttu-id="b9ffe-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="b9ffe-197">tableKind</span></span> |<span data-ttu-id="b9ffe-198">Liczba całkowita 16</span><span class="sxs-lookup"><span data-stu-id="b9ffe-198">Integer 16</span></span> |

 <span data-ttu-id="b9ffe-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="b9ffe-200">Atrybut</span><span class="sxs-lookup"><span data-stu-id="b9ffe-200">Attribute</span></span> | <span data-ttu-id="b9ffe-201">Typ</span><span class="sxs-lookup"><span data-stu-id="b9ffe-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="b9ffe-202">id</span><span class="sxs-lookup"><span data-stu-id="b9ffe-202">id</span></span> |<span data-ttu-id="b9ffe-203">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-203">String</span></span> |
| <span data-ttu-id="b9ffe-204">key</span><span class="sxs-lookup"><span data-stu-id="b9ffe-204">key</span></span> |<span data-ttu-id="b9ffe-205">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-205">String</span></span> |
| <span data-ttu-id="b9ffe-206">Właściwość KeyType</span><span class="sxs-lookup"><span data-stu-id="b9ffe-206">keyType</span></span> |<span data-ttu-id="b9ffe-207">Liczba całkowita 64</span><span class="sxs-lookup"><span data-stu-id="b9ffe-207">Integer 64</span></span> |
| <span data-ttu-id="b9ffe-208">Tabela</span><span class="sxs-lookup"><span data-stu-id="b9ffe-208">table</span></span> |<span data-ttu-id="b9ffe-209">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-209">String</span></span> |
| <span data-ttu-id="b9ffe-210">wartość</span><span class="sxs-lookup"><span data-stu-id="b9ffe-210">value</span></span> |<span data-ttu-id="b9ffe-211">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="b9ffe-212">Tabela danych</span><span class="sxs-lookup"><span data-stu-id="b9ffe-212">Data table</span></span>

<span data-ttu-id="b9ffe-213">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="b9ffe-213">**TodoItem**</span></span>

| <span data-ttu-id="b9ffe-214">Atrybut</span><span class="sxs-lookup"><span data-stu-id="b9ffe-214">Attribute</span></span> | <span data-ttu-id="b9ffe-215">Typ</span><span class="sxs-lookup"><span data-stu-id="b9ffe-215">Type</span></span> | <span data-ttu-id="b9ffe-216">Uwaga</span><span class="sxs-lookup"><span data-stu-id="b9ffe-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9ffe-217">id</span><span class="sxs-lookup"><span data-stu-id="b9ffe-217">id</span></span> | <span data-ttu-id="b9ffe-218">Ciąg, oznaczona jako wymagana</span><span class="sxs-lookup"><span data-stu-id="b9ffe-218">String, marked required</span></span> |<span data-ttu-id="b9ffe-219">klucz podstawowy w magazynie zdalnym</span><span class="sxs-lookup"><span data-stu-id="b9ffe-219">Primary key in remote store</span></span> |
| <span data-ttu-id="b9ffe-220">Zakończenie</span><span class="sxs-lookup"><span data-stu-id="b9ffe-220">complete</span></span> | <span data-ttu-id="b9ffe-221">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b9ffe-221">Boolean</span></span> | <span data-ttu-id="b9ffe-222">Pole elementu zadań do wykonania</span><span class="sxs-lookup"><span data-stu-id="b9ffe-222">To-do item field</span></span> |
| <span data-ttu-id="b9ffe-223">Tekst</span><span class="sxs-lookup"><span data-stu-id="b9ffe-223">text</span></span> |<span data-ttu-id="b9ffe-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-224">String</span></span> |<span data-ttu-id="b9ffe-225">Pole elementu zadań do wykonania</span><span class="sxs-lookup"><span data-stu-id="b9ffe-225">To-do item field</span></span> |
| <span data-ttu-id="b9ffe-226">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="b9ffe-226">createdAt</span></span> | <span data-ttu-id="b9ffe-227">Date</span><span class="sxs-lookup"><span data-stu-id="b9ffe-227">Date</span></span> | <span data-ttu-id="b9ffe-228">(opcjonalnie) Mapuje **createdAt** właściwości systemu</span><span class="sxs-lookup"><span data-stu-id="b9ffe-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="b9ffe-229">updatedAt</span><span class="sxs-lookup"><span data-stu-id="b9ffe-229">updatedAt</span></span> | <span data-ttu-id="b9ffe-230">Date</span><span class="sxs-lookup"><span data-stu-id="b9ffe-230">Date</span></span> | <span data-ttu-id="b9ffe-231">(opcjonalnie) Mapuje **updatedAt** właściwości systemu</span><span class="sxs-lookup"><span data-stu-id="b9ffe-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="b9ffe-232">Wersja</span><span class="sxs-lookup"><span data-stu-id="b9ffe-232">version</span></span> | <span data-ttu-id="b9ffe-233">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b9ffe-233">String</span></span> | <span data-ttu-id="b9ffe-234">(opcjonalnie) Używane do wykrywania konfliktów, mapy wersji</span><span class="sxs-lookup"><span data-stu-id="b9ffe-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="b9ffe-235"><a name="setup-sync"></a>Należy zmienić to zachowanie synchronizacji aplikacji</span><span class="sxs-lookup"><span data-stu-id="b9ffe-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="b9ffe-236">W tej sekcji możesz zmodyfikować aplikację tak, aby nie synchronizuje się na początku aplikacji lub podczas wstawiania i aktualizowania elementów.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="b9ffe-237">Synchronizuje tylko wtedy, gdy jest wykonywana na przycisku odświeżania gestu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="b9ffe-238">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-238">**Objective-C**:</span></span>

1. <span data-ttu-id="b9ffe-239">W **QSTodoListViewController.m**, zmień **viewDidLoad** metodę, aby usunąć wywołanie `[self refresh]` na końcu metody.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="b9ffe-240">Teraz danych nie jest zsynchronizowane z serwerem, po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="b9ffe-241">Zamiast tego jest synchronizowany z zawartością magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="b9ffe-242">W **QSTodoService.m**, zmodyfikować definicję `addItem` tak, aby nie synchronizacji, po wstawieniu elementu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="b9ffe-243">Usuń `self syncData` blokować i zastąp go następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="b9ffe-244">Zmodyfikować definicję `completeItem` jak wspomniano powyżej.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="b9ffe-245">Usuń blok dla `self syncData` i zastąp go następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="b9ffe-246">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-246">**Swift**:</span></span>

<span data-ttu-id="b9ffe-247">W `viewDidLoad`w **ToDoTableViewController.swift**, komentarz dwa wiersze, które są wyświetlane tutaj, aby zatrzymać synchronizację po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="b9ffe-248">W momencie pisania tego dokumentu aplikacji Swift Todo nie powoduje aktualizacji usługi, gdy ktoś dodaje lub zakończeniu elementu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="b9ffe-249">Aktualizuje usługę tylko po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="b9ffe-250"><a name="test-app"></a>Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b9ffe-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="b9ffe-251">W tej sekcji można podłączyć się do nieprawidłowego adresu URL do symulowania scenariusz w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="b9ffe-252">Po dodaniu elementów danych są przechowywane w magazynu danych podstawowych lokalnym, ale nie są one zsynchronizowane z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="b9ffe-253">Zmień adres URL aplikacji mobilnej w **QSTodoService.m** nieprawidłowy adres URL, i ponownie uruchom aplikację:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="b9ffe-254">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-254">**Objective-C**.</span></span> <span data-ttu-id="b9ffe-255">W QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="b9ffe-256">**Kod SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-256">**Swift**.</span></span> <span data-ttu-id="b9ffe-257">W ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="b9ffe-258">Dodać niektóre elementy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-258">Add some to-do items.</span></span> <span data-ttu-id="b9ffe-259">Zamknij symulator (lub Wymuś Zamknij aplikację), a następnie uruchom go ponownie.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="b9ffe-260">Sprawdź, czy zachować zmiany.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="b9ffe-261">Wyświetlanie zawartości zdalnego **TodoItem** tabeli:</span><span class="sxs-lookup"><span data-stu-id="b9ffe-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="b9ffe-262">Dla środowiska Node.js zaplecze, przejdź do [portalu Azure](https://portal.azure.com/) i w Twojej aplikacji mobilnej wewnętrznej, kliknij przycisk **łatwe tabel** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="b9ffe-263">Dla programu .NET w ponownie zakończyć, użyj narzędzia SQL, takich jak SQL Server Management Studio lub klienta REST, takiego jak Fiddler lub Postman.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="b9ffe-264">Upewnij się, że nowe elementy *nie* zostały zsynchronizowane z serwerem.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="b9ffe-265">Zmień adres URL właściwą **QSTodoService.m**, a następnie ponownie uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="b9ffe-266">Wykonuje gestu odświeżania ściąganie w dół na liście elementów.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="b9ffe-267">Pokrętła postępu jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="b9ffe-268">Widok **TodoItem** danych ponownie.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="b9ffe-269">Nowe i zmienione wykonania powinna być teraz wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="b9ffe-270">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b9ffe-270">Summary</span></span>
<span data-ttu-id="b9ffe-271">Aby zapewnić obsługę funkcji synchronizacji w trybie offline, użyliśmy `MSSyncTable` interfejsu i zainicjować `MSClient.syncContext` z lokalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="b9ffe-272">W takim przypadku Magazyn lokalny jest bazy danych opartej na danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="b9ffe-273">Korzystając z lokalnego magazynu danych podstawowe, należy zdefiniować wiele tabel o [Popraw właściwości systemu](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="b9ffe-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="b9ffe-274">Normalne tworzenia, odczytu, aktualizacji operacji i usuwania (CRUD) na pracę aplikacji mobilnych tak, jakby aplikacji jest nadal połączony, ale wszystkie operacje są wykonywane przed magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="b9ffe-275">Lokalny magazyn firma Microsoft synchronizowane z serwerem, użyliśmy **MSSyncTable.pullWithQuery** metody.</span><span class="sxs-lookup"><span data-stu-id="b9ffe-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9ffe-276">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b9ffe-276">Additional resources</span></span>
* <span data-ttu-id="b9ffe-277">[synchronizacji danych w trybie Offline w aplikacjach mobilnych]</span><span class="sxs-lookup"><span data-stu-id="b9ffe-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="b9ffe-278">[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services] \(jest wideo dotyczące usługi Mobile Services, ale działa synchronizacja Mobile Apps w tryb offline w podobny sposób.\)</span><span class="sxs-lookup"><span data-stu-id="b9ffe-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="b9ffe-279">[tworzenie aplikacji systemu iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b9ffe-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="b9ffe-280">[synchronizacji danych w trybie Offline w aplikacjach mobilnych]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="b9ffe-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="b9ffe-281">[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="b9ffe-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
