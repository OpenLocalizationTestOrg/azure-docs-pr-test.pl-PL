---
title: Synchronizacja w trybie offline aaaEnable aplikacji mobilnej Azure (Xamarin Android)
description: "Dowiedz się, jak toouse aplikacji usługi Mobile App toocache i synchronizacji danych w trybie offline w aplikacji platformy Xamarin Android"
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a>Włączanie synchronizacji w trybie offline dla aplikacji mobilnej platformy Xamarin.Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Omówienie
W tym samouczku wprowadzono funkcję synchronizacji w trybie offline hello aplikacji mobilnej Azure dla platformy Xamarin.Android. Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe. Zmiany są przechowywane w lokalnej bazie danych.
Po powrocie do trybu online urządzenia hello te zmiany są zsynchronizowane z hello usługi zdalnej.

W tym samouczku, zaktualizuj powitania klienta projektu z samouczka hello [tworzenie aplikacji dla systemu Xamarin Android] toosupport hello funkcji w trybie offline z usługą Azure Mobile Apps. Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać hello danych access rozszerzenia pakietów tooyour projektu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Aktualizacja funkcji w trybie offline aplikacji toosupport powitania klienta
Funkcje platformy Azure w trybie offline aplikacji mobilnej umożliwia toointeract z lokalnej bazy danych są w trybie offline scenariuszu. toouse te funkcje w aplikacji, należy zainicjować [SyncContext] tooa magazynu lokalnego. Następnie odwołać się do tabeli za pomocą hello [IMobileServiceSyncTable] [IMobileServiceSyncTable] interfejsu. SQLite jest używany w lokalnym magazynie hello na urządzeniu hello.

1. W programie Visual Studio Otwórz hello Menedżera pakietów NuGet w projekcie hello wypełnione hello [tworzenie aplikacji dla systemu Xamarin Android] samouczka.  Wyszukiwanie i instalowanie hello **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet.
2. Otwórz plik o nazwie ToDoActivity.cs hello i Usuń komentarz hello `#define OFFLINE_SYNC_ENABLED` definicji.
3. W programie Visual Studio, naciśnij klawisz hello **F5** kluczy toorebuild i wykonywania powitania klienta aplikacji. Aplikacja Hello działa hello została tak samo jak przed włączeniem synchronizacji w trybie offline. Jednak hello lokalnej bazy danych jest teraz wypełniona dane, które mogą być używane w scenariuszu w trybie offline.

## <a name="update-sync"></a>Zaktualizuj toodisconnect aplikacji hello z hello wewnętrznej bazy danych
W tej sekcji możesz przerwać hello połączenia tooyour aplikacji mobilnej zaplecza toosimulate sytuacji w trybie offline. Po dodaniu elementów danych z programu obsługi wyjątków informuje, że danej aplikacji hello jest w trybie offline. W tym stanie nowych elementów dodanych w lokalne powitania przechowywania i zsynchronizowaniu do zaplecza aplikacji mobilnej hello podczas wypychania jest wykonywany jest niepodłączony.

1. Edytowanie hello projektu udostępnionego o nazwie ToDoActivity.cs. Zmień hello **applicationURL** toopoint tooan nieprawidłowy adres URL:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Zachowanie w trybie offline można także pokazują, wyłączając sieci Wi-Fi i sieci komórkowych na urządzeniu hello lub przy użyciu tryb samolotowy.
2. Naciśnij klawisz **F5** toobuild i uruchamianie aplikacji hello. Zwróć uwagę, synchronizacji nie powiodło się podczas odświeżania po hello uruchomienia aplikacji.
3. Wprowadź nowe elementy i zwróć uwagę, że wypychania nie powiedzie się ze stanem [CancelledByNetworkError] każdym kliknięciu **zapisać**. Jednak hello nowych zadań do wykonania istnieje w magazynie lokalnym hello dopóki nie może zostać umieszczony toohello zaplecza aplikacji mobilnej.  W środowisku produkcyjnym aplikacji, jeśli pominąć te wyjątki, który aplikacja kliencka hello zachowuje się tak, jakby nadal jest połączony toohello zaplecza aplikacji mobilnej.
4. Zamknij aplikację hello i uruchom ją ponownie tooverify hello nowe elementy utworzone czy toohello utrwalonego magazynu lokalnego.
5. (Opcjonalnie) W programie Visual Studio Otwórz **Eksploratora serwera**. Przejdź do bazy danych tooyour w **Azure**->**baz danych SQL**. Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**. Teraz można przeglądać tooyour tabeli w bazie danych SQL i jego zawartość. Sprawdź, czy hello danych w bazie danych zaplecza hello nie uległy zmianie.
6. (Opcjonalnie) Za pomocą narzędzia REST, takie jak Fiddler lub Postman tooquery Twojego zaplecze aplikacji mobilnej, za pomocą zapytania GET w formie `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Zaktualizuj tooreconnect aplikacji hello zaplecza aplikacji mobilnej
W tej sekcji ponownie nawiąż połączenie zaplecza aplikacji mobilnej toohello aplikacji hello. Przy pierwszym uruchomieniu aplikacji hello, hello `OnCreate` wywołań obsługi zdarzeń `OnRefreshItemsSelected`. Ta metoda wywołuje `SyncAsync` toosync przechowywać lokalne powitania wewnętrznej bazy danych.

1. Otwórz o nazwie ToDoActivity.cs w projekcie udostępnionym hello i przywrócić zmiana hello **applicationURL** właściwości.
2. Naciśnij klawisz hello **F5** kluczy toorebuild i hello uruchomienia aplikacji. Witaj aplikacji synchronizuje lokalne zmiany z zaplecza aplikacji mobilnej Azure hello przy użyciu operacji wypychania i ściągania podczas hello `OnRefreshItemsSelected` metoda jest wykonywana.
3. (Opcjonalnie) Widok hello zaktualizowane dane przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler. Powiadomienie hello danych został zsynchronizowany między bazy danych zaplecza aplikacji mobilnej Azure hello i hello magazynu lokalnego.
4. W aplikacji hello, kliknij przycisk wyboru hello pole obok kilka elementów toocomplete je w lokalnym magazynie hello.

   `CheckItem`wywołania `SyncAsync` elementu toosync każdego ukończone z hello zaplecza aplikacji mobilnej. `SyncAsync`wywołuje wypychania i ściągania. **W przypadku, gdy wykonanie ściągania na tabeli powitania klienta wprowadził zmiany, wypychania jest zawsze wykonywana automatycznie**. Dzięki temu wszystkie tabele w lokalnym magazynie wraz z relacji zachować spójność. To zachowanie może spowodować nieoczekiwane wypychania. Aby uzyskać więcej informacji dotyczących tego zachowania, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps].

## <a name="review-hello-client-sync-code"></a>Przejrzyj powitania klienta synchronizacji kodu
Witaj Xamarin klienta pobrany projekt po ukończeniu samouczka hello [tworzenie aplikacji dla systemu Xamarin Android] już zawiera kod obsługujący synchronizacji w trybie offline przy użyciu lokalnej bazy danych SQLite. Oto krótkie omówienie co to jest już uwzględniony w hello samouczek kodu. Omówienie koncepcji hello funkcji, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps].

* Aby można było wykonać wszystkie operacje tabeli, muszą zostać zainicjowane hello lokalnego magazynu. Witaj magazynu lokalnego jest inicjowana po `ToDoActivity.OnCreate()` wykonuje `ToDoActivity.InitLocalStoreAsync()`. Ta metoda tworzy lokalnej bazy danych SQLite przy użyciu hello `MobileServiceSQLiteStore` klasy powitania klienta usługi Azure Mobile Apps SDK.

    Witaj `DefineTable` metoda tworzy tabelę w magazynie lokalnym hello odpowiadającego pola hello w typie hello podane `ToDoItem` w takim przypadku. Typ Hello nie ma tooinclude wszystkich kolumn hello w hello zdalnej bazy danych. Jest możliwe toostore tylko podzbiór kolumn.

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* Witaj `toDoTable` członkiem `ToDoActivity` jest hello `IMobileServiceSyncTable` wpisz zamiast `IMobileServiceTable`. Witaj IMobileServiceSyncTable kieruje wszystkie tworzenia, odczytu, aktualizacji i usuwania (CRUD) toohello tabeli operacyjna baza danych o magazynu lokalnego.

    Zdecyduj, gdy zmiany są usuwane toohello zaplecza aplikacji mobilnej Azure, wywołując `IMobileServiceSyncContext.PushAsync()`. Witaj kontekstu synchronizacji ułatwia zachowanie relacje między tabelami, śledzenia i wypychanie zmiany we wszystkich tabelach aplikacji klienckiej został zmodyfikowany podczas obliczania `PushAsync` jest wywoływana.

    Witaj podany kod wywołuje `ToDoActivity.SyncAsync()` toosync przy każdym odświeżeniu listy todoitem hello lub dodano lub wykonać zadania do wykonania. synchronizacje kod powitania po każdej zmianie lokalnego.

    W kodzie hello podać wszystkie rekordy hello zdalnego `TodoItem` badane są tabele tabeli, ale jest również możliwe toofilter rekordów przez przekazanie identyfikator zapytania i zapytań za`PushAsync`. Aby uzyskać więcej informacji, zobacz sekcję hello *synchronizacja przyrostowa* w [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps].

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Synchronizowanie danych w trybie offline w usłudze Azure Mobile Apps]
* [Porada zestawu SDK .NET usługi Azure Mobile Apps][8]

<!-- URLs. -->
[Tworzenie aplikacji dla systemu Xamarin Android]: ../app-service-mobile-xamarin-android-get-started.md
[Synchronizowanie danych w trybie offline w usłudze Azure Mobile Apps]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Tworzenie aplikacji dla systemu Xamarin Android]: app-service-mobile-xamarin-android-get-started.md
[Synchronizowanie danych w trybie offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
