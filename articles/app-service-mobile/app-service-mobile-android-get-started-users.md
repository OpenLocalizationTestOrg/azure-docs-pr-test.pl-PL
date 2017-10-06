---
title: "aaaAdd uwierzytelniania w systemie Android w usłudze Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello funkcji Mobile Apps w usłudze Azure App Service tooauthenticate użytkowników aplikacji systemu Android za pomocą różnych dostawców tożsamości, obejmującej Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Dodawanie aplikacji dla systemu Android tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Podsumowanie
W tym samouczku można dodać projekt szybkiego startu todolist toohello uwierzytelniania w systemie Android przy użyciu dostawcy tożsamości obsługiwane. W tym samouczku jest oparta na powitania [Rozpoczynanie pracy z usługą Mobile Apps] — samouczek, należy najpierw wykonać.

## <a name="register"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi Azure App Service
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello

Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji. Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji. W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu. Można jednak użyć dowolnego wybranego schematu URL. Powinna być unikatowa tooyour aplikacji mobilnej. Przekierowanie hello tooenable na powitania po stronie serwera:

1. W hello [portalu Azure] wybierz usługę aplikacji.

2. Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.

3. W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `appname://easyauth.callback`.  Witaj _appname_ ten ciąg jest hello schemat adresu URL aplikacji mobilnej.  Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).  Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.

4. Kliknij przycisk **OK**.

5. Kliknij pozycję **Zapisz**.

## <a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* W programie Android Studio Otwórz projekt hello Ukończono z samouczka hello [Rozpoczynanie pracy z usługą Mobile Apps]. Z hello **Uruchom** menu, kliknij przycisk **uruchamianie aplikacji**i sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.

     Ten wyjątek spowodowany prób aplikacji hello tooaccess Witaj ponownie kończyć się jako użytkownik nieuwierzytelniony, ale hello *TodoItem* tabeli teraz wymaga uwierzytelniania.

Następnie zaktualizuj użytkownicy tooauthenticate aplikacji hello przed wysłaniem żądania zasobów z hello kończyć Mobile Apps ponownie. 

## <a name="add-authentication-toohello-app"></a>Dodaj aplikację toohello uwierzytelniania
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Tokeny uwierzytelniania pamięci podręcznej na powitania klienta
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuować tooone hello następujące samouczki:

* [Dodawanie aplikacji dla systemu Android tooyour powiadomień wypychanych](app-service-mobile-android-get-started-push.md).
  Dowiedz się, jak tooconfigure aplikacji mobilnych z powrotem kończyć powiadomień wypychanych toosend toouse Azure notification hubs.
* [Włączanie synchronizacji w trybie offline dla aplikacji systemu Android](app-service-mobile-android-get-started-offline-data.md).
  Dowiedz się, jak w trybie offline tooadd obsługują tooyour aplikacji przy użyciu zaplecza aplikacji mobilnej. Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Rozpoczynanie pracy z usługą Mobile Apps]: app-service-mobile-android-get-started.md
