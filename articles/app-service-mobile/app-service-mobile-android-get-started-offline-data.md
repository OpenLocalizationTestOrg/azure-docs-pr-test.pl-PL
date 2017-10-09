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
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Włączanie synchronizacji w trybie offline dla twojej aplikacji mobilnej systemu Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Omówienie
Ten samouczek obejmuje funkcji synchronizacji w trybie offline hello Azure Mobile Apps dla systemu Android. Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe. Zmiany są przechowywane w lokalnej bazie danych. Po powrocie do trybu online urządzenia hello te zmiany są synchronizowane z hello zdalnego wewnętrznej bazy danych.

Jeśli jest to środowiska pierwszy z usługą Azure Mobile Apps, najpierw należy wykonać samouczek hello [Utwórz aplikację systemu Android]. Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać hello danych access rozszerzenia pakietów tooyour projektu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn więcej informacji na temat funkcji synchronizacji w trybie offline hello, zobacz temat hello [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps].

## <a name="update-hello-app-toosupport-offline-sync"></a>Synchronizacja w trybie offline toosupport aplikacji hello aktualizacji
Z synchronizacji w trybie offline, przeczytaj zapisu tooand z *synchronizacji tabeli* (przy użyciu hello *IMobileServiceSyncTable* interfejsu), który jest częścią **SQLite** bazy danych na urządzeniu.

zmiany toopush i ściągania między hello urządzeń i usług Azure Mobile Services, użyj *kontekst synchronizacji* (*MobileServiceClient.SyncContext*), który należy zainicjować z lokalnej bazy danych hello dane toostore lokalnie.

1. W `TodoActivity.java`, komentarz hello istniejącą definicję `mToDoTable` i Usuń komentarz hello synchronizacji tabeli wersji:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. W hello `onCreate` metody komentarz inicjowanie istniejących hello `mToDoTable` i Usuń komentarz tej definicji:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. W `refreshItemsFromTable` komentarz definicję hello `results` i Usuń komentarz tej definicji:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Komentarz definicję hello `refreshItemsFromMobileServiceTable`.
5. Usuń znaczniki komentarza definicji hello `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Usuń znaczniki komentarza definicji hello `sync`:
   
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

## <a name="test-hello-app"></a>Aplikacja hello testu
W tej sekcji testu na powitania zachowanie w przypadku sieci Wi-Fi, a następnie wyłącz toocreate sieci Wi-Fi scenariusz w trybie offline.

Po dodaniu elementów danych przechowywane są w lokalnym magazynie SQLite hello, ale nie zsynchronizowano toohello usługi mobilnej do momentu kliknięcia hello **Odśwież** przycisku. Inne aplikacje mogą mieć inne wymagania dotyczące gdy danych potrzebuje toobe zsynchronizowane, ale dla celów demonstracyjnych ten samouczek ma hello użytkownik jawnie żądania.

Po naciśnięciu tego przycisku uruchamiania nowego zadania w tle. Wypycha go najpierw wszystkie zmiany wprowadzone toohello magazynu lokalnego przy użyciu kontekstu synchronizacji, a następnie ściąga zmienione dane z lokalnej tabeli toohello platformy Azure.

### <a name="offline-testing"></a>Testowanie w trybie offline
1. Miejsce hello urządzenie lub symulator w *tryb samolotowy*. Spowoduje to utworzenie scenariusz w trybie offline.
2. Dodaj raporty *ToDo* elementy lub znak niektóre elementy jako ukończone. Zamknij hello urządzenie lub symulator (lub hello wymuszanie zamknięcia aplikacji) i uruchom ponownie. Sprawdź, czy zmiany zostały utrwalone na urządzeniu hello ponieważ są one przechowywane w lokalnym magazynie SQLite hello.
3. Wyświetl zawartość hello hello Azure *TodoItem* tabeli za pomocą narzędzia SQL, takich jak *programu SQL Server Management Studio*, lub klienta REST, takich jak *Fiddler* lub  *Postman*. Sprawdź, czy nowe elementy hello *nie* zostały zsynchronizowane toohello serwera
   
       + Dla zaplecza Node.js go toohello [portalu Azure](https://portal.azure.com/), i w aplikacji mobilnej kliknij zaplecza **łatwe tabel** > **TodoItem** tooview zawartość hello hello `TodoItem` tabeli.
       + Dla zaplecza .NET, Wyświetl hello tabelę zawartości za pomocą narzędzia SQL takich jak *programu SQL Server Management Studio*, lub klienta REST, takich jak *Fiddler* lub *Postman*.
4. Włącz sieci Wi-Fi w hello urządzenie lub symulator. Następnie naciśnij klawisz hello **Odśwież** przycisku.
5. Przeglądanie danych TodoItem hello w hello portalu Azure. Witaj, które są nowe i zmienione TodoItems powinien zostać wyświetlony.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]
* [Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services] \(Uwaga: hello wideo znajduje się w usłudze Mobile Services, ale synchronizacji w trybie offline działa w podobny sposób jak w usłudze Azure Mobile Apps\)

<!-- URLs. -->

[synchronizacji danych w trybie Offline w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md

[Utwórz aplikację systemu Android]: app-service-mobile-android-get-started.md

[Okładce chmury: Synchronizacja w trybie Offline w usłudze Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

