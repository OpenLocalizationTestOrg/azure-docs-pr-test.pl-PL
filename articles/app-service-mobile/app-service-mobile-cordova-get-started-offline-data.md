---
title: "Włączanie synchronizacji w trybie offline dla aplikacji mobilnej Azure (Cordova) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać aplikacji usługi Mobile App do pamięci podręcznej i synchronizacji danych w trybie offline w aplikacji Cordova"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="b7a21-103">Włączanie synchronizacji w trybie offline dla aplikacji mobilnej oprogramowania Cordova</span><span class="sxs-lookup"><span data-stu-id="b7a21-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="b7a21-104">Ten samouczek przedstawia funkcję synchronizacji w trybie offline w usłudze Azure Mobile Apps dla oprogramowania Cordova.</span><span class="sxs-lookup"><span data-stu-id="b7a21-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="b7a21-105">Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="b7a21-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="b7a21-106">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b7a21-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="b7a21-107">Gdy urządzenie jest w trybie online, te zmiany są synchronizowane z usługi zdalnej.</span><span class="sxs-lookup"><span data-stu-id="b7a21-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="b7a21-108">W tym samouczku opiera się na rozwiązanie szybkiego startu Cordova Mobile Apps, utworzony po ukończeniu samouczka [szybki start dla oprogramowania Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="b7a21-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="b7a21-109">W tym samouczku należy zaktualizować rozwiązania Szybki Start można dodać funkcji w trybie offline z usługą Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="b7a21-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="b7a21-110">Możemy również zaznacz kodu w trybie offline określonych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="b7a21-111">Aby dowiedzieć się więcej na temat funkcji synchronizacji w trybie offline, zobacz temat [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b7a21-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="b7a21-112">Aby uzyskać szczegółowe informacje dotyczące użycia interfejsu API, zobacz [dokumentacji interfejsu API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="b7a21-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="b7a21-113">Dodaj synchronizacji w trybie offline do rozwiązania Szybki Start</span><span class="sxs-lookup"><span data-stu-id="b7a21-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="b7a21-114">Kod synchronizacji w trybie offline, należy dodać do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="b7a21-115">Synchronizacja w trybie offline wymaga wtyczki cordova sqlite magazynu, który automatycznie pobiera dodany do aplikacji po wtyczkę Azure Mobile Apps jest dołączony do projektu.</span><span class="sxs-lookup"><span data-stu-id="b7a21-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="b7a21-116">Projekt szybkiego startu zawiera oba te wtyczki.</span><span class="sxs-lookup"><span data-stu-id="b7a21-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="b7a21-117">W Eksploratorze rozwiązań programu Visual Studio Otwórz index.js i Zastąp następujący kod</span><span class="sxs-lookup"><span data-stu-id="b7a21-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="b7a21-118">o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="b7a21-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="b7a21-119">Następnie zastąp następujący kod:</span><span class="sxs-lookup"><span data-stu-id="b7a21-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="b7a21-120">o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="b7a21-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="b7a21-121">Dodatki kod z powyższej zainicjować magazynu lokalnego i zdefiniuj lokalnej tabeli, która odpowiada wartości w kolumnie używane w sieci Azure zaplecza.</span><span class="sxs-lookup"><span data-stu-id="b7a21-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="b7a21-122">(Nie trzeba obejmują wszystkie wartości w kolumnie w tym kodu).  `version` Pole jest obsługiwany przez zaplecze aplikacji mobilnej, służy do rozwiązywania konfliktów.</span><span class="sxs-lookup"><span data-stu-id="b7a21-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="b7a21-123">Możesz odwołać się do kontekstu synchronizacji przez wywołanie metody **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="b7a21-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="b7a21-124">Kontekst synchronizacji pomaga zachować relacje między tabelami, śledzenia i wypychanie zmiany we wszystkich tabelach aplikacji klienckiej został zmodyfikowany podczas obliczania `.push()` jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="b7a21-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="b7a21-125">Zaktualizuj adres URL aplikacji do adresu URL aplikacji w Twojej aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b7a21-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="b7a21-126">Następnie Zastąp ten kod:</span><span class="sxs-lookup"><span data-stu-id="b7a21-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="b7a21-127">o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="b7a21-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="b7a21-128">Poprzedni kod inicjuje kontekstu synchronizacji, a następnie wywołuje getSyncTable (zamiast getTable), aby pobrać odwołanie do lokalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="b7a21-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="b7a21-129">To kod korzysta z lokalnej bazy danych dla wszystkich tworzenia, odczytu, aktualizacji i usuwania (CRUD) operacje tabeli.</span><span class="sxs-lookup"><span data-stu-id="b7a21-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="b7a21-130">W tym przykładzie przeprowadza prosty błąd obsługi na konfliktów synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="b7a21-131">Rzeczywistej aplikacji będzie obsługiwać różne błędy, takie jak warunków sieciowych, powoduje konflikt z serwera i inne.</span><span class="sxs-lookup"><span data-stu-id="b7a21-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="b7a21-132">Aby uzyskać przykłady kodu, zobacz [próbki synchronizacji w trybie offline].</span><span class="sxs-lookup"><span data-stu-id="b7a21-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="b7a21-133">Następnie dodaj tę funkcję, aby wykonać rzeczywiste synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="b7a21-134">Podjęcie decyzji dotyczącej Wypchnij zmiany do zaplecza aplikacji mobilnej, wywołując **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="b7a21-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="b7a21-135">Na przykład można wywołać **syncBackend** w obsłudze zdarzeń przycisk powiązane przycisk synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="b7a21-136">Zagadnienia dotyczące synchronizacji w trybie offline</span><span class="sxs-lookup"><span data-stu-id="b7a21-136">Offline sync considerations</span></span>

<span data-ttu-id="b7a21-137">W przykładzie **wypychania** metody **syncContext** wywołać tylko podczas uruchamiania aplikacji w funkcji wywołania zwrotnego dla nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="b7a21-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="b7a21-138">W przypadku aplikacji rzeczywistych można także spowodować tej funkcji synchronizacji wywołane ręcznie lub zmiany stanu sieci.</span><span class="sxs-lookup"><span data-stu-id="b7a21-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="b7a21-139">Podczas wykonywania ściąganie względem tabeli, która ma oczekujące aktualizacje z lokalnego śledzone przez kontekstu, która ściągnięcia operacji automatycznie wyzwalacze wypychania.</span><span class="sxs-lookup"><span data-stu-id="b7a21-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="b7a21-140">Podczas odświeżania, dodawanie i wykonując elementów w tym przykładzie można pominąć jawnych **wypychania** wywołać, ponieważ może być nadmiarowe.</span><span class="sxs-lookup"><span data-stu-id="b7a21-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="b7a21-141">Podany kod odpytywane będą wszystkie rekordy w tabeli todoItem zdalnego, ale jest również możliwe filtrowanie rekordów przez przekazanie identyfikator zapytania i kwerendę **wypychania**.</span><span class="sxs-lookup"><span data-stu-id="b7a21-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="b7a21-142">Aby uzyskać więcej informacji, zobacz sekcję *synchronizacja przyrostowa* w [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b7a21-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="b7a21-143">(Opcjonalnie) Wyłącz uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="b7a21-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="b7a21-144">Jeśli nie chcesz skonfigurować uwierzytelnianie przed testowych synchronizacją w trybie offline, funkcja wywołania zwrotnego dla logowania w komentarz, ale pozostawić kodu wewnątrz odkomentowana funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="b7a21-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="b7a21-145">Po komentowania wierszy logowania, następujący kod:</span><span class="sxs-lookup"><span data-stu-id="b7a21-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="b7a21-146">Teraz aplikacja przeprowadza synchronizację z wewnętrznej bazy danych Azure po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="b7a21-147">Uruchamianie aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="b7a21-147">Run the client app</span></span>
<span data-ttu-id="b7a21-148">Teraz włączony synchronizacja w trybie offline umożliwia uruchamianie aplikacji klienckiej co najmniej raz na każdej z platform do wypełniania bazy danych magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b7a21-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="b7a21-149">Później symulować scenariusz w trybie offline i modyfikować danych w magazynie lokalnym, gdy aplikacja jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="b7a21-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="b7a21-150">(Opcjonalnie) Testowanie zachowanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="b7a21-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="b7a21-151">W tej sekcji możesz zmodyfikować projekt klienta, aby symulować scenariusz w trybie offline za pomocą nieprawidłowy adres URL aplikacji w danym zapleczu.</span><span class="sxs-lookup"><span data-stu-id="b7a21-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="b7a21-152">Podczas dodawania lub zmienić elementów danych, zmiany te są przechowywane w lokalnym magazynie, ale nie są zsynchronizowane z wewnętrznej bazy danych magazynu danych, dopóki nie zostanie ponownie nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="b7a21-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="b7a21-153">W Eksploratorze rozwiązań Otwórz plik projektu index.js i zmień adres URL aplikacji, aby wskazywał nieprawidłowy adres URL, podobnie do następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="b7a21-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="b7a21-154">Dostawca usług Kryptograficznych aktualizacji index.html, `<meta>` element o tej samej nieprawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="b7a21-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="b7a21-155">Skompiluj i uruchom aplikację klienta i zwróć uwagę, że wyjątek jest rejestrowane w konsoli, gdy aplikacja próbuje synchronizować z wewnętrznej bazy danych po logowaniu.</span><span class="sxs-lookup"><span data-stu-id="b7a21-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="b7a21-156">Nowe elementy, które można dodać istnieje tylko w lokalnym magazynie, dopóki nie są one przenoszone do zaplecza aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="b7a21-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="b7a21-157">Aplikacja kliencka zachowuje się tak, jakby nie jest połączona z wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b7a21-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="b7a21-158">Zamknij aplikację i uruchom ponownie, aby sprawdzić, czy nowe elementy utworzone zostały utrwalone w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b7a21-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="b7a21-159">(Opcjonalnie) Aby wyświetlić tabelę bazy danych SQL Azure, aby zobaczyć, czy dane w bazie danych zaplecza nie uległy zmianie, należy użyć programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7a21-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="b7a21-160">W programie Visual Studio Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="b7a21-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="b7a21-161">Przejdź do bazy danych w **Azure**->**baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="b7a21-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="b7a21-162">Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b7a21-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="b7a21-163">Możesz teraz przejść do tabeli bazy danych SQL i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="b7a21-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="b7a21-164">(Opcjonalnie) Testowanie ponowne nawiązanie połączenia z wewnętrzną bazą danych w przenośnych</span><span class="sxs-lookup"><span data-stu-id="b7a21-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="b7a21-165">W tej sekcji ponowne łączenie aplikacji zaplecza mobilnego, która symuluje aplikacji powracające do trybu online.</span><span class="sxs-lookup"><span data-stu-id="b7a21-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="b7a21-166">Podczas logowania danych jest synchronizowany z przenośnymi wewnętrzną bazą danych.</span><span class="sxs-lookup"><span data-stu-id="b7a21-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="b7a21-167">Otwórz ponownie index.js i przywrócić adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="b7a21-168">Otwórz ponownie index.html i popraw adres URL aplikacji w dostawcy CSP `<meta>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b7a21-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="b7a21-169">Ponownie skompilować i uruchomić aplikację klienta.</span><span class="sxs-lookup"><span data-stu-id="b7a21-169">Rebuild and run the client app.</span></span> <span data-ttu-id="b7a21-170">Aplikacja próbuje synchronizować z zaplecza aplikacji mobilnej po logowania.</span><span class="sxs-lookup"><span data-stu-id="b7a21-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="b7a21-171">Upewnij się, że żadne wyjątki są rejestrowane w konsoli debugowania.</span><span class="sxs-lookup"><span data-stu-id="b7a21-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="b7a21-172">(Opcjonalnie) Wyświetlanie zaktualizowanych danych przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b7a21-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="b7a21-173">Należy zauważyć, że zsynchronizowano dane między wewnętrzna baza danych i magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b7a21-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="b7a21-174">Zwróć uwagę, dane zostały zsynchronizowane między bazy danych i Magazyn lokalny i zawiera elementy, które dodano odłączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a21-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7a21-175">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b7a21-175">Additional resources</span></span>
* <span data-ttu-id="b7a21-176">[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="b7a21-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="b7a21-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="b7a21-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7a21-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7a21-178">Next steps</span></span>
* <span data-ttu-id="b7a21-179">Przejrzyj bardziej zaawansowane funkcje synchronizacji w trybie offline, takie jak rozwiązywania konfliktów w [próbki synchronizacji w trybie offline]</span><span class="sxs-lookup"><span data-stu-id="b7a21-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="b7a21-180">Przejrzyj odwołanie do synchronizacji w trybie offline interfejsu API w [dokumentacji interfejsu API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="b7a21-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="b7a21-181">[szybki start dla oprogramowania Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b7a21-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b7a21-182">[próbki synchronizacji w trybie offline]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="b7a21-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="b7a21-183">[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="b7a21-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="b7a21-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="b7a21-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
