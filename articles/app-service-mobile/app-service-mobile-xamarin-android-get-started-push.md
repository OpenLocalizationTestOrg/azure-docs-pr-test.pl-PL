---
title: "Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.Android | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane do aplikacji platformy Xamarin.Android za pomocą usługi Azure App Service i usługi Azure Notification Hubs"
services: app-service\mobile
documentationcenter: xamarin
author: conceptdev
manager: crdun
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: crdun
ms.openlocfilehash: c7d2b68d2b523a04c38881d53747adfbb8b295cc
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2018
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a>Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Przegląd
W tym samouczku, dodawanie powiadomień wypychanych do [Xamarin.Android szybki start](app-service-mobile-windows-store-dotnet-get-started.md) projektu, aby powiadomienia wypychane są wysyłane do urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz Projekt serwera pobrany szybki start, konieczne będzie pakiet rozszerzenia powiadomień wypychanych. Zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.

## <a name="prerequisites"></a>Wymagania wstępne
Dla tego samouczka wymagane są następujące elementy:

* Aktywne konto Google. Można założyć konto Google na [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Usługa Google Cloud Messaging składnik klienta](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Włącz Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a>Konfigurowanie usługi Azure do wysyłania żądań wypychania
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Aktualizowanie projektów serwera do wysyłania powiadomień wypychanych
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Konfigurowanie projektu klienta dla powiadomień wypychanych
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Dodaj kod powiadomienia wypychane do aplikacji
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Testowych powiadomień wypychanych w aplikacji
Aby przetestować aplikację, należy w emulatorze za pomocą urządzenia wirtualnego. Brak dodatkowych czynności konfiguracyjnych wymaganych podczas uruchamiania emulatora.

1. Upewnij się, czy wdrożenie lub debugowanie na urządzeniu wirtualnym, który ma ustawioną jako docelową, interfejsy API Google, jak pokazano poniżej, w programie Android Virtual Device (AVD) manager.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Dodaj konto Google na urządzeniu z systemem Android, klikając **aplikacje** > **ustawienia** > **Dodaj konto**, postępuj zgodnie z monitami.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Uruchamianie aplikacji todolist jako przed i Wstaw nowe zadanie do wykonania. Teraz, w obszarze powiadomień jest wyświetlana ikona powiadomienia. Można także otworzyć menu powiadomień, aby wyświetlić pełny tekst powiadomienia.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
