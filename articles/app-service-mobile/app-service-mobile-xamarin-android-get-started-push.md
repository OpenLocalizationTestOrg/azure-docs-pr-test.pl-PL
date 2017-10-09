---
title: "aplikacji platformy Xamarin.Android tooyour powiadomień wypychanych aaaAdd | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacji platformy Xamarin.Android tooyour powiadomienia push toouse usłudze Azure App Service i toosend usługi Azure Notification Hubs"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Dodawanie aplikacji platformy Xamarin.Android tooyour powiadomień wypychanych
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Omówienie
W tym samouczku, możesz dodać toohello powiadomień wypychanych [Xamarin.Android szybki start](app-service-mobile-windows-store-dotnet-get-started.md) projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych. Zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* Aktywne konto Google. Można założyć konto Google na [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Usługa Google Cloud Messaging składnik klienta](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Włącz Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Skonfiguruj żądań wypychania Azure toosend
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Zaktualizuj powiadomień wypychanych toosend powitania serwera projektu
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Konfigurowanie powitania klienta projektu powiadomień wypychanych
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Dodaj aplikację tooyour kodu powiadomień wypychanych
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Testowych powiadomień wypychanych w aplikacji
Aplikacja hello można testować przy użyciu urządzenia wirtualnego w emulatorze hello. Brak dodatkowych czynności konfiguracyjnych wymaganych podczas uruchamiania emulatora.

1. Upewnij się, że jest wdrażany tooor debugowania na urządzeniu wirtualnym z interfejsów API Google, ustawić jako cel hello, jak pokazano poniżej w hello Android Virtual Device (AVD) manager.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Dodanie urządzenia Android toohello konto Google, klikając **aplikacje** > **ustawienia** > **Dodaj konto**, następnie postępuj zgodnie z monitami hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Uruchamianie aplikacji todolist hello jako przed i Wstaw nowe zadanie do wykonania. Teraz, w obszarze powiadomień hello jest wyświetlana ikona powiadomienia. Można także otworzyć hello powiadomień szuflady tooview hello pełny tekst hello powiadomień.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
