---
title: Synchronizacja w trybie offline aaaEnable aplikacji mobilnej Azure (Cordova) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse aplikacji usługi Mobile App toocache i synchronizacji danych w trybie offline w aplikacji Cordova"
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
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="91b76-103">Włączanie synchronizacji w trybie offline dla aplikacji mobilnej oprogramowania Cordova</span><span class="sxs-lookup"><span data-stu-id="91b76-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="91b76-104">Ten samouczek zawiera funkcję synchronizacji w trybie offline hello z usługą Azure Mobile Apps dla oprogramowania Cordova.</span><span class="sxs-lookup"><span data-stu-id="91b76-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="91b76-105">Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="91b76-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="91b76-106">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="91b76-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="91b76-107">Po powrocie do trybu online urządzenia hello te zmiany są zsynchronizowane z hello usługi zdalnej.</span><span class="sxs-lookup"><span data-stu-id="91b76-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="91b76-108">W tym samouczku jest oparta na hello Cordova rozwiązania szybkiego startu dla Mobile Apps, utworzonych po ukończeniu hello samouczek [szybki start dla oprogramowania Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="91b76-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="91b76-109">W tym samouczku należy zaktualizować hello szybkiego startu rozwiązania tooadd funkcji w trybie offline z usługą Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="91b76-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="91b76-110">Możemy również zaznacz kodu w trybie offline określonych hello w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="91b76-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="91b76-111">toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="91b76-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="91b76-112">Aby uzyskać szczegółowe informacje dotyczące użycia interfejsu API, zobacz hello [dokumentacji interfejsu API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="91b76-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="91b76-113">Dodaj rozwiązanie szybkiego startu toohello synchronizacji w trybie offline</span><span class="sxs-lookup"><span data-stu-id="91b76-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="91b76-114">Hello synchronizacji w trybie offline kod należy dodać toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91b76-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="91b76-115">Synchronizacja w trybie offline wymaga hello wtyczki cordova sqlite magazynu, który automatycznie pobiera dodawane tooyour aplikacji, gdy wtyczkę Azure Mobile Apps hello jest uwzględnione w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="91b76-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="91b76-116">Projekt szybkiego startu Hello zawiera oba te wtyczki.</span><span class="sxs-lookup"><span data-stu-id="91b76-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="91b76-117">W Eksploratorze rozwiązań programu Visual Studio Otwórz index.js i Zastąp hello następującego kodu</span><span class="sxs-lookup"><span data-stu-id="91b76-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="91b76-118">o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="91b76-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="91b76-119">Następnie zastąp hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="91b76-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="91b76-120">o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="91b76-120">with this code:</span></span>

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

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="91b76-121">Hello poprzedni kod dodatków zainicjować hello lokalnego magazynu i zdefiniuj lokalnej tabeli, która odpowiada wartości w kolumnie hello używane w sieci Azure zaplecza.</span><span class="sxs-lookup"><span data-stu-id="91b76-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="91b76-122">(Nie trzeba tooinclude wszystkie wartości kolumn tego kodu.)  Witaj `version` pole jest obsługiwany przez zaplecze aplikacji mobilnej hello, służy do rozwiązywania konfliktów.</span><span class="sxs-lookup"><span data-stu-id="91b76-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="91b76-123">Pobierz odwołanie kontekst synchronizacji toohello przez wywołanie metody **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="91b76-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="91b76-124">Witaj kontekstu synchronizacji ułatwia zachowanie relacje między tabelami, śledzenia i wypychanie zmiany we wszystkich tabelach aplikacji klienckiej został zmodyfikowany podczas obliczania `.push()` jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="91b76-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="91b76-125">Aktualizowanie aplikacji hello adres URL aplikacji mobilnej tooyour aplikacji adresu URL.</span><span class="sxs-lookup"><span data-stu-id="91b76-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="91b76-126">Następnie Zastąp ten kod:</span><span class="sxs-lookup"><span data-stu-id="91b76-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="91b76-127">o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="91b76-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="91b76-128">Witaj poprzedni kod inicjuje hello kontekstu synchronizacji, a następnie wywołuje tooget getSyncTable (zamiast getTable) toohello odwołanie do lokalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="91b76-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="91b76-129">Ten kod używa hello lokalnej bazy danych dla wszystkich tworzenia, odczytu, aktualizacji i usuwania (CRUD) operacje tabeli.</span><span class="sxs-lookup"><span data-stu-id="91b76-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="91b76-130">W tym przykładzie przeprowadza prosty błąd obsługi na konfliktów synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="91b76-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="91b76-131">Czy obsługa rzeczywistej aplikacji hello różne błędy, takie jak warunków sieciowych, powoduje konflikt z serwera i inne.</span><span class="sxs-lookup"><span data-stu-id="91b76-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="91b76-132">Przykłady kodu, zobacz hello [próbki synchronizacji w trybie offline].</span><span class="sxs-lookup"><span data-stu-id="91b76-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="91b76-133">Następnie dodaj to funkcja tooperform hello rzeczywiste synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="91b76-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="91b76-134">Zdecydujesz toopush zmiany zaplecza aplikacji mobilnej toohello przez wywołanie metody **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="91b76-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="91b76-135">Na przykład można wywołać **syncBackend** w przycisk synchronizacji przycisk wiązanej tooa obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="91b76-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="91b76-136">Zagadnienia dotyczące synchronizacji w trybie offline</span><span class="sxs-lookup"><span data-stu-id="91b76-136">Offline sync considerations</span></span>

<span data-ttu-id="91b76-137">W przykładowym hello hello **wypychania** metody **syncContext** wywołać tylko podczas uruchamiania aplikacji hello funkcji wywołania zwrotnego dla nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="91b76-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="91b76-138">W przypadku aplikacji rzeczywistych można także spowodować tej funkcji synchronizacji wywołane ręcznie lub po zmianie stanu sieci hello.</span><span class="sxs-lookup"><span data-stu-id="91b76-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="91b76-139">Podczas wykonywania ściąganie względem tabeli, która ma oczekujące aktualizacje z lokalnego śledzone przez hello kontekstu, który ściągnięcia operacji automatycznie wyzwalacze wypychania.</span><span class="sxs-lookup"><span data-stu-id="91b76-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="91b76-140">Podczas odświeżania, dodawania i kończenie elementów w tym przykładzie, można pominąć hello jawne **wypychania** wywołać, ponieważ może być nadmiarowe.</span><span class="sxs-lookup"><span data-stu-id="91b76-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="91b76-141">W kodzie hello pod warunkiem, będą proszeni wszystkie rekordy w tabeli todoItem zdalnego hello, ale jest również możliwe toofilter rekordów przez przekazanie identyfikator zapytania i zapytań za**wypychania**.</span><span class="sxs-lookup"><span data-stu-id="91b76-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="91b76-142">Aby uzyskać więcej informacji, zobacz sekcję hello *synchronizacja przyrostowa* w [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="91b76-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="91b76-143">(Opcjonalnie) Wyłącz uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="91b76-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="91b76-144">Jeśli nie ma tooset się uwierzytelniania przed testowaniem synchronizacji w trybie offline, komentarz hello funkcja wywołania zwrotnego dla nazwy logowania, ale pozostaw hello kodu wewnątrz odkomentowana hello funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="91b76-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="91b76-145">Po komentowania hello logowania wierszy, kod hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="91b76-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="91b76-146">Teraz hello aplikacji przeprowadza synchronizację z wewnętrznej bazy danych Azure po uruchomieniu aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="91b76-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="91b76-147">Uruchom aplikację klienta hello</span><span class="sxs-lookup"><span data-stu-id="91b76-147">Run hello client app</span></span>
<span data-ttu-id="91b76-148">Teraz włączony synchronizacja w trybie offline umożliwia uruchamianie aplikacji klienckiej hello co najmniej raz na każdej z platform do wypełniania bazy danych magazynu lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="91b76-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="91b76-149">Później symulować scenariusz w trybie offline i modyfikować danych hello w lokalnym magazynie hello, gdy aplikacja hello jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="91b76-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="91b76-150">(Opcjonalnie) Zachowanie synchronizacji hello testu</span><span class="sxs-lookup"><span data-stu-id="91b76-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="91b76-151">W tej sekcji możesz zmodyfikować powitania klienta projektu toosimulate scenariusz w trybie offline za pomocą nieprawidłowy adres URL aplikacji w danym zapleczu.</span><span class="sxs-lookup"><span data-stu-id="91b76-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="91b76-152">Podczas dodawania lub zmienić elementy danych te zmiany są przechowywane w magazynie lokalnym, ale nie są magazynu danych zsynchronizowanej toohello wewnętrznej bazy danych do momentu ponownym nawiązaniu połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="91b76-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="91b76-153">W Eksploratorze rozwiązań hello Otwórz plik projektu index.js hello i zmień toopoint adres URL aplikacji hello nieprawidłowy adres URL, takie jak hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="91b76-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="91b76-154">W index.html, zaktualizuj hello dostawcy usług Kryptograficznych `<meta>` element z hello tego samego nieprawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="91b76-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="91b76-155">Tworzenie i uruchamianie powitania klienta aplikacji i zwróć uwagę, czy wyjątek jest rejestrowane w konsoli hello, gdy aplikacja hello próbuje synchronizować z zapleczem hello po logowania.</span><span class="sxs-lookup"><span data-stu-id="91b76-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="91b76-156">Nowe elementy, które można dodać istnieją tylko w lokalnym magazynie hello, dopóki nie są one usuwane toohello zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="91b76-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="91b76-157">Aplikacja kliencka Hello zachowuje się tak, jakby była połączonych toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="91b76-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="91b76-158">Zamknij aplikację hello i uruchom ją ponownie tooverify hello nowe elementy utworzone czy toohello utrwalonego magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="91b76-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="91b76-159">(Opcjonalnie) Za pomocą programu Visual Studio tooview toosee tabeli bazy danych SQL Azure, sieci danych hello w hello wewnętrznej bazy danych w bazie danych nie zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="91b76-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="91b76-160">W programie Visual Studio Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="91b76-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="91b76-161">Przejdź do bazy danych tooyour w **Azure**->**baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="91b76-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="91b76-162">Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="91b76-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="91b76-163">Teraz można przeglądać tooyour tabeli w bazie danych SQL i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="91b76-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="91b76-164">(Opcjonalnie) Test hello ponowne nawiązanie połączenia tooyour zaplecze aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="91b76-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="91b76-165">W tej sekcji ponownym hello aplikacji toohello zaplecze aplikacji mobilnej, która symuluje aplikacji hello powracające do trybu online.</span><span class="sxs-lookup"><span data-stu-id="91b76-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="91b76-166">Podczas logowania, dane są zsynchronizowane tooyour zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="91b76-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="91b76-167">Otwórz ponownie index.js i przywrócić hello adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91b76-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="91b76-168">Otwórz ponownie index.html i popraw adres URL aplikacji hello w hello dostawcy usług Kryptograficznych `<meta>` elementu.</span><span class="sxs-lookup"><span data-stu-id="91b76-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="91b76-169">Ponownie skompilować i uruchomić powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91b76-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="91b76-170">Aplikacja Hello prób toosync z zaplecza aplikacji mobilnej powitania po logowaniu.</span><span class="sxs-lookup"><span data-stu-id="91b76-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="91b76-171">Upewnij się, że żadne wyjątki są rejestrowane w konsoli debugowania hello.</span><span class="sxs-lookup"><span data-stu-id="91b76-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="91b76-172">(Opcjonalnie) Widok hello zaktualizowane dane przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler.</span><span class="sxs-lookup"><span data-stu-id="91b76-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="91b76-173">Powiadomienie hello danych został zsynchronizowany między hello wewnętrznej bazy danych i hello magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="91b76-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="91b76-174">Zwróć uwagę, hello dane zostały zsynchronizowane między hello bazy danych i magazynu lokalnego hello i zawiera elementy hello dodane odłączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91b76-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91b76-175">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="91b76-175">Additional resources</span></span>
* <span data-ttu-id="91b76-176">[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="91b76-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="91b76-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="91b76-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="91b76-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91b76-178">Next steps</span></span>
* <span data-ttu-id="91b76-179">Przejrzyj bardziej zaawansowane funkcje synchronizacji w trybie offline, takie jak rozwiązywania konfliktów w hello [próbki synchronizacji w trybie offline]</span><span class="sxs-lookup"><span data-stu-id="91b76-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="91b76-180">Przejrzyj synchronizacji w trybie offline hello dokumentacja interfejsu API w hello [dokumentacji interfejsu API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="91b76-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[szybki start dla oprogramowania Apache Cordova]: app-service-mobile-cordova-get-started.md
[próbki synchronizacji w trybie offline]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
