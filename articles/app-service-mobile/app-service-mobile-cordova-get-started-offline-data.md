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
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Włączanie synchronizacji w trybie offline dla aplikacji mobilnej oprogramowania Cordova
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

Ten samouczek zawiera funkcję synchronizacji w trybie offline hello z usługą Azure Mobile Apps dla oprogramowania Cordova. Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe. Zmiany są przechowywane w lokalnej bazie danych.  Po powrocie do trybu online urządzenia hello te zmiany są zsynchronizowane z hello usługi zdalnej.

W tym samouczku jest oparta na hello Cordova rozwiązania szybkiego startu dla Mobile Apps, utworzonych po ukończeniu hello samouczek [szybki start dla oprogramowania Apache Cordova]. W tym samouczku należy zaktualizować hello szybkiego startu rozwiązania tooadd funkcji w trybie offline z usługą Azure Mobile Apps.  Możemy również zaznacz kodu w trybie offline określonych hello w aplikacji hello.

toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]. Aby uzyskać szczegółowe informacje dotyczące użycia interfejsu API, zobacz hello [dokumentacji interfejsu API](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Dodaj rozwiązanie szybkiego startu toohello synchronizacji w trybie offline
Hello synchronizacji w trybie offline kod należy dodać toohello aplikacji. Synchronizacja w trybie offline wymaga hello wtyczki cordova sqlite magazynu, który automatycznie pobiera dodawane tooyour aplikacji, gdy wtyczkę Azure Mobile Apps hello jest uwzględnione w projekcie hello. Projekt szybkiego startu Hello zawiera oba te wtyczki.

1. W Eksploratorze rozwiązań programu Visual Studio Otwórz index.js i Zastąp hello następującego kodu

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    o tym kodzie:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Następnie zastąp hello następującego kodu:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    o tym kodzie:

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

    Hello poprzedni kod dodatków zainicjować hello lokalnego magazynu i zdefiniuj lokalnej tabeli, która odpowiada wartości w kolumnie hello używane w sieci Azure zaplecza. (Nie trzeba tooinclude wszystkie wartości kolumn tego kodu.)  Witaj `version` pole jest obsługiwany przez zaplecze aplikacji mobilnej hello, służy do rozwiązywania konfliktów.

    Pobierz odwołanie kontekst synchronizacji toohello przez wywołanie metody **getSyncContext**. Witaj kontekstu synchronizacji ułatwia zachowanie relacje między tabelami, śledzenia i wypychanie zmiany we wszystkich tabelach aplikacji klienckiej został zmodyfikowany podczas obliczania `.push()` jest wywoływana.

3. Aktualizowanie aplikacji hello adres URL aplikacji mobilnej tooyour aplikacji adresu URL.

4. Następnie Zastąp ten kod:

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    o tym kodzie:

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

    Witaj poprzedni kod inicjuje hello kontekstu synchronizacji, a następnie wywołuje tooget getSyncTable (zamiast getTable) toohello odwołanie do lokalnej tabeli.

    Ten kod używa hello lokalnej bazy danych dla wszystkich tworzenia, odczytu, aktualizacji i usuwania (CRUD) operacje tabeli.

    W tym przykładzie przeprowadza prosty błąd obsługi na konfliktów synchronizacji. Czy obsługa rzeczywistej aplikacji hello różne błędy, takie jak warunków sieciowych, powoduje konflikt z serwera i inne. Przykłady kodu, zobacz hello [próbki synchronizacji w trybie offline].

5. Następnie dodaj to funkcja tooperform hello rzeczywiste synchronizacji.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Zdecydujesz toopush zmiany zaplecza aplikacji mobilnej toohello przez wywołanie metody **syncContext.push()**. Na przykład można wywołać **syncBackend** w przycisk synchronizacji przycisk wiązanej tooa obsługi zdarzeń.

## <a name="offline-sync-considerations"></a>Zagadnienia dotyczące synchronizacji w trybie offline

W przykładowym hello hello **wypychania** metody **syncContext** wywołać tylko podczas uruchamiania aplikacji hello funkcji wywołania zwrotnego dla nazwy logowania.  W przypadku aplikacji rzeczywistych można także spowodować tej funkcji synchronizacji wywołane ręcznie lub po zmianie stanu sieci hello.

Podczas wykonywania ściąganie względem tabeli, która ma oczekujące aktualizacje z lokalnego śledzone przez hello kontekstu, który ściągnięcia operacji automatycznie wyzwalacze wypychania. Podczas odświeżania, dodawania i kończenie elementów w tym przykładzie, można pominąć hello jawne **wypychania** wywołać, ponieważ może być nadmiarowe.

W kodzie hello pod warunkiem, będą proszeni wszystkie rekordy w tabeli todoItem zdalnego hello, ale jest również możliwe toofilter rekordów przez przekazanie identyfikator zapytania i zapytań za**wypychania**. Aby uzyskać więcej informacji, zobacz sekcję hello *synchronizacja przyrostowa* w [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].

## <a name="optional-disable-authentication"></a>(Opcjonalnie) Wyłącz uwierzytelnianie

Jeśli nie ma tooset się uwierzytelniania przed testowaniem synchronizacji w trybie offline, komentarz hello funkcja wywołania zwrotnego dla nazwy logowania, ale pozostaw hello kodu wewnątrz odkomentowana hello funkcja wywołania zwrotnego.  Po komentowania hello logowania wierszy, kod hello są następujące:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Teraz hello aplikacji przeprowadza synchronizację z wewnętrznej bazy danych Azure po uruchomieniu aplikacji hello hello.

## <a name="run-hello-client-app"></a>Uruchom aplikację klienta hello
Teraz włączony synchronizacja w trybie offline umożliwia uruchamianie aplikacji klienckiej hello co najmniej raz na każdej z platform do wypełniania bazy danych magazynu lokalne powitania. Później symulować scenariusz w trybie offline i modyfikować danych hello w lokalnym magazynie hello, gdy aplikacja hello jest w trybie offline.

## <a name="optional-test-hello-sync-behavior"></a>(Opcjonalnie) Zachowanie synchronizacji hello testu
W tej sekcji możesz zmodyfikować powitania klienta projektu toosimulate scenariusz w trybie offline za pomocą nieprawidłowy adres URL aplikacji w danym zapleczu. Podczas dodawania lub zmienić elementy danych te zmiany są przechowywane w magazynie lokalnym, ale nie są magazynu danych zsynchronizowanej toohello wewnętrznej bazy danych do momentu ponownym nawiązaniu połączenia hello.

1. W Eksploratorze rozwiązań hello Otwórz plik projektu index.js hello i zmień toopoint adres URL aplikacji hello nieprawidłowy adres URL, takie jak hello następującego kodu:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. W index.html, zaktualizuj hello dostawcy usług Kryptograficznych `<meta>` element z hello tego samego nieprawidłowy adres URL.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Tworzenie i uruchamianie powitania klienta aplikacji i zwróć uwagę, czy wyjątek jest rejestrowane w konsoli hello, gdy aplikacja hello próbuje synchronizować z zapleczem hello po logowania. Nowe elementy, które można dodać istnieją tylko w lokalnym magazynie hello, dopóki nie są one usuwane toohello zaplecze aplikacji mobilnej. Aplikacja kliencka Hello zachowuje się tak, jakby była połączonych toohello wewnętrznej bazy danych.

4. Zamknij aplikację hello i uruchom ją ponownie tooverify hello nowe elementy utworzone czy toohello utrwalonego magazynu lokalnego.

5. (Opcjonalnie) Za pomocą programu Visual Studio tooview toosee tabeli bazy danych SQL Azure, sieci danych hello w hello wewnętrznej bazy danych w bazie danych nie zostały zmienione.

    W programie Visual Studio Otwórz **Eksploratora serwera**. Przejdź do bazy danych tooyour w **Azure**->**baz danych SQL**. Kliknij prawym przyciskiem myszy bazę danych i wybierz **Otwórz w Eksploratorze obiektów SQL Server**. Teraz można przeglądać tooyour tabeli w bazie danych SQL i jego zawartość.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Opcjonalnie) Test hello ponowne nawiązanie połączenia tooyour zaplecze aplikacji mobilnej

W tej sekcji ponownym hello aplikacji toohello zaplecze aplikacji mobilnej, która symuluje aplikacji hello powracające do trybu online. Podczas logowania, dane są zsynchronizowane tooyour zaplecze aplikacji mobilnej.

1. Otwórz ponownie index.js i przywrócić hello adres URL aplikacji.
2. Otwórz ponownie index.html i popraw adres URL aplikacji hello w hello dostawcy usług Kryptograficznych `<meta>` elementu.
3. Ponownie skompilować i uruchomić powitania klienta aplikacji. Aplikacja Hello prób toosync z zaplecza aplikacji mobilnej powitania po logowaniu. Upewnij się, że żadne wyjątki są rejestrowane w konsoli debugowania hello.
4. (Opcjonalnie) Widok hello zaktualizowane dane przy użyciu Eksplorator obiektów SQL Server lub narzędzia REST, takiego jak Fiddler. Powiadomienie hello danych został zsynchronizowany między hello wewnętrznej bazy danych i hello magazynu lokalnego.

    Zwróć uwagę, hello dane zostały zsynchronizowane między hello bazy danych i magazynu lokalnego hello i zawiera elementy hello dodane odłączeniu aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]
* [Visual Studio Tools for Apache Cordova]

## <a name="next-steps"></a>Następne kroki
* Przejrzyj bardziej zaawansowane funkcje synchronizacji w trybie offline, takie jak rozwiązywania konfliktów w hello [próbki synchronizacji w trybie offline]
* Przejrzyj synchronizacji w trybie offline hello dokumentacja interfejsu API w hello [dokumentacji interfejsu API](https://azure.github.io/azure-mobile-apps-js-client).

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
