---
title: "aaaAdd wypychania powiadomień tooyour aplikacji systemu Android z usługą Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosend Mobile Apps toouse push aplikacji systemu Android tooyour powiadomienia."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a>Dodawanie aplikacji dla systemu Android tooyour powiadomień wypychanych
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Omówienie
W tym samouczku, możesz dodać toohello powiadomień wypychanych [Android szybki start] projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych. Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Wymagania wstępne
Potrzebne są następujące hello:

* IDE, w zależności od projektu zaplecza:

  * [Android Studio](https://developer.android.com/sdk/index.html) Jeśli ta aplikacja ma zaplecza Node.js.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) lub nowszym, jeśli ta aplikacja ma zaplecze .NET firmy Microsoft.
* Android 2.3 i nowszy, poprawki repozytorium Google 27 lub nowszym i usług Google Play 9.0.2 lub nowszy Firebase Cloud Messaging.
* Zakończenie hello [Android szybki start].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Tworzenie projektu obsługującego usługę Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Konfigurowanie powiadomień wypychanych Azure toosend
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Włącz powiadomienia wypychane na powitania serwera projektu
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Dodaj aplikację tooyour powiadomień wypychanych
W tej sekcji należy zaktualizować klienta powiadomień wypychanych toohandle aplikacji systemu Android.

### <a name="verify-android-sdk-version"></a>Sprawdź wersję zestawu SDK systemu Android
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

Następnym krokiem jest tooinstall usług Google Play. Google Cloud Messaging ma niektóre minimalne interfejsu API poziomu wymagania dotyczące projektowania i testowania, które hello **minSdkVersion** właściwości w manifeście hello muszą być zgodne.

Jeśli testujesz starsze urządzenia, należy skontaktować się [ustawić się Google Play zestaw SDK usług] toodetermine jak niska, ustaw tę wartość i odpowiednio ją ustawić.

### <a name="add-google-play-services-toohello-project"></a>Dodaj projekt toohello usług Google Play
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Dodawanie kodu
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Test aplikacji hello hello opublikowane usługi mobilnej
Można przetestować aplikacji hello, dołączając bezpośrednio telefonie z systemem Android za pomocą kabla USB lub za pomocą urządzenia wirtualnego w emulatorze hello.

## <a name="next-steps"></a>Następne kroki
Po ukończeniu tego samouczka, rozważ kontynuować tooone hello następujące samouczki:

* [Dodawanie aplikacji dla systemu Android tooyour uwierzytelniania](app-service-mobile-android-get-started-users.md).
  Dowiedz się, jak projektu tooadd uwierzytelniania toohello todolist — Szybki Start w systemie Android przy użyciu dostawcy tożsamości obsługiwane.
* [Włączanie synchronizacji w trybie offline dla aplikacji systemu Android](app-service-mobile-android-get-started-offline-data.md).
  Dowiedz się, jak w trybie offline tooadd obsługują tooyour aplikacji przy użyciu zaplecza aplikacji mobilnej. Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- URLs -->
[Android szybki start]: app-service-mobile-android-get-started.md

[ustawić się Google Play zestaw SDK usług]:https://developers.google.com/android/guides/setup
