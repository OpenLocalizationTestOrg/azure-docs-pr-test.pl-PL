---
title: "aaaEnable synchronizacji w trybie offline dla aplikacji uniwersalnych platformy systemu Windows (UWP) z usługą Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse aplikacji mobilnej Azure toocache i synchronizacji danych w trybie offline w aplikacji Windows platformy Uniwersalnej."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Włączanie synchronizacji w trybie offline dla aplikacji systemu Windows
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak w trybie offline tooadd obsługują tooa Windows platformy Uniwersalnej aplikacji przy użyciu zaplecza aplikacji mobilnej Azure. Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe. Zmiany są przechowywane w lokalnej bazie danych. Po powrocie do trybu online urządzenia hello te zmiany są synchronizowane z hello zdalnego wewnętrznej bazy danych.

W tym samouczku zaktualizować projekt aplikacji platformy uniwersalnej systemu Windows hello z samouczka hello [tworzenie aplikacji systemu Windows] toosupport hello funkcji w trybie offline z usługą Azure Mobile Apps. Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać hello danych access rozszerzenia pakietów tooyour projektu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].

## <a name="requirements"></a>Wymagania
Ten samouczek wymaga hello następujące wymagania wstępne:

* Visual Studio 2013 uruchomiony w systemie Windows 8.1 lub nowszym.
* Zakończenie [tworzenie aplikacji systemu Windows][Tworzenie aplikacji systemu windows].
* [Azure Mobile Services SQLite magazynu][sqlite store nuget]
* [SQLite do tworzenia aplikacji platformy uniwersalnej systemu Windows](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Aktualizacja funkcji w trybie offline aplikacji toosupport powitania klienta
Funkcje platformy Azure w trybie offline aplikacji mobilnej umożliwia toointeract z lokalnej bazy danych są w trybie offline scenariuszu. toouse te funkcje w aplikacji, należy zainicjować [SyncContext] [ synccontext] tooa magazynu lokalnego. Następnie odwołać się do tabeli za pomocą hello [IMobileServiceSyncTable][IMobileServiceSyncTable] interfejsu. SQLite jest używany w lokalnym magazynie hello na urządzeniu hello.

1. Zainstaluj hello [środowiska wykonawczego SQLite dla platformy uniwersalnej systemu Windows hello](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. W programie Visual Studio, otwórz Menedżera pakietów NuGet hello projekt aplikacji platformy uniwersalnej systemu Windows hello wypełnione hello [tworzenie aplikacji systemu Windows] samouczka.
    Wyszukiwanie i instalowanie hello **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet.
3. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** > **Dodawanie odwołania...** >**Uniwersalnych systemu Windows** > **rozszerzenia**, następnie włączyć zarówno **SQLite dla platformy uniwersalnej systemu Windows** i **2015 środowiska uruchomieniowego Visual C++ dla aplikacji platformy uniwersalnej systemu Windows**.

    ![Dodaj odwołanie do bazy danych SQLite platformy uniwersalnej systemu Windows][1]
4. Otwórz plik MainPage.xaml.cs hello i Usuń komentarz hello `#define OFFLINE_SYNC_ENABLED` definicji.
5. W programie Visual Studio, naciśnij klawisz hello **F5** kluczy toorebuild i wykonywania powitania klienta aplikacji. Aplikacja Hello działa hello została tak samo jak przed włączeniem synchronizacji w trybie offline. Jednak hello lokalnej bazy danych jest teraz wypełniona dane, które mogą być używane w scenariuszu w trybie offline.

## <a name="update-sync"></a>Zaktualizuj toodisconnect aplikacji hello z hello wewnętrznej bazy danych
W tej sekcji możesz przerwać hello połączenia tooyour aplikacji mobilnej zaplecza toosimulate sytuacji w trybie offline. Po dodaniu elementów danych z programu obsługi wyjątków informuje, że danej aplikacji hello jest w trybie offline. W tym stanie nowych elementów dodanych w lokalne powitania przechowywania i będą synchronizowane z hello zaplecza aplikacji mobilnej przy następnym uruchomieniu wypychania jest niepodłączony.

1. Edytowanie pliku App.xaml.cs hello projektu udostępnionego. Komentarz hello inicjowanie hello **MobileServiceClient** i Dodaj powitania po wierszu, który korzysta z aplikacji mobilnej nieprawidłowy adres URL:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    Można również pokazują zachowania w trybie offline, wyłączając sieci Wi-Fi i sieci komórkowych na urządzeniu hello lub tryb samolotowy.
2. Naciśnij klawisz **F5** toobuild i uruchamianie aplikacji hello. Zwróć uwagę, synchronizacji nie powiodło się podczas odświeżania po hello uruchomienia aplikacji.
3. Wprowadź nowe elementy i zwróć uwagę, że wypychania kończy się niepowodzeniem z [CancelledByNetworkError] stanu każdorazowo po kliknięciu **zapisać**. Jednak hello nowych zadań do wykonania istnieje w magazynie lokalnym hello dopóki nie może zostać umieszczony toohello zaplecza aplikacji mobilnej.  W środowisku produkcyjnym aplikacji, jeśli pominąć te wyjątki, który aplikacja kliencka hello zachowuje się tak, jakby nadal jest połączony toohello zaplecza aplikacji mobilnej.
4. Zamknij aplikację hello i uruchom ją ponownie tooverify hello nowe elementy utworzone czy toohello utrwalonego magazynu lokalnego.
5. (Opcjonalnie) W programie Visual Studio Otwórz **Eksploratora serwera**. Przejdź do bazy danych tooyour w **Azure**->**baz danych SQL**. Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**. Teraz można przeglądać tooyour tabeli w bazie danych SQL i jego zawartość. Sprawdź, czy hello danych w bazie danych zaplecza hello nie uległy zmianie.
6. (Opcjonalnie) Za pomocą narzędzia REST, takie jak Fiddler lub Postman tooquery Twojego zaplecze aplikacji mobilnej, za pomocą zapytania GET w formie `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Zaktualizuj tooreconnect aplikacji hello zaplecza aplikacji mobilnej
W tej sekcji ponownym zaplecza aplikacji mobilnej toohello aplikacji hello. Te zmiany zasymulować ponowne połączenie sieciowe na powitania aplikacji.

Przy pierwszym uruchomieniu aplikacji hello, hello `OnNavigatedTo` wywołań obsługi zdarzeń `InitLocalStoreAsync`. Ta metoda z kolei wywołuje `SyncAsync` toosync przechowywać lokalne powitania wewnętrznej bazy danych. Aplikacja Hello prób toosync podczas uruchamiania.

1. Otwórz App.xaml.cs w projekcie udostępnionym hello i Usuń komentarz z poprzednich inicjowanie `MobileServiceClient` toouse hello poprawne hello aplikacji mobilnej z adresu URL.
2. Naciśnij klawisz hello **F5** kluczy toorebuild i hello uruchomienia aplikacji. Witaj aplikacji synchronizuje lokalne zmiany z zaplecza aplikacji mobilnej Azure hello przy użyciu operacji wypychania i ściągania podczas hello `OnNavigatedTo` wykonuje program obsługi zdarzeń.
3. (Opcjonalnie) Widok hello zaktualizowane dane przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler. Powiadomienie hello danych został zsynchronizowany między bazy danych zaplecza aplikacji mobilnej Azure hello i hello magazynu lokalnego.
4. W aplikacji hello, kliknij przycisk wyboru hello pole obok kilka elementów toocomplete je w lokalnym magazynie hello.

   `UpdateCheckedTodoItem`wywołania `SyncAsync` elementu toosync każdego ukończone z hello zaplecza aplikacji mobilnej. `SyncAsync`wywołuje wypychania i ściągania. Jednak **przy każdym wykonaniu ściągania na tabeli powitania klienta wprowadził zmiany, wypychania jest zawsze wykonywana automatycznie**. Takie zachowanie gwarantuje, że wszystkie tabele w lokalnym magazynie hello wraz z relacji zachować spójność. To zachowanie może spowodować nieoczekiwane wypychania.  Aby uzyskać więcej informacji dotyczących tego zachowania, zobacz [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].

## <a name="api-summary"></a>Podsumowanie interfejsu API
toosupport hello w trybie offline funkcji usługi mobilne, użyliśmy hello [IMobileServiceSyncTable] interfejsu i zainicjować [MobileServiceClient.SyncContext] [ synccontext] z lokalnej bazy danych SQLite. Jeśli w trybie offline, hello normalnych operacji CRUD dla aplikacji mobilnych pracować tak, jakby aplikacji hello jest nadal połączony, podczas gdy operacje hello są wykonywane przed hello lokalnego magazynu. następujące metody Hello są używane toosynchronize hello lokalnego magazynu z serwerem hello:

* **[PushAsync]**  , ponieważ ta metoda jest elementem członkowskim [IMobileServicesSyncContext], zmiany we wszystkich tabelach są usuwane toohello wewnętrznej bazy danych. Tylko rekordy z lokalne zmiany są wysyłane toohello serwera.
* **[PullAsync]**  ściąganie jest uruchamiany z [IMobileServiceSyncTable]. Gdy w tabeli hello śledzonych zmian, niejawne wypychania jest uruchamiane toomake się upewnić, że wszystkie tabele w lokalnym magazynie hello wraz z relacji zachować spójność. Witaj *pushOtherTables* parametr określa, czy inne tabele w kontekście hello są przenoszone w niejawnych wypychania. Witaj *zapytania* przyjmuje parametr [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] lub hello toofilter ciąg zapytania OData zwróciła dane. Witaj *identyfikatora kwerendy* zostanie użyty parametr toodefine synchronizacji przyrostowej. Aby uzyskać więcej informacji, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  aplikacji z lokalnego magazynu hello powinny wywoływać okresowo dane stare toopurge metody. Użyj hello *wymusić* parametru, gdy będziesz potrzebować toopurge wszelkie zmiany, które nie zostały jeszcze zsynchronizowane.

Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Więcej informacji
Hello poniższe tematy zawierają dodatkowe informacje na temat funkcji synchronizacji w trybie offline hello aplikacji mobilnej:

* [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]
* [Porada zestawu SDK .NET usługi Azure Mobile Apps][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Tworzenie aplikacji systemu windows]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
