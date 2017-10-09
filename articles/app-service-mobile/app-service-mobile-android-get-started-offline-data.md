---
title: Synchronizacja w trybie offline aaaEnable aplikacji mobilnej Azure (Android)
description: "Dowiedz się, jak toouse App Service Mobile Apps toocache i synchronizacji danych w trybie offline w aplikacji systemu Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="75247-103">Włączanie synchronizacji w trybie offline dla twojej aplikacji mobilnej systemu Android</span><span class="sxs-lookup"><span data-stu-id="75247-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="75247-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="75247-104">Overview</span></span>
<span data-ttu-id="75247-105">Ten samouczek obejmuje funkcji synchronizacji w trybie offline hello Azure Mobile Apps dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="75247-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="75247-106">Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="75247-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="75247-107">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="75247-107">Changes are stored in a local database.</span></span> <span data-ttu-id="75247-108">Po powrocie do trybu online urządzenia hello te zmiany są synchronizowane z hello zdalnego wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="75247-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="75247-109">Jeśli jest to środowiska pierwszy z usługą Azure Mobile Apps, najpierw należy wykonać samouczek hello [Utwórz aplikację systemu Android].</span><span class="sxs-lookup"><span data-stu-id="75247-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="75247-110">Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać hello danych access rozszerzenia pakietów tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="75247-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="75247-111">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="75247-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="75247-112">toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="75247-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="75247-113">Synchronizacja w trybie offline toosupport aplikacji hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="75247-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="75247-114">Z synchronizacji w trybie offline, przeczytaj zapisu tooand z *synchronizacji tabeli* (przy użyciu hello *IMobileServiceSyncTable* interfejsu), który jest częścią **SQLite** bazy danych na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="75247-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="75247-115">zmiany toopush i ściągania między hello urządzeń i usług Azure Mobile Services, użyj *kontekst synchronizacji* (*MobileServiceClient.SyncContext*), który należy zainicjować z lokalnej bazy danych hello dane toostore lokalnie.</span><span class="sxs-lookup"><span data-stu-id="75247-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="75247-116">W `TodoActivity.java`, komentarz hello istniejącą definicję `mToDoTable` i Usuń komentarz hello synchronizacji tabeli wersji:</span><span class="sxs-lookup"><span data-stu-id="75247-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="75247-117">W hello `onCreate` metody komentarz inicjowanie istniejących hello `mToDoTable` i Usuń komentarz tej definicji:</span><span class="sxs-lookup"><span data-stu-id="75247-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="75247-118">W `refreshItemsFromTable` komentarz definicję hello `results` i Usuń komentarz tej definicji:</span><span class="sxs-lookup"><span data-stu-id="75247-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="75247-119">Komentarz definicję hello `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="75247-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="75247-120">Usuń znaczniki komentarza definicji hello `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="75247-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="75247-121">Usuń znaczniki komentarza definicji hello `sync`:</span><span class="sxs-lookup"><span data-stu-id="75247-121">Uncomment hello definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a><span data-ttu-id="75247-122">Aplikacja hello testu</span><span class="sxs-lookup"><span data-stu-id="75247-122">Test hello app</span></span>
<span data-ttu-id="75247-123">W tej sekcji testu na powitania zachowanie w przypadku sieci Wi-Fi, a następnie wyłącz toocreate sieci Wi-Fi scenariusz w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="75247-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="75247-124">Po dodaniu elementów danych przechowywane są w lokalnym magazynie SQLite hello, ale nie zsynchronizowano toohello usługi mobilnej do momentu kliknięcia hello **Odśwież** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75247-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="75247-125">Inne aplikacje mogą mieć inne wymagania dotyczące gdy danych potrzebuje toobe zsynchronizowane, ale dla celów demonstracyjnych ten samouczek ma hello użytkownik jawnie żądania.</span><span class="sxs-lookup"><span data-stu-id="75247-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="75247-126">Po naciśnięciu tego przycisku uruchamiania nowego zadania w tle.</span><span class="sxs-lookup"><span data-stu-id="75247-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="75247-127">Wypycha go najpierw wszystkie zmiany wprowadzone toohello magazynu lokalnego przy użyciu kontekstu synchronizacji, a następnie ściąga zmienione dane z lokalnej tabeli toohello platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="75247-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="75247-128">Testowanie w trybie offline</span><span class="sxs-lookup"><span data-stu-id="75247-128">Offline testing</span></span>
1. <span data-ttu-id="75247-129">Miejsce hello urządzenie lub symulator w *tryb samolotowy*.</span><span class="sxs-lookup"><span data-stu-id="75247-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="75247-130">Spowoduje to utworzenie scenariusz w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="75247-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="75247-131">Dodaj raporty *ToDo* elementy lub znak niektóre elementy jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="75247-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="75247-132">Zamknij hello urządzenie lub symulator (lub hello wymuszanie zamknięcia aplikacji) i uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="75247-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="75247-133">Sprawdź, czy zmiany zostały utrwalone na urządzeniu hello ponieważ są one przechowywane w lokalnym magazynie SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="75247-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="75247-134">Wyświetl zawartość hello hello Azure *TodoItem* tabeli za pomocą narzędzia SQL, takich jak *programu SQL Server Management Studio*, lub klienta REST, takich jak *Fiddler* lub  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="75247-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="75247-135">Sprawdź, czy nowe elementy hello *nie* zostały zsynchronizowane toohello serwera</span><span class="sxs-lookup"><span data-stu-id="75247-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="75247-136">Dla zaplecza Node.js go toohello [portalu Azure](https://portal.azure.com/), i w aplikacji mobilnej kliknij zaplecza **łatwe tabel** > **TodoItem** tooview zawartość hello hello `TodoItem` tabeli.</span><span class="sxs-lookup"><span data-stu-id="75247-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="75247-137">Dla zaplecza .NET, Wyświetl hello tabelę zawartości za pomocą narzędzia SQL takich jak *programu SQL Server Management Studio*, lub klienta REST, takich jak *Fiddler* lub *Postman*.</span><span class="sxs-lookup"><span data-stu-id="75247-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="75247-138">Włącz sieci Wi-Fi w hello urządzenie lub symulator.</span><span class="sxs-lookup"><span data-stu-id="75247-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="75247-139">Następnie naciśnij klawisz hello **Odśwież** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75247-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="75247-140">Przeglądanie danych TodoItem hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="75247-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="75247-141">Witaj, które są nowe i zmienione TodoItems powinien zostać wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="75247-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75247-142">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="75247-142">Additional Resources</span></span>
* <span data-ttu-id="75247-143">[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="75247-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="75247-144">[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services] \(Uwaga: hello wideo znajduje się w usłudze Mobile Services, ale synchronizacji w trybie offline działa w podobny sposób jak w usłudze Azure Mobile Apps\)</span><span class="sxs-lookup"><span data-stu-id="75247-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md

[Utwórz aplikację systemu Android]: app-service-mobile-android-get-started.md

[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

