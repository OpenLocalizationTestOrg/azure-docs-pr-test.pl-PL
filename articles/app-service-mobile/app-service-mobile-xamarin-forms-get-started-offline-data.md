---
title: Synchronizacja w trybie offline aaaEnable aplikacji mobilnej Azure (platformy Xamarin.Forms) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse aplikacji usługi Mobile App toocache i synchronizacji danych w trybie offline w aplikacji platformy Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="3c38a-103">Włączanie synchronizacji w trybie offline dla aplikacji mobilnej platformy Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="3c38a-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="3c38a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3c38a-104">Overview</span></span>
<span data-ttu-id="3c38a-105">W tym samouczku wprowadzono funkcję synchronizacji w trybie offline hello aplikacji mobilnej Azure dla platformy Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="3c38a-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="3c38a-106">Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="3c38a-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="3c38a-107">Zmiany są przechowywane w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="3c38a-107">Changes are stored in a local database.</span></span> <span data-ttu-id="3c38a-108">Po powrocie do trybu online urządzenia hello te zmiany są zsynchronizowane z hello usługi zdalnej.</span><span class="sxs-lookup"><span data-stu-id="3c38a-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="3c38a-109">W tym samouczku opiera się na powitania rozwiązania szybkiego startu platformy Xamarin.Forms Mobile Apps, utworzony po ukończeniu samouczka [tworzenie aplikacji platformy Xamarin.IOS].</span><span class="sxs-lookup"><span data-stu-id="3c38a-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="3c38a-110">Hello rozwiązanie szybkiego startu dla platformy Xamarin.Forms zawiera hello kodu toosupport synchronizacji w trybie offline, którą właśnie należy toobe włączone.</span><span class="sxs-lookup"><span data-stu-id="3c38a-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="3c38a-111">W tym samouczku należy zaktualizować hello szybkiego startu rozwiązania tooturn na powitania funkcji w trybie offline z usługą Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="3c38a-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="3c38a-112">Możemy również zaznacz kodu w trybie offline określonych hello w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="3c38a-113">Nie należy używać rozwiązania szybkiego startu hello pobrane, należy dodać hello danych access rozszerzenia pakietów tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="3c38a-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="3c38a-114">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="3c38a-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="3c38a-115">toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="3c38a-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="3c38a-116">Włączanie funkcji synchronizacji w trybie offline w rozwiązaniu szybkiego startu hello</span><span class="sxs-lookup"><span data-stu-id="3c38a-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="3c38a-117">Witaj synchronizacji w trybie offline zostanie dołączony kod projektu hello przy użyciu dyrektywy preprocesora C#.</span><span class="sxs-lookup"><span data-stu-id="3c38a-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="3c38a-118">Gdy hello **OFFLINE\_SYNCHRONIZACJI\_włączone** zdefiniowano symbol, tych ścieżek kodu zostaną uwzględnione w kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="3c38a-119">Dla aplikacji systemu Windows należy również zainstalować hello SQLite platformy.</span><span class="sxs-lookup"><span data-stu-id="3c38a-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="3c38a-120">W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello > **Zarządzaj pakietami NuGet rozwiązania...** , następnie wyszukaj i zainstaluj **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet dla wszystkich projektów w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="3c38a-121">W Eksploratorze rozwiązań hello, otwórz plik TodoItemManager.cs hello z projektu hello z **przenośnych** w polu Nazwa hello jest projektu biblioteki przenośnej klasy, następnie usuń komentarz hello następujące dyrektywy preprocesora:</span><span class="sxs-lookup"><span data-stu-id="3c38a-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="3c38a-122">Urządzeń z systemem Windows (opcjonalnie) toosupport zainstalować jednego z powitania po SQLite środowiska uruchomieniowego pakiety:</span><span class="sxs-lookup"><span data-stu-id="3c38a-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="3c38a-123">**Środowisko uruchomieniowe Windows 8.1:** zainstalować [SQLite dla Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="3c38a-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="3c38a-124">**Windows Phone 8.1:** zainstalować [SQLite dla Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="3c38a-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="3c38a-125">**Platforma uniwersalna systemu Windows** zainstalować [SQLite dla uniwersalnych uniwersalnych systemu Windows hello][5].</span><span class="sxs-lookup"><span data-stu-id="3c38a-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="3c38a-126">Mimo że hello szybkiego startu zawiera projektów uniwersalnych systemu Windows, platforma uniwersalna systemu Windows hello jest obsługiwana w programie Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="3c38a-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="3c38a-127">(Opcjonalnie) W każdym projekcie aplikacji systemu Windows, kliknij prawym przyciskiem myszy **odwołania** > **Dodawanie odwołania...** , rozwiń węzeł hello **Windows** folder > **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="3c38a-128">Włącz odpowiednie hello **SQLite dla systemu Windows** zestawu SDK oraz hello **Visual C++ 2013 środowiska wykonawczego systemu Windows** zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="3c38a-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="3c38a-129">Witaj nazwy zestawu SDK SQLite się nieco różnić z każdej z platform Windows.</span><span class="sxs-lookup"><span data-stu-id="3c38a-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="3c38a-130">Przejrzyj powitania klienta synchronizacji kodu</span><span class="sxs-lookup"><span data-stu-id="3c38a-130">Review hello client sync code</span></span>
<span data-ttu-id="3c38a-131">Oto krótkie omówienie co to jest już uwzględniony w hello samouczek kodu wewnątrz hello `#if OFFLINE_SYNC_ENABLED` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="3c38a-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="3c38a-132">Funkcja synchronizacji w trybie offline jest w pliku projektu hello TodoItemManager.cs projektu biblioteki klas przenośnych hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="3c38a-133">Omówienie koncepcji hello funkcji, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="3c38a-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="3c38a-134">Aby można było wykonać wszystkie operacje tabeli, muszą zostać zainicjowane hello lokalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c38a-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="3c38a-135">Witaj magazynu lokalnego jest inicjowana w hello **TodoItemManager** konstruktora klasy przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="3c38a-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="3c38a-136">Ten kod tworzy nowy lokalnej bazy danych SQLite przy użyciu hello **MobileServiceSQLiteStore** klasy.</span><span class="sxs-lookup"><span data-stu-id="3c38a-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="3c38a-137">Witaj **DefineTable** metoda tworzy tabelę w magazynie lokalnym hello odpowiadającego pola hello w typie hello podane.</span><span class="sxs-lookup"><span data-stu-id="3c38a-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="3c38a-138">Typ Hello nie ma tooinclude wszystkich kolumn hello w hello zdalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3c38a-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="3c38a-139">Jest możliwe toostore podzbiór kolumn.</span><span class="sxs-lookup"><span data-stu-id="3c38a-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="3c38a-140">Witaj **todoTable** w **TodoItemManager** jest **IMobileServiceSyncTable** wpisz zamiast **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="3c38a-141">Ta klasa korzysta hello lokalnej bazy danych dla wszystkich tworzenia, odczytu, aktualizacji i usuwania operacje tabeli (CRUD).</span><span class="sxs-lookup"><span data-stu-id="3c38a-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="3c38a-142">Zdecyduj, kiedy te zmiany są usuwane toohello zaplecza aplikacji mobilnej, przez wywołanie metody **PushAsync** na powitania **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="3c38a-143">Witaj kontekstu synchronizacji ułatwia zachowanie relacje między tabelami, śledzenia i wypychanie zmiany we wszystkich tabelach aplikacji klienckiej został zmodyfikowany podczas obliczania **PushAsync** jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="3c38a-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="3c38a-144">następujące Hello **SyncAsync** metoda jest wywoływana toosync z zaplecza aplikacji mobilnej hello:</span><span class="sxs-lookup"><span data-stu-id="3c38a-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    <span data-ttu-id="3c38a-145">W przykładzie użyto prostych obsługi hello domyślne synchronizacji obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="3c38a-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="3c38a-146">Rzeczywistej aplikacji będzie obsługiwać hello różne błędy, takich jak warunki w sieci i serwera, który powoduje konflikt przy użyciu niestandardowego **IMobileServiceSyncHandler** implementacji.</span><span class="sxs-lookup"><span data-stu-id="3c38a-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="3c38a-147">Zagadnienia dotyczące synchronizacji w trybie offline</span><span class="sxs-lookup"><span data-stu-id="3c38a-147">Offline sync considerations</span></span>
<span data-ttu-id="3c38a-148">W przykładowym hello hello **SyncAsync** wywoływana jest metoda tylko rozruchu i kiedy zażądano synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="3c38a-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="3c38a-149">tooinitiate synchronizacji w aplikacji systemu Android i iOS, ściągnięcia w dół na liście elementy hello; w systemie Windows, użyj hello **synchronizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3c38a-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="3c38a-150">W przypadku aplikacji rzeczywistych można również upewnij wyzwalacza synchronizacji powitania po zmianie stanu sieci hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="3c38a-151">Podczas wykonywania ściąganie względem tabeli, która ma oczekujące aktualizacje lokalnego śledzone przez kontekstu hello, który automatycznie pobierać operacji wyzwalaczy poprzedniego wypychania kontekstu.</span><span class="sxs-lookup"><span data-stu-id="3c38a-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="3c38a-152">Podczas odświeżania, dodawania i kończenie elementów w tym przykładzie, można pominąć hello jawne **PushAsync** wywołania.</span><span class="sxs-lookup"><span data-stu-id="3c38a-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="3c38a-153">W kodzie hello pod warunkiem, będą proszeni wszystkie rekordy w tabeli zdalnej TodoItem hello, ale jest również możliwe toofilter rekordów przez przekazanie identyfikator zapytania i zapytań za**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="3c38a-154">Aby uzyskać więcej informacji, zobacz sekcję hello *synchronizacja przyrostowa* w [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="3c38a-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="3c38a-155">Uruchom aplikację klienta hello</span><span class="sxs-lookup"><span data-stu-id="3c38a-155">Run hello client app</span></span>
<span data-ttu-id="3c38a-156">Teraz włączony synchronizacja w trybie offline uruchamianie aplikacji klienckiej hello co najmniej raz w każdej bazie platformy toopopulate hello lokalnego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="3c38a-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="3c38a-157">Później symulować scenariusz w trybie offline i modyfikować danych hello w lokalnym magazynie hello, gdy aplikacja hello jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="3c38a-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="3c38a-158">Zaktualizuj zachowanie synchronizacji hello powitania klienta aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c38a-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="3c38a-159">W tej sekcji należy zmodyfikować powitania klienta projektu toosimulate scenariusz w trybie offline, nieprawidłowy adres URL aplikacji w danym zapleczu.</span><span class="sxs-lookup"><span data-stu-id="3c38a-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="3c38a-160">Alternatywnie można wyłączyć połączeń sieciowych przez przeniesienie urządzenia zbyt "Tryb samolotowy".</span><span class="sxs-lookup"><span data-stu-id="3c38a-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="3c38a-161">Podczas dodawania lub zmienić elementy danych te zmiany są przechowywane w magazynie lokalnym hello, ale nie zsynchronizowano danych zaplecza toohello przechowywania, dopóki nie zostanie ponownie nawiązać połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="3c38a-162">W Eksploratorze rozwiązań hello, otwórz plik projektu Constants.cs hello z hello **przenośne** projektu i zmienić wartość hello `ApplicationURL` toopoint tooan nieprawidłowy adres URL:</span><span class="sxs-lookup"><span data-stu-id="3c38a-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="3c38a-163">Otwórz hello TodoItemManager.cs pliku z hello **przenośne** projektu, a następnie dodaj **catch** dla podstawowej hello **wyjątek** toohello klasy **try... catch** blok w **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="3c38a-164">To **catch** bloku zapisuje hello konsoli toohello komunikat wyjątku, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3c38a-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="3c38a-165">Skompiluj i uruchom aplikację klienta hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-165">Build and run hello client app.</span></span>  <span data-ttu-id="3c38a-166">Dodać niektóre nowe elementy.</span><span class="sxs-lookup"><span data-stu-id="3c38a-166">Add some new items.</span></span> <span data-ttu-id="3c38a-167">Zwróć uwagę, że wyjątek jest rejestrowana w hello konsoli dla każdego toosync próba z zapleczem hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="3c38a-168">Te nowe elementy istnieje tylko w lokalnym magazynie hello, dopóki nie może zostać umieszczony toohello zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="3c38a-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="3c38a-169">Aplikacja kliencka Hello zachowuje się tak, jakby była połączonych toohello wewnętrznej bazy danych, obsługa wszystkich tworzyć, odczytywać, update, operacji usuwania (CRUD).</span><span class="sxs-lookup"><span data-stu-id="3c38a-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="3c38a-170">Zamknij aplikację hello i uruchom ją ponownie tooverify hello nowe elementy utworzone czy toohello utrwalonego magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3c38a-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="3c38a-171">(Opcjonalnie) Za pomocą programu Visual Studio tooview toosee tabeli bazy danych SQL Azure, sieci danych hello w hello wewnętrznej bazy danych w bazie danych nie zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="3c38a-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="3c38a-172">W programie Visual Studio Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="3c38a-173">Przejdź do bazy danych tooyour w **Azure**->**baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="3c38a-174">Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="3c38a-175">Teraz można przeglądać tooyour tabeli w bazie danych SQL i jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="3c38a-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="3c38a-176">Zaktualizuj powitania klienta aplikacji tooreconnect Twojego zaplecze aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="3c38a-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="3c38a-177">W tej sekcji Połącz się ponownie hello aplikacji toohello zaplecze aplikacji mobilnej, która symuluje aplikacji hello powracające tooan do trybu online.</span><span class="sxs-lookup"><span data-stu-id="3c38a-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="3c38a-178">Podczas wykonywania gestu odświeżania hello dane są zsynchronizowane tooyour zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="3c38a-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="3c38a-179">Otwórz ponownie Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="3c38a-179">Reopen Constants.cs.</span></span> <span data-ttu-id="3c38a-180">Poprawne hello `applicationURL` toopoint toohello Popraw adres URL.</span><span class="sxs-lookup"><span data-stu-id="3c38a-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="3c38a-181">Ponownie skompilować i uruchomić powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c38a-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="3c38a-182">Aplikacja Hello prób toosync z zaplecza aplikacji mobilnej powitania po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="3c38a-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="3c38a-183">Upewnij się, że żadne wyjątki są rejestrowane w konsoli debugowania hello.</span><span class="sxs-lookup"><span data-stu-id="3c38a-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="3c38a-184">(Opcjonalnie) Widok hello zaktualizowane dane przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler lub [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="3c38a-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="3c38a-185">Powiadomienie hello danych został zsynchronizowany między hello wewnętrznej bazy danych i hello magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3c38a-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="3c38a-186">Zwróć uwagę, hello dane zostały zsynchronizowane między hello bazy danych i magazynu lokalnego hello i zawiera elementy hello dodane odłączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c38a-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c38a-187">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3c38a-187">Additional Resources</span></span>
* <span data-ttu-id="3c38a-188">[Synchronizacja danych w trybie offline w usługi Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="3c38a-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="3c38a-189">[Porada zestawu SDK .NET usługi Azure Mobile Apps][8]</span><span class="sxs-lookup"><span data-stu-id="3c38a-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
