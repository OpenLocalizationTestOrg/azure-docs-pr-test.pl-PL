---
title: "Włączanie synchronizacji w trybie offline dla aplikacji mobilnej Azure (Android)"
description: "Dowiedz się, jak używać App Service Mobile Apps do pamięci podręcznej i synchronizacji danych w trybie offline w aplikacji systemu Android"
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
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="f3ba3-103">Włączanie synchronizacji w trybie offline dla twojej aplikacji mobilnej systemu Android</span><span class="sxs-lookup"><span data-stu-id="f3ba3-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="f3ba3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f3ba3-104">Overview</span></span>
<span data-ttu-id="f3ba3-105">Ten samouczek obejmuje funkcję synchronizacji w trybie offline w usłudze Azure Mobile Apps dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="f3ba3-106">Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="f3ba3-107">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-107">Changes are stored in a local database.</span></span> <span data-ttu-id="f3ba3-108">Gdy urządzenie jest w trybie online, te zmiany są synchronizowane z zdalnego wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="f3ba3-109">Jeśli jest to środowiska pierwszy z usługą Azure Mobile Apps, należy najpierw Ukończ samouczek [Utwórz aplikację systemu Android].</span><span class="sxs-lookup"><span data-stu-id="f3ba3-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="f3ba3-110">Jeśli nie używasz szybki start pobrany Projekt serwera, należy dodać pakietów rozszerzenia dostępu do danych do projektu.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="f3ba3-111">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f3ba3-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="f3ba3-112">Aby dowiedzieć się więcej na temat funkcji synchronizacji w trybie offline, zobacz temat [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="f3ba3-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="f3ba3-113">Aktualizowanie aplikacji do obsługi synchronizacji w trybie offline</span><span class="sxs-lookup"><span data-stu-id="f3ba3-113">Update the app to support offline sync</span></span>
<span data-ttu-id="f3ba3-114">Z synchronizacji w trybie offline do odczytu i zapisu z *synchronizacji tabeli* (przy użyciu *IMobileServiceSyncTable* interface), który jest częścią **SQLite** bazy danych na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="f3ba3-115">Aby wypychania i ściągania zmiany między urządzeniami i usług Azure Mobile Services, należy użyć *kontekst synchronizacji* (*MobileServiceClient.SyncContext*), który zainicjować z lokalnej bazy danych do przechowywania dane lokalne.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="f3ba3-116">W `TodoActivity.java`, komentarz definicja `mToDoTable` i Usuń komentarz wersję usługi synchronizacji tabeli:</span><span class="sxs-lookup"><span data-stu-id="f3ba3-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="f3ba3-117">W `onCreate` metody komentarz istniejących inicjowanie `mToDoTable` i Usuń komentarz tej definicji:</span><span class="sxs-lookup"><span data-stu-id="f3ba3-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="f3ba3-118">W `refreshItemsFromTable` komentarz definicję `results` i Usuń komentarz tej definicji:</span><span class="sxs-lookup"><span data-stu-id="f3ba3-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="f3ba3-119">Komentarz definicję `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="f3ba3-120">Usuń znaczniki komentarza definicji `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="f3ba3-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="f3ba3-121">Usuń znaczniki komentarza definicji `sync`:</span><span class="sxs-lookup"><span data-stu-id="f3ba3-121">Uncomment the definition of `sync`:</span></span>
   
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

## <a name="test-the-app"></a><span data-ttu-id="f3ba3-122">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f3ba3-122">Test the app</span></span>
<span data-ttu-id="f3ba3-123">W tej sekcji testy na zachowanie w przypadku sieci Wi-Fi, a następnie wyłącz sieci Wi-Fi, aby utworzyć scenariusz w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="f3ba3-124">Po dodaniu elementów danych są przechowywane w lokalnym magazynie SQLite, ale nie zostały zsynchronizowane z usługi mobilnej, dopóki nie zostanie naciśnięty klawisz **Odśwież** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="f3ba3-125">Inne aplikacje mogą mieć inne wymagania dotyczące po danych muszą być zsynchronizowane, ale dla celów demonstracyjnych w tym samouczku został jawnie żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="f3ba3-126">Po naciśnięciu tego przycisku uruchamiania nowego zadania w tle.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="f3ba3-127">Najpierw wypycha dane wszystkich zmian w lokalnym magazynie przy użyciu kontekstu synchronizacji, a następnie ściąga zmienione dane platformy Azure z lokalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="f3ba3-128">Testowanie w trybie offline</span><span class="sxs-lookup"><span data-stu-id="f3ba3-128">Offline testing</span></span>
1. <span data-ttu-id="f3ba3-129">Umieść urządzenie lub symulator w *tryb samolotowy*.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="f3ba3-130">Spowoduje to utworzenie scenariusz w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="f3ba3-131">Dodaj raporty *ToDo* elementy lub znak niektóre elementy jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="f3ba3-132">Zamykania urządzenie lub symulator (lub Wymuś aplikacji) i uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="f3ba3-133">Sprawdź, czy zmiany zostały utrwalone na urządzeniu, ponieważ są one przechowywane w lokalnym magazynie SQLite.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="f3ba3-134">Wyświetlanie zawartości platformy Azure *TodoItem* tabeli za pomocą narzędzia SQL, takich jak *programu SQL Server Management Studio*, lub klienta REST, takich jak *Fiddler* lub  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="f3ba3-135">Upewnij się, że nowe elementy *nie* zostały zsynchronizowane z serwerem</span><span class="sxs-lookup"><span data-stu-id="f3ba3-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="f3ba3-136">Dla zaplecza Node.js, przejdź do [portalu Azure](https://portal.azure.com/), a w aplikacji mobilnej kliknij wewnętrznej bazy danych **łatwe tabel** > **TodoItem** do wyświetlania zawartości `TodoItem`tabeli.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="f3ba3-137">Dla zaplecza .NET, Wyświetl zawartość tabeli SQL za pomocą narzędzi takich jak *programu SQL Server Management Studio*, lub klienta REST, takich jak *Fiddler* lub *Postman*.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="f3ba3-138">Włącz sieci Wi-Fi w urządzenie lub symulator.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="f3ba3-139">Następnie naciśnij klawisz **Odśwież** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="f3ba3-140">Wyświetl dane TodoItem ponownie w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="f3ba3-141">Nowe i zmienione TodoItems powinien zostać wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="f3ba3-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3ba3-142">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f3ba3-142">Additional Resources</span></span>
* <span data-ttu-id="f3ba3-143">[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="f3ba3-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="f3ba3-144">[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services] \(Uwaga: plik wideo jest w usłudze Mobile Services, ale synchronizacji w trybie offline działa w podobny sposób jak w usłudze Azure Mobile Apps\)</span><span class="sxs-lookup"><span data-stu-id="f3ba3-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="f3ba3-145">[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="f3ba3-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="f3ba3-146">[Utwórz aplikację systemu Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f3ba3-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="f3ba3-147">[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="f3ba3-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

