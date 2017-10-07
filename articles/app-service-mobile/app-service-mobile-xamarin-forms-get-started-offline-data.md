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
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Włączanie synchronizacji w trybie offline dla aplikacji mobilnej platformy Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Omówienie
W tym samouczku wprowadzono funkcję synchronizacji w trybie offline hello aplikacji mobilnej Azure dla platformy Xamarin.Forms. Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe. Zmiany są przechowywane w lokalnej bazie danych. Po powrocie do trybu online urządzenia hello te zmiany są zsynchronizowane z hello usługi zdalnej.

W tym samouczku opiera się na powitania rozwiązania szybkiego startu platformy Xamarin.Forms Mobile Apps, utworzony po ukończeniu samouczka [tworzenie aplikacji platformy Xamarin.IOS]. Hello rozwiązanie szybkiego startu dla platformy Xamarin.Forms zawiera hello kodu toosupport synchronizacji w trybie offline, którą właśnie należy toobe włączone. W tym samouczku należy zaktualizować hello szybkiego startu rozwiązania tooturn na powitania funkcji w trybie offline z usługą Azure Mobile Apps. Możemy również zaznacz kodu w trybie offline określonych hello w aplikacji hello. Nie należy używać rozwiązania szybkiego startu hello pobrane, należy dodać hello danych access rozszerzenia pakietów tooyour projektu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][1].

toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Włączanie funkcji synchronizacji w trybie offline w rozwiązaniu szybkiego startu hello
Witaj synchronizacji w trybie offline zostanie dołączony kod projektu hello przy użyciu dyrektywy preprocesora C#. Gdy hello **OFFLINE\_SYNCHRONIZACJI\_włączone** zdefiniowano symbol, tych ścieżek kodu zostaną uwzględnione w kompilacji hello. Dla aplikacji systemu Windows należy również zainstalować hello SQLite platformy.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello > **Zarządzaj pakietami NuGet rozwiązania...** , następnie wyszukaj i zainstaluj **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet dla wszystkich projektów w rozwiązaniu hello.
2. W Eksploratorze rozwiązań hello, otwórz plik TodoItemManager.cs hello z projektu hello z **przenośnych** w polu Nazwa hello jest projektu biblioteki przenośnej klasy, następnie usuń komentarz hello następujące dyrektywy preprocesora:

        #define OFFLINE_SYNC_ENABLED
3. Urządzeń z systemem Windows (opcjonalnie) toosupport zainstalować jednego z powitania po SQLite środowiska uruchomieniowego pakiety:

   * **Środowisko uruchomieniowe Windows 8.1:** zainstalować [SQLite dla Windows 8.1][3].
   * **Windows Phone 8.1:** zainstalować [SQLite dla Windows Phone 8.1][4].
   * **Platforma uniwersalna systemu Windows** zainstalować [SQLite dla uniwersalnych uniwersalnych systemu Windows hello][5].

     Mimo że hello szybkiego startu zawiera projektów uniwersalnych systemu Windows, platforma uniwersalna systemu Windows hello jest obsługiwana w programie Xamarin Forms.
4. (Opcjonalnie) W każdym projekcie aplikacji systemu Windows, kliknij prawym przyciskiem myszy **odwołania** > **Dodawanie odwołania...** , rozwiń węzeł hello **Windows** folder > **rozszerzenia**.
    Włącz odpowiednie hello **SQLite dla systemu Windows** zestawu SDK oraz hello **Visual C++ 2013 środowiska wykonawczego systemu Windows** zestawu SDK.
    Witaj nazwy zestawu SDK SQLite się nieco różnić z każdej z platform Windows.

## <a name="review-hello-client-sync-code"></a>Przejrzyj powitania klienta synchronizacji kodu
Oto krótkie omówienie co to jest już uwzględniony w hello samouczek kodu wewnątrz hello `#if OFFLINE_SYNC_ENABLED` dyrektywy. Funkcja synchronizacji w trybie offline jest w pliku projektu hello TodoItemManager.cs projektu biblioteki klas przenośnych hello. Omówienie koncepcji hello funkcji, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps][2].

* Aby można było wykonać wszystkie operacje tabeli, muszą zostać zainicjowane hello lokalnego magazynu. Witaj magazynu lokalnego jest inicjowana w hello **TodoItemManager** konstruktora klasy przy użyciu hello następującego kodu:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Ten kod tworzy nowy lokalnej bazy danych SQLite przy użyciu hello **MobileServiceSQLiteStore** klasy.

    Witaj **DefineTable** metoda tworzy tabelę w magazynie lokalnym hello odpowiadającego pola hello w typie hello podane.  Typ Hello nie ma tooinclude wszystkich kolumn hello w hello zdalnej bazy danych. Jest możliwe toostore podzbiór kolumn.
* Witaj **todoTable** w **TodoItemManager** jest **IMobileServiceSyncTable** wpisz zamiast **IMobileServiceTable**. Ta klasa korzysta hello lokalnej bazy danych dla wszystkich tworzenia, odczytu, aktualizacji i usuwania operacje tabeli (CRUD). Zdecyduj, kiedy te zmiany są usuwane toohello zaplecza aplikacji mobilnej, przez wywołanie metody **PushAsync** na powitania **IMobileServiceSyncContext**. Witaj kontekstu synchronizacji ułatwia zachowanie relacje między tabelami, śledzenia i wypychanie zmiany we wszystkich tabelach aplikacji klienckiej został zmodyfikowany podczas obliczania **PushAsync** jest wywoływana.

    następujące Hello **SyncAsync** metoda jest wywoływana toosync z zaplecza aplikacji mobilnej hello:

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

    W przykładzie użyto prostych obsługi hello domyślne synchronizacji obsługi błędów. Rzeczywistej aplikacji będzie obsługiwać hello różne błędy, takich jak warunki w sieci i serwera, który powoduje konflikt przy użyciu niestandardowego **IMobileServiceSyncHandler** implementacji.

## <a name="offline-sync-considerations"></a>Zagadnienia dotyczące synchronizacji w trybie offline
W przykładowym hello hello **SyncAsync** wywoływana jest metoda tylko rozruchu i kiedy zażądano synchronizacji.  tooinitiate synchronizacji w aplikacji systemu Android i iOS, ściągnięcia w dół na liście elementy hello; w systemie Windows, użyj hello **synchronizacji** przycisku. W przypadku aplikacji rzeczywistych można również upewnij wyzwalacza synchronizacji powitania po zmianie stanu sieci hello.

Podczas wykonywania ściąganie względem tabeli, która ma oczekujące aktualizacje lokalnego śledzone przez kontekstu hello, który automatycznie pobierać operacji wyzwalaczy poprzedniego wypychania kontekstu. Podczas odświeżania, dodawania i kończenie elementów w tym przykładzie, można pominąć hello jawne **PushAsync** wywołania.

W kodzie hello pod warunkiem, będą proszeni wszystkie rekordy w tabeli zdalnej TodoItem hello, ale jest również możliwe toofilter rekordów przez przekazanie identyfikator zapytania i zapytań za**PushAsync**. Aby uzyskać więcej informacji, zobacz sekcję hello *synchronizacja przyrostowa* w [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps][2].

## <a name="run-hello-client-app"></a>Uruchom aplikację klienta hello
Teraz włączony synchronizacja w trybie offline uruchamianie aplikacji klienckiej hello co najmniej raz w każdej bazie platformy toopopulate hello lokalnego magazynu danych. Później symulować scenariusz w trybie offline i modyfikować danych hello w lokalnym magazynie hello, gdy aplikacja hello jest w trybie offline.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Zaktualizuj zachowanie synchronizacji hello powitania klienta aplikacji
W tej sekcji należy zmodyfikować powitania klienta projektu toosimulate scenariusz w trybie offline, nieprawidłowy adres URL aplikacji w danym zapleczu. Alternatywnie można wyłączyć połączeń sieciowych przez przeniesienie urządzenia zbyt "Tryb samolotowy".  Podczas dodawania lub zmienić elementy danych te zmiany są przechowywane w magazynie lokalnym hello, ale nie zsynchronizowano danych zaplecza toohello przechowywania, dopóki nie zostanie ponownie nawiązać połączenie hello.

1. W Eksploratorze rozwiązań hello, otwórz plik projektu Constants.cs hello z hello **przenośne** projektu i zmienić wartość hello `ApplicationURL` toopoint tooan nieprawidłowy adres URL:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Otwórz hello TodoItemManager.cs pliku z hello **przenośne** projektu, a następnie dodaj **catch** dla podstawowej hello **wyjątek** toohello klasy **try... catch** blok w **SyncAsync**. To **catch** bloku zapisuje hello konsoli toohello komunikat wyjątku, w następujący sposób:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Skompiluj i uruchom aplikację klienta hello.  Dodać niektóre nowe elementy. Zwróć uwagę, że wyjątek jest rejestrowana w hello konsoli dla każdego toosync próba z zapleczem hello. Te nowe elementy istnieje tylko w lokalnym magazynie hello, dopóki nie może zostać umieszczony toohello zaplecze aplikacji mobilnej. Aplikacja kliencka Hello zachowuje się tak, jakby była połączonych toohello wewnętrznej bazy danych, obsługa wszystkich tworzyć, odczytywać, update, operacji usuwania (CRUD).
4. Zamknij aplikację hello i uruchom ją ponownie tooverify hello nowe elementy utworzone czy toohello utrwalonego magazynu lokalnego.
5. (Opcjonalnie) Za pomocą programu Visual Studio tooview toosee tabeli bazy danych SQL Azure, sieci danych hello w hello wewnętrznej bazy danych w bazie danych nie zostały zmienione.

    W programie Visual Studio Otwórz **Eksploratora serwera**. Przejdź do bazy danych tooyour w **Azure**->**baz danych SQL**. Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**. Teraz można przeglądać tooyour tabeli w bazie danych SQL i jego zawartość.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Zaktualizuj powitania klienta aplikacji tooreconnect Twojego zaplecze aplikacji mobilnej
W tej sekcji Połącz się ponownie hello aplikacji toohello zaplecze aplikacji mobilnej, która symuluje aplikacji hello powracające tooan do trybu online. Podczas wykonywania gestu odświeżania hello dane są zsynchronizowane tooyour zaplecze aplikacji mobilnej.

1. Otwórz ponownie Constants.cs. Poprawne hello `applicationURL` toopoint toohello Popraw adres URL.
2. Ponownie skompilować i uruchomić powitania klienta aplikacji. Aplikacja Hello prób toosync z zaplecza aplikacji mobilnej powitania po uruchomieniu. Upewnij się, że żadne wyjątki są rejestrowane w konsoli debugowania hello.
3. (Opcjonalnie) Widok hello zaktualizowane dane przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler lub [Postman][6]. Powiadomienie hello danych został zsynchronizowany między hello wewnętrznej bazy danych i hello magazynu lokalnego.

    Zwróć uwagę, hello dane zostały zsynchronizowane między hello bazy danych i magazynu lokalnego hello i zawiera elementy hello dodane odłączeniu aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Synchronizacja danych w trybie offline w usługi Azure Mobile Apps][2]
* [Porada zestawu SDK .NET usługi Azure Mobile Apps][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
